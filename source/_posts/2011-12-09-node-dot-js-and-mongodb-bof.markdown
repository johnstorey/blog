---
layout: post
title: "Node.js and mongoDB BOF"
date: 2011-12-09 16:47
comments: true
categories: mongoDB
---

*These are unedited notes from the MongoSV 2011 Conference*

mongoDB node.js driver has native and JS BSON libraries. Many forums recommend using the JS one. Moderator agrees. He may split the JS driver out to a completely separate repository and project. 

Now it does cool things like getting the raw, unparsed BSON data. Good for HTML5 games for example, where the parsing is too slow.

Then native C++ driver is 2X slower serializing data, and 5X faster deserializer. Moderator blames it on his own limited C++ skills. In practice he does not see this as a limiting factor in most applications.

# GridFS

Moderator experimenting with a feature like GridFS. Uses a collection of documents that have a chunk in them that is binary. Wants to make binary types in mongo much more efficent. Basically the moment it hits binary, like a video, it starts streaming it without much overhead.

# Mongoose

If you want performance, don't use it. It's all about validating types; getters and setters; more expressive query builder; etc. It's alot slower.

In V8 try / catch and getter / setter are just not optimized. Also there are some crazy overloading of operator types.

# Safe Writes

Off by default in JS and most mongoDB drivers. Considering making it on by default. Otherwise there is no way for you to know if your transactions work for example.

# SSL Support

v2.2 they will add SSL support to the drivers. It's only waiting on US Export license approval.

# Multi CPU systems

In Node.js you used to have to fire up a node process per CPU. Now it's in a configuration file.

# Advantage of V8

Because you are on V8 you get to use the latest JS stuff all the time. object.create(), not this.prototype for example.

Buffer objects are created outside of V8 heap and stays until you release it. But is direct memory access speed. Increased JS driver speed by 5x.

