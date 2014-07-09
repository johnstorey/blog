---
layout: post
title: "Deficencies with Vagrant"
date: 2012-01-07 08:13
comments: true
categories: vagrant drupal
---

I love the Vagrant project. Someday, hopefully soon, I'll be able to switch my whole developer organization over to using it. Here's a note to myself about what needs to happen first. I'm posting so I can refer back from time to time and see if it's something we can use now (don't look at me, I'm hacking on (Drupal)[http://drupal.org/]). 

# Cannot Run in Bridged Mode

You know what? For some reason in Virtual Box XDebug can only talk to a host  debugger if it's running in bridged networking mode. Unfortunately that is not a current Vagrant feature. I have seen a patch to network.rb that does not seem to work for me. Also I heard there is a patch in branch on Debian that was recently submitted.

On a personal level, if anyone can help me get XDebug working on OSX Lion and talking to MacGDP back on the host, I'd greatly appreciate it. For my own work.

# Cannot Run on Windows Well

This is a problem with gems that use native DLLs. Why do I care? *I* don't. Windows can disappear off the surface of hard drives across the planet for my money. But much of my company is full of developers who don't and don't desire to learn to work with anything other than Windows. I'm just not going to move them anytime soon.

Unfortunately here is a current reality

-  On Windows, Vagrant does not work on Ruby. 
-  It does work on JRuby.
-  JRuby does not allow gems that use native API components.
-  Chef requires native API components.

# When These Issues Resolve

I'll be able to move the organization to Vagrant. Until then I'll get some of the value by distributing virtual machines and letting people share their source code folders into it.

It's annoying though. Vagrant is a great piece of software.
