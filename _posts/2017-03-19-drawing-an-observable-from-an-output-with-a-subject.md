---
layout: post
cover: false
title: Drawing an observable from an output without using a subject
date:   2017-03-19
subclass: 'post'
categories: 'casper'
published: false
disqus: true
---

When you are implementing something with the reactive paradigm in mind, it's really usefull to be able to draw an observable from an `@Output` from a child component. The way I used to mimic this behaviour before was using a `ReplaySubject` while in fact, we can do this a lot easier. Lets check out how.

## How I used to do it
Before I used a subject to be able to draw an observable from an output of a component.

```typescript

  @ViewChild(GenderFilterComponent) genderFilter;

  ngAfterViewInit() {
    this.genderFilter.filterChange.map(() => "mqlskdfj").subscribe(console.log);
  }

```