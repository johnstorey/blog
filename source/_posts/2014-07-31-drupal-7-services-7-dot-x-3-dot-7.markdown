---
layout: post
title: "Drupal 7 Services 7.x-3.7"
date: 2014-07-31 21:01:05 -0700
comments: true
categories: drupal
---

# Environment.
Drupal 7
Services Module 7.x-3.7

# Instructions for Authenticating a User.
This is a reminder of the current process to log in a user and authenticate with the Drupal Services module. To be honest, when I have time to look at it, I think the RESTful module by Gizra will be a better solution for headless Drupal projects, but today Services is what I know and use.

This came about because I needed to jump in and make an existing NodeJS API work with Drupal on the back-end for a team member.

I assume that you are familiar with Drupal and Services, and want to log in using the basic authentication bundled with Services. OAuth is a different (but when needed, awesome) beast.

## /api/user/login.

This part is simple. POST to the /user/login resource on your endpoint.

1.  No Drupal specific headers.
2.  The POST should work with a header of Content-Type =  application/json, but I always need to set it to application/x-www-urlencoded. I have no idea why.
3.  In the requestbody set the values for username and password.
4.  You will get back a login response with session_name, sessid, and token parameters.
5.  In all subsequent calls set the following headers
  1. Cookie must be set to <session_name>=<sessid>. Yes, session_name and sessid become the value, separated by an equal sign.
  2. Set X-CSRF-Token to <token>.

You are done -- Drupal now knows who your client is logged in as.

## /system/connect.
POST to this endpoint, and if you have configured things correctly, you should get the user you logged in as back as an object. If you get the anonymous user, you've done something wrong.

## /user/logout.
To be extra sure, call /user/logout. You should get a value of TRUE back in your response body. Calling /system/connect now gives you back the anonymous user object.

# Summary.

There are many descriptions of how to log users in and out, and the advice changes with different releases of the module. This works in the environment specified at the top of this blog post.

I hope this helps others out there -- I'm sure I'll refer to this six months from now, when I myself have forgotten the details!

