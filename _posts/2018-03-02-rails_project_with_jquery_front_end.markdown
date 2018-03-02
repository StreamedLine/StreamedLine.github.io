---
layout: post
title:      "Rails Project With JQuery Front End"
date:       2018-03-02 15:41:03 -0500
permalink:  rails_project_with_jquery_front_end
---


## Using AJAX In Rails

### Ingredients
* Rails
* jquery-rails Gem
* active_model_serializers Gem

### Directions

#### Step 1
##### Install the Gems
Add these 2 gems to your Gemfile
* jquery-rails Gem
* active_model_serializers Gem

In the console: run `bundle install`

#### Step 2
##### Create the Serializers
Create a new folder: `app/serializers`

In this folder you will create a serializer for each model you want turned into Json.

Example: if a model is called **Category**

`app/serializers/category_serializer.rb`

```
class CategorySerializer < ActiveModel::Serializer
  attributes :id, :name, :updated_at
  has_many :tags
  has_many :items
end
```

Notice the associations to **Tag** and **Item**

Even if they are actually joined with a join table, the above serializer will still work!!

#### Step 3
##### Tweak the controller to return Json
```
class CategoriesController < ApplicationController
  before_action :authenticate_user!

  def index
	@categories = Category.all
    respond_to do |format|
      format.html {render :index}
      format.json {render json: @categories}
    end
  end

  def show
	@category = Category.find(params[:id])
    respond_to do |format|
      format.html 
      format.json {render json: @category}
    end
  end
	
	...
	
end
```
It's as simple as that!

#### Step 4
##### AJAX 

in `app/assets/javascripts` create a new .js file

example: `categories_index.js`

In the file I'll add an event that will fire when the page loads.

```
$( document ).on('turbolinks:load', function(){
	if (location.pathname.match(/categories/)) {
		$.getJSON('/categories', function(response){
		  // Do something with response!!
	  });
	}	
})

```

In the above example, the Ajax call was triggered by a page load event.
Of course such a call could be used anywhere.
One common pattern is to hijack a buttons click event:

```
$('form#new_category').on('submit', function(e){
		e.preventDefault();
		//ajax post request
});
```

`e.preventDefault();` stops the regular behavior from happening (in this case submitting the form) and allows us to make a request to the server without reloading the page.

