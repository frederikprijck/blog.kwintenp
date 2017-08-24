---
layout: post
cover: false
title: Multicasting operators in RxJS
date:   2017-08-20
subclass: 'post'
categories: 'casper'
published: false
disqus: true
---

With the arrival of RxJS 5.4 a while back, the RxJS team has given us yet another way to support multicasting in our applications. They introduced the `shareReplay` operator. With this new one around the corner, you might start wondering when to use which one. That's what this post is all about.



Categories:

Connectable, Retryable, Repeatable, Replayable(check tests to know for sure)

share replay
false, true, false,