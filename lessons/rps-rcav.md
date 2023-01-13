# Rock, Paper, Scissors RCAV 

- Notes:

  - [Original video](https://canvas.uchicago.edu/courses/41147/pages/video-rps-rcav-intro-to-routing){target="_blank"} transcription is in [`adding-routes-RPS-RCAV.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/adding-routes-RPS-RCAV.md){target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/rps-rcav](https://github.com/appdev-projects/rps-rcav){target="_blank"}

  - Target: [https://rps-rcav.matchthetarget.com](https://rps-rcav.matchthetarget.com){target="_blank"}

  - Useful chapters:

    - [`adding-routes.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/adding-routes.md){target="_blank"}
    - [`rcav-flowchart.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/rcav-flowchart.md){target="_blank"}
    - [Routing - RCAV Slides](https://firstdraft.slides.com/raghubetina/06-routing-rcav?token=43w7FD8Q){target="_blank"}


## Video Segment: Dynamic Web Applications and URLs

- Notes:

  - request lifecycle of Route, Controller, Action, View
  - web interface and URLs
  - actions
  - render and redirect

We have worked hard and learned HTML, CSS, and Ruby. We're now especially proficient in writing Ruby programs, especially with the aid of gems and APIs. **BENP: have we discussed gems and APIs up to this point though?** 

However, if we (the developers) are the only ones that can _run_ these programs (from the command line through the `ruby` interpreter), then they aren't much use. It's time to start adding a **web interface** on top of our Ruby programs so that external users can interact with and benefit from them.

We already have all the tools to build our first dynamic web application. **BENP: need to clearly define RCAV early in any video or document now so we aren't left wondering, added next sentence**. Before we begin building, we need to understand the URL *request lifecycle* of Route, Controller, Action, View (RCAV).

Let's recall that Software as a Service (SaaS) has eaten the world. What does this mean? For an application that runs on a server and transmits information across the internet, the **interface** consists of a set of URLs that a user can visit. People can type in a URL, click a link, or submit a form, and then get back some information relevant and valuable to them.

![](assets/rps-rcav/airbnb-url.png)

Each URL will either

 - _display_ a page with some information ("get" in HTTP terminology)
 - trigger the _storing_ of some information ("post" in HTTP terminology)
 - trigger the _deleting_ of some information ("delete" in HTTP terminology)
 - trigger the _updating_ of some information ("patch" in HTTP terminology)
 - forward to another URL
 - or some combination of the above

Our goal was to demistify what happens between the user action and the return of information. Now we have the vocabulary to talk about this.

The world turns around the humble Uniform Resource Locator, or URL. Most obviously, the user might be visiting the URLs in their browser by typing into the address bar or clicking on links. Or, more and more commonly, users might be visiting from native iPhone or Android apps without even knowing that, behind the scenes, they are visiting URLs to store and retrieve the information they need. 

When somebody puts that URL into the address bar, and something happens between the URL and the page being rendered, we now can say what that is. When a user visits a URL, they are actually triggering a specific Ruby method.

But make no mistake: if there is information being stored in a central database, then there's a web server running somewhere and URLs are being visited with each **action** a user takes.

In the background somewhere, there is an object and method and somebody is saying `Something.something`, and that method is actually going to do the work of drawing the correct page of information with exactly the right information for that user and outputting it in the right format (almost alway HTML). So our job is to write those Ruby methods (called "actions") and allow users to trigger those methods when they visit each URL. 

So we can write any Ruby we want in those action methods. We can generate random numbers, read from APIs, calculate things, send text messages, and more. But every action must do one of two things:

1. *Render* a response, by sending back some HTML and displaying a new page

2. *Redirect*, or forward the user onward to another URL.

And that's everything that happens between the user visiting a URL and getting a response, and it is now a complete Route + Controller + Action + Response *request lifecycle*. We map every URL to one Ruby method that we write in advance and then we wire everything together so that Rails will listen for user visits and when someone visits a particular URL, then Rails will call the method we prepared that will handle getting the database information and wrapping it in bootstrapped markup and sending the HTML to the user's browser. 

You can fully _specify_ a web application by listing out the URLs that users can visit, and what happens when each URL is visited. For example, let's say we wanted to build an interactive game of Rock, Paper, Scissors. The complete specifications (or **specs**, for short) for this app might look like this:

 - **http://[OUR APP DOMAIN]/rock** — Should display "You played rock.", a random move by the computer, and the outcome.
 - **http://[OUR APP DOMAIN]/paper** — Should display "You played paper.", a random move by the computer, and the outcome.
 - **http://[OUR APP DOMAIN]/scissors** — Should display "You played scissors.", a random move by the computer, and the outcome .
 - **http://[OUR APP DOMAIN]/** — A welcome page that displays
    - "Happy Monday!" (or whatever day it is).
    - The rules of the game.
    - For example,
        
       ```
       Happy Tuesday!
       Rock beats Scissors, Paper beats Rock, Scissors beats Paper.
       Point your browser at /rock, /paper, or /scissors to play the game.
       ```

Now — how do we get our web server to perform the above tasks when users visit the above URLs?

### Potential Quiz Question

- First bullet point is the question itself?
- First option
    - This is not correct because of xyz reason
- Second option
    - This is not correct because of xyz reason
    - Also not correct because of abc reason
- Third option
    - That's right! Because of xyz reason
- Fourth option
    - This is not correct because of xyz reason
{: .choose_best #bin points="30" answer="3" }


### Text Companion: Dynamic Web Applications and URLs

## Video Segment: Route

- Notes:

  - all about routing and `config/routes.rb`
  - `get()`

The key thing is *routes*. *Routes* are how to connect a URL to an *action*. The very important file `config/routes.rb` contains all of our routes. This is a list of everything our application can do. We're moving out of our `public/` and `tasks/` folder, and using more of our Rails application, by working in the `app/` folder, where most of our code goes, and with this one file `routes.rb` that is in the `config/` folder.

The super important `config/routes.rb` file included in every Rails app says all the URLs (*routes*) that a user can visit and when someone visits the URL we say which class and which method Rails should execute to handle the request. Here is an example of a route:

```ruby
# config/routes.rb

self.get("/rock", { :controller => "application", :action => "play_rock" })
```

The method here is `get`[^other_verbs] and there are parentheses for its **two arguments**: 
  - **The first argument to `get` is a `String`**: the _path_ that we want users to be able to visit (the path is the portion of the URL that comes after the domain name). Here it is `"/rock"`
  - **The second argument to `get` is a `Hash`**: this is where we tell Rails which method to call when a user visits the path in the first argument. (We'll have to actually write this method in the next step, after we write the route.)

    The `Hash` must have two key/value pairs:

    - `:controller`: The value for this key is what we're going to name the _class_ that contains the method we want Rails to call when the user visits the path. For now we're going to default this value to `"application"` — you'll see why in a minute.
    - `:action`: The value for this key is the what we're going to name the method itself. "Action" is the term used to refer to Ruby methods that are triggered by users visiting URLs.
    - The `Hash` is saying: "Use a `Class` (controller) called `application_controller`, and in that `Class` use a `method` (action) called `play_rock` to generate a response for the user."

Don't be confused by the key names `:controller` and `:action`, these are equivalent to a Ruby `Class` and `method`. They just have special names in the lingo of web applications.

The `get` method is *inherited*, we don't need to build this method ourselves, which saves us a lot of time. We get the plumbing for free and we just need to tell Rails how we want each request to be handled by declaring our routes. 

[^other_verbs]: Later we'll use other methods, `post()`, etc, if we want to support requests using the other HTTP verbs.

### Text Companion: Route

## Video Segment: Controller, Action, View

- Notes:

  - all about `app/controllers/`
  - `ApplicationController` inheritance

All of our controller classes will be in the `app/controllers/` folder. There's already one controller that comes with every Rails app out-of-the-box: `ApplicationController`, found in `app/controllers/application_controller.rb`. This is the controller that the above route is referring to. We will just use this controller for now. Later we will make separate controllers to keep our code organized.

An example of an action looks like this:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def play_rock
    self.redirect_to("https://www.wikipedia.org")
  end 
end
```

We get the first line class definition for "free":

```ruby
class ApplicationController < ActionController::Base
```

It comes with Rails. It inherits `<` from the `Base` class which is inside the Rails gem, so we would need to go into the Rails gem on GitHub to actually look at it. **BENP: gem has maybe not be defined or discussed yet. possible footnote here. Also this is our first time talking about inheritence, so may need some expansion**

Then we define a method:

```ruby
def play_rock
```

And inside of that we could write whatever steps we want (like calls to GoogleMaps or weather services from DarkSky **BENP: I don't think either of these have been presented at this point in the class**). At the end of the day, the job of an _action_ is to send back a response to the user. A response can be either:

 - **Rendering** some data, in any one of many formats:
  - Plain text.
  - JSON for an application to consume — we've seen JSON before (in APIs), and consumed it ourselves with our Ruby scripts.
  - HTML for their browser to draw — we'll learn this soon.
  - Less commonly, any other format: CSV, PDF, XML, etc.
 - Or, the action can forward the user to _another_ URL. This is known as **redirecting**. 

 We get a method for each of these two: `render` for the first, and `redirect_to` for the second.
 
 In this case, we *redirect* to another URL:

```ruby
self.redirect_to("https://www.wikipedia.org")
```

As you can see, the argument to `redirect_to` is a `String` which contains some URL that you want the user to simply be forwarded to. This will come in handy later when, for example, we want to send the user directly back to a list of all photos after they've deleted a photo.

### Text Companion: Controller, Action, View

## Video Segment: Dropping `self.`

- Notes:

  - why we drop `self.`

Just to get something out of the way: Usually we always call `object.method`, and we are using the `self` keyword above because we are calling these methods on the instance of the class (`ApplicationController`) that we are defining the method (`play_rock`) for. Kind of like when we learned about the `Person` class and there is `first_name` and `last_name`, and if we wanted a `full_name` method we called `self.first_name + self.last_name`. In this case we're defining `play_rock` and we want use the method `redirect` which already exists on `ApplicationController`, since it's inherited via `< ActionController::Base`. The point is, we are using a method that already exists to build our new method, hence `self.redirect_to`. In Ruby, when you're calling a method on `self`, you can drop the `self.`, and Ruby will figure it out, so we can rewrite the route, controller, action steps to:

```ruby
# config/routes.rb

get("/rock", { :controller => "application", :action => "play_rock" })
```
{: mark_lines="3" }

and

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def play_rock
    redirect_to("https://www.wikipedia.org")
  end 
end
```
{: mark_lines="5" }

### Text Companion: Dropping `.self`

## Video Segment: Our First RCAV

- Notes:

  - debugging an RCAV for **/rock** 
  - RTEM
  - ends with `redirect_to`

Our workflow for a dynamic web application is always the same: Route, Controller, Action, View (RCAV). Remember, the world is ruled by URLs. So we will always start with what URL we want to build and get it to work.

If we begin by navigating to the route **/rock** in our Rails browser: **http://[YOUR APP DOMAIN]/rock**, then we get an error message: No route matches [GET] "/rock".

![](assets/rps-rcav/err-no-routes-match.png)

We need to *Read The Error Message* (RTEM) and define the first route that will allow us to support a request of the form for our users. 

Let's open the file `config/routes.rb` and define the route by adding the following code:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/rock", { :controller => "application", :action => "play_rock" })

end
```
{: mark_lines="5" }

(All of our routes must be contained within the block following `Rails.application.routes.draw`. A new Rails app will already come with this code pre-written in `routes.rb`.)

Again, we have our route `"/rock"` and our key/value pairs for the `:controller` (or `Class`) and `:action` (or `method`). We need to choose values for the `:controller` that Rails will use and the `:action` within the controller that will be called. For now we are just using the `app/controllers/application_controller.rb` for the controller, and we will define our action `play_rock` in there.

We now need to open `app/controllers/application_controller.rb` to add some code. Note that Rails is smart and will add `_controller.rb` to our `:controller` argument in `get`, and within that controller file you will see the class has the underscores removed and is capitalized as `ApplicationController`. These are helpful conventions, and are best followed. **BENP: is that last thing a fair statment?** 

In this file we will add the following:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout(false)

  # Add your actions below this line
  # ================================

  def play_rock
  end
end
```
{: mark_lines="9-10"}

We need our action to exactly match what we wrote in the `config/routes.rb` file, here `play_rock`. Between the `def play_rock` and `end` that we added, we could put whatever and however much code we would like to execute in that action for the user. In the end we will need to either *render* some HTML back to the user or *redirect* the user to another place. Let's begin by just redirecting to some other URL:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout(false)

  # Add your actions below this line
  # ================================
  
  def play_rock
    # write your code here

    redirect_to("https://www.wikipedia.org")
  end
end
```
{: mark_lines="10-12"}

And we just created a full RCAV request lifecycle. If we go back to the browser and refresh the URL: **http://[YOUR APP DOMAIN]/rock**, then we will end up on Wikipedia.

If I go back to GitPod and look in my server log (use `Cmd + J` to open and close the log, `Cmd + K` to clear the log), then I will see something like:

![](assets/rps-rcav/rock-to-wikipedia-server-log.png)

We can see exactly what happened. Someone tried to `GET "/rock"` from a given IP address at a given time, we found a route with instructions to use `ApplicationController#play_rock` (where the `Something#something` is Ruby shorthand for `Class.method`, with the `.` exchanged for a `#`), calling this controller-action pair resulted in a redirect to the given URL (`https://www.wikipedia.org`), and the entire request lifecycle completed in the stated time with no errors.

### Text Companion: Our First RCAV

## Video Segment: Render HTML

- Notes:

  - from `render({ :plain => "Hello, world!" })` to `render({ :template => "game_templates/user_rock.html.erb" })`
  - `.html` vs. `.html.erb`
  - `app/views/` view templates rather than `public/`

We've written our first functional action, which just forwards someone to a new page. Now let's try to render some of our own HTML, rather than redirecting to Wikipedia. We can change the previous code in `app/controllers/application_controller.rb` to:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout(false)

  # Add your actions below this line
  # ================================
  
  def play_rock
    # write your code here

    # redirect_to("https://www.wikipedia.org")
    
    render({ :plain => "Hello, world!" })
  end
end
```
{: mark_lines="12-14"}

Rather than using `redirect_to()`, which we inherited `<` from the Rails `Base` class, we'll use another inherited method to complete the request lifecycle: `render()`. 

This method, takes a `Hash` as an argument with a key/value pair. The key has many options, here we will use `:plain`, which will just send back plain text. A boring response, but good to start with.

Now if I pretend I'm a user and visit **http://[YOUR APP DOMAIN]/rock**, then I get a page with my `"Hello, world!"` rendered. 

Congratulations! You've wired up a route; prepare to do it a million more times, because all developers do all day is pick the next **spec** , wire up the route for the URL so that a user can visit it, and then implement the logic to send back the correct information.

Remember, we did not create and send a file, we are using Ruby to generate this reponse, opening a world of possibilities. For instance, what if we instead rendered a random number:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout(false)

  # Add your actions below this line
  # ================================
  
  def play_rock
    # write your code here

    # redirect_to("https://www.wikipedia.org")
    
    render({ :plain => rand(100) })
  end
end
```
{: mark_lines="14"}

Now everytime we refresh **http://[YOUR APP DOMAIN]/rock**, we get a different random number, generated automatically by Ruby. This is a dynamic response, not just a static page that we placed in the public folder. 

This is a simple example, but fundamentally that's it. We connected a URL to a method that can do *anything*. It can call APIs, parse CSVs, compute whatever you want, run machine learning models. With this we can do anything. Of course, there is a lot more to learn, but fundamentally this is it. 

Now let's send back some actual HTML:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout(false)

  # Add your actions below this line
  # ================================
  
  def play_rock
    # write your code here

    # redirect_to("https://www.wikipedia.org")
    
    render({ :html => "<h1>Hellow, world!</h1>".html_safe })
  end
end
```
{: mark_lines="14"}

The `:html` key to `render()` allows us to place whatever HTML we want in a string that will be shown on the page. We need the `.html_safe` on the end of the string, which is a bit of Rails security to make sure that one user can't inject malicious HTML into another user's browser, in case we were getting the given HTML string from another user (e.g., from a `<form>`). Don't worry about this, we will see a better way of doing this in a moment.

If we refresh **http://[YOUR APP DOMAIN]/rock**, then we will see our HTML. We could go crazy and put our entire HTML document in that string. But a much, much better way to to write what's called an *embedded Ruby template*.

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout(false)

  # Add your actions below this line
  # ================================
  
  def play_rock
    # write your code here

    # redirect_to("https://www.wikipedia.org")
    
    # render({ :html => "<h1>Hellow, world!</h1>".html_safe })

    render({ :template => "game_templates/user_rock.html.erb" })
  end
end
```
{: mark_lines="16"}

The `:template` key to `render()` allows us to assign a template to render. We specify the name of a folder `game_templates/` and file `user_rock.html.erb` that will contain all of our HTML. This is an `.erb` for *embedded Ruby template* file, rather than a plain old `.html` file. 

We create this file in the existing `app/views/` folder, which is a way better place than `public/`, because users do not have access to all of its contents. We will keep things organized and put different templates in different sub-folders. Do not put the `.html.erb` file in the `app/views/layouts/` folder that already exists, first make a new folder in `app/views/` called `game_templates/` then make the new file in this folder called `user_rock.html.erb`.

**BENP: insert image(s) (gifs? would be better here; cf. video 00:25:20) of new folder and new file steps in GitPod**

You can call the `game_templates/user_rock.html.erb` folder and file whatever you want. The user will not see the folder or the file, they will only see `"/rock"`, the specified route.

Now you can enter in your new `user_rock.html.erb` file some HTML to render:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>
```

Don't forget to save the file changes if you haven't done so. 

And now when we refresh **http://[YOUR APP DOMAIN]/rock**, we get the text from our file rendered in HTML.

So after all of that we have an HTML page that basically does what we could have done quickly if we made a file called `rock.html` in the `public/` folder. 

### Text Companion: Render HTML

## Video Segment: Embedded Ruby Tags

- Notes:

  - all about `<% %>` and `<%= %>` in a view template

But we can do something way better with this new system. Let's add the following to our embedded Ruby file:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<h2>
  They played <%= %>!
</h2>
```
{: mark_lines="5-7"}

Now we created a new tag that looks like HTML, but contains a doorway to Ruby: `<%= %>`. We can write any Ruby we want in that *embedded Ruby tag*, and this is what makes the whole effort of RCAV worthwhile. For instance we can write:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<h2>
  They played <%= 6 * 7 %>!
</h2>
```
{: mark_lines="6"}

And we will see the result of this computation when we refresh **http://[YOUR APP DOMAIN]/rock**. But if we go to view source in the browser, we won't see the Ruby code. We only see the result `42`. The browser only understands HTML and has no idea of the code that allows us to make the web application dynamic. So rails is processing all of the embedded Ruby tags and injecting them in the document before it sends the plain HTML file to the browser. 

We could also do something like

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= 6 * 7 %>!
</h2>
```
{: mark_lines="5"}

Here, we used a slightly different embedded Ruby tag: `<% %>`. We left off the `=` sign, which means the output of this Ruby code will be hidden in the final HTML. But, the variable `comp_move` (which is the result of randomly sampling an array of three possble string values) is still available and we can render it by changing the file again:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= comp_move %>!
</h2>
```
{: mark_lines="8"}

Such that our calculated variable `comp_move` is now rendered in the final HTML output, because it is in a `<%= %>` tag, with the `=` sign. And we will see the result of this computation when we refresh **http://[YOUR APP DOMAIN]/rock**. View the source code here and you won't see any sign of the `comp_move` variable computation from the `<% %>` tag.

**BENP: Now could be time for a screenshot or better GIF of refreshing /rock a couple of times to see the output and showing the source code.**

Alright, we are now finally building dynamic web applications. We are able to render a template, we are able to write some HTML, and we able use *embedded Ruby tags*: `<% %>` for hidden content, and `<%= %>` for rendered content that the user will see.

### Text Companion: Embedded Ruby Tags

## Video Segment: Control Flow with Embedded Ruby

- Notes:

  - conditionals
  - all about `<% if ... %>`



Now we can actually compute who won or lost our Rock Paper Scissors match. Let's add this long `if-else` Ruby code to our `game_templates/` file:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= comp_move %>!
</h2>

<% if comp_move == "rock" %>
  <h2>We tied!</h2>
<% elsif comp_move == "paper" %>
  <h2>We lost!</h2>
<% elsif comp_move == "paper" %>
  <h2>We won!</h2>
<% end %>
```
{: mark_lines="11-17"}

Above, we used hidden `<% %>` embedded Ruby tags in our control flow on each line we wanted to hide, so none of this will be rendered to the user. Only the result of this control flow `<h2>We tied!</h2>`, `<h2>We lost!</h2>`, `<h2>We won!</h2>` will be rendered, depending on the randomly sampled `comp_move` variable. Refresh **http://[YOUR APP DOMAIN]/rock** to see. 

And now would be a good time to run `rails grade` at the GitPod console to check our progress. And remember to **A**lways **B**e **C**ommitting, by making a `/git` commit. We have a lot done, but we still have a lot to do.

### Text Companion: Control Flow with Embedded Ruby

## Video Segment: Homepage

- Notes:

  - RCAV with `render` for **/**

The [target](https://rps-rcav.matchthetarget.com/){:target="_blank"} has a homepage at the root URL, **/**. In the old days, we would create a file in `public/` called `index.html`, but now we are pretty much done with `public/` except maybe for static assets like images or css files, but we won't put any more user-facing URL pages there. Those will be connected up with routes from here on. Let's go to our `config/routes.rb` and add a homepage route:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  
  get("/", { :controller => "application", :action => "homepage" })

  get("/rock", { :controller => "application", :action => "play_rock" })

end
```
{: mark_lines="5" }

We are adding the `"/"` homepage route, we are using the `application_controller.rb` file, and we are using the action (or the method within the `ApplicationController`) that we call `homepage`. 

Now if I refresh the **http://[YOUR APP DOMAIN]/** page, I get an error message that the `homepage` action cannot be found in `ApplicationController`:

```ruby
The action 'play_rock' could not be found for ApplicationController
```

![](assets/rps-rcav/err-action-not-in-contoller.png)

This is good! That means we defined the route correctly. If you still see a "No route matches" error, then double-check your route syntax and get that error to go away before you proceed further. The error occurs because we did not yet define the action. So we need to go to our `app/controllers/application_controller.rb` file and add:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout(false)

  # Add your actions below this line
  # ================================
  
  def homepage
    render({ :template => "game_templates/rules.html.erb" })
  end

  def play_rock
    # write your code here
    
    # redirect_to("https://www.wikipedia.org")
    
    # render({ :html => "<h1>Hellow, world!</h1>".html_safe })

    render({ :template => "game_templates/user_rock.html.erb" })
  end
end
```
{: mark_lines="9-11"}

And now we can create that new file `game_templates/rules.html.erb`, and add to it:

```html
<!-- app/views/game_templates/rules.html.erb -->

<h1>Welcome to RPS</h1>
```

Now when we refresh **http://[YOUR APP DOMAIN]/**, there is no error and our HTML template is rendered. And we did not put any HTML in the public folder! You will almost always want some kind of dynamic behavior on every page. So our new workflow is always RCAV: Define a route, assign a controller, create an action in that controller, and view the result.

### Text Companion: Homepage

## Video Segment: Reinforce RCAV with /paper

- Notes:

  - RCAV with `render` for **/paper**

Let's start with the **/paper** route, for when we play paper. First we define the route in `config/routes.rb` with a controller:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  
  get("/", { :controller => "application", :action => "homepage" })

  get("/rock", { :controller => "application", :action => "play_rock" })

  get("/paper", { :controller => "application", :action => "play_paper" })

end
```
{: mark_lines="9" }

Again, we use the `application_controller.rb`. If we pretend we are a user now and go to **http://[YOUR APP DOMAIN]/paper**, we again get the "action not found" error. The helpful error message (RTEM!) tells us we need to define another method for the action in our controller called `play_paper`. 

We are in our **Route, Controller, Action, View** sequence that makes Rails so useful! It's the same flow, over and over again. All we need to do is keep visiting the route and RTEM to find the next step.

Ok, let's define the action in our `app/controllers/application_controller.rb`:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout(false)

  # Add your actions below this line
  # ================================
  
  def homepage
    render({ :template => "game_templates/rules.html.erb" })
  end

  def play_rock
    # write your code here
    
    # redirect_to("https://www.wikipedia.org")
    
    # render({ :html => "<h1>Hellow, world!</h1>".html_safe })

    render({ :template => "game_templates/user_rock.html.erb" })
  end

  def play_paper

    render({ :template => "game_templates/user_paper.html.erb" })
  end

end
```
{: mark_lines="23-26"}

Now we can pretend we are a user and again refresh **http://[YOUR APP DOMAIN]/paper**. And we'll get a new error message that tells us we are missing the view template:

![](assets/rps-rcav/err-missing-view-template.png)

If you cannot figure out what your typo is and why an error message keeps coming up, then delete what you wrote and try to type it again from scratch (or talk to your rubber duck). 

We RTEM above and that tells us to go and make the new `game_templates/user_paper.html.erb` file that will be rendered to the user:

```html
<!-- app/views/game_templates/user_paper.html.erb -->

<h2>
    We played paper!
</h2>
```

And now our view at **http://[YOUR APP DOMAIN]/paper** renders content with no error message. A successful RCAV!

### Text Companion: Reinforce RCAV with /paper

## Video Segment: Embedded Ruby in the Controller with Instance Variables

- Notes:

  - moving conditional control flow `<% if ... %>` from **/rock** into the `ApplicationController` action `play_rock`
  - local variables vs. instance variables with `@`-notation

Now that we are RCAV pros, let me show you another (perhaps better, depending on your taste) way of writing our embedded Ruby code. Let's return to the `game_templates/user_rock.html.erb` file:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= comp_move %>!
</h2>

<% if comp_move == "rock" %>
  <h2>We tied!</h2>
<% elsif comp_move == "paper" %>
  <h2>We lost!</h2>
<% elsif comp_move == "paper" %>
  <h2>We won!</h2>
<% end %>
```
{: mark_lines="5"}

The highlighted code `<% comp_move = ["rock", "paper", "scissors"].sample %>` is okay, but you could imagine that in a real application there may be dozens of lines of code to prepare the information that we actually want to show the user. Our example is trivial. In reality we may lookup data from a database, doing math on it, finding API data, and more. Think of our "take your umbrella" example **BENP: insert link to this DarkSky API example; but wait, has it even been presented up to this point?**, which took around 30 lines of Ruby code to produce. We want somewhere other than the HTML template to put this code.

We can in fact do that!

Let's go back to the `game_templates/user_paper.html.erb` file, since we didn't get as far there and see how we can make this modification. We would like our file to look like this:

```html
<!-- app/views/game_templates/user_paper.html.erb -->

<h2>
    We played paper!
</h2>

<h2>
    They played <%= comp_move %>!
</h2>

<h2>
    We <%= outcome %>!
</h2>
```
{: mark_lines="7-13"}

We wish we could just do this and avoid all the lines of embedded Ruby that are in the previous `user_rock.html.erb` view template. The responsibility for these computations really don't belong here, the view templates should be given some data and then the job should just be to format and present it beautifuly and usably to the user. In the backend the responsibility should be marshalling the correct data and sending it to the view template.

We can return to our `app/controllers/application_controller.rb` controller file and do the following:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout(false)

  # Add your actions below this line
  # ================================
  
  def homepage
    render({ :template => "game_templates/rules.html.erb" })
  end

  def play_rock
    # write your code here
    
    # redirect_to("https://www.wikipedia.org")
    
    # render({ :html => "<h1>Hellow, world!</h1>".html_safe })

    render({ :template => "game_templates/user_rock.html.erb" })
  end

  def play_paper
    comp_move = ["rock", "paper", "scissors"].sample
    
    if comp_move == "rock"
      outcome = "won"
    elsif comp_move == "paper"
      outcome =  "tied"
    elsif comp_move == "scissors"
      outcome = "lost"
    end

    render({ :template => "game_templates/user_paper.html.erb" })
  end

end
```
{: mark_lines="23-31"}

In the above highlighted code we have removed all of the embedded Ruby tags (`<% %>` and `<%= %>`) from the code we had in the `.html.erb` view template. Now when a user visits the route **http://[YOUR APP DOMAIN]/paper**, the action `play_paper` in the controller `ApplicationController` will be triggered, and the code will be run before the template is rendered. 

So let's try to visit **http://[YOUR APP DOMAIN]/paper** again. Oops, we get this error:

![](assets/rps-rcav/err-undefined-local-var-or-meth.png)

In our `game_templates/user_paper.html.erb` view template, when we get to the first embedded Ruby tag:

```html
<!-- app/views/game_templates/user_paper.html.erb -->

<h2>
    We played paper!
</h2>

<h2>
    They played <%= comp_move %>!
</h2>

<h2>
    We <%= outcome %>!
</h2>
```
{: mark_lines="8"}

That *local variable* `comp_move` is undefined! A *local variable* only exists in the scope it was defined. If I create a local variable in a loop, it will only exist in that loop. If I want some variable available outside the loop, then I would need to create it outside the loop and modify it in the loop. So there's a scope to local variables and I can't just use it in my template if I created it in the `play_paper` method (action). The variable is effectively "dead" after `play_paper` executes. 

So how do we make the controller variables available in the view template? Let's modify our `app/controllers/application_controller.rb`:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout(false)

  # Add your actions below this line
  # ================================
  
  def homepage
    render({ :template => "game_templates/rules.html.erb" })
  end

  def play_rock
    # write your code here
    
    # redirect_to("https://www.wikipedia.org")
    
    # render({ :html => "<h1>Hellow, world!</h1>".html_safe })

    render({ :template => "game_templates/user_rock.html.erb" })
  end

  def play_paper
    @comp_move = ["rock", "paper", "scissors"].sample
    
    if @comp_move == "rock"
      @outcome = "won"
    elsif @comp_move == "paper"
      @outcome =  "tied"
    elsif @comp_move == "scissors"
      @outcome = "lost"
    end

    render({ :template => "game_templates/user_paper.html.erb" })
  end

end
```
{: mark_lines="23 25-30"}

All we did was place an `@` symbol before any variable that we want access to in our view template. This is a new kind of variable called an *instance variable*. This type of variable will survive as long as the instance the object in which its created survives **BENP: last sentence a bit confusing**. In this case when someone visits **/paper**, Rails is going to create an instance of the `ApplicationController` class and then run the `play_paper` method. So as long as the `ApplicationController` instance is alive (Rails keeps it until the response is sent to the user), the variables produced by `play_paper` will exist. 

When someone visits **/paper**, we now have `@comp_move` and `@outcome` available for our template. We just need to make sure those instance variables are also properly referenced in `game_templates/user_paper.html.erb`:

```html
<!-- app/views/game_templates/user_paper.html.erb -->

<h2>
    We played paper!
</h2>

<h2>
    They played <%= @comp_move %>!
</h2>

<h2>
    We <%= @outcome %>!
</h2>
```
{: mark_lines="8 12"}

Again, we just use the leading `@` symbols on our variables to tie them to the instance variables in the controller. And if we visit the **/paper** URL, it works! And we have a much improved organization. 

Most computation work like this should go in the controller as we have done it here. We will have cases where embedded Ruby goes in the template (e.g., rendering database records with `each` loops, `if` statements to check if a user is allowed to see something, other conditional statements). If it can happen in the controller, it should happen there.

Time for a `rails grade` and a `/git` commit!

### Text Companion: Embedded Ruby in the Controller with Instance Variables

## Video Segment: Linking Pages with Layouts

- Notes:

  - all about `app/views/layouts/wrapper.html.erb` to get some headers, footers, and navigation links
  - `layout("wrapper.html.erb")` in `ApplicationController`
  - `:layout` argument for `render()`

It would now be nice to add some links so we don't need to type in the URL addresses, like in our [target](https://rps-rcav.matchthetarget.com/){:target="_blank"}. 

Let's start with our `game_templates/user_paper.html.erb`:

```html
<!-- app/views/game_templates/user_paper.html.erb -->

<div>
  <a href="/rock">Play Rock</a>
</div>
<div>
  <a href="/paper">Play Paper</a>
</div>

<h2>
    We played paper!
</h2>

<h2>
    They played <%= @comp_move %>!
</h2>

<h2>
    We <%= @outcome %>!
</h2>
```
{: mark_lines="3-8"}

And now if we visit our **/paper** URL, then we have the links. But if we click on "Play Rock" here, and we are taken to the **/rock** URL, then the links are not there, because we only put them in the `game_templates/user_paper.html.erb` file, and not in the `game_templates/user_rock.html.erb` file, which is what visiting the **/rock** URL will render.

**BENP: In the below example, we use the `app/views/layouts/wrapper.html.erb` file that we create, but in all other class work we use `app/views/layouts/application.html.erb` to place our headers and footers. Maybe we change the below section to just do it with that, which also I think allows us to omit the `layout("wrapper.html.erb)"` call?**

How can we avoid repeating these HTML navigation links in all of our view templates? Well, here is one of the great benefits of working in Rails instead of HTML. We are dynamically generating responses rather than hard-coding into a bunch of files. If there is common stuff we want on every page, like a nav-bar or footer, then we can make a special file in `app/views/layouts/` and call it whatever we like. Let's create a file in that folder called `wrapper.html.erb` and let's fill our new `app/views/layouts/wrapper.html.erb` file with:

```html
<!-- app/view/layouts/wrapper.html.erb -->

<div>
  <a href="/rock">Play Rock</a>
</div>
<div>
  <a href="/paper">Play Paper</a>
</div>
<div>
  <a href="/scissors">Play Scissors</a>
</div>

<%= yield %>

<div>
  <a href="/">Rules</a>
</div>

Copyright, Appdev 2022. All rights reserved.
```
{: mark_lines="13"}

Now every page that we visit will have all of its contents placed where the above highlighted code says `<%= yield %>`. We just need to also change our `application_controller.rb` file to note this and have it take effect:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout("wrapper.html.erb")
```
{: mark_lines="4"}

This `layout` method takes one argument and it already knows to look in the folder `app/views/layouts/` for the file that we created.

After this change, try visiting your pages using the links on every page. It should work (except for **/scissors** because we haven't done the RCAV for that page yet).

If we only wanted the layout to apply on a per-page basis we could also leave `layout(false)` in the previous code, and we could in the `play_rock` method (action) change our render statement to:

```ruby
render({ :template => "game_templates/user_rock.html.erb", :layout => "wrapper.html.erb" })
```

This additional `:layout` argument would then only put the nav-bar and footer in `wrapper.html.erb` on the **/rock** route.

Time for a `rails grade` and a `/git` commit! 

The rest of the project is up to you to finish. Visit the **specs** and wire them all up. You have all the tools now.

### Text Companion: Linking Pages with Layouts

## Finish and Submit RPS RCAV

- Notes:

  - Refer students to [`rails grade`][`rails grade`], [git][Git], and [Sharing a Gitpod Snapshot][Sharing a Gitpod Snapshot] sections for how to get help

## RCAV Addendums

- Notes:

  - Stuff that I did not zip in from the chapter `adding-routes.md`:

### Addendum: Rendering JSON

Imagine that we wanted to build a native iPhone app that asked our server for some information; in this simple example, for a random computer move and an outcome, but in the real-world things like the local weather given a latitude and a longitude.

Rather than rendering a pre-defined message in plain text, it's usually more helpful to the iPhone developer to render the data in JSON format, so that they can parse it, easily fetch whichever values they need, and assemble their own interface.

Here is some JSON that would be convenient for an external application to parse:

```json
{ "player_move":"rock", "comp_move":"paper", "outcome":"lost" }
```

Notice that JSON uses strings as keys — this is because JavaScript doesn't have the equivalent of Ruby's `Symbol` class. Also, there are no hash rockets; JSON just uses colons to separate keys and values.

Fortunately, just as it was easy for us to convert a `String` containing JSON into Ruby `Array`s/`Hash`es using the `JSON.parse` method, it is also easy for us to go in the other direction: both `Array` and `Hash` have methods called `.to_json`. Let's create a Ruby `Hash` that resembles the JSON above:

```ruby
response_hash = { :player_move => "rock", :comp_move => "paper", :outcome => "lost" }
```

We can then convert this into a `String` in JSON format with `.to_json`:

```ruby
response_hash.to_json
```

returns:

```ruby
"{\"player_move\":\"rock\",\"comp_move\":\"paper\",\"outcome\":\"lost\"}"
```

The `\"` represents double-quotes; we need the backslash, known as an "escape", because we're already within a double-quoted string and don't want to terminate it. You can `puts` the string to see it formatted:

```ruby
puts response_hash.to_json
```

displays:

```
{"player_move":"rock","comp_move":"paper","outcome":"lost"}
```

Great! That means we can update our action if we want to send back JSON instead:

```ruby
class ApplicationController < ActionController::Base
  def play_rock
    moves = ["rock", "paper", "scissors"]

    comp_move = moves.sample
    
    if comp_move == "rock"
      outcome = "tied"
    elsif comp_move == "paper"
      outcome = "lost"
    elsif comp_move == "scissors"
      outcome = "won"
    end

    response_hash = { :player_move => "rock", :comp_move => "paper", :outcome => "lost" }

    render({ :plain =>  response_hash.to_json })
  end
end
```

Congratulations — you just built your first API endpoint! 🙌🏾

### Addendum: Custom Controller Files

We don't have to put all of our actions within the default `ApplicationController` file that comes included with any Rails app; we can add our own controllers, if we want to organize things a bit more. With an app of any non-trivial size, you'll end up with hundreds of actions, and it can get unwieldy to put them all in one gigantic `application_controller.rb`.

Instead, we can change our route for **/rock** to this:

```ruby
get("/rock", { :controller => "game", :action => "play_rock" })
```

Now when a user visits **/rock**, they will see an error `uninitialized constant GameController`.

As we know, when Ruby says "uninitialized constant" it means "I can't find that class".

So, what's going on here? When we said `:controller => "game"` in the route, we _told_ Rails to look for a class called `GameController` when someone visits **/rock**.

 - All of the controller class names will end in `...Controller`, and they will begin with whatever value we provided for the key `:controller` in the route.
 - Like all Ruby classes, the name must be `CamelCase` (not `snake_case` or `Some_Hybrid`). So in this case, it will be `GameController`.
 - The class must be defined in a Ruby file that is the `snake_cased` version of its name. Rails will itself use the `.underscore` method to figure out the name; we can try it ourselves in `rails console`:

    ```ruby
    [2] pry(main)> "GameController".underscore
    => "game_controller"
    ```
 - The Ruby file must be placed within the `app/controllers/` folder. So, in this case, we create a file called `app/controllers/game_controller.rb` (don't forget the `.rb` file extension).
 - Finally, within this file, we define the class:

    ```ruby
    class GameController < ApplicationController
    end
    ```
 - We inherit from `ApplicationController`, which in turn inherits from `ActionController::Base`; much like our models inherited from `ActiveRecord::Base` via `ApplicationRecord`.
 
    Our models inherited `.save`, `.where`, and a bunch of other awesome database-related methods from `ActiveRecord::Base`; whereas our controllers are going to inherit a bunch of methods like `render`, `redirect_to`, and a bunch of other awesome interface-related methods from `ActionController::Base`.
 - Don't forget the `end` that goes with the `class`; type it before you forget it.
 - Move your `play_rock` action over from `application_controller.rb` into this new class.
 - Now, when a user visits the path **/rock**, the "uninitialized constant" error should go away and you should see a response as before.

    If you still see the "unitialized constant" error, then:

    - You named your class wrong; it must exactly match the value in `routes.rb`, followed by `Controller` (singular), and `CamelCase`.
    - You named the file wrong. Try doing `.underscore` on a string containing the class name in `rails console` to figure out the correct filename.
    - You put the file in the wrong folder. It has to be within `app/controllers/`. Not within, for example, `app/` or `app/controllers/concerns/`.
    - You forgot the `.rb` file extension.
    - If you can't find which of the above it is, try deleting what you did and paving over your work again from scratch. Sometimes you just can't spot your own typos, and paving over is the best approach.

You can make as many controllers as you like; in general, a rule of thumb is to have one controller per database table.

