---
layout: post
title:  "Beginner Ruby Notes"
date:   2017-01-15 15:39:19 -0500
---


## Trying to transition from Javascript to Ruby.

**1**. Ruby lines do not end with ';' .

**
2**. variables are defined without the 'var' keyword.


**3**. 'if' statements do not use curly braces {}
```

Javascript:

if (1 > 2) {
  false
} else if (1 > 1) {
  false
} else {
  true
}

=======================

Ruby:

if 1 > 2
  false
elsif 1 > 1
  false
else
  true
end

```


**4**. functions do not use curly braces either

```

Javascript:

function funcName(param) {
  param += 1
	return param
}

========================

Ruby:

def funcName(param)
  param += 1
end
	 
```

Notice that not only did we not use curly braces, but also, there is no need to use the 'return' keyword in Ruby.
It will return whatever the last line computes into.


**5**. the ++ and - - shortcuts do not work in ruby.

```

Javascript:

var a = 0;
a++;
console.log(a) //==> 1

========================

Ruby:

a = 0
a++
puts a #==> 0
 
```



**6**. comment are made with '#' not '//'


**7**. parentheses are optional in Ruby
 
```

puts 123   #=>123
puts (123) #=>123

def mirror(e)
  e
end

mirror(123) #=>123
mirror 123 #=>123	

```





