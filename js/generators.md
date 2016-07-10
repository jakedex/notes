# [Generators](https://www.youtube.com/watch?v=QO07THdLWQo) Notes

(Source: [https://gist.github.com/learncodeacademy/bf04432597334190bef4](https://gist.github.com/learncodeacademy/bf04432597334190bef4))

## What are generators

- They're pausable functions, pausable iterable functions, to be more precise
- They're defined with the *
- every time you `yield` a value, the function pauses until `.next(modifiedYieldValue)` is called


```javascript
var myGen = function*() {
  var one = yield 1;
  var two = yield 2;
  var three = yield 3;
  console.log(one, two, three);
};
```
Define the generator and now run it
```javascript
var gen = myGen(); //get the generator ready to run
//when you run next() on a generator, it runs until a yield, then waits until next() is called again
console.log(gen.next()); //{value:1, done: false}
console.log(gen.next()); //{value:2, done: false}
console.log(gen.next()); //{value:3, done: false}
console.log(gen.next()); //{value:undefined, done: true}
console.log(gen.next()); //errors because you can't call next() on a closed generator
```
The only problem here is that the final result it will log will be `undefined, undefined, undefined`
Since yield sits in-between the yielded value and the rest of the function,
we have to pass a value back in for it to get assigned to the variable.
```javascript
console.log(gen.next()); //{value:1, done: false}
console.log(gen.next(1)); //{value:2, done: false}
console.log(gen.next(2)); //{value:3, done: false}
console.log(gen.next(3)); //{value:undefined, done: true}
```
So yippee, when do I ever have to yield numbers?<br/>
At first generators seem somewhat useless<br/>
The magic happens when smarter code wraps the generator<br/>
Here's a pretty dumb version of a smart wrapper (full code at bottom of gist)
```javascript
function smartCode(generator) { //give me a generator function
  var gen = generator();//start up the generator
  var yieldedVal = gen.next().value;//get the first yielded value
  if(yieldedVal.then) { //is it a promise?
    //it's a promise!!!
    yieldedVal.then(gen.next);//wait for it to resolve, then pass the resolved value back in
  }
}
```

So, let's use a library with the smarts, like Bluebird, Co, Q
```javascript
//Bluebird
Promise.coroutine(function* () {
  var tweets = yield $.get('tweets.json');
  console.log(tweets);
})();
//Bluebird runs the generator, notices yield is a promise
//so it waits on that promise, then passes it's value back to the generator when complete

//here, it runs them in sequence, waiting for each to complete before proceeding
Promise.coroutine(function* () {
  var tweets = yield $.get('tweets.json');
  var profile = yield $.get('profile.json');
  var friends = yield $.get('friends.json');
  console.log(tweets, profile, friends);
})();
```

AWESOME!
If you want to run them at the same time, yield an object or an array.
```javascript
//Bluebird needs a little pre-config to yield arrays,
//add this setup codesomewhere in your app
Promise.coroutine.addYieldHandler(function(yieldedValue) {
    if (Array.isArray(yieldedValue)) return Promise.all(yieldedValue);
});


Promise.coroutine(function* () {
  var [tweets, profile] = yield [$.get('tweets.json'), yield $.get('profile.json')];
  console.log(tweets, profile);
})();

//or set it up to yield an object and run this

Promise.coroutine(function* () {
  var data = yield {
    tweets: $.get('tweets.json'),
    profile: yield $.get('profile.json')
  };
  console.log(data.tweets, data.profile);
})();
```


**Here's that full code of a generator wrapper
```javascript
function smartCode(generator) {
  return function() {
    var gen = generator.apply(this,arguments);

    function handleNext(yielded) {
      if (yielded.done) return yielded.value; //return final return value

      if (yielded.value.then) {
        return yielded.value.then(function(res) {
          return handleNext(gen.next(res));
        }, function(err) {
          return handleNext(gen.throw(err));
        });
      } else {
        return handleNext(gen.next(yielded.value));
      }
    }
  }
}
```
