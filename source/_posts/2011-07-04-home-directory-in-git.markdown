---
layout: post
title: "Home Directory in Git"
date: 2011-07-04 07:03
comments: true
categories: 
---


#Why
Saturday morning a friend of mine, lets call him
Michael, and I were having breakfast. I asked why he was buying his own laptop
when his employer gives him one. His response was that he had been through 
layoffs where his laptop was seized and he lost his personal work and projects.
That let me back to this old item on my personal project list.

Over the years most seasoned developers become intrigued by the idea of using
version control to keep their configuration files and home directories backed
up and portable between machines. It's a natural urge after all. Version control
is something they use with code text daily, and it has saved their behinds many
times over the years. A natural thing is to notice all text -- writing, 
configuration files, everything -- would benefit from the same tools.

Today we also tend to use multiple virtual machines. I am not an individual
contributor as much these days, yet I still log into multiple virtual machines
to spot check the solutions my teams are building. My teams are on these sites every
day, often SSH'd in, sometimes piping the UI back to their local machine. All
of us have tools and configuration files unique to our workflows.

It is pretty easy to see where it becomes very useful to have your home directory
in a version control system that you can quickly replicate into each 
machine you deal with. The mindset is quite accurately seen [in this
blog post](http://kitenet.net/~joey/svnhome/) by Joey Hess.

#Issues

In my mind there are three issues to think through if you do decide to version
control your digital life. 
-  Where do you store it?
-  How do you separate public data, personal data, and machine specific configuration data?
-  What do you and do you not version?

##Where do you store it?
Let's be honest, if you don't own the machine where your repository is stored,
you are opening yourself up to losing it. But on the other hand the convenience
of having an organization maintain the repository for you is very nice. We must 
tread carefully here as we see what happens to people who blindly put their
personal data on social networking sites then are suprised to find what those
sites do with it. I would hate that to happen to, say, tax documents!

If you use a distributed versioning system such as git, your gain some safety against losing your data. Because every
machine gets a full copy of the repository (though you have to ask for all the
branches, which is not often mentioned!) every machine potentially has everything
stored on it.

As for hosting, I recommend using your own hosted machine. Especially if you
plan to version something like SSH keys. Hell, putting SSH keys in a repo 
that goes somewhere is risky as it is! But on the plus side it means you can
easily sync them between your home and work machines, or anywhere else you 
need to. You'll have to make that call yourself, considering the risk of the
keys being compromised, the effect if they are, and the convenience of being
able to get them on a nem machine with 'git pull'.

For this it is probably safe enough to use an Amazon micro-instance. That
means part of bootstrapping a new machine will be uploading
the correct Amazon key pair. I'm willing to go down that path for now.

##Separating Data
Many of the blog posts I read on this topic suggest storing different types of
data in different repositories. One for public, one for private, etc. That
is pretty necessary when, say, you use a version control system like SVN. 

But again, we are using git. Branches are cheap. So maybe we really want to have branches for
public data that goes on all machines; private data we need only some of the
time; etc. Then make the master branch the public data. Fork it and add in the 
data. Rebase the private data branch to the public on a regular basis. Repeat
as needed, then automate the rebasing with a nice cron or startup script. 
Probably startup so the script itself can be in the public data branch.

Now here is the cool part. Only want the public data on your new machine?
Just git-clone it. Want the private as well? Check it out.

There are definite problem with this approach. If you are on the private branch
and want to change something in the public branch, you need to remember to
switch back to the public branch first. Which (a) will interfere with your
workflow, and (b) mean you have to remember which branch everything came from.

Because of this you may still want to have separate repositories. That will also
provied another layer of protection in that if a machine with the public 
repo is compromised, the attacker cannot easiy git clone the private branch.

That is the way I will go. I love the simplicity of having one repository,
but fear the security threat it represents.

##What to version
You could version everything. Your 100GB of music and video may not be the 
best choice though. On the other hand, maybe parts of /etc is. This requires
considered thought. When in doubt on this, I like to use a general rule: start
small, live with it awhile, then slowly add more. This is not a race and mistakes
can carry high penalties. Block out time
time on your Friday AM calendar, say 15 minutes, to decide whether to version
more stuff or to schedule a time to re-design your versioning scheme because the
current layout is not holding up in day to day use.

For my part, I am going to start with stealing the layout described at [this blog post](http://kristian-domagala.blogspot.com/2008/10/home-direcotry-version-control.html)
by Kristian Domagala. The rest of his ideas, especially the use of Growl on the
Mac to notify you of changes, also looks good. It only applies to one machine
for me though so I think I'll leave it out for now.

#Concrete steps
It's hard to be sure my steps are correct without testing them, but this seems
to be the process.
-  Really stop and rethink your directory layout and how it will work with the way your version control setup will work. Or steal a good idea, as I have above!
-  Set up your repositories somewhere safe. Again, I am using an Amazon micro-instance, but that may not be secure enough for you.
-  Think through what scripts you want to run to maintain this, and either write them now or add them to your project list
-  Try using your setup in a practice run to see how it goes!

I'll get back to you on the results of this process as soon as I can. I'm curious 
myself, and to be honest, a bit excited. I lost my resume once many years ago and 
never really got back all the information. That was decades ago, but I could see
it happening today as well. Seeing how things change on my machine over time, 
like a living journal, woud be another plus. Maybe I could do that with my email
in Thunderbird somehow?

Well, one thing at a time.

  
