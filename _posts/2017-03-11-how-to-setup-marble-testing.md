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

### Setting up the marble diagram testing

The steps to set this up are really easy. First we need to copy two files from the rxjs source code into our own codebase. This is the `marble-testing.ts` and `test-helper.ts` file which you can find <a href="https://github.com/ReactiveX/rxjs/tree/master/spec/helpers" target="_blank">here</a>.
The next thing you need to do import these files in a test where you want to use the marble testing, and that's it :)!

### Example

The marble diagram for the example looks like this:

![marble-diagram](https://www.dropbox.com/s/zhj0xvz6d5e84m4/Screenshot%202017-03-04%2016.12.24.png?raw=1)

We have a stream containing the characters and one containing a value to filter the characters based on the gender. We use the `combineLatest` to create a new stream which hold the filtered characters.