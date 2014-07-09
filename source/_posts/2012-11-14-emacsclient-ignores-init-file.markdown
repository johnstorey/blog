---
layout: post
title: "Emacsclient Ignores Init File"
date: 2012-11-14 21:47
comments: true
categories: emacs
---

Strangely 

<code>
    emacsclient -t
</code>

does not seem to use my ~/.emacs.d/init.el file in the latest Emacs 24 when I start it as a daemon and open a frame. This is true on Ubuntu 12.?? and OSX.

This is really irritating, but since I really only need one frame 99% of the time I guess I'll ignore it. I did put an hour into playing with it and following Google Searches, but if anyone can tell me why this is so, I'd love to know. I'd like to have the daemon started when I boot my Macbook and my development VM, then have the client come up fast.

Interestingly if I load the init file in a buffer and evaluate the buffer, it all works fine.

Humpf.

**UPDATE:** Of course this was simple late night, unclear thinking. All that was not working was keyboard-translate, which makes sense. Adding an alias to my environment worked around the issue and now all is well. 

<code>
	alias emacs=emacsclient -t --eval '(keyboard-translate ?\C-t ?\C-x)'
</code>

Now my emacs setup runs in all my environments properly. Next: move the various dotfilies into a *dotfiles/* directory, toss it on github, and replicate that across environments. This will also neccessitate some thought as I commonly run tmux on my Macbook, ssh to my development server, then run tmux there. So the same .tmux-conf file with the same control key clearly won't work.

Maybe it's time to simply stop doing that and change my workflow. A problem to think about after a good nights sleep ...



