# Rock, Paper, Scissors (RPS) -- Route, Controller, Action, View (RCAV) Part 1

We can now use HTML and CSS for designing web pages, and Ruby for writing programs. However, if we (the developers) are the only ones that can _run_ these programs (through the `ruby` interpreter), then they aren't much use. It's time to start adding an _interface_ on top of our Ruby programs so that external users can interact with them.

We already have all the tools to build our first **dynamic web application**. But, before we begin building, we need to understand the URL request lifecycle of _Route, Controller, Action, View (RCAV)_.

In this lesson, we will explore routing. In practice, the project we work through will make our Rock, Paper, Scissors webpage dynamic; meaning it will actually work by having the computer opponent randomly choose a move rather than always playing paper. We will then be able to compute outcomes based on the computer's move.

## Starting Our Gitpod Workspace

Before we proceed, let's get the Gitpod project setup for this lesson. The basic steps are outlined below, but you can refresh your memory on the details [here](https://learn.firstdraft.com/lessons/29){:target="_blank"}.

<div class="proj" markdown="1">

  Open the Gitpod [RPS-RCAV](https://github.com/appdev-projects/rps-rcav-v2){:target="_blank"} project on Canvas by clicking the "Load in new window" button, then click on the green button to "Create new workspace on Gitpod", which will fork the workspace to your appdev organization.
  
  As usual:

  1. Start the web server by running `bin/server`.
  2. Navigate to your live application preview.
  3. As you work, remember to navigate to **/git** and *Always Be Committing (ABC)*.
  4. Organize your workspace tabs.
  5. Run `rails grade` as often as you like to see how you are doing, but make sure you *test your app manually first* to make sure it matches the target's behavior.

  The [target](https://rps-rcav.matchthetarget.com/){:target="_blank"} for this project, looks similar to what we have produced. But, the key difference is that the computer plays different moves, so the application is finally *dynamic*.

   Keep the Gitpod tab open. If you close the Gitpod workspace, you can always click the Canvas link again, but this time click "Find existing workspace in Gitpod Dashboard". In a separate tab in the same browser window, keep the [target](https://rps-rcav.matchthetarget.com/){:target="_blank"} open. Also, keep this lesson open in another tab.

</div>

----

#### Quiz Question

- Were you able to start the Gitpod workspace, including running `bin/server` and opening the browser?
- Yes
    - Great, you are ready to move on.
- No
    - Debug the issue by visiting these instructions: https://learn.firstdraft.com/lessons/29 before proceeding, you need the workspace open and working.
{: .choose_best #open_gitpod points="10" answer="1" }

<!-- **TODO:** hide URL in No answer when we get HTML rendering properly there -->

----

## URLs and Specs

For an application that runs on a server and transmits information across the internet (i.e. Software as a Service, **SaaS**), the interface consists of a set of Uniform Resource Locators (**URLs**) that a user can visit, and receive some information relevant and valuable to them.

<!-- ![](assets/rps-rcav/airbnb-url.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1676597248/airbnb-url_ywgt3x.png)

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
Recall that `Object#method` notation symbolizes an [**_instance_ method**](https://learn.firstdraft.com/lessons/19#defining-instance-methods){:target="_blank"}, while `Object.method` notation symbolizes a [**_class_ method**](https://learn.firstdraft.com/lessons/19#defining-class-methods){:target="_blank"}.
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

----

#### Quiz Question

- What happens when a user in our app visits a URL from their address bar? Choose all that apply.
- A Ruby Class is created for the page
    - Not quite, recall the term **instance method**
- This URL is added to our specs
    - No, because we the developers specify the available URLs
- A Ruby method connected to the URL is called
    - That's right! This is the _action method_ that does the work of rendering or redirecting
- The user is redirected somewhere, or some content is rendered for them
    - That's right! These are typically the two actions that result from someone visiting a URL
{: .choose_all #user_visits_url points="10" answer="[3,4]" }

----

# What's an RCAV?

For the next few sections, just follow along with the text, in the next part of the lesson, we will actually be typing things out in our Gitpod workspace.

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

----

#### Quiz Question

- What are the `:controller` and `:action` arguments in the `get` function equivalent to?
- They both indicate methods (_verbs_) that we call on an object (_noun_)
    - Not quite, only one of them is a method, which one?
- `:controller` indicates a Class object and `:action` is a method in that Class
    - That's right, the Class is `application_controller` and the method is `play_rock`.
- `:controller` indicates a method and `:action` is the Class that method is in
    - Not quite, it's actually the other way around.
{: .choose_best #controller_action points="10" answer="2" }

----

#### Quiz Question

- Based on the `Hash` input to our `get` method, which action will be triggered when the user visits the URL path **/rock**?
- :controller
    - The `:controller` is a key to the `Hash`, but what is it pointing it?
- :action
    - The `:action` is a key to the `Hash`, but what is it pointing it?
- application
    - The `"application"` value for the `:controller` key indicates _where_ the action that we want to call is. That is, which Class the action method is inside of.
- play_rock
    - Correct! The `play_rock` action is indicated by `:action` in the `Hash`.
{: .free_text #play_rock points="10" answer="4" }

----

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
Since the `ActionController::Base` Class is contained in the Rails `gem` in our `Gemfile`, we would need to go to GitHub to actually look at it. Remember, `gem`s are just Ruby code libraries written by other developers that we import into our project to avoid reinventing the wheel.
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

----

#### Quiz Question

- How did we get the `redirect_to` function?
- We got it from `ActionController::Base`
    - Yes, via the `<` notation for *inherited*. And that Class where the function lives is in the Rails `gem`
- We don't have access to this function.
    - Not quite, look above at the term *inherited*.
- We defined it ourselved.
    - Not quite, look above at the term *inherited*.
{: .choose_best #redirect_to points="10" answer="1" }

----

#### Quiz Question

- What does the _V_ in RCAV actually mean?
- Very good job rendering the page.
    - Nope, re-read the previous section and try again.
- Value has been added to the software we are building by adding a page.
    - Nope, re-read the previous section and try again.
- View the result as the developer and check it looks good.
    - Not quite, can we be more specific with one of the other answers here?
- Setup the action to either render or redirect the user somewhere (i.e., setup a new "view" for them).
    - Yes, this is the last step in the RCAV, where we provide the user with some result.
{: .choose_best #v_in_rcav points="10" answer="4" }

----

## Dropping `self.`

Before proceeding, let's get something out of the way. 

We are using the `self` keyword in our example because we are calling these methods on the Class (`ApplicationController`) that we are defining the action (`play_rock`) for. [Recall](https://learn.firstdraft.com/lessons/19#defining-instance-methods){:target="_blank"} when we learned about the `Person` Class, with the instance methods `first_name` and `last_name`. If we wanted a `full_name` method we called `self.first_name + self.last_name`. 

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

----

#### Quiz Question

- What does the `self` keyword refer to?
- The user
    - Nope, re-read the previous section and try again.
- The developer
    - Nope, re-read the previous section and try again.
- The Class that a given object or method is being called from within
    - Yes, that's correct.
{: .choose_best #drop_self points="10" answer="3" }

----

## Conclusions

Okay, that was a lot of information. It's time to actually move over into our [Gitpod project space](https://learn.firstdraft.com/lessons/22#starting-our-gitpod-workspace){:target="_blank"} and start typing things out to get our application running! 

<span style="font-size: x-large">[Proceed to the next part of the lesson](https://learn.firstdraft.com/lessons/23){:target="_blank"}</span>

----