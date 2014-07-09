---
layout: post
title: "Vagrant and Chef"
date: 2011-12-06 17:08
comments: true
categories: [ chef, vagrant ]
---

Vagrant and Chef, oh my!

I read with interest the high level discussion over at [Matt Butcher's Blog](http://technosophos.com/content/building-custom-drupal-image-vagrant) regarding the use of [Vagrant](http://vagrantup.com) to improve your Drupal development this morning with some interest. Matt is a super smart guy who has previously written about a hobby horse of mine, namely, that development is best done in a virtual machine. Check his blog for the reasoning -- it's solid.

But today I felt he really glossed over the use of Vagrant. We are working with Vagrant internally for a Drupal project and a J2EE project. This is still early stage -- our Chef recipes are somewhat primitive for example -- but already we are seeing marked increases in development velocity. As we contine to find time here and there to work with Chef Servers and refine the workflow it seems obvious that one really should maintain base Vagrantfiles representing major architectures used for major categories of sites in house. Likely we'll end up forking a base Vagrantfile template to refine based on the individual needs of each client. For instance, Varnish should be tweaked based on site content and usage patterns.

In addition there is an argument for company repositories for

-  custom Vagrant boxes
-  packages for the applications being installed for each client
-  the Drupal code and modules being used
-  the tools used to build the solution, and so forth

This is a contentious point though. The old school philosophy of "keep copies of everything, even the tools you used to build it, in case you can't get them elsewhere when you need them in the future" seems a bit overzealous. But then again, I would not feel that way if 5 years from now we need to spin up an old CentOS site with applications that are no longer available on the web ...

No point in drawing you into our internal dialogues though. The point is, really doing this right is much more complex than Matt has made it out to be. When we feel we've settled into the right setup for our company I'll make a point of revisiting the topic in this space for all of you. Give it a couple of months. Meanwhile Vagrant and Chef are incredibly powerful tools being implemented in the company and, honestly, we could not be happier to have them. It's the magic in the computer all over again.


Now if I could figure out why the mods to this Redmine cookbook don't seem to be taking full effect ...
