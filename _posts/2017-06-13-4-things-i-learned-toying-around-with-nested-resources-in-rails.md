---
layout: "post"
title: "4 things i learned toying around with nested resources in Rails"
date: "2017-06-13 20:19"
author: Jared Johnson
---

Let’s table set — what is a nested resource?

I’m referring to a type of routing mechanism available to use in Ruby on Rails. The _‘resources’_ syntax is a useful way to have Rails generate each of the CRUD routes for you. Take a look below.

![config/routes.rb in my rails application](/assets/images/nested1.png)
_config/routes.rb in my rails application_

Here, in my _config/routes.rb_ file, I am using the _‘resources’_ keyword to draw routes for my _‘Artist’_ model. Now, when I run _‘rake routes,’_ I can see that the following routes have been generated for me.

![‘rake routes’ returns the full list of rails routes to your terminal — ‘rake’ is a ruby gem that is required for this call](/assets/images/nested2.png)
_‘rake routes’ returns the full list of rails routes to your terminal — ‘rake’ is a ruby gem that is required for this call_

If i want to expand my model to include songs, I have some choices to make. I could have Rails generate a suite of routes beginning with _‘/songs’_ for me, just as I have done with artists OR I could choose to nest these routes underneath those that I have already drawn for artists. The latter would look like this.

![Here, I am passing my songs resources in as a block underneath ‘artists’](/assets/images/nested3.png)
_Here, I am passing my songs resources in as a block underneath ‘artists’_

The nested approach provides me with the following list of routes.

![routes](/assets/images/nested4.png)

And here lies the first thing that I learned about nested routes.

## #1 The :id is appended with the name of previous model at each level of nesting.

My _‘/artists/:id’_ convention becomes _‘/artists/:artist_id/songs/:id’_ once I navigate into my song routes. Why is this syntax change important? Now when my application receives a request to any of the actions defined in my SongsController, an artist ID is passed to me in the format of _‘params[:artist_id].’_

If I want my _songs#index_ action to display a collection of songs that belong to the artist that I am navigating under, I will need to pass _‘params[:artist_id]’_ in as an argument to stipulate that I only want songs from the artist who’s ID matches (see below).

![app/controllers/songs_controller.rb](/assets/images/nested5.png)

## #2 The ‘form_for’ Rails helper method requires you to pass in an object for each level of nesting.

Rails comes pre-loaded with a bunch of different useful helper methods, one of which is _‘form_for,’_ which assists with the routing for model-based form input.

Typically, I would use an instance of a model as the sole argument in a form. When we create a new song, with the models outlined earlier, what we are really doing is creating a new song object that belongs to an artist object. Therefore, without letting our _‘form_for’_ element which artist we want to relate the form input to as well as which song, our ‘form_for’ model will not work. An example of my form for creating a new song is below.

![form_For](/assets/images/nested6.png)

## #3 Nesting can get out of hand very quickly

Simple demonstration: I’m going to add resources for _‘lyrics’_ underneath my nested _‘songs’_ resources.

![yeah, there’s gotta be a better way](/assets/images/nested7.png)
_yeah, there’s gotta be a better way_

## #4 Nesting best practices



From [Jamis Buck’s blog post][f1d50707] (also referenced in the Rails guide):
> Resources should never be nested more than 1 level deep.

Buck’s blog post suggests an advanced method for keeping your routes and URLs from getting out of control but I wanted to highlight two quick ways that you can refactor your code.

### Shallow nesting
Adding the _‘shallow: true’_ parameter to your nested resource will define routes at the base level, _‘/songs/’_, for four of our RESTful routes — _show_, _edit_, _update_ and _destroy_, while leaving the remaining routes — _index, new, create_— at the nested level. So how is this useful to us?

In my model, with artists and songs, we are now able to use the routes starting with _‘/songs/:id’_ to view or modify existing songs on an individual basis. Recall that songs belong to artists, so upon creation, we still need to initialize a song with an artist relationship. However, once a song is created, it doesn’t matter to artist relationship if we would like to edit or delete it. And so, we don’t need to follow a lengthy route, such as _‘/artists/:artist_id/songs/:id/edit’_ to make our changes.

### Collection/Member blocks

While it would not help to simplify my model, collection and member blocks can be used to create routes with specific dependencies.

Thank you for reading and be sure to check out the additional resources linked below.

  [f1d50707]: http://weblog.jamisbuck.org/2007/2/5/nesting-resources "Nesting resources"

[f333]: https://stackoverflow.com/questions/2034700/form-for-with-nested-resources

  1. [Nesting resources, http://weblog.jamisbuck.org/2007/2/5/nesting-resources][f1d50707]
  2. [Form for with nested resources, https://stackoverflow.com/questions/2034700/form-for-with-nested-resources][f333]
