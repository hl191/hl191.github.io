---
layout: post
title:  "Scheduling"
date:   2021-07-15 11:53:46 +0200
categories: coding
---

So I checked out some scheduling mechanisms for a Java application in a clustered environment.

The most popular framework to do this is [Quartz](/java/quartz).

But there are also innate Spring mechanisms to schedule tasks in a cluster such as Kubernetes, Openshift etc.

I sketched out different approaches in my this repository: [quartz-playground](https://github.com/hl191/quartz-playground)
