---
layout: post
title: "Tech Changes"
date: 2011-12-09 12:21
comments: true
categories: 
---

I am writing this at the Silicon Valley MongoDB conference, MongoSV. MongoDB is interesting to me as it is a re-imagining of an object database I used in the 1990's. Not that they copied it -- but it's been re-invented in the form of mongoDB. mmap() is again a major thing in databases.

So at the Q&A I naturally wondered if the major theme of those years of my life, allocating memory so that related data was on a single page in memory, was relevant to MongoDB. I used to maintaing a custom memory allocater, help clients rewrite their code and more, all to reduce the number of pages that would be swapped in and out of memory by the data store.

The accurate response from the engineer? "I think that is a micro-optimization that should only be considered inside the Mongo server itself." Which is something he said they should think more about internally. (Aside: 25K+ writes per second on cheap commodity hardware and they weren't yet totally tweaked? Wow!)

I had sort of expected the response, but still it triggered a small introspection that led to the words you are reading now.

Things change, others are just re-implemented, and if you don't keep re-imagining yourself with that in mind you are tech job roadkill. Everytime I turn around I see engineers ossifying because they now have richer personal lives, or have seen too many ideas re-tread, or feel they have been unfairly treated in a startup. But you know what? *Now* is the best time I can imagine to be in tech. *Now* is all the opportunity. *Now* in the best chance for your experience to shine in bigger, greater challenges that have real world impact. So keep pushing on and constantly learning. True, we will have less of a personal life than other professions, but be honest. For us the computer *is* the game. If they did not pay us we would be driven to do it ourselves.

Now I have to go. The mongoDB on AWS talk is starting ...
