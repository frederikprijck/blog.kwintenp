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
If you subscribe to an observable, you are going to start executing that observable. What this means is the observable will start producing values. When you are working with a cold observable, every new subscription will 'restart' the observable's producer. 

**Note**: If you do not know what hot and cold observables mean, you can read this excellent article on the Thoughtram blog <a href="" target="_blank">here</a>.
**Note2:** The fact that an observable is either cold or hot is somewhat debatable as we'll see later on. An observable can also hold properties from both of these states. In the Thoughtram article described above, they point to these observables as being 'semi-hot'.

Let's take a look at an example:

<a class="jsbin-embed" href="http://jsbinqsdf.com/kilobozuro/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?4.0.4"></script>

Here we can see an interval observable that will emit 5 values with half a second between them. We subscribe to this observable immediately and again after 1,5 seconds. As you can see, when the second subscription happens, it doesn't get the same values as the first subscription. Instead, it starts with the value '0'. 
We can conclude from this that for every subscription, the observable is 'restarted' and the observable will restart the production of values. 

This might feel a little weird in the beginning, but it gives us the benefit to re-use observables, which is a quite powerfull concept once you get the hang of it. It however also introduces some weird side effects. Let's take a look at an example:

<a class="jsbin-embed" href="http://qsdfjsbin.com/xejojucicu/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?4.0.4"></script>

```typescript
const getCharacter = () => {
  return fetch('https://swapi.co/api/people/1', {method: 'get'})
          .then(response => response.json());
}

const getLuke$ = Rx.Observable.of('')
  .mergeMap(() => getCharacter());

const name$ = getLuke$
  .map(char => char.name);

const age$ = getLuke$
  .map(char => char.gender);

name$.subscribe(console.log);
age$.subscribe(console.log);

```
 
We create an observable, `getLuke$`, which will perform a call to fetch the character of Luke Skywalker from the swapi.co API. We use this as a source to create two new observables. One holds the name of the character, the other one holds the gender of the character. We immediately subscribe to both of the observables. If you open your devtools onto the network tab, you will see that there are acutally two network request being performed. 
This might seem weird at first, but in fact, it's quite logical. The `getLuke$` observable we created is a cold one. The two new observables we create both use this one as a source. So in fact, subscribing to our `gender$` and `name$` observable, is the equivalent of subscribing to the `getLuke$` observable twice. And, as we have seen above, every subscription to a cold observable, will trigger two executions of the observable, two times the production of values, two network requests.

While this behaviour can be usefull, sometimes you might want two backend calls, it can also be quite annoying. The problem that we are facing here is that the execution of the observable is restarted on every subscription. While sometimes, we want to share the underlying subscription. Sharing the underlying subscription is what multicasting is all about. 

### Multicasting example

Let's change our example to share the underlying subscription. For this we will use the `share` operator for now. We will investigate all the other ones later on.

<a class="jsbin-embed" href="http://qsdfjsbin.com/vejaqorixa/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?4.0.4"></script>

If you run this example while opening your devtool's network tab, you can see that there is only one request. That's because the underlying subscription 

Categories:

Connectable, Retryable, Repeatable, Replayable(check tests to know for sure)

share replay
false, true, false,