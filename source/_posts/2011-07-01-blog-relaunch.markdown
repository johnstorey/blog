---
layout: post
title: "Blog Relaunch"
date: 2011-07-01 07:03
comments: true
categories: 
---
#Slacker

I admit it -- I have been slack about posting to my blog in its short 3 years
of existence. It's always seemed a huge effort, and work is always a time sink.
Right now I'm running an offshoring company and am up, literally, at all hours
keeping teams on three continents running. Once I smooth things out I'm sure
there will be other reasons why I can't post.

But I want to write for my blog.

So I have done a few things:
-  I usually want to post when in my IDE and looking at code
-  Dave Winer interested me in his blog post letting me know that Amazon S3 buckets can be used static web sites now
-  Wordpress, more and more, seemed too bloated to blog on. Ditto Drupal

So I finally started searching for static web site generators, and have settled
on Jekyll, the generator for the wonderful GitHub. Many users maintain their
Jekyll based blogs as public GitHub repositories, so I took a clone of one 
Elijah Miller's site (attribution in right hand column). Enabling S3 as a 
website was trivial once I read the S3 documentation. Where my domain was 
hosted I did a hard redirect of 'www.johnstorey.org' to the Amazon supplied site.
Bam! My blog is there, running fast, and gorgeous.

Now there are some steps I have skipped on this lazy Saturday afternoon, namely
-  Get my local Jenkins server to watch git commits of my blog text, auto-rebuild it, and push to both GitHub and Amazon S3
-  Run or write a script to get Amazon 53 DNS services working with the blog.
  -  Should fix the address bar so every page says 'www.johnstorey.org'
  -  Should avoid breaking Google Analytics, which I am sure I have done
- Write a script to be called by Jenkins to do the moving of the new blog contents to Amazon S3

Still, this is a fast, low maintenance, source code verisioned blog. Very nice!

Now if you will excuse me, my buddy here is doing some interesting work with
programming GPUs. Also I have 
-  To learn CoffeScript.
-  A book on Maven to read.
-  To research how to localize Groovy and use property files so I can show my offshore team how to improve their code.
-  And I see the cloned CSS does not handle &lt;ul&gt; tags at all. Need to fix that.

Let's see if I don't maintain this blog better in the years to come.
