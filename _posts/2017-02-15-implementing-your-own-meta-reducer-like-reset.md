---
layout: post
cover: false
title: Implementing your own meta reducer like reset
date:   2017-02-15
subclass: 'post'
categories: 'casper'
published: false
disqus: true
---

## Implementing your a meta reducer like reset

A few weeks ago, I was asked if it was possible to implement some logic to clear the store, or at least reset is, when a user logged out. If you know what a meta reducer is, this is really easy to implement. I'll show you in the next paragraphs, what a meta reducer is and how we can implement one ourselves. We will create one to reset the store back to it's iniital state as soon as a user logs out.

#### What is a meta reducer?

When u are using Redux or @ngrx/store, you have to implement reducers to teach your store how to update the state. At init time, you have to pass a single reducer to the store, this one is called your root reducer. Of course, you don't put all your logic in a single reducer. 

For this, Redux provides you with a utility method called 'combineReducers'. What this method does for you is turn this:

```typescript
econst usersReducer = () => {....};
const tweetsReducer = () => {....};

const rootReducer = combineReducers({
    users: usersReducer,
    tweets: tweetsReducer
});
```

into the following reducer tree:

