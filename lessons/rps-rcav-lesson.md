# Rock, Paper, Scissors RCAV

We can now use HTML and CSS for designing web pages, and Ruby for writing programs. However, if we (the developers) are the only ones that can _run_ these programs (through the `ruby` interpreter), then they aren't much use. It's time to start adding an _interface_ on top of our Ruby programs so that external users can interact with them.

We already have all the tools to build our first **dynamic web application**. But, before we begin building, we need to understand the URL request lifecycle of _Route, Controller, Action, View (RCAV)_.

In this lesson, we will explore routing. In practice, the project we work through will make our Rock, Paper, Scissors webpage dynamic; meaning it will actually work.


## URLs and Specs

For an application that runs on a server and transmits information across the internet (i.e. Software as a Service, **SaaS**), the interface consists of a set of Uniform Resource Locators (**URL**s) that a user can visit, and receive some information relevant and valuable to them.

![](assets/rps-rcav/airbnb-url.png)

Each URL will either:

 - _display_ a page with some information (`get` in **HTTP** terminology)
 - trigger the _storing_ of some information (`post` in HTTP terminology)
 - trigger the _deleting_ of some information (`delete` in HTTP terminology)
 - trigger the _updating_ of some information (`patch` in HTTP terminology)
 - forward to another URL
 - or some combination of the above

Most obviously, the user might be visiting the URLs in their browser by typing into the address bar or clicking on links. Or, more and more commonly, users might be visiting from native iPhone or Android apps without even knowing that, behind the scenes, they are visiting URLs to store and retrieve the information they need. 

But make no mistake: if there is information being stored in a central database, then there's a **web server** running somewhere and URLs are being visited with each _action_ a user takes. When somebody puts that URL into the address bar and hits <kbd>Enter</kbd>, they are triggering a specific Ruby method.

In the background, there is a a _noun_ (the object) and a _verb_ (the instance method): `Object#method`. This method does the work of drawing the correct page of information for the user. Our job is to write those Ruby methods (called _actions_), and allow users to trigger them when they visit each URL. 

<aside markdown="1">
Recall that `Object#method` notation symbolizes an **_instance_ method**, while `Object.method` notation symbolizes a **_class_ method**.
</aside>

We can write any Ruby we want in those **action methods**. We can generate random numbers, read from **API**s, calculate things, send text messages, and more. But every action must do one of two things:

1. ***Render*** a response, by sending back some HTML and displaying a new page

2. ***Redirect***, or forward the user onward to another URL.

And that's _everything_ that happens between the user visiting a URL and getting a response, it is a complete **_request lifecycle_**. Every URL is mapped to one Ruby method, and then we wire everything together so that Rails will listen for user visits. When someone visits a particular URL, then Rails will call the method we prepared, which will handle getting any database information, wrapping it in bootstrapped markup, and sending the HTML to the user's browser. 

You can fully _specify_ a web application by listing out the URLs that users can visit, and what happens when each URL is visited. For example, let's say we wanted to build an interactive game of Rock, Paper, Scissors. The complete specifications (or **_specs_**, for short) for this app might look like this:

 - **http\://[APP DOMAIN]/rock** — Should display "You played rock.", a random move by the computer, and the outcome.
 - **http\://[APP DOMAIN]/paper** — Should display "You played paper.", a random move by the computer, and the outcome.
 - **http\://[APP DOMAIN]/scissors** — Should display "You played scissors.", a random move by the computer, and the outcome.
 - **http\://[APP DOMAIN]/** — A welcome page that displays some information and the rules of the game.

Now — how do we get our web server to perform the above tasks when users visit the above URLs?

### Quiz Question

- What happens when a user in our app visits a URL from their address bar?
- A Ruby Class is created for the page
    - Not quite, recall the term **instance method**
- This URL is added to our specs
    - No, because we the developers specify the available URLs
