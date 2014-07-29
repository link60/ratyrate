# RatyRate Stars Rating Gem [![endorse](http://api.coderwall.com/wazery/endorsecount.png)](http://coderwall.com/wazery)

A Ruby Gem that provides the same functionality of [jQuery Raty](https://github.com/wbotelhos/raty) library, and adds IMDB style rating.

[![Gem Version](https://badge.fury.io/rb/money-rails.png)](http://badge.fury.io/rb/money-rails)
[![Build Status](https://travis-ci.org/wazery/ratyrate.svg)](http://travis-ci.org/wazery/ratyrate)
[![Dependency Status](https://gemnasium.com/wazery/letsrate.svg)](https://gemnasium.com/wazery/letsrate)
[![Code Climate](https://codeclimate.com/github/wazery/ratyrate.png)](https://codeclimate.com/github/wazery/ratyrate)
[![License](http://img.shields.io/license/MIT.png?color=green)](http://opensource.org/licenses/MIT)
[![Support jQuery Raty](http://img.shields.io/gittip/wbotelhos.svg)](https://www.gittip.com/wazery "Git Tip")

## Repository

This is a fork against the repository [muratguzel/letsrate](https://github.com/muratguzel/letsrate), the aim of this fork is to refresh the development in this Gem with a new scope and features, so please if you have any pull request issue it here.

## Changelog from the main repository

```
1. Exposed a lot of jQuery Raty plugin [features](http://wbotelhos.com/raty)
  1. Added cancel button that can be customized and inserted to left or right
  2. Added the ability to set custom star images for on, half or off state
  3. Added the ability to set a custom path for the images
  4. Added the ability to enable/disable half stars
  5. Added the ability to turn on/off half star
2. User can now disable or enable the rating after the first rate
3. Added a star style to show just the score of the dimension, but this star is not editable
4. Added an overall average star just like IMDB style
3. Nothing else
4. :wq
```

## Detailed view of the new features

![Detailed view of the new featurews](https://dl.dropboxusercontent.com/u/71605080/RatyRate%20Features.png)

## Instructions

### Install

Add the ratyrate gem into your Gemfile

```ruby
gem 'ratyrate'
```

### Generate

```
rails g ratyrate User
```

The generator takes one argument which is the name of your existing devise user model UserModelName. This is necessary to bind the user and rating datas.
Also the generator copies necessary files (jQuery Raty plugin files, star icons and JavaScripts)

Example:

Suppose you will have a devise user model which name is User. The devise generator and ratyrate generator should be like below

```
rails g devise:install
rails g devise user

rails g ratyrate user # => user is the model generated by devise
```

This generator will create Rate and RatingCache models and link to your user model.

### Prepare

I suppose you have a car model

```
rails g model car name:string
```

You should add the ratyrate_rateable function with its dimensions option. You can add multiple dimensions.

```ruby
class Car < ActiveRecord::Base
  ratyrate_rateable "speed", "engine", "price"
end
```

Then you need to add a call ratyrate_rater in the user model.

```ruby
class User < ActiveRecord::Base
  ratyrate_rater
end
```

### Using

There is a helper method which name is rating_for to add the star links. By default rating_for will display the average rating and accept the
new rating value from authenticated user.

```erb
<%# show.html.erb -> /cars/1 %>

Speed  : <%= rating_for @car, "speed" %>
Engine : <%= rating_for @car, "engine" %>
Price  : <%= rating_for @car, "price" %>
```

### Available Options

1- If you need to change the star number, you should use star option like below.
```erb
Speed : <%= rating_for @car, "speed", :star => 10 %>
Speed : <%= rating_for @car, "engine", :star => 7 %>
Speed : <%= rating_for @car, "price" %>
```
2- To enable half stars use the option *enable_half*
```erb
Speed : <%= rating_for @car, "speed", :enable_half => true %>
```
3- To show or hide the half stars use *half_show*
```erb
Speed : <%= rating_for @car, "speed", :half_show => true %>
```
4- To change the path in which the star images (star-on.png, star-off.png, star-half.png, ..etc) are located use
```erb
Speed : <%= rating_for @car, "speed", :star_path => true %>
```

To just change one of the star images choose from these options (star_on, star_off, star_half)

5- To add the cancel button to the left, or right of the stars use **(default is false)**
```erb
Speed : <%= rating_for @car, "speed", :cancel => true %>
```
6- To change the place of the cancel button (left, or right) use **(default is left)**
```erb
Speed : <%= rating_for @car, "speed", :cancel_place => left %>
```
7- To change the hint on the cancel button use **(default is )**
```erb
Speed : <%= rating_for @car, "speed", :cancel_hint => "Cancel this rating!" %>
```
8- To change the image of the cancel on button use
```erb
Speed : <%= rating_for @car, "speed", :cancel_on => "cancel-on2.png" %>
```
9- To change the image of the cancel off use
```erb
  Speed : <%= rating_for @car, "speed", :cancel_off => "cancel-off2.png" %>
```
### Other Helpers

You can use the *rating_for_user* helper method to show the star rating for the user.

```erb
Speed : <%= rating_for_user @car, current_user, "speed", :star => 10 %>
```

And you can use the *imdb_style_rating_for* to show a similar to IMDB rating style.

```erb
Speed : <%= imdb_style_rating_for @car, current_user %>
```

## Feedback
If you find bugs please open a ticket at [https://github.com/wazery/ratyrate/issues](https://github.com/wazery/ratyrate/issues)

