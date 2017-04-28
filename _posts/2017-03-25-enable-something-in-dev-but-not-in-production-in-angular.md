---
layout: post
cover: false
title: Enable in dev but not in production with the Angular CLI
date:   2017-03-19
subclass: 'post'
categories: 'casper'
published: false
disqus: true
---
Using the Angular CLI it's really easy to enable a certain feature in development while removing that feature in production environment. If you, for example, want to use the Redux Devtools during development but not in production, you can easily configure this in any Angular CLI generated project.
Lets see how we can accomplish this!

## The

Use the environment class provided by the angular cli to determine what should be loaded and what not.

