---
layout: post
cover: false
title: How to setup marble testing
date:   2017-02-15
subclass: 'post'
categories: 'casper'
published: false
disqus: true
---

In an earlier blogpost, I showed you guys how to do client side filtering with streams (<a href="http://blog.kwintenp.com/client-side-filtering-with-streams/" target="_blank">here</a>). I tried to show you how you could use marble diagrams to draw out how the data will flow in your streams. Turns out that drawing your marble diagrams up front can help you a lot in testing your code as well. Using the marble diagram testing provided by RxJS, we can easily test the code we've written in the previous post. Let's see how.

### Setting up the marble diagram testing

The steps to set this up are really easy. First we need to copy two files from the RxJS source code into our own codebase. This is the `marble-testing.ts` and `test-helper.ts` file which you can find <a href="https://github.com/ReactiveX/rxjs/tree/master/spec/helpers" target="_blank">here</a>.
The next thing you need to do is import these files in a test where you want to use the marble testing.

```typescript
import "./helpers/test-helper.ts";
// I'll come back to these imports later
import { hot, cold, expectObservable, expectSubscriptions } from './helpers/marble-testing';
```

That's it, you are ready to start testing!

### Example

The marble diagram for the example looks like this:

![marble-diagram](https://www.dropbox.com/s/zhj0xvz6d5e84m4/Screenshot%202017-03-04%2016.12.24.png?raw=1)

We have a stream containing the characters and one containing a value to filter the characters based on the gender. We use the `combineLatest` operator to create a new stream which hold the filtered characters. The code to create this stream based on the two input streams looks like this:

```typescript
public createFilterCharacters(
        filter$: Observable<string>,
        characters$: Observable<StarWarsCharacter[]>) {
  return characters$.combineLatest(
    filter$, (characters: StarWarsCharacter[], filter: string) => {
      if (filter === 'All') {
        return characters;
      }
      return characters.filter(
            (character: StarWarsCharacter) =>
              character.gender.toLowerCase() === filter.toLowerCase()
      );
  });
}
```

Trying to test this code without using marble diagram testing is quite verbose. First of all, we would need to create two streams ourselves to mock the input streams. Then we would need to feed them to the method and take back the resulting stream. In our test, we would have to subscribe ourselves to this stream to check if the resulting next events are the ones we expect. We can write this a lot easier using marble diagram testing. Let's take a look at the code.

```typescript
describe('component: ClientSideFilterComponent', () => {
  it('on createFilterCharacters', () => {
    // we define a few values where the key will be used later
    // on to denote an observable value
    const values = {a: 1, b: 2, c: 3, d: 4};
    // using this cold method we imported above we can create
    // cold stream likes this
    const a = cold(' a-----b-----c----|', values)
    const asub = ( '^-----------------!')
    const b = cold('---------d----------|', values)
    const bsub = '^-------------------!'
    const expected = '-a-----b-d---c------|'

    expectObservable(a.merge(b).take(5)).toBe(expected, values);
    expectSubscriptions(a.subscriptions).toBe(asub);
    expectSubscriptions(b.subscriptions).toBe(bsub);
  });
});

```