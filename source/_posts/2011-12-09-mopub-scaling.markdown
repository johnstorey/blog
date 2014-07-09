---
layout: post
title: "MoPub Scaling"
date: 2011-12-09 16:47
comments: true
categories: mongoDB
---

*These are unedited notes from the MongoSV 2011 Conference*

50ms to process each event.

-  Started as 3 founders hoping to bring Angry Birds on to the platform. Their customers are app developers.
-  Needed to scale quickly as customers came on
-  0 time to spend time on ops
-  chose Google App Engine
-  Python (?Guido? works on this team)

Business objects are siloed per user account. One to many relationships.

Collect stats for every ad serve and ad interaction.

On app engine have a simple stats model.

# Realtime stats in GAE

- datastore
  -  expensive writes
  -  slow writes 1 / sec/ entity group
  -  fast reads 3 ms
-  memcache
-  TaskQueues

Cannot do sums over objects in GAE or even native map / reduces 

Solution: Buffer into memcache then periodically flush to the datastore by pushing them into a TaskQueue.

# GAE Shortcomings

-  Transient downtime for writes
-  Read before write
-  memcache is fleeting, leading to data loss
-  Objects have become too large for transactions
-  writing to datastore, even buffered is expensive
  -  pay for datastore CPU and app CPU. Way too costly.
  
# AWS + Mongo

-  We have control of each service and the machines on which they run
-  access to RAM!
-  fire and forget increments
-  our entire machinery for recording mulitple stats is a series of increment instructions sent to MongoDB (which handles all buffering and flushing.)

# First Attempt: Data Model

One document per published advertiser per month. Each document stores data for all days and hours in the month.

## Initial results

- Pros
  -  Scales with # business objects
  -  Queries for highel level cross products
  -  Queries for stats for a given date range result in only reading the # of months total documents in the range
-  Cons
  -  Lots of little documents
  -  more
  
# Solution: New Data Model

Account for ??? in our data model.

Everything in the account stored with hash table.

Created IndexDocument to store the reverse indices to do the higher-level cross sections

## Results

-  2 machines handle all the writes
-  Mongo load is now miniscule
-  each update really 2 (StatsDocument and StatsIndex)
-  Each get is really 2 gets (same objects)
-  One document per account per day
  -  # documents scale with # accounts
  -  we do the simple aggregation in python
  -  size of document scales with # business objects within account
  -  more
  
# Lessons Learned

-  Better to have fewer, larger documents if there is a logical hierarchy than many smaller documents arranged flatly
-  Log everything because you will make mistakes
  -  This has saved us time and again
-  Buy more memory
  -  It's cheap!
  -  Solved our cache misses
  -  Some problems cannot be solved just by throwing memory at the problem
  
# Future Work

Mobile User store 

-  will record every interaction of every user
-  ML: map / reduce jobs to glean data about our suers and segment them
-  per user targeting with minimum latency
-  relevancy => better user experience => app devs make more money

