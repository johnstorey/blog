---
layout: post
title: "Foursquare"
date: 2011-12-09 16:46
comments: true
categories: mongoDB
---

*These are unedited notes from the MongoSV 2011 Conference*

# Stats

-  15 M users
-  Peak 2500 HTTP QPS
-  80 check ins per sec
-  8 production mongodb clisuter
-  8 shards of users, 12 shards of check-ins
-  Users: 250 updates / sec, 4k ops per sec, 46MB per sec

Using Solr as their search stack.

EC2 supports 50 faults / sec / drive.

They retain the entire working set in RAM. Once they go to disk they see huge volume of errors.

Right now using 4 EBS volumes with RAID 0. Thinking about RAID 10.

Overtime fragmentation leads to bloat. If you view db.stats you can see this in data size, index size, and storage size.

# Problem: EBS performance degrades

Solution? Kill the mongodb process and restart on a new EBS volume. Then do the same with the backup.

Symptons

-  ioutil % on one volume > 90%
-  qr / qw counts spike
-  fault rates > 10 in mongostat
-  sometimes tcploss counts spike

# Problem: Fresh Mongo instance has not paged in all the data

Solution

-  cat > /dev/null works too unless your dataset is > RAM

Also cool ideas are in the Instagram blog with something they call 'intouch'.

# Hits

-  Always set new replica set members to initialSync from a secondary or they will hammer primary
-  It's easy to inadvertently steal page cache from mongod (hint: less -n)
-  Booleans are 2 bytes long in BSON. We now use bitfields.

# Backfills

Common pattern: we want to instert / update a recond on every user / checkin / venue.

Used to do this sequentially by ID.

Now have a library that connects to mongoC, retrieves shard ranges, and runs 1 thread per shard.

# Migrating Collections

You can migrate at the mongoDB level.

Oplogs to the rescue.

each oplog entry is idempotent, so long as data is replayed to the current op, consistency is.

This is basically how Mongo implements RECOVERING state.

## Not all Roses

-  Since moving from unshareded to sharded cluster, add to add shard key
-  Insert / update ops required transformation for shard key
