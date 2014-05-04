---
layout: post
title: "Reasons why AWS Elastic Beanstalk Sucks"
date: 2013-05-16 20:22
comments: true
categories: 
 - PaaS
 - Heroku
 - Elastic Beanstalk
---

So I've been using Amazon Web Services Elastic Beanstalk for a few PHP and
Java apps. I've decided I definitely don't like it. Here's why.

Well actually, a quick bit of background. I love how straightforward and 
powerful Heroku is (and I can maybe even forgive them for that whole dyno 
routing debacle), but the dealbreaker for me is it being US-based. I live in 
Australia, and while our routing to the East Coast isn't terrible, it's still
not ideal to serve a predominantly Australian website from there.

Small history lesson aside, here are the main reasons why I dislike Elastic
Beanstalk.

## Slow

Okay okay, this might be quibbling a bit, because any kind of orchestrated
deployment platform like Beanstalk/Heroku is _probably_ much faster than even
the most experienced sysadmin could run up a LAMP stack, configure it, and 
deploy your crappy PHP app to. That said, Beanstalk is quite painfully slow to
start up a new app, or make changes to, especially when you compare it to 
Heroku.

## Weird

Vague title yes, but allow me to explain. Elastic Beanstalk does things I just
don't understand:

 * Destroys and recreates EC2 images unnecessarily. Why do I need a whole new
   instance when I simply change a security group?
 * Why does `git aws.push` repush the entire repo if there was no changes since
   last push?

Some of these might just be me doing things wrong, but that ties in well with
my next point, and it's the big one.

## TERRIBLE Documentation

Oh my GOD. AWS has notoriously bad documentation in general, but Elastic 
Beanstalk __HAS__ to be an elaborate joke Amazon is playing on the world. What
little documentation there actually is on entire swathes of functionality 
provided by Elastic Beanstalk is chaotically organized. There's two different
command line toolsets available to interact with Elastic Beanstalk. The newer
one has tragic documentation coverage, but is quite powerful when you scrounge
enough information on how to use it.

I really cannot overstate how poor the Elastic Beanstalk documentation is. It's
extremely frustrating as I've been spoiled by fairly excellent documentation
resources on the internets. Again, contrast Elastic Beanstalk with Heroku on
the documentation front - there's really no comparison.

## Okay, Some Positives

So as much as Elastic Beanstalk can be frustrating, it does have some positive
aspects. It's a great way to deploy applications to AWS, when comparing to
tedious approaches like manually setting up an AWS environment, or using complex
solutions like Netflix Asgard, or CloudFormation. Also, it really is the only
decent PaaS available in Australia.

I have noticed that Elastic Beanstalk has been receiving fairly frequent 
updates and improvements, so perhaps the shortcomings in documentation for it
could be attributed to the velocity in which the core service is being iterated
on.

## /rant

As much as I don't like Elastic Beanstalk in its current state, I will continue
to use it for applications I develop/maintain that have a predominantly
Australian audience. I will cross my fingers and hope that Elastic Beanstalk
service and documentation improve over the coming months, or that AWS OpsWorks
evolves to be a better alternative.
