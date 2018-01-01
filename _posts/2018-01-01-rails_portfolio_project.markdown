---
layout: post
title:      "Rails Portfolio Project"
date:       2018-01-01 19:49:47 +0000
permalink:  rails_portfolio_project
---


It took me some time to decide what I wanted to create, but I settled on something that would be useful for me in my everyday life.
I work in retail, and I spend my time talking to customers on the phone, usually offering some kind of technical support on a very wide variety of products.
So I decided to write a CRUD application that would help my department work together, and share our knowledge with each other.

This seemed simple at first but quickly spiraled out of control! 
Real life is messy, and modeling the data in a way that would be future-proof took some careful thought.

I experimented with Polymorphic Associations.
These are useful when you want to allow a model to belong_to many other models, but without needing to create a join table for each one.
The issue I ran into is that it's not so easy to jump from the polymorphic object itself to its parent, since rails doesn't automatically create that method for you.

Another challange is using the same controller for regular and nested objects (when you want the nested object to be associated with the nesting object).
One way of dealing with this, is just having a messy controller that looks at the params object and behaves accordingly.
Another way, is to create another controller that inherits from the original one. This allows you to just call 'super' when appropiate and remain with a slimmer controller.

I'm looking forward to combining AJAX with rails!
