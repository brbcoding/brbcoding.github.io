---
layout: post
title: "Shorthand Function Queues with JavaScript"
date: 2013-12-12 10:47:36 -0500
comments: true
categories: [javascript, functions, testing]
---

This is a short post explaining the line that blew my mind from John Resig's [Secrets of the JavaScript Ninja](http://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X/). It turns out that it's a cool shorthand way of iterating over and calling multiple (anonymous) functions from a queue. The following is the function in question.

``` javascript queue.js mark:3,3
function runTest() {
  if (!paused && queue.length) {
    queue.shift()();
    if (!paused) {
      resume();
    }
  }
}
```

Let's go ahead and break it out of the original function so that we can see what's actually happening (this block comes from a big test suite, so that's not helpful in this concise example). So, this is what we will be looking at:  

``` javascript
queue.shift()()
```

Before we get into the queue part though, let's take a gander at the [`shift()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift) function. 

{% blockquote %}
The shift method removes the element at the zeroeth index and shifts the values at consecutive indexes down, then returns the removed value.
{% endblockquote %}

``` javascript
// create an array
var arrToShift = [1, 2, 3, 4, 5]
// shift returns the value it removes, so let's log that
console.log(arrToShift.shift()) // 1
console.log(arrToShift) // [ 2, 3, 4, 5 ]
```

Not so useful yet? Ok... how about if we replace the array of integers with an array of functions? 

``` javascript
var queue = [ function(){ return 'foo' },
			  function(){ return 'bar' },
			  function(){ return 'bat' } 
			]

console.log(queue.shift()) // [Function]
```

So our `shift()` did exactly what it did in the first example. It removed *and* returned the value at queue[0], which in this case, was a function. How do we run a function in javascript? By appending `()` to the function, of course! So, now check this out...

``` javascript
console.log(queue.shift()()) // foo
// woohoo! we returned that first function and ran it
```

You should now be able to see how we could use this as I mentioned earlier. Let's run ALL of our functions in the queue.

``` javascript
sLen = queue.length; // starting queue length
for(var i = 0; i < sLen; i++) {
	console.log(queue.shift()())
}
// foo
// bar
// bat
```

That's kind of long though, and this was about shorthand... SO, we can use `shift()` to our advantage here as well. Since the 0th element is REMOVED from the array, we should be able to just check if there is something at the 0th index. If so, we can keep going. This is the shorter version that I came up with.

```
while(queue[0]) { console.log(queue.shift()()); }
// while anything is at the 0th index, continue running
// foo
// bar
// bat
```

Pretty cool, right? We could also accomplish a queue-like system with `map()`, something like `queue.map(function(x){ console.log(x()) })`... That's a different story though. Hopefully you took something away from this post... Feel free to catch up with me (or point out errors) on twitter [@CodyHenshaw](https://twitter.com/CodyHenshaw).