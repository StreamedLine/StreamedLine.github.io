---
layout: post
title:      "CLI Data Gem Project"
date:       2017-02-09 18:46:12 -0500
permalink:  cli_data_gem_project
---


I'm almost done my project, and I've learned a lot. 

One thing that is now firmly part of my brain, is the file structure of a basic ruby project.
lib, bin and gemfile (not to mention gemfile.lock..) used to be a blur in my brain.

The '**bin**' folder is what contains my *entry-point* into the program.
The '**lib**' folder contains my code.

My code requires externel dependencies in order to work.
This means two things:
1. I need to have those dependencies installed on my computer.
2. I need to 'require' them in my code.

At first I was manually typing 
```
$> gem install nokogiri
$> gem install launchy
$> gem install clipboard
$> gem install colorize
```

every single time... this was very annoying...

And then it clicked- **bundler install**!! that's the solution!
No more will my brain glaze over at the mention of bundler.

So that's why a gemfile is so useful.
My life is better now.

I do wish I would have started my project by creating a gem and not tried to convert it to a gem later.


