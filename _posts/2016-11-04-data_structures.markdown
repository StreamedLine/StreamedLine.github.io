---
layout: post
title:  "Data Structures"
date:   2016-11-04 20:48:06 +0000
---

Disclaimer: this post is aimed at the begginer who has seen all the basic syntax of Javascript (if statements, loops) but is just starting to make his/her own projects.

## What is a data structure?

If you have coded for more than a few weeks you are probably already using them. for example, an Array is a data structure.

A data structure is a way of organizing information, and different structures will be suitable for different tasks.

## Examples

Let's look at Arrays and Objects in javascript:

```
var digits = [1, 2, 3]

for (var i = 0; i < digits.length; i++) {
  console.log(nums[i] + '; ') 
}

//logs=> 1; 2; 3; 
```

This is a great way to store the digits 1,2 and 3.
Now, if I wanted each number to be associated with a name things get a little more complicated:

```
var digits = [1, 2, 3];

var names = ['name1', 'name2', 'name3'];

for (var i = 0; i < digits.length; i++) {
  console.log(names[i] + ': ' + digits[i] + ';') 
}

//logs=> name1: 1; name2: 2; name3: 3;
```

We now have 2 seperate variable, *digits* is storing the digits and *names* is storing the names. The problem is that the more variable we have the more messy our program can become.

This is where object might make things more simple:

```
var people = [{name: 'name1', digit: 1}, {name: 'name2', digit: 2}, {name: 'name3', digit: 3}]
 
for (var i = 0; i < people.length; i++) {
  console.log(people[i].name + ': ' + people[i].digit + ';') 
}

//logs=> name1: 1; name2: 2; name3: 3;
```

We now have everything stored in one array which can be more easily passed to a function.
consider:

```
var people = {
  digits: [1, 2, 3],
  names: ['name1', 'name2', 'name3']
}
```

This also accomplishes the same goal of having one object to pass to a function.

## So When Do I Use What?
The short answer is: it depends.
The long answer is: practice makes perfect.

When we read other peoples code we will notice new ways of organizing code, and when our code starts getting too messy or complicated we start appreciating what 'best practices' are there for. So although we don't need to reinvent the wheel, actually getting stuck while writing code is probably the best way to cement the proper 'best practices' into our code.

## Conclusion

Write a lot of code, get stuck, pay attention to best practices, and choosing the correct data structure will become more intuitive.




