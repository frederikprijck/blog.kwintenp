---
layout: post
cover: false
title: How to setup marble testing
date:   2017-02-15
subclass: 'post'
categories: 'casper'
published: true
disqus: true
---

In an earlier blogpost, I showed you guys how to do client side filtering with streams (<a href="http://blog.kwintenp.com/client-side-filtering-with-streams/" target="_blank">here</a>). I tried to show you how you could use marble diagrams to draw out how the data will flow in your streams. Turns out that drawing your marble diagrams up front can help you a lot in testing your code as well. Using the marble diagram testing provided by RxJS, we can easily test the code we've written in the previous post. Let's see how.