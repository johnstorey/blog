---
layout: post
title: "Mobile Drupal Made Easy"
date: 2012-01-01 14:58
comments: true
categories: drupal mobile
---

January 1st, 2012. What a great year 2011 has been! A VP Engineering position where we turned the company around from self-immolation, and moving in with the girlfriend. No matter what else you can say, it's been exciting and one of the bigger growth experiences of my life. So how to top it in 2012? Hey, how to match it? 

I have no idea. So instead I took my one week off at the end of the year (hey, turning that company around was a 7 day a week job!) to return to my favorite technology, Drupal. After some struggles with the Drupal 7 core code I can create entities and fields willy nilly. In real life it's almost always better to create them in the UI and export them with Features, but for really understanding what's happening you need to get as deep into the code as possible. So I did that, and used the knowledge to sketch out a new module idea with a friend. You should see the fruits of that around March. She's busy writing a book for Packt, and I have real life coming back in two days. That's going to slow us down.

Now, on to the topic of this post ...

# Mobile Drupal Made Easy

That company where they hired me in as VPE? After a year the first project has come along where Drupal seems the most appropriate answer (along with Apache Solr and possibly Node.js). We have the client kickoff the second week of January, then it's a pell mell rush for a three month delivery. Having had a months warning one of the first things we did was sketch out a preliminary architecture, then map out the areas where we had missing experience or an unclear idea how to proceed. One of those was in how to make mobile apps connected to Drupal in the most convienent way possible.

The short story was, for this client, make a standalone app makes little sense. Yes, we want to be in the app store, but we are going to use about zero percent of the native functionality. So despite a strong Sencha Touch skillset we want to try a new approach.

# Proposed: Responsive Web in a Phone Gap Wrapper

We plan to create a responsive web design (we've done some internal development tests with the Omega Theme to great success.) Then wrap it in PhoneGap or Sencha Touch wrapped in Phone Gap. That's the part we have not tried yet.

So I have a full day until real life work starts up. The emails already indicate the client pressure will be huge, and the new project starting up won't lessen anything. Let's see if you get a post showing PhoneGap wrapping XHTML and sized with a responsive web design. I have high hopes the approach will work fine because (a) it makes sense, and (b) it turns out there is a session on how to do the same thing being given at Drupalcon Denver in March.

Look for a post showing how to do this over the next few weeks.

Happy New Year!
John

