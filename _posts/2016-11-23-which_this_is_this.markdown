---
layout: post
title:  "Which This Is This"
date:   2016-11-23 03:43:58 +0000
---


A concept that isn't completely clear when starting out with javascript is the *this* keyword.
In order to fully appreciate this (no pun intended) a firm understanding of **scope** in javascript is needed.

The following sentence is very important and I will explain it:
>     What the *this* keyword in a given scope will point to, is determined by the way the scope is invoked.

What does that mean...?
It's example time:

```
//global scope

var foo = 'baz';

console.log(this) // => Window {speechSynthesis: SpeechSynthesis, caches: Cac…}

console.log(this.foo) // => "baz"
```

What's *this*? the above example shows us that in the global scope *this* points to the Window object.
Note that global variables are actually properties of the Window object. In the above example console.log(foo) would have been the same thing.

Yay! another code snippet!

```
//global scope

var foo = 'baz';


function inner_scope() {
  var foo = 'will not be accessed' ;
	
	console.log(this.foo);
}

inner_scope.call( {foo: 'this is the this.foo that will be accessed'} ); // => "this is the this.foo that will be accessed"
inner_scope() // => "baz"

console.log(this) // => Window {speechSynthesis: SpeechSynthesis, caches: Cac…}
console.log(this.foo) // => "baz"
```

We see that *this* in *inner_scope* was defined by the way the function was called.

When invoked with the *call* method, the parameter we passed to the function became our *this*.
When we invoked the function in the normal way, however, *this* still referred to the Window object.

Let's consider one more example:

```
//global scope

var foo = 'baz';


function inner_scope() {
  var foo = 'will not be accessed' ;
	
	console.log(this.foo);

    (function(){console.log(this.foo)}()); // What will this write to the console..?
}

inner_scope.call( {foo: 'this is the this.foo that will be accessed'} ); 

```

The first `console.log(this)  ` will return "this is the this.foo that will be accessed" just like we'd expect.
But what do you think the second `console.log(this.foo)  ` will return?


If you answered "baz" then you are correct. *this* was pointing to the Window object.
The lesson here is that *this*, unlike other variables, **cannot be accessed from an inner scope**
An inner scope will revert back to the window object no matter what *this* in the containing scope is pointing to.

### So how do I control *this*?
I'm glad you asked.

**O**ne way of setting the *this* of a scope has been covered in the above example.
  `function_name.call('my this')` 
	you might be familiar with .apply and .bind which for our purposes will do the same thing but are beyond the scope of    
	this humble post.

**A**nother way is by invoking a method through the containing object (simpler than it sounds)
  ```
var myObject = {
	  myProperty: 'hi!',
	  myMethod: function() { console.log(this.myProperty) }
	};

myObject.myMethod() // => "hi!"
```

But beware...

  ```
var myObject = {
	  myProperty: 'hi!',
	  myMethod: function() { console.log(this.myProperty) }
	};

var func_ref = myObject.myMethod;

func_ref() // => undefined
```

func_ref is a reference to the function, but not to the method that we originally wrote the function on.

**A**nd finally when invoking a function using the *new* keyword *this* is the new object returned by the function
```
function Monster(eyes) {
   this.type = 'Monster';
	 this.who = eyes + ' eyed monster! aarrggghhh! hungry!';
}

var scary = new Monster(3)
console.log(scary.who) // => "3 eyed monster! aarrggghhh! hungry!"
```


And that's basically it!

##### The End.





