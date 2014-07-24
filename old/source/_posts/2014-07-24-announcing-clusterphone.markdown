---
layout: post
title: "Announcing clusterphone"
date: 2014-07-24 21:38
comments: true
categories:
 - node.js
 - open source
---

A couple of weeks ago I released a new Node.js library called [clusterphone](https://github.com/samcday/clusterphone), to assist with intra-cluster messaging. It provides a clean, robust API to pass messages from workers to master, and vice-versa. The README has all the juicy specifics.

So what can you do with clusterphone that you can't do with the built-in Node.js cluster messaging? Here's a short list:

* Dispatch messages to specific handlers on both master and worker ends.
* Acknowledge the receipt and handling of messages.
* Send messages to workers straight away, without worrying about them being online yet (messages are queued and sent when worker is ready).
* Namespace messaging, so your library has no risk of conflicting with other libraries / the application using the messaging layer.
* Acknowledge / wait for acknowledgement API supports either Node-style callbacks or Promises.

I wrote this library because I wanted to trivialize Node.js cluster messaging. I found some existing libraries out there, but none of them had all the features I wanted. Worse, very few of them had enough tests for me to be very confident in them. At the time of writing, clusterphone has 98% test coverage.

If you end up using the library, or have some thoughts about it, please feel free to get in touch!
