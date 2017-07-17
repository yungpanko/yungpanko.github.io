---
layout: post
title:  "Quit being difficult and just tell me what the hell a closure is"
date:   2017-07-02
---

> functions in JavaScript form closures. A closure is the combination of a function and the lexical
> environment within which that function was declared. (Mozilla Developer Network)

Great. We can all go home now.

…..I’m kidding.

We’re going to look at some code but let’s break down what this definition is trying to tell us. *“a function is a closure”* — cool — , and *“a closure is the combination of a function and the lexical environment within which that function was declared.”* This means that functions in JavaScript are more aware of their surrounding than functions or methods in other languages that do not have closures. JavaScript functions are familiar with the variables that exist in the environment where we create them.

If you employ the services of google to help you understand what a closure is, you will likely come across code examples with nested functions. There is a valid reason for this, as these functions help to demonstrate how different environments can change our closures, but the definition above explains that **ALL** functions are closures. We don’t have to get fancy to explain what the hell this thing really is.

In my first example, I am declaring a variable, *name*, with the value of my name. Then, I am writing a function, *printName*, that console logs the name variable that I declared above it. If you test this out yourself, you will see that it works.

![img1]({{ site.url }}/assets/images/qbd1.png)

It may seem obvious that this works but — look closely — we never called our *printName* function with an argument. What’s remarkable about what this function is doing is the very thing that makes it a closure. Our function was able to grab the name variable declared outside of itself, and within the global environment, to complete our operation.

## Now we understand what a closure is but how and why would we use it?
### Private methods and module pattern

I’m going to cover two examples where your newfound understanding of closures can help. The first is private methods. A private method in JavaScript is a function that can only be accessed through another function. A quick example is below.

![img2]({{ site.url }}/assets/images/qbd2.png)

Here, I have defined a function, *publicFunction*, that returns another function, secretFunction. Both of these functions are closures, by definition, but only *publicFunction* can be readily called by itself. When we try to console log our *secretFunction*, we are told that it is not defined.
In *publicFunction*, I have employed a syntax that will be familiar if you have dealt with objects in JavaScript. By writing the return for *publicFunction* as *“function name: function,”* or in module pattern, we are able to call the inner function by chaining our call, similar to how we would retrieve attributes from an object. Let’s see that in action.

![img3]({{ site.url }}/assets/images/qbd3.png)

JavaScript’s use of closures allows us to hide our secretFunction from the rest of our global scope and even reuse the name in other functions.

### Partial application and currying

Understanding closures is also important for understanding the mechanics of partial application and currying. When we pass arguments into functions that return functions, our return functions, or closures, are aware of these arguments.

Let’s examine the code below.

![img4]({{ site.url }}/assets/images/qbd4.png)

Here, I am defining a function, *multiplyNumbers*, that accepts two numbers and returns their product. I have written this function to return another function in the case that it only receives one argument. This return function, or closure, can access the first variable that we gave our outer function, *multiplyNumbers*, and complete our operation. At the bottom of the screenshot, you can see that both ways (passing both arguments into the outer function AND passing the first argument to the outer function and the second to the inner function) return the same result.

We can supply our outer function only one argument and name the resulting function (see below).

![img5]({{ site.url }}/assets/images/qbd5.png)

I believe that the power of closures truly shines here. Our named methods, *multiplyByFive* and *multiplyByFour*, were birthed by the same function, *multiplyNumbers*. They only differ in the environment scope that they refer to. The first argument for *multiplyByFive* is still 5, even after the creation of an additional function, *multiplyByFour*, that takes in a different first argument. Pretty cool, right?

Thanks for reading this. I hope you’ve learned that functions in JavaScript can be more than meets the eye. Below are additional resources on closures and how understanding them becomes useful in functional programming.

## Additional resources:

1. [Master the JavaScript Interview: What is a Closure?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36)

2. [MDN: Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)

3. [JavaScript Modules: A Beginner’s Guide](https://medium.freecodecamp.org/javascript-modules-a-beginner-s-guide-783f7d7a5fcc)
