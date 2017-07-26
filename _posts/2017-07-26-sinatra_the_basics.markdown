---
layout: post
title:  "Sinatra, the Basics"
date:   2017-07-26 04:13:26 +0000
---

## What we will do -
## Create a simple app that starts a server, and serves some text to our browser.
### file tree-
```
basicApp
|--config.ru
|--sinatraApp.rb
```
## Step 1
### Install Sinatra

In the the terminal, type 'gem install sinatra' like so:
```
console//> gem install sinatra  
Successfully installed sinatra-2.0.0
Parsing documentation for sinatra-2.0.0
Done installing documentation for sinatra after 1 seconds
1 gem installed
```
## Step 2
### Create The config.ru File

in the config.ru file we will add 3 lines of code.
```
1   require 'sinatra'
2   require './sinatraApp.rb'
3 
4   run ApplicationController.new
```
You might have noticed that line 2 is requiring a file that doesn't exist! let's create it now!

## Step 3
### Create The sinatraApp.rb File

we will add lines of code.
```
1   class ApplicationController < Sinatra::Base
2    	 get '/' do
3    		   erb "Hello World!"
4  	   end
5   end
```
## We did it!
### Run The Program

In the terminal, type 'rackup' like so:
```
console//> rackup
[2017-07-25 23:53:03] INFO  WEBrick 1.3.1
[2017-07-25 23:53:03] INFO  ruby 2.3.0 (2015-12-25) [x86_64-darwin16]
[2017-07-25 23:53:03] INFO  WEBrick::HTTPServer#start: pid=4051 port=9292
```

## See It In The Browser
Type http://localhost:9292/ into the address bar of your favorite browser!

The browser will display:

Hello World!