- A Ruby method connected to the URL is called
    - That's right! This is the _action method_ that does the work of rendering or redirecting
{: .choose_best #bin points="30" answer="3" }


## RCAV: Route

The key is _routes_. _Routes_ are how we connect a URL to an _action_. 

The `config/routes.rb` file included in every Rails app lists all of the URLs (_routes_) that a user can visit. When someone visits the URL we say which class and which method Rails should execute to handle the request. Here is an example of a route:

<aside markdown="1">
It's finally time to move out of our `public/` and `tasks/` folders, and use more of our Rails application by working in the `app/` folder, where most of our code goes, and with this one file `routes.rb` that is in the `config/` folder.
</aside>

```ruby
# config/routes.rb

self.get("/rock", { :controller => "application", :action => "play_rock" })
```

The method here is `get` and there are parentheses for its _two arguments_: 

<aside markdown="1">
Later we'll use other methods besides `get`, like `post`, if we want to support requests using the other HTTP verbs.
</aside>

  1. A `String`: the _path_ that we want users to be able to visit (the **path** is the portion of the URL that comes after the **domain name**). Here it is `"/rock"`.

  2. A `Hash`: this is where we tell Rails which method to call when a user visits the path in the first argument. (We'll have to actually write this method in the next step, after we write the route.)

The `Hash` must have two key/value pairs:

  - `:controller`: The value for this key is what we're going to name the Class that _contains_ the method we want Rails to call when the user visits the path. For now we're going to default this value to `"application"`.

  - `:action`: The value for this key is what we're going to name the method itself. _Action_ is the term used to refer to Ruby methods that are triggered by users visiting URLs.

The `Hash` is saying: _"Use a `Class` (controller) called `application_controller`, and in that `Class` use a `method` (action) called `play_rock` to generate a response for the user."_

Don't be confused by the key names `:controller` and `:action`, these are equivalent to a Ruby Class and method. They just have special names in the lingo of web applications.

The `get` method is _inherited_, we don't need to build this method ourselves, which saves us a lot of time. We get the plumbing for free and we just need to tell Rails how we want each request to be handled by declaring our routes. 


## RCAV: Controller, Action, View

All of our controller Classes will be in the `app/controllers/` folder. There's already one controller that comes with every Rails app: `ApplicationController`, found in `app/controllers/application_controller.rb`. _This_ is the controller that the `get("/rock", ...)` route is referring to. We will just use this default controller for now. Later we will make separate controllers to keep our code organized.

Here is an example of an action in the controller:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def play_rock
    self.redirect_to("https://www.wikipedia.org")
  end 
end
```

We get the Class definition "for free":

```ruby
class ApplicationController < ActionController::Base
```

`ApplicationController` inherits, with the symbol `<`, from the `ActionController::Base` Class, which is inside the Rails **`gem`**.

<aside markdown="1">
Since the `ActionController::Base` Class is contained in the Rails `gem` in our `Gemfile`, we would need to go to GitHub to actually look at it.
</aside>

Inside of this Class, we define a method:

```ruby
def play_rock
```

We could write whatever Ruby steps we want in this method, like getting a random number, calling APIs, etc. But, in the end, the job of an _action_ is to send back a response to the user. A response can be either:

 1. _Rendering_ some data, in any one of many formats:
    - Plain text.
    - HTML for their browser to draw — we'll learn this soon.
    - JSON for an application to consume — we'll see JSON when we cover APIs.
    - Less commonly, any other format: CSV, PDF, XML, etc.

 2. Or, the action can _redirect_ the user to _another_ URL. 

In fact, we inherited (via `< ActionController::Base`) a method for each of these: `render` for the first, and `redirect_to` for the second.
 
In our example, we chose to _redirect_ to another URL:

```ruby
self.redirect_to("https://www.wikipedia.org")
```

The argument to `redirect_to` is a `String` which contains some URL that we want the user to be forwarded to. 

This is the _V_ in _RCAV_. We defined a _route_ to the URL path **/rock**, and in that route we indicated a _controller_ and an _action_ within that controller. After creating this Class and method, we give the user something to _view_ in their browser.

More often, we will `render` some HTML for the user, but `redirect_to` will come in handy in later projects. For example, when we want to send the user directly back to a list of all photos after they've deleted a photo.


## Dropping `self.`

Before proceeding, let's get something out of the way. 

We are using the `self` keyword in our example because we are calling these methods on the Class (`ApplicationController`) that we are defining the action (`play_rock`) for. Recall when we learned about the `Person` Class, with the instance methods `first_name` and `last_name`. If we wanted a `full_name` method we called `self.first_name + self.last_name`. 

In our example, we're defining `play_rock` and we want use the method `redirect` that already exists on `ApplicationController`. We don't see `def redirect` in our Class, since it's inherited via `< ActionController::Base` and is defined there. So, we are using a method that already exists in the Class to build our new method, hence `self.redirect_to`. 

But, in Ruby, when we call a method on `self`, we can drop the `self.`, and Ruby will figure it out. Before anything, Ruby will look to see if that object exists in the Class, no `self.` required! 

In practice, that means we can re-write the code to:

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


## Starting Our Gitpod Workspace

Enough theory. It's time to open the Gitpod project so we can visualize the steps and see some results. We'll finally make our Rock, Paper, Scissors game work, by having the computer opponent randomly choose a move rather than always playing paper. We will then be able to compute outcomes based on the computer's move.

[Here](https://github.com/appdev-projects/rps-rcav){:target="_blank"} is the assignment. As usual:

  1. Start the web server by running `bin/server`.
  2. Navigate to your live application preview.
  3. As you work, remember to navigate to **/git** and *Always Be Committing (ABC)*.
  4. Organize your workspace tabs.
  5. Run `rails grade` as often as you like to see how you are doing, but make sure you *test your app manually first* to make sure it matches the target's behavior.

If you need a refresher in starting the workspace, see the [Technical Setup][Technical Setup]

The [target](https://rps-rcav.matchthetarget.com/){:target="_blank"} for this project, looks similar to what we have produced. But, the key difference is that the computer plays different moves, so the application is finally *dynamic*. 


## Our First RCAV

Our workflow for a ***dynamic web application*** is always the same: Route, Controller, Action, View (RCAV). *The world is ruled by URLs*, so we will always start with what URL we want to build and get it to work.

Navigate to the route **/rock** in our Rails browser. We will no longer write out the entire URL path with **http\://[APP DOMAIN]** preceeding the route of interest. A lone **/** signifies the homepage and anything else is another route (page) in the app.

At **/rock**, you should see an error message: 

```
No route matches [GET] "/rock".
```

![](assets/rps-rcav/err-no-routes-match.png)

We need to *Read The Error Message (**RTEM**)*. This error message is telling us that we need to define the route. 

Open the file `config/routes.rb` and define the route by adding the following code:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/rock", { :controller => "application", :action => "play_rock" })

end
```
{: mark_lines="5" }

All of our routes must be contained within the block following `Rails.application.routes.draw`. A new Rails app will already come with this code pre-written in `config/routes.rb`.

Again, we have our route `"/rock"` and our key/value pairs for the `:controller` (or Class) and `:action` (or method). We need to choose a value for the `:controller` that Rails will use, and the `:action` within the controller that will be executed. For now we are just using the `app/controllers/application_controller.rb` for the controller, and we will define our action `play_rock` in there.

Now, open the file `app/controllers/application_controller.rb`. Rails is smart and will add `_controller.rb` to our `:controller` argument in `get`, and within that controller file you will see the Class has the underscores removed and is capitalized as `ApplicationController`. You should follow these conventions.

<aside markdown="1">
To summarize the naming convention: In `get`, the controller is `application`. That refers to the `snake_case` controller `application_controller`, which contains the `CamelCase` Class `ApplicationController`. 
</aside>

Add the following code:

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

Our action `play_rock` exactly matches what we wrote in the `config/routes.rb` file: `:action => "play_rock"`. Between the `def play_rock` and `end`, we could put *whatever* and *however* much code we would like to execute in that action for the user. In the end, we will need to either *render* some HTML back to the user or *redirect* the user to another place. Let's begin with a redirect:

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

Go back to the browser and refresh the URL **/rock**. You should be sent to Wikipedia. Boom! We just created a full RCAV *request lifecycle*. 

Check out the server log in your Gitpod workspace. That is the terminal running `bin/server`. (Use <kbd>Ctrl</kbd> + <kbd>J</kbd> to open and close the terminal pane, find the `bin/server` terminal, and possibly use <kbd>Ctrl</kbd> + <kbd>K</kbd> to clear it for a cleaner view.) We should see something like:

![](assets/rps-rcav/rock-to-wikipedia-server-log.png)

The server log tells us *exactly* what happened. Someone tried to `GET "/rock"` from a given IP address at a given time, we found a route with instructions to use `ApplicationController#play_rock`, calling this controller/action pair resulted in a redirect to the given URL (`https://www.wikipedia.org`), and the entire request lifecycle completed in the stated time with no errors. Hooray!

### Our First RCAV: Completed Code

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/rock", { :controller => "application", :action => "play_rock" })

end
```

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

## Render HTML

We've written our first functional action, which just redirects someone to a new page. Now let's *render* some of our own HTML. 

Change the previous code in `app/controllers/application_controller.rb` to:

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

Rather than `redirect_to`, we'll use another inherited method to complete the request lifecycle: `render`.

This method, takes a `Hash` as an argument with a key/value pair. The key has many options, here we use `:plain`, which will just send back plain text. A boring response, but good to start with.

Now, pretend you're a user and visit **/rock** in the Gitpod browser. You should see a mostly empty page with the text "Hello, world!" rendered. 

Congratulations! You've wired up a route; prepare to do it a million more times, because all developers do all day is pick the next *spec*, wire up the route for the URL so that a user can visit it, and then implement the logic to send back the correct information.

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

Now everytime we refresh **/rock**, we get a different random number, generated automatically by Ruby. This is a *dynamic response*, not just a static page that we placed in the `public/` folder. This is a simple example, but fundamentally that's it. We connected a URL to a method that can do *anything*. It can call APIs, parse CSVs, compute whatever we want, run machine learning models, etc. Of course, there is a lot more to learn, but *fundamentally this is it*. 

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

The `:html` key allows us to place whatever HTML we want in a `String` that will be shown on the page. We need the `.html_safe` on the end of the `String`. Don't worry about this, we will see a better way in a moment.

<aside markdown="1">
If you really want to know, `.html_safe` is a bit of Rails security to prevent one user from injecting malicious HTML into another user's browser, in case we were getting the given HTML `String` from the user (e.g. from a `<form>`). 
</aside>

If we refresh **/rock**, then we should see our rendered HTML. We could go crazy and put our entire HTML document in that `String`. But a much better way is to use an **embedded Ruby template** file.

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

The `:template` key to `render` lets us assign a **view template**. We specify the name of a folder `game_templates/` and file `user_rock.html.erb` that will contain all of our HTML. This file is an `.html.erb`, for *embedded Ruby template*, rather than a plain `.html` file. 

We can now create this file in the existing `app/views/` folder. All of our application view templates will go here. It is far safer folder than `public/`, because users do not have access to its contents, and cannot modify the source code. 

We want to keep things organized and put different templates in different sub-folders. Do not put the `.html.erb` file in the `app/views/layouts/` folder that already exists. 

First make a new folder in `app/views/` by right-clicking on the folder and selecting "New Folder...", then naming the folder `game_templates`. Then, right-click on this new folder, select "New File...", and create `user_rock.html.erb`. The entire filepath will look like `app/views/game_templates/user_rock.html.erb`.

**BENP: insert gif of create new folder and create new file steps in Gitpod**

By using `:template =>` in `render`, Rails knows to look in `app/views/`. We could call the `game_templates/user_rock.html.erb` folder and file whatever we want. The user will not see the folder or the file, they will only see **/rock**, the specified route, in their browser.

Open the newly created `user_rock.html.erb` file and add some HTML to render:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>
```

*Don't forget to save the file changes if you haven't done so.*

And now when we refresh **/rock**, we get the text from our *new file* rendered in HTML.

After all of that, we have an HTML page that does what we could have done quickly if we made a file called `rock.html` in the `public/` folder. But we can do something way better with this new system. 

### Completed Code

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

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>
```


## Embedded Ruby Tags

What can we do with this new system? Add the following to our embedded Ruby file:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<h2>
  They played <%= %>!
</h2>
```
{: mark_lines="5-7"}

We created a new tag that *looks* like HTML, but contains a *doorway to Ruby*: `<%= %>`. We can write any Ruby we want in that ***embedded Ruby tag***. *This is what makes the whole effort of RCAV worthwhile!* 

For instance, we can write:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<h2>
  They played <%= 6 * 7 %>!
</h2>
```
{: mark_lines="6"}

And we will see the result of this computation when we refresh **/rock**. (Did you *save* the changes in the file before refreshing the browser?) But, if we right-click and "View page source" in the browser, we won't see the Ruby code. We only see the result `42`. 

The browser *only* understands HTML and has no idea of the code that allows us to make the web application dynamic. Rails is processing all of the embedded Ruby tags and injecting them in the document before it sends the plain HTML file to the browser. 

We could also do something like:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= 6 * 7 %>!
</h2>
```
{: mark_lines="5"}

Here, we used a slightly different embedded Ruby tag: `<% %>`. We left off the `=` sign, which means the output of this Ruby code will be hidden in the rendered HTML. But, the variable `comp_move` (the result of randomly sampling an array of three possible `String` values) is still available and we can render that by changing the file again:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= comp_move %>!
</h2>
```
{: mark_lines="8"}

Our calculated variable `comp_move` is now rendered in the final HTML output, because it is in a `<%= %>` tag, with the `=` sign. And we will see the result of this computation when we refresh **/rock**. Again, "View page source" here and you won't see any sign of the `comp_move` variable computation from the `<% %>` tag.

Alright, we are now finally building dynamic web applications. We are able to render a template, we are able to write some HTML, and we are able to use *embedded Ruby tags*: `<% %>` for hidden content, and `<%= %>` for rendered content.

### Completed Code

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= comp_move %>!
</h2>
```

## Control Flow with Embedded Ruby

With the power of Ruby, we can actually compute who won or lost our Rock, Paper, Scissors match on the page before rendering the HTML to the user. Add the following `if-else` embedded Ruby code to our view template:

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

Do you understand this added code? *Read* it carefully and try to understand the logic before you keep reading.

We used hidden `<% %>` embedded Ruby tags in our **control flow** on each line we wanted to hide from the user. Only the result of this control flow `<h2>We tied!</h2>`, `<h2>We lost!</h2>`, or `<h2>We won!</h2>` will be rendered, *depending on the randomly sampled `comp_move` variable*. Refresh **/rock** a few times to see. 

If you haven't, now would be a good time to run `rails grade` at the Gitpod terminal to check your progress. And remember to *Always Be Committing (ABC)*, by making a **/git** commit. We have a lot done, but we still have a lot to do.

### Completed Code

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


## Reinforce RCAV with /

Before we go on with the embedded Ruby, let's reinforce RCAV a couple of times.

The [target](https://rps-rcav.matchthetarget.com/){:target="_blank"} has a homepage at the root URL, **/**. In the old days, we would create a file in `public/` called `index.html`, but from here on we will connect any URL with routes. 

Open the `config/routes.rb` file and add a homepage route:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  
  get("/", { :controller => "application", :action => "homepage" })

  get("/rock", { :controller => "application", :action => "play_rock" })

end
```
{: mark_lines="5" }

We are using `get` to add the `"/"` homepage route. `:controller => "application"` signifies that we are using the `app/controllers/application_controller.rb` file for our controller, and `:action => "homepage"` is a yet to be defined action in the controller. 

In the browser, pretend to be a user and navigate to the URL **/** in the address bar. **RTEM**.

```
The action 'play_rock' could not be found for ApplicationController
```

![](assets/rps-rcav/err-action-not-in-contoller.png)

This is good! That means we defined the route correctly. If you still see a "No route matches" error, then double-check your route syntax in the `get` method, save the changes, and get that error to go away before you proceed. 

The new error occurs because we did not yet define the action! So we need to open `app/controllers/application_controller.rb` and add:

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

Now create the view template file `game_templates/rules.html.erb`, again in `app/views/` where *all* our view templates live in organized subfolders. Once you create the file, add some HTML copy to it:

```html
<!-- app/views/game_templates/rules.html.erb -->

<h1>Welcome to RPS</h1>
```

Now refresh **/**. There is no error and our HTML template is rendered. And we did not put any HTML in the `public/` folder! You will almost always want some kind of dynamic behavior on every page. So our new workflow is *always RCAV*: Define a *route*, assign a *controller*, create an *action* in that controller, and *view* the result.

### Completed Code

```ruby
# config/routes.rb

Rails.application.routes.draw do
  
  get("/", { :controller => "application", :action => "homepage" })

  get("/rock", { :controller => "application", :action => "play_rock" })

end
```

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

```html
<!-- app/views/game_templates/rules.html.erb -->

<h1>Welcome to RPS</h1>
```

## Reinforce RCAV with /paper

Let's reinforce the steps again with the **/paper** route, for when the user plays paper. First, define the route in `config/routes.rb` with a controller:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  
  get("/", { :controller => "application", :action => "homepage" })

  get("/rock", { :controller => "application", :action => "play_rock" })

  get("/paper", { :controller => "application", :action => "play_paper" })

end
```
{: mark_lines="9" }

Again, we use the `application_controller.rb`. If we pretend we are a user now and go to **/paper**, we again get the "action not found" error. The helpful error message (RTEM!) tells us we need to define another method for the action in our controller called `play_paper`. 

It's the same flow, over and over again. Make a change, visit the route, RTEM, and find the next step.

Ok, then define the action in our controller:

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

Refresh **/paper**, and we'll get a new error message:

```
Missing template game_templates/user_paper.html.erb
```

![](assets/rps-rcav/err-missing-view-template.png)

If you keep getting the same error message, there are a few steps you can try:

  1. Carefully scan your code for a typo. Your syntax needs to be exact. *Grammar* matters!
  1. If you cannot figure out what your typo is and why an error message keeps coming up, then delete what you wrote and try to type it again from scratch.
  1. Explain the code line-by-line out loud to yourself or someone else.

Back to our new error, we RTEM, and that tells us to go and make the new `game_templates/user_paper.html.erb` file (in `app/views/`) that will be rendered to the user:

```html
<!-- app/views/game_templates/user_paper.html.erb -->

<h2>
  We played paper!
</h2>
```

Refresh **/paper**. No error message? A successful RCAV!

### Completed Code

```ruby
# config/routes.rb

Rails.application.routes.draw do
  
  get("/", { :controller => "application", :action => "homepage" })

  get("/rock", { :controller => "application", :action => "play_rock" })

  get("/paper", { :controller => "application", :action => "play_paper" })

end
```

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

```html
<!-- app/views/game_templates/user_paper.html.erb -->

<h2>
  We played paper!
</h2>
```

## Embedded Ruby in the Controller with Instance Variables

Now that we are RCAV pros, we can go back to the embedded Ruby we used to make **/rock** truly dynamic. Let's see another (perhaps better) way of writing our embedded Ruby code. 

Open the `user_rock.html.erb` file:

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

The highlighted code `<% comp_move = ["rock", "paper", "scissors"].sample %>` is okay for this trivial example, but in a real application there may be dozens of lines of code to prepare the information for the user. We may lookup data from a database, do some math on it, find API data, and more. We want somewhere other than the HTML template to put this code.

Go back to the `game_templates/user_paper.html.erb` file associated with **/paper**, since we didn't get far there. We would like our file to look like this:

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

We *wish* we could just do this and avoid all the lines of embedded Ruby that are in the previous `user_rock.html.erb` view template. These computations really don't belong here. The view templates should be given some data and then their job should just be to format and present it beautifuly and usably to the user. In the *backend* the responsibility should be marshalling the correct data and sending it to the view template.

Well, return to our controller file and add the following:

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

*STOP*. Read the added code. Do you understand it? Yes? Okay, keep reading.

We have removed all of the embedded Ruby tags (`<% %>` and `<%= %>`) from the code we had in the `user_rock.html.erb` view template and added a new `outcome` variable to hold a `String` that depends on the control flow associated with the random computer move `comp_move`. 

Now, when a user visits the route **/paper**, the action `play_paper` in the controller `ApplicationController` will be triggered, and the code will be run *before* the template is rendered. 

So let's try to visit **/paper** again. Oops, we get this error:

```
undefined local variable or method `comp_move' for #<#Class...
```

![](assets/rps-rcav/err-undefined-local-var-or-meth.png)

This error is coming from our `user_paper.html.erb` view template, when the browser gets to the first embedded Ruby tag:

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

That *local variable* `comp_move` is undefined! 

A **local variable** only exists in the scope it was defined. If we create a local variable in a loop, it will only exist *in that loop*. If I want some variable available outside the loop, then I would need to create it outside the loop and modify it in the loop. We can't just use the `comp_move` local variable in our template if we created it in the `play_paper` method (action). The variable is effectively "dead" after `play_paper` executes. 

Then how do we make the controller variables available in the view template? We can do this by modifying our controller:

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

All we did was place an `@` character before any variable that we want access to in our view template. This is a new kind of variable called an **instance variable**. This type of variable will survive as long as the *instance of the object in which it's created survives*. 

When someone visits **/paper**, Rails creates an instance of the `ApplicationController` Class and then executes the `play_paper` method (because `get` in `config/routes.rb` told it how to respond to this route!). As long as the `ApplicationController` instance is "alive" (until the response is sent to the user by rendering HTML in their browser), the *instance variables* produced by `play_paper` will exist! 

All that is to say, by adding `@`, we now have `@comp_move` and `@outcome` available for our template. We just need to make sure those instance variables are also properly referenced in `user_paper.html.erb`:

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

Again, we just use the leading `@` on our variables to tie them to the instance variables in the controller. And if we visit the **/paper** URL, it works! And we have a vastly improved organization. 

Most computation work like this should go in the controller as we have done it here. We will have some cases where more embedded Ruby goes in the template (e.g. rendering database records with `.each` loops, `if` statements to check if a user is allowed to see something, other conditional statements). In general, if it *can* happen in the controller, it *should* happen there.

If **/paper** appears to work when you test it manually, then it's time for a `rails grade` and a **/git** commit.

### Completed Code

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

## Linking Pages with Layouts

Before you tackle the rest of the project on your own, it would now be nice to add some links (like in our [target](https://rps-rcav.matchthetarget.com/){:target="_blank"}), so we don't need to keep typing in the URL addresses.

Start with our `user_paper.html.erb` view template:

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

Now we should see links at **/paper**. But, if we click on "Play Rock", and we are taken to the **/rock** URL, then the links are not there. Because we only put them in the `user_paper.html.erb` file, and not in the `user_rock.html.erb` file, which is what visiting the **/rock** URL will render.

How can we avoid repeating these HTML navigation links in all of our view templates? 

Here is one of the great benefits of working in Rails instead of HTML. We are dynamically generating responses rather than hard-coding into a bunch of files. If there is common stuff we want on every page, like a navbar or footer, then we can make a special file in `app/views/layouts/`. 

Create a file in that folder called `wrapper.html.erb` and fill it with:

```html
<!-- app/views/layouts/wrapper.html.erb -->

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

Copyright, Appdev. All rights reserved.
```
{: mark_lines="13"}

Every page will now have all of its contents placed in the location of `<%= yield %>`, and everything above and below this will be rendered on that page. `yield` is one of many special Ruby objects that we have access to in our Rails application. We just need to also change our `application_controller.rb` file to note this, and have it take effect:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout("wrapper.html.erb")
  ...
```
{: mark_lines="4"}

This inherited `layout` method takes one argument. It already knows to look in the folder `app/views/layouts/` for the file that we created.

<aside markdown="1">
We never defined `layout` in our `ApplicationController` or anywhere else. So we know it is **inherited** and coming from `< ActionController::Base`.
</aside>

After this change, try visiting your pages using the links. It should work, except for **/scissors**, because we haven't done the RCAV yet.

If we only wanted the layout to apply on a per-page basis we could also leave `layout(false)` in the controller. Then, in the `play_rock` method (action), we could change our render statement to:

```ruby
render({ :template => "game_templates/user_rock.html.erb", :layout => "wrapper.html.erb" })
```

This additional `:layout` argument would then only put the navbar and footer from `wrapper.html.erb` on the **/rock** route.

Time for a `rails grade` and a **/git** commit! 

### Completed Code

```html
<!-- app/views/layouts/wrapper.html.erb -->

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

Copyright, Appdev. All rights reserved.
```

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  layout("wrapper.html.erb")
  ...
```

## Finish and Submit RPS RCAV

The rest of the project is up to you to finish. 

Here is the project: [https://github.com/appdev-projects/rps-rcav](https://github.com/appdev-projects/rps-rcav){:target="_blank"}

And the target: [https://rps-rcav.matchthetarget.com](https://rps-rcav.matchthetarget.com){:target="_blank"}

Visit the **specs** and wire them all up. You have all the tools now. Use the resources in this chapter, including an [RCAV cheat-sheet][Addendum: RCAV Flowchart]. 

Remember [`rails grade`][`rails grade`], [git][Using Git to freely experiment and save work], and [Sharing a Gitpod Snapshot][Sharing a Gitpod Snapshot] if you're uncertain about the technical setup and getting help along the way.


## Addendum: RCAV Flowchart

Our apps are nothing more than a collection of URLs that we decide to allow users to access:

 - **mydomain.com/products**
 - **mydomain.com/photos/193**
 - **mydomain.com/signin**

So remember: everything always starts with a *route* between an *address* we want users to be able to visit and a *Ruby method* that will be responsible for generating a response to the user's browser.

In order to support a URL in your app such as **https://3000-your-gitpod-workspace.gitpod.io/home**, there are a lot of dots to connect!

![](assets/rps-rcav/rcav-chart.png)

 1. A user visits an address in our app; in this case, we chose **/home**.
 2. If we want to allow users to visit that address, we have to add a *route* for it in `config/routes.rb`.
 
    The complete route looks like this:
    
    ```ruby
    get("/home", { :controller => "pages", :action => "home" })
    ```
    
    Here's what's going on:

    A route is defined using the `get()` method, which has two arguments. The first argument is a `String` that contains the address we want to support; in this case, `"/home"`.
    
    The second argument to `get()` is a `Hash` that tells Rails what to do when someone visits the address. The `Hash` has two keys: `:controller` and `:action`.
 
    "Controllers" contain the logic of how to respond to requests (they're just Ruby classes).
    
    "Actions" are the actual logic that gets executed by Rails when a user visits an address (they're just Ruby methods).
    
    The key `:controller` must go to the name of a Ruby class; in this case, we chose `"pages"`.
    
    The key `:action` must go to the name of a Ruby method that we want Rails to execute when a user visits **/home**; in this case, we chose `"home"`. This name is *not required to match the route*.
  
3. Rails finds a match for the controller name we specified in the `app/controllers/` folder. Files that contain controllers must always end in `_controller.rb`, and begin with what we said in the route would be the name of the controller; in this case, `pages_controller.rb`.
  
    Rails finds the Ruby class in the file. The name of the class must be `CamelCased` and always end in `...Controller < ApplicationController`. In this case, `PagesController < ApplicationController`.
    
    Rails finds the method we specified as the action and executes it; in this case, we defined a method called `home`.
    
    We can write as much or as little Ruby as necessary within the action to satisfy the request — reading from APIs, doing math, whatever.
  
4. Once we've computed the final values that should be displayed to the user, we tell Rails the name of an *HTML view template* to use to format the output. To do so, we use the `render()` method. The complete `render()` method looks like this:
    
    ```ruby
    render({ :template => "page_templates/home.html.erb"})
    ```

    Here's what's going on:

    `render()` takes one argument, a `Hash`. The Hash must have a key, `:template`, with a `String` value. The `String` specifies the location of an Embedded Ruby HTML template to use to format the output. The first part of the `String` specifies the name of a folder, in this case `pages_templates` and the second part of the `String` specifies the name of a file, in this case `home.html.erb`.
  
    We have to create a folder within `app/views/` that matches the name that we specified in the `render()` statement.
  
    We have to create a file within that folder that matches the name that we specified in the `render()` statement.

    Finally, if we've connected all the dots correctly, Rails will embed the variables in the `.html.erb` template, produce a final plain `.html` file, and send it back to the user's browser. Hurray!
 
If you _didn't_ connect the dots correctly, you will usually see a very descriptive error message; try to read and understand it.

Some things to keep in mind:

 - Capitalization (all file, folder, method, variable, and symbol names should be `snake_case`; only class names are `CamelCase`).
 - Spelling/pluralization matters (by convention, controller names are usually plural, but don't have to be).
 - Location (controller files must be in `app/controllers/`).
 - *READ THE ERROR MESSAGE!* It usually tells you exactly what is going wrong, and where. It will at least give you a strong hint.


## Addendum: Custom Controller Files

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
 - Don't forget the `end` that goes with the Class; type it before you forget it.
 - Move your `play_rock` action over from `application_controller.rb` into this new class.
 - Now, when a user visits the path **/rock**, the "uninitialized constant" error should go away and you should see a response as before.

    If you still see the "unitialized constant" error, then:

    - You named your class wrong; it must exactly match the value in `routes.rb`, followed by `Controller` (singular), and `CamelCase`.
    - You named the file wrong. Try doing `.underscore` on a string containing the class name in `rails console` to figure out the correct filename.
    - You put the file in the wrong folder. It has to be within `app/controllers/`. Not within, for example, `app/` or `app/controllers/concerns/`.
    - You forgot the `.rb` file extension.
    - If you can't find which of the above it is, try deleting what you did and paving over your work again from scratch. Sometimes you just can't spot your own typos, and paving over is the best approach.

You can make as many controllers as you like; in general, a rule of thumb is to have one controller per database table.

## Addendum: Rendering JSON

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

