---
layout: post
title: "Mobile_Web-and-Drupal.markdown"
date: 2011-12-02 11:06
comments: true
categories: [ emacs, drupal ]
---


Recently I've been looking at a number of projects that end my temprorary sojurn from the joys and frustrations of Drupal. It's a family people, and I'm glad to be home.

Along the way I have been reading and thinking alot about mobile design with Drupal. My analysis is that it is all in the air right now, but some key thoughts seem to hold sway in the overall community.

1.  Responsive web design just needs the height and width of the device from the CSS media queries, and all will be well with the world. 
2.  If you have an existing site, the [Mobile Tools](http://drupal.org/projects/mobile_tools) is the way to go. It relies on the HTTP user agent information, not media queries.
3.  Omega Theme is the risen star for mobile web design. (It really does have some nice features, or at least the web themer GF assures me they are incredible).


Now I have issues with all these memes, which irritates me as I have two web applications that need to be delivered. Maybe one of the web gurus out there has some thoughts?

Choice \#1 ignores the platform. Well, Android 2.3 on tablet A and tablet B might be modified in a way that works differently yet is important to me. Recently we did a custom app for an internal device for a global manufacturer where this was the case. True, it may only happen one more time in my life, but I want to be able to account for it.

Choice \#2 has lots of appeal because it is a solution integrated to Panels. Panels continues to be one of the major value adds we get out of the Drupal platform. But I am not convinced I can rely on the user agent telling me enough -- I need that media query as well.

Chocie \#3 really does have my attention, but without a clean Panels integration, and without the information from user agent I feel like there are too many combinations that cannot be covered.

Possibly I am letting perfect be the enemy of good here. I'll leave the final decision to the themer of course, but my current thought is we should use

-  Panels
-  a Panels friendly theme that can leverage responsive design
-  a module that passes user agent info into a responsive theme in case it's useful to the themer

So what's the web think? Am I on the right path, or am I overthinking? The weekend projects involve putting a solution like this together (once I go through the [Vagrant](http://vagrantup.com) setup for Drupal I've been using lately with some friends.) So I'd love the feedback.
