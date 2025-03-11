---
title: "Roll Your Own Debounce"
date: 2025-03-11T21:32:15+10:00
draft: false
tags: ["JavaScript", "Roll Your Own", "TypeScript", "Debounce"]
---

Debounce is a technique used to ensure that a function is not called more than once in a given time period. This can be useful when dealing with events that fire rapidly, such as scroll or resize events, or input events that might trigger API calls. 

Alot of people import 3rd party libraries to handle this, but it's actually quite simple to implement yourself. So, in this post, we'll look at how to roll our own debounce functionality in JavaScript.

## The Debounce Function
Here's a simple implementation of a debounce function and an example of how to use it:

```javascript
    function debounce(functionToDebounce: Function, delay: number) {
      let timeoutId: ReturnType<typeof setTimeout>
      return function (...args: any) {
        clearTimeout(timeoutId)
        timeoutId = setTimeout(() => functionToDebounce(...args), delay)
      }
    }

    const handleResize = debounce((val: string) => {
      console.log(val)
    }, 1000)

    window.addEventListener('resize', () => handleResize("resize"))
``` 

In this example, we create a `debounce` function that takes a function and a delay time as arguments. The `debounce` function returns a new debounced/wrapper function that accepts any number of arguments. 

When called, this newly returned wrapper function's job is to call the originally desired function after the specified delay time has passed, passing along any arguments to the originally desired function.

If the newly returned wrapper function is called again before the delay time has passed, the previous timeout is cleared and a new one is set. This ensures that the originally desired function is only triggered once, after the specified delay time has passed in its entirety without having been called again.

Let's break things down further by stepping through an example:

1. We define our `debounce` function
2. We create a `handleResize` function, which is the debounced/wrapper version of the function we want to call.
3. We add an event listener to the window's `resize` event.
4. The `handleResize` wrapper function is called with the argument `"resize"` when the window's resize event triggers. 
5. The debounced version of our desired function is called after the specified delay time has passed without the function being called again.

It's quite a neat little implementation and not too difficult to get your head around after stepping through a few times. 

Don't immediately reach for lodash just for debounce. Consider rolling your own. 