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
If you subscribe to an observable, you are going to start executing that observable. What this means is the observable will start producing values. When you are working with a cold observable, every new subscription will 'restart' the observable's producer. Let's take a look at an example:

<a class="jsbin-embed" href="http://jsbin.com/kilobozuro/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?4.0.4"></script>

Here we can see an interval observable that will emit 5 values with half a second between them. We subscribe to this observable immediately and again after 1,5 seconds. As you can see, when the second subscription happens, it doesn't get the same values as the first subscription. Instead, it starts with the value '0'. 
We can conclude from this that for every subscription, the observable is 'restarted' and the observable will restart the production of values. 

This might feel a little weird in the beginning, but it gives us the benefit to re-use observables, which is a quite powerfull concept once you get the hang of it. It however also introduces some  

**Note**: If you do not know what hot and cold observables mean, you can read this excellent article on the Thoughtram blog <a href="" target="_blank">here</a>.
**Note2:** The fact that an observable is either cold or hot is somewhat debatable as we'll see later on. An observable can also hold properties from both of these states. In the Thoughtram article described above, they point to these observables as being 'semi-hot'.

Categories:

Connectable, Retryable, Repeatable, Replayable(check tests to know for sure)

share replay
false, true, false,