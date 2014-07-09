---
layout: post
title: "MongoDB on AWS"
date: 2011-12-09 16:46
comments: true
categories: mongoDB
---

*These are unedited notes from the MongoSV 2011 Conference*

Jared Rosoff
jsr@10gen.com

# Single node setup

## Instance sizing

mongoDB's storage engine is meant to work on a 64-bit platform.

Micro instances are terrible DB servers. The CPU bursts then slows. You only want to do development and testing. You never want to run a production DB. But they make great arbiters and config servers.

Large + normal way people go. Cluster compute instances are great for really huge mongoDB instances.

mongoDB uses disk and RAM, so high CPU instance probably a waste of money.

## OS

Any Gnu Linux good. 10gen starts with AMZN one.

-  turn off atime
-  raise file descriptior limits

   cat >> /etc/security/limits.conf << EOF
   * hard nofile 65536
   * soft profile 65536
   EOF
   
-  DO NOT use large VM pages
-  Use ext4, xfs (ext3 preallocate files and db will pause during this)
-  Use RAID
  -  RAID10 on mongoD
  -  RAID1 on configDB
-  *Warning!* Known problems with Ubuntu 10.04 & EBS

# mongoDB Data Note

Reccomend

-  64 bit instance
-  more RAM = better
-  run ext4 or xfs file system
-  turn off atmie & diratime
-  EBS volumes in RAID10

MTBF of EBS > an actual disk drive. RAID10 helps compensate for this.

Each EBS can sustaine 100 IOPS (i/o per second) so more stripes the more IOPs per mongoDB instance. So more disk drives is very important. This run in production by many clients.

## Config Server

-  64 bit instance
  -  micro is fine
-  EBS volumes in RAID1 is fine

## Arbiter

Just needs a network

-  micro is fine
-  no storage requirements
-  must be separate from rest of replica sets

# Single region replica set

3 mongoDBs in a region, in separate availability zones. Gives some guarantee that the instances run on different boxes, avoiding a single point of failure.

Still vulnerable to a region going down.

## Disaster recovery site

To avoid single region death people commonly keep 2 mongoDBs in region-1, and that is production. region-2 is just a hot copy. If region-1 goes down, we can stand up region-2 quickly and change the DNS entry. Maybe takes a few hours max until AWS sorts itself out.

# Multi Data Center

Want to run in multiple regions with auto-failover. To do that you need 3 regions. Within mongoDB to get a quorum you need > 50% to select a master. So set up replica sets in 3 separate regions, region-1, region-2 and region-3. 

When one region goes down the mongo replicate set will select a master from the other two.

You pay a price in latency. Writing may be across the country (assuming all regions are in the same country).

# Sharded Clusters

definition: Lots of replica sets grouped together as a cluster.

So all the above advice applies. Just set up shards in each region instead of one instance.

# Provisioning

Create one secruity group with mongodB instances. Create another with app servers. Grant access to mongoDB security group for app server group.


# Backups

If you are using EBS you can take snapshots, even of multiple EBSs for RAID setups.

Other considerations are architecture specific.
