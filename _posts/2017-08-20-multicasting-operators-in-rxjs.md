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

## What is multicasting

First of all, I would like to go a litlle deeper into the subject of multicasting. What does this really mean. As you hopefully know, observable can be divided into two categories, hot and cold. 
If you subscribe to an observable, you are going to start executing that observable. What this means is the observable will start producing values. Let's take a look at an example:



**Note**: If you do not know what hot and cold observables mean, you can read this excellent article on the Thoughtram blog <a href="" target="_blank">here</a>.
**Note2:** The fact that an observable is either cold or hot is somewhat debatable as we'll see later on. An observable can also hold properties from both of these states. In the Thoughtram article described above, they point to these observables as being 'semi-hot'.

Categories:

Connectable, Retryable, Repeatable, Replayable(check tests to know for sure)

share replay
false, true, false,