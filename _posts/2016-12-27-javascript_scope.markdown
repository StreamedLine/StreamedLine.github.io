---
layout: post
title:  "Javascript Scope"
date:   2016-12-27 04:38:31 +0000
---


## What is scope?
If a variable is *in scope* this means that I have access to it. For a function to be *in scope*, it needs to be callable.
for example:
```
1.  function anonymous(){
2.    var foo = 3
3.	
4.    console.log(foo) //=> 3; because foo is in scope
5.  }
6.
7.  console.log(foo) //=> Uncaught ReferenceError: foo is not defined; because foo is not in scope
```

The function declared in line 1 has its own scope. var foo was declared within that scope and can only be accessed within that scope.

## The Global Scope
If a variable is not declared within any function it is called a *global variable*. Global Variables, which are declared in the *global scope* are in danger of being overwritten by variables with the same name. Even if we are very careful, they might get overwritten by variables in other applications that are running in the browser!
It is therefore customary and a best practice to have as few global variables as possible.

## Creating Scope
Creating a new scope in javascript is easy: just create an anonymous function! also know as iife (Immediately Invoked Function Expressions).
An iife is created as follows:
```
1. (function(){
2.    //some code
3. })();
```

A function is created and immediately invoked! some people think it's nicer to write it like this.

```
1. (function(){
2.    //some code
3. }());
```

David Crockford has a particular way of describing the apprentices hanging out over the side. (you can google it..)

This can be useful in unexpected ways! 
consider the following code:

```
1. for (var i = 0; i < 8; i++) {
2.   window.setTimeout(function(){console.log(i), 1000})
3. }
```

What do you think the output will be?

It will actually be -
8
8
8
8
8
8
8
8

Yup, I'm not kidding.

now consider this:

```
1. for (var i = 0; i < 8; i++) {
2.   (function(x){
3.     window.setTimeout(function(){console.log(x), 1000})
4.   }(i))
5. }
```

The output is now:
0
1
2
3
4
5
6
7

The function in the *setTimeout* will only get invoked after the for loop is over. And since it is referencing the **i** variable after the* for loop* is done, it will equal 8.

In the second example we created a local variable **x** which equaled whatever **i** was at the time it was invoked, therefore when *setTimeout* fires it will still equal that number.

So scope can see the outside world but cannot be accessed by it, but the above example uses scope to shield from the outside world.. Now that is pretty cool!!

Hope that wasn't too mind bending.. if it was, just disregard the last part and it will plant seeds for the future.
Happy coding!




