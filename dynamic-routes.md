# Dynamic Routes

## The Limit of Static Routes

A **static route** is a route that can _only_ be accessed when a person visits the route **exactly**.

Meaning, if we define a route for `/about` like this:

```rb
# config/routes.rb
get("/about", { :controller => "application", :action => "about" })
```

Then this route **can only be activated** when a person visits `www.our-app-name.com/about`.

This works great for pages with content that <u>doesn't change</u>, like a Home, Rules, or About page.

This technique also works well when we get input from a user through a form submission, since **Query Strings** are optional and can be added to the end of _any_ route.

While we often use Query Strings for processing form submissions, they can be used for other dynamic app features. YouTube, for example, uses a Query String to determine which video you're watching.

Note the Query String present at the end of any video URL:

> https://www.youtube.com/watch<strong>?v=pKO9UjSeLew</strong>

<small>The route (or path) is `/watch`, while the query string is `?v=pKO9UjSeLew`</small>

For other features in large apps like YouTube, the New York Times, or GitHub we want routes that are more readable and memorizable that look like this instead:

YouTube:
- `https://youtube.com/c/google`
- `https://youtube.com/c/gorailstv`
- `https://youtube.com/c/jablinskigames`

New York Times:
- `https://www.nytimes.com/section/todayspaper`
- `https://www.nytimes.com/section/politics`
- `https://www.nytimes.com/section/sports`

GitHub
- `https://github.com/raghubetina`
- `https://github.com/appdev-projects`
- `https://github.com/firstdraft`

Where each route follows a pattern. The routes have the same beginning segment (`/c/`, `/section/`) but then the next segment is something unique.

If we wanted to define those routes for YouTube, using static routes, we would need to define very similar looking routes; one for each channel at YouTube.

```rb
get("/c/google", { :controller => "...", :action => "..." })
get("/c/gorailstv", { :controller => "...", :action => "..." })
get("/c/jablinskigames", { :controller => "...", :action => "..." })
```

Using this approach, when a user signs up and creates a new channel, a developer would need to write a new route, controller action, and view template _instantly_, before the user could even view their channel. Writing and deploying code _that_ quickly and frequently isn't feasible for human developers.

What do we do then? The solution here is to use dynamic routes and have Ruby write our view templates for us.

## What are Dynamic Routes?

(a.k.a. dynamic route segments, flexible path segments, url slugs, or pretty urls)

A Dynamic route is one route that can match _multiple_ different values. You define a "route pattern", where any URL that matches the pattern is accepted and runs the designated controller action. This is in contrast to Static Routes that only work with **exact** values.

For example, we could define **one dynamic route** that matches `/post/1`, `/post/abc`, or `/posts/literally-anything`.

### Why do we use them

Defining only static routes with exact paths is not always enough for complex applications where we need to:

- support infinite route variations
- save time defining routes, controller actions, and view templates
- identify and use a piece of information from the dynamic part (?)

## How to define a Dynamic Route

Instead of a **static route**, that will only be activated when a person matches exactly one route that a person can visit:

```rb
get("/rps/rock", { :controller => "moves", :action => "play_rock" })
get("/rps/paper", { :controller => "moves", :action => "play_paper" })
get("/rps/scissors", { :controller => "moves", :action => "play_scissors" })
```

By beginning a segment of the route with a colon (`:`), we make that segment dynamic. Rails will, for the purpose of routing, allow anything there; it’s like a wildcard.

Notice that each of these routes are similar in structure. They all start with `/rps/` and end with some move name. With a dynamic route we can define one route that will match all three of those move names:

```rb
get("/rps/:move", { :controller => "moves", :action => "play" })
```

This saves space in our `routes.rb` file, but introduces a new problem. When we used static routes for each rock paper scissors move, each route had it's own Controller Action and could safely assume that when someone visited `/rps/paper` that they "choose paper" as their move and we wrote code with that assumption. Now that there's only one route, how can we determine when someone visits `/rps/paper` vs `/rps/rock`?

Fortunately for us, we have access to the value in the dynamic path segment through the `params` Hash.

### Using `params`

While defining a dynamic path segment in the routes with the `:` will allow the router to match _any_ route that matches the pattern, usually, the actual value entered in the dynamic segment is important and we want to use somewhere in the view template to make the UI dynamic.

Just like with query strings, we can retreive the value from the dynamic path using the name we choose in the routes.

The value is available in the `params` Hash and the key for the value is the name of the dynamic path segment (`"move"` in this case).

So if the user is visiting `/rps/rock`, we can access `"rock"` from the `params` Hash in the controller action like this:

```rb
class MovesController < ApplicationController
  def play
    # Parameters look like:  { "move" => "rock" }
    @player_move = params.fetch("move")
    # ...
    render({ :template => "moves/play.html.erb" })
  end
end
```

## Demo

<div style="overflow: hidden;padding-top: 100%;position: relative;"><iframe loading="lazy" style="border: 0;height: 100%;left: 0;position: absolute;top: 0;width: 100%;" src="https://jelani.dev/dynamic-path-segment-demo/"></iframe></div>
