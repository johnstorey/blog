---
layout: post
title: "Personal Projects AMI 0.5"
date: 2011-07-10 07:03
comments: true
categories: [ amazon ]
---

#The Need

Every developer has their own projects. Mostly you can keep local source code repositories and
be happy. But what if you are working with a friend or two, and want to share your code? Github gives a decent answer
for this, and if you want a private repository the cost is not too bad. But what if, as I wrote about in an earlier
post, you want to keep your own private configuration files for moving from machine to machine? Or you just don't want
someone else holding your code? In that case you want your own repository.

Might as well make it into an Amazon AMI.

So here is the first release (well v0.21) of an Amazon AMI that will let you quickly set up multiple projects with
git and and a great defect tracker.

#Solution Choices

##EC2 is Cheap

Recently I looked again at Amazon instance costs as part of a cost and security audit for a client. It turns out that 
small instances, if bought reserved for a year, are now US $54. Micro-instances are $14 month to month, and less if
reserved for a year.

Which such low costs it makes sense to just run the repository on Amazon. My goal is, as features are added in later
versions, to keep this running smoothly on a micro-instance. 

##Which AMI?

Again, this is not a hard choice. I wanted a 32-bit AMI image of Ubuntu, and Canoncial has helpful links
at http://cloud.ubuntu.com. Why 32-bit? Because Amazon small instances are not available on 64-bit AMIs.

For the current release the AMI is in the US West region. Clearly this is not acceptable, and getting it 
available in all regions is in the works.

##Gitosis or Gitalite?

It's not enough to have a git repository. You want features such as
-  Be able to add and remove users with public keys, not by creating user accounts for them
-  Be able to host multiple repositories easily
-  Be able to add and remove user access to repositories via configuration
-  Have all your configuration choices versioned so you can roll back to earlier setups

Both Gitosis and Gitalite achieve these goals by keeping a text configuration file stored in their underlying Git repositories.
You can add users, remove them, attach them to various project repositories, and control the type of access you desire. This 
is great! But Gitosis has one fault in my mind. There seems to be no way to *control access at the branch level*. In public
projects this is necessary in order to allow you to manage a project, let others branch within it, then only allow them to
issue pull requests to you rather than commit directly to the main branch itself. In the enterprise this functionality
is required to implement development workflow policies. People *will* commit to the main branch if they have access to it,
no matter what policies are in place. They will do it the night before a major deliverable, break the build, and cause 
you major pain. 

Don't let this happen to you. Use Gitolite, with it's branch level ACLs.

I installed it according to these [blog instructions](http://computercamp.cdwilson.us/git-gitolite-git-daemon-gitweb-setup-on-ubunt).

Unfortunately I never got the Gitweb working with these instructions.

##Mantis or JIRA or ?

You want a bug tracker with multiple project support, because you'll have multiple projects (or this solution
may be overkill for you). The choice here was quick and simple for me:

-  I believe JIRA to be more functional, and all my clients use it
-  I believe Mantis to be less functional
-  My impression is Mantis requires drastically fewer resources
-  Since I'll interact with them mostly through Eclipse's Mylyn plugin, they will look the same to me
-  I want to keep resources down to run an an EC2 micro-instance

Victor: Mantis.

Installed as specified [in this blog post](http://www.ghacks.net/2009/09/08/install-mantis-bug-tracking-tool-on-your-ubuntu-server/). As it
stands Mantis cannot send e-mail, which will cripple it. So I recommend you [follow these instructions](http://www.mantisbt.org/forums/viewtopic.php?t=15398&f=3)
 and you'll have it sending e-mail via GMail in 5 minutes. Specifically, the AMI is set-up for GMail. You just need to add in your GMail
 username and password by editing /var/www/mantis/config.inc.php.
 
 Of course you can set up a full-fledged mail server and do it properly. 

##Gitweb or Gitalist?

Ah, now the real choices. I must have spent 6 hours over 3 days trying to get either these working with Gitolite. All to get functionality
I already have and am more likely to use via my Eclipse IDE. At that point I stepped back, decided the value add of the web interface did not
match the effort I was putting in. It's not in this version of the AMI.

That being said, even with the few themes I found, Gitweb appears ugly. If anyone can get it running and let me know how before I
get back to this I'd use it. But more, I'd love to see [Gitalist](http://www.gitalist.com/) running here. Much prettier and 
maybe just a bit more functional.

For now though there is no web interface to Git on the AMI. Did I mention that your IDE already does all this? Why leave it?

#How To Use It

##Get It

Log into your Amazon account and select the US-West region. The AMI you want is ami-6dbeec28.

Make sure you give it a security group with ports 22, 80, 443 and 9418 open.

##Set-up Mantis

Mantis is configured with the default log-in user

    administrator
    root
    
I'd advise you change it ASAP, then follow the link above to get email working. Really, all I have done is take out my GMail account settings
and left the rest in. So if you insert your GMail username and password you should be good to go.

That's it. Issue tracking is now enabled.

##Set-up Gitolite

Now here I had to stop part way through. Why? Setting up Gitolite requires the use of *your* public key. That's how administrative access is controlled.
There is not much left to do though. Do the following

-  SCP your public key to the /tmp directory of your EC2 instance (let's call it username.pub)
-  SSH into the EC2 instance
-  sudo chmod 666 /tmp/username.pub
-  sudo -H -u gitolite gl-setup /tmp/username.pub
-  sudo chmod g+r /var/lib/gitolite/projects.list
-  sudo chmod -R g+rx /var/lib/gitolite/repositories
-  sudo vi /var/lib/gitolite/.gitolite.rc
  -  Change the $REPO_MASK to 027
-  Reboot the instance
  -  sudo reboot
  
Now we can test it out on the local machine

-  git clone gitolite@git.server:gitolite-admin.git
-  cd gitolite-admin
-  vi conf/gitolite.conf
-  For the testing repo enable the git-daemon access by adding
  -  R = daemon
-  Commit the file and push it
  -  git commit -a -m "Enable git-daemon for testing.git"
  -  git push
- Now you can clone the testing repository with
  -  git clone git://git.server/testing.git
  
  
That's it! Go read up on the details of how to configure Gitolite -- you'll be very happy with what
you can now do!

#Futures

Clearly there are a number of features missing that need to be in future versions of this solution.
In order of importance to me they are
-  OpenVPN: I want to optionally lock down the solution for client projects
-  Gitalist: web repository browsers are very popular, and I should provide that for team members at work
-  Script the final set-up steps for Gitolite 
-  Gerrit: Code reviews are something I strongly support, and I want support built into workflows around this AMI
-  CI: Probably Hudson/Jenkins. The only worry here is the overhead may mean it does not work in an EC2 micro-instance

Feedback is welcome. This was put together quickly, and I'm sure there are many improvements that can be made
beyond the ones I've listed above!
