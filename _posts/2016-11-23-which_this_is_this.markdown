---
layout: post
title:  "Which This Is This"
date:   2016-11-22 22:43:58 -0500
---


A concept not always completely clear in javascript is the *this* keyword.
Note: to fully appreciate this (no pun intended) you'll need to understand javascript **scope**.

Let's start with the global scope - 
```
//global scope

var foo = 'baz';

console.log(this) // => Window {speechSynthesis: SpeechSynthesis, caches: Cac…}

console.log(this.foo) // => "baz"
```

What's *this*? the above example shows us that in the global scope *this* refers to the Window object.
Note that global variables are actually properties of the Window object. In the above example console.log(foo) would have also printed "baz" into the console.

Now let's define a function named inner_scope, what does *this* refer to within the function?

```
//global scope

var foo = 'baz';

function inner_scope() {
  var foo = 'will not be accessed';
	
  console.log(this.foo);
}

inner_scope() // => "baz"
inner_scope.call( {foo: 'this is the this.foo that will be accessed'} ); // => "this is the this.foo that will be accessed"

console.log(this) // => Window {speechSynthesis: SpeechSynthesis, caches: Cac…}
console.log(this.foo) // => "baz"
```

We see that *this* in *inner_scope* changed depending on how the function was called.

When we invoked the function in the regular way, *this* referred to the Window object.
When invoked it with the *call* method, the parameter we passed to the function became our *this*.


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
An inner scope will revert back to the window object no matter what *this* in the containing scope refers to.

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





