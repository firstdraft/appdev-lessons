# Fortune Teller

- Notes:

  - [Original video](https://uchicago.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=8c2e54f8-4bed-47d2-82b2-aeca0102f92c){target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/fortune-teller.md){target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/fortune-teller](https://github.com/appdev-projects/fortune-teller){target="_blank"}

  - Target: [https://fortune-teller.matchthetarget.com/](https://fortune-teller.matchthetarget.com/){target="_blank"}

  - Useful chapters:

    - [Adding Routes][Adding Routes]
    - [RCAV Flowchart][RCAV Flowchart]
    - [Routing - RCAV Slides](https://firstdraft.slides.com/raghubetina/06-routing-rcav?token=43w7FD8Q){target="_blank"}

## Video Segment: Routes and Controllers in Fortune Teller

- Notes:

  - time stamp 00:03:28 to 00:10:50
  - practice routing
  - stepping away from `app/controllers/application_controller.rb`, and using `app/controllers/numbers_controller.rb`
  - inheritance: `NumbersController < ApplicationController < ActionController::Base`

Our plan for today is to practice the very important thing for this week which is *routing*. How do you connect a particular visit to a URL to a Ruby method, and then generate some dynamic HTML and send it back. So that will be the day today. Practicing that over and over. **BENP: insert references to previous RCAV material here, like adding-routes.md and RCAV-flowchart.md**

This fortune teller project will be the first in a series of *debugging* projects. So rather than building up an app from scratch, we'll start with a completed app that we have planted pernicious bugs in. You have to go through and figure out how to *Read The Error Messages, RTEM*. Again, RTEM is the most important skill to develop, not being able to just scan the code and spot what's wrong. Let the error messages help you.

If navigate to your app in the browser, you should be on the homepage **/lottery/lucky** which shows you five lucky numbers in a bulleted list. Each time we refresh, the numbers are changing. So this is a dynamic page and not a static page in the `/public` folder on GitPod. 

Let's see what we are starting out with by going to our application on the GitPod workspace and opening our file `config/routes.rb`:

```ruby
# config/routes.rb

Rails.application.routes.draw do  
  # PART 1: EACH IN ERB
  # ===================

  get("/lottery/lucky", { :controller => "numbers", :action => "winners" })
  get("/", { :controller => "numbers", :action => "winners" })

  # Let users visit URLs:

  # - /lottery/unlucky

  # PART 2: R→C→A→V DEBUGGING
  # ======================

  # Uncomment each route below ONE AT A TIME and debug.
  # Do NOT uncomment more than one at a time, or you'll be dealing with multiple syntax errors at once.

  # get("/zodiacs/aries", { :controller =>  fire, action =>  "ram" })
  # get("/zodiacs/leo", { :controller => "fire", :action => "lion" })
  # get("/zodiacs/sagittarius" { :controller => "fire", :action => "archer" })
  
  ...

end
```

**BENP: not sure about the `...` notation above to indicate code**

In many senses, this is the most important file. This is the list of all of the URLs that users are allowed to visit in our app, so it's also a great place for us to start when we're trying to get to know a new codebase. 

If we look at this we can see there are two routes users can currently visit **/lottery/lucky** and **/**. We can return to our browser and test those two URLs. They will bring us to the same lucky numbers page. But if I try to visit anything else, like if I click on any of the navbar links, all other URLs don't work right now.

One thing we notice right away is that both paths in our `config/routes.rb` are using the same controller and action: `{ :controller => "numbers", :action => "winners" }`. And also, this controller called `"numbers"`, is different from `"application"`. The `app/controllers/application_controller.rb` is the file we have always used up to this point, as this is the `ApplicationController` that comes with every Rails application out-of-the-box. But, we can create our own controllers to keep things more organized.

If you specify something after `:controller =>` besides `"application"`, like `"numbers"`, then you need to create the file yourself in the `app/controllers/` folder. If we navigate to that folder, we see we have six controllers now. `application_controller.rb` is in there, but if we open it we see it's empty:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base

end
```

because we haven't used it in our app. Instead if we open the `"numbers"` controller:

```ruby
# app/controllers/numbers_controller.rb

class NumbersController < ApplicationController
  
  ...

  end 
end
```

We see that we've inherited (`<`) from `ApplicationController`, so we get all the power -- all the methods -- that our `ApplicationController` inherited from the Rails `ActionController::Base`. `ApplicationController` is a "child" of `ActionController::Base` and `ApplicationController` is a "parent" of `NumbersController`. 

Written out that would look like `NumbersController < ApplicationController < ActionController::Base`. **BENP: added that last two sentences based off some student questions in video**

This is a better way of organizing our controllers because in any standard app you are going to have dozens or hundreds of actions and `ApplicationController` would get cluttered if we put them all in the same file.

We may ask, with multiple controllers, can we share data (e.g., instance variables with the `@`-notation) across the controllers? The answer is, not really. Because when someone visits a particular URL in our app, at that moment Rails goes and looks up a single controller action and runs it. At any given moment, only one route is every being used by a user. So it doesn't matter if I have ten thousand actions in `ApplicationController` or spread across multiple child controllers, but they don't need to every communicate with each other. The action is run, we send the HTML back, and the request is done until the user visits another route. 

### Text Companion: Routes and Controllers in Fortune Teller

## Video Segment: `.each` Loop on `@` Instance Variable

- Notes:

  - time stamp 00:10:50 to 00:17:37
  - from `@zebra` instance variable array to `.each` loop in the view template for **/lottery/lucky**
  - embedded Ruby tags `<%= %>` vs. `<% %>`

Okay, so as we saw in our `config/routes.rb`, the action triggered when visiting **/lottery/lucky** or **/** is called `winners` in our controller:

```ruby
# app/controllers/numbers_controller.rb

class NumbersController < ApplicationController
  def winners
    @zebra = Array.new

    5.times do
      giraffe = rand(1...100)
      
      @zebra.push(giraffe)
    end

    render({ :template => "lottery_stuff/woohoo.html.erb"})
  end 
end
```
{: mark_lines="4-14"}

We chose to write this by first creating a new array (`@zebra = Array.new`), then we used the `times` method to generate a random number in a variable called `giraffe` and `push` the number into the `@zebra` array five times. There are other ways to do this, like creating five separate variables and putting a random number in each, that would have worked, but in this case I'm rendering the template `"lottery_stuff/woohoo.html.erb"`, with only one instance variable, the array `@zebra`.

Let's look at that template in `app/views/lottery_stuff`:

```html
<!-- app/views/lottery_stuff/woohoo.html.erb -->

<h1>Lucky numbers</h1>

<p>Your lucky numbers for today are:</p>

<ul>
  <% @zebra.each do |elephant| %>
    <li>
      <%= elephant %>
    </li>
  <% end %>
</ul>
```
{: mark_lines="8-12"}

**BENP: Again, notes about using `elephant`, `zebra`, `giraffe`. I wonder if it's better to use thoughtful variable names from the beginning and avoid this.**

The crucial part is highlighted. In our `.erb` template, we are using `.each` on our instance variable array `@zebra`. Inside of the looping block, we write HTML to display the variable using the `<%= %>` embedded Ruby tag. We could name the block variable `elephant` whatever we want (as long as we change the name in the loop as well as between the pipes `||`). It only exists in our loop and is not from the controller action.

This instance variable loop-and-display technique is something we are going to be doing a lot. This is a main reason we spent all that time learning about `.each`. Very often we have records from a database table and we need to format and display those records with this technique.

We could change the above code and see what happens. Let's do this:

```html
<!-- app/views/lottery_stuff/woohoo.html.erb -->

<h1>Lucky numbers</h1>

<p>Your lucky numbers for today are:</p>

<ul>
  <%= @zebra.each do |elephant| %>
    <li>
      <%= elephant %>
    </li>
  <% end %>
</ul>
```
{: mark_lines="8"}

We added an `=` sign to the first embedded Ruby tag. Now if we refresh the app in our browser on the **/lottery/lucky** page, we will see the full array printed below our list, because we have made this previously invisible line (this tag: `<% %>`) visible (this tag: `<%= %>`). When done looping, `.each` returns the array itself when it is called. We don't typically want or need to view this though. 

You can remove that added `=` sign from the HTML view template after you do this, because this line is not meant to be displayed, but rather to *control the flow* of our embedded Ruby. We already saw this with `if` statements for our Rock Paper Scissors RCAV project.



### Text Companion: `.each` Loop on `@` Instance Variable

## Video Segment: RCAV /lottery/unlucky

- Notes:

  - time stamp 00:17:37 to 00:27:18
  - RCAV practice. re-do the **/lottery/lucky** but with different copy. try to type everything, avoid copy-paste

Our first task in the README, was to study **/lottery/lucky**, and we've done that. Now let's take a moment to build **/lottery/unlucky**. This is basically the same page, just with some different copy.

Follow the usual RCAV. If you want a reference sheet you can have a look [here](rcav-flowchart.md). **BENP: do we want that chapter linked still?**

We click the navbar or manually enter the URL to get to **/lottery/unlucky**, and we see the "No route matches" error. So we go into `config/routes.rb and add that`:

```ruby
# config/routes.rb

Rails.application.routes.draw do  
  # PART 1: EACH IN ERB
  # ===================

  get("/lottery/lucky", { :controller => "numbers", :action => "winners" })
  get("/", { :controller => "numbers", :action => "winners" })

  get("/lottery/unlucky", { :controller => "numbers", :action => "losers" })

  # Let users visit URLs:

  # - /lottery/unlucky

  # PART 2: R→C→A→V DEBUGGING
  # ======================

  # Uncomment each route below ONE AT A TIME and debug.
  # Do NOT uncomment more than one at a time, or you'll be dealing with multiple syntax errors at once.

  # get("/zodiacs/aries", { :controller =>  fire, action =>  "ram" })
  # get("/zodiacs/leo", { :controller => "fire", :action => "lion" })
  # get("/zodiacs/sagittarius" { :controller => "fire", :action => "archer" })
  
  ...

end
```
{: mark_lines="10"}

Now we can refresh the browser and see we need to add the `losers` action to our controller:

```ruby
# app/controllers/numbers_controller.rb

class NumbersController < ApplicationController
  def losers
  
  end

  def winners
    @zebra = Array.new

    5.times do
      giraffe = rand(1...100)
      
      @zebra.push(giraffe)
    end

    render({ :template => "lottery_stuff/woohoo.html.erb"})
  end 
end
```
{: mark_lines="4-6"}

Now it is up to you to complete the action code and render the result in a view template that will be very similar (though not identical) to `app/views/lottery_stuff/woohoo.html.erb`. Try to type everything out by yourself and avoid any copy-pasting. This is good practice!

**BENP: Break here where the students worked on this from 00:19:30 to 00:25:00**

Let's look at the completed action code:

```ruby
# app/controllers/numbers_controller.rb

class NumbersController < ApplicationController
  def losers
    @numbers = Array.new

    5.times do
      a_number = rand(1...100)
      
      @numbers.push(a_number)
    end

    render({ :template => "lottery_stuff/ohno.html.erb"})
  end

  def winners
    @zebra = Array.new

    5.times do
      giraffe = rand(1...100)
      
      @zebra.push(giraffe)
    end

    render({ :template => "lottery_stuff/woohoo.html.erb"})
  end 
end
```
{: mark_lines="5-13"}

Note that we used some different variable names, and these are up to us to choose: `@numbers` for the array of random numbers and we call each individual number `a_number`. And we also can create the specified view template and filled it in. We start with this:

```html
<!-- app/views/lottery_stuff/ohno.html.erb -->

<h1>Unluck numbers</h1>

<p>Your unlucky numbers for today are:</p>

<%= @numbers %>
```

Now refreshing **/lottery/unlucky** should display our copy and our array of numbers with no formatting. Nice, almost there. Let's add a loop and put our numbers into the proper format:

```html
<!-- app/views/lottery_stuff/ohno.html.erb -->

<h1>Unluck numbers</h1>

<p>Your unlucky numbers for today are:</p>

<ul>
  <%= @numbers.each do |num| %>
    <li>
      <%= num %>
    </li>
  <% end %>
</ul>
```
{: mark_lines="7-12"}

And now **/lottery/unlucky** should match the target. Test it manually to see, and when you've done that...

Time for a `/git` commit, and maybe even a `rails grade` to see what's left to do.



### Text Companion: RCAV /lottery/unlucky

## Video Segment: Navbar and Zodiac Debugging

- Notes:

  - time stamp 00:27:18 to 00:36:30
  - aside to `app/views/layouts/application.html.erb` to show <nav>
  - debug **/zodiacs/aries** together
  - RTEM

In the [target](https://fortune-teller.matchthetarget.com){target="_blank"}, there are three navbar sections. We already did the top lottery section. 

There are twelve links in the horoscopes section. If you click the link you will see that each displays some text and then lucky numbers again. Below the horoscipes there is a section for dice, which simulates rolling a certain number of dice with a certain number of sides. For instance, "5d6" means roll five six-sided dice. 

In our app (not the target), none of the horoscope or dice links work. Here's your task.

First, the required part of this homework is debugging the 12 zodiacs. There are already links and routes.

**BENP: An aside starts below, could be moved elsehwere**

By the way, where does all the navbar HTML come from? In the templates we made (e.g., `app/views/lottery_stuff/woohoo.html.erb`), we did not include any header information in the HTML code. That's because all of this is in the *wrapper* file, specifically `app/views/layouts/application.html.erb`:

```html
<!-- app/views/layouts/application.html.erb -->

<!DOCTYPE html>
<html>
  <head>
    <title>Fortune Teller</title>
    <%= csrf_meta_tags %>

    <!-- Expand the number of characters we can use in the document beyond basic ASCII 🎉 -->
    <meta charset="utf-8">

    <!-- Make it responsive to small screens -->
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <%= csp_meta_tag %>
    <%= stylesheet_link_tag    'application', media: 'all' %>
  </head>

  <body>
    <nav>
      ...
    </nav>
    
    <%= yield %>

  </body>
</html>
```

Where we have the `...`, you should see all of the navbar links in an HTML table, which is applied as a header to all of our pages. The pages are placed where we see the `<%= yield %>` tag. This `app/views/layouts/application.html.erb` file that comes with every Rails app is where you would place anything that you want on all of your pages.

Okay, back to the zodiac debugging. If we go to our routes, we will see:

```ruby
# config/routes.rb

Rails.application.routes.draw do  
  # PART 1: EACH IN ERB
  # ===================

  get("/lottery/lucky", { :controller => "numbers", :action => "winners" })
  get("/", { :controller => "numbers", :action => "winners" })

  get("/lottery/unlucky", { :controller => "numbers", :action => "losers" })

  # Let users visit URLs:

  # - /lottery/unlucky

  # PART 2: R→C→A→V DEBUGGING
  # ======================

  # Uncomment each route below ONE AT A TIME and debug.
  # Do NOT uncomment more than one at a time, or you'll be dealing with multiple syntax errors at once.

  # get("/zodiacs/aries", { :controller =>  fire, action =>  "ram" })
  # get("/zodiacs/leo", { :controller => "fire", :action => "lion" })
  # get("/zodiacs/sagittarius" { :controller => "fire", :action => "archer" })
  
  ...

end
```
{: mark_lines="22-24"}

And we can just begin uncommenting (remove the leading `#` from the line) each route and debugging them one at a time. 

**Uncomment each route ONE AT A TIME and debug it ONE AT A TIME.** Don't uncomment multiple at once, or you'll have multiple syntax errors at once and the error messages can't help you.

Let's begin by uncommenting `get("/zodiacs/aries", { :controller =>  fire, action =>  "ram" })` and then in our app try to visit the given path: **/zodiacs/aries**. Now ***RTEM***:

```
There's a problem with your routes.rb file.
unrecognized `fire' .
```

So let's look at our routes file, and what do we see? Oops, where is says `:controller => fire`, it should say `:controller => "fire"`, with string quotation marks. Without the quotations, Ruby thinks `fire` is a local variable because it begins with a lowercase letter. But we never defined a variable called `fire`, that is the name we assigned to our controller and we have a controller file called `app/controllers/fire_controller.rb`, which is what we want Rails to look for.

Okay, we made this change and now we refresh our browser on **/zodiacs/aries**, and we get a new error:

```
There's a problem with your routes.rb file.
unrecognized `aciton' . Did you mean? action_path
```

Because in our route we have `action =>  "ram"`, which should be `:action =>  "ram"`, adding a colon to make action into a symbol in the hash. And refresh **/zodiacs/aries** again, and another error to deal with:

```
ActionController::RoutingError at /zodiacs/aries
uninitialized constant FireController
Did you mean? FiresController
         AirController
```

Hmm. This means we have not defined the class `FireController`. So let's look in our `app/controllers/` directory and we see a controller called `fires_controller.rb`. There is an extra `s` on `fires`, whereas we wrote in our route: `:controller => "fire"`. So rename the controller to `fire_controller.rb` and refresh again **/zodiacs/aries**, and we succeeded!

One thing to note. If you think you did everything correctly but are still getting error messages, then go to GitPod, shut down your server in the terminal by using `Ctrl + C`, and restart with `bin/server`. This sometimes happens with filename or foldername changes.

Time for a `/git` commit, and maybe even a `rails grade` to see what's left to do.

And now you can proceed on your own with the `config/routes.rb` file as we've done above. Uncomment, RTEM, and proceed.



### Text Companion: Navbar and Zodiac Debugging

## Finish and Submit Fortune Teller

- Notes:

  - Below are relevant notes for the rest of the project taken from the README

### Debugging checklist

1. READ the error message. Extract as much useful information from it as possible.
2. If there's no error message, find another way to give yourself feedback; **make the invisible visible**.
- Use the server log.
- Print things; in this new world, that means use embedded Ruby tags (`<%=  %>`) in the view templates. We can't use the `p` method anymore since we aren't writing command line programs anymore.
3. If all else fails — the error message isn't helpful, or there isn't one and you can't spot the issue visually — delete the offending code (or comment it out), and re-type the R→C→A→V from scratch. Hopefully you've been making lots of git commits, so there's no fear in doing so.


### More RCAV Practice

In the nav, there are links to 18 pages that simulate rolling dice in various combinations that are useful for board games (six-sided dice, from one die up to six dice) and other, more exotic dice combinations that are useful for e.g. [Dungeons & Dragons](https://en.wikipedia.org/wiki/Dungeons_%26_Dragons#Game_mechanics).

Right now, none of those URLs work; and the routes don't even exist. Implement them, one at a time. Try to type them out rather than copy-pasting; the point is to build muscle memory and encounter error messages in a controlled setting.

There are no automated tests for Part 3; this is just extra reps for practice.


### Reflections

 - Of the error messages that you encountered during debugging, which ones were most helpful? Which ones were least helpful?
 - In this project, the subfolders within `app/views/` that we store our ERB templates in had various different suffixes:
    - `app/views/lottery_stuff/`
    - `app/views/flame_interface/`
    - `app/views/nature_templates/`
    - `app/views/wind_html/`
    - `app/views/aqua/` (no suffix)

    If you had to pick one style for us to use consistently in the future, which do you prefer? Or can you think of a different subfolder naming convention that you would prefer more?
 - You now know how to respond to visits to URLs with dynamically generated HTML. This is, fundamentally, how Twitter, GitHub, Basecamp, NYTimes, Airbnb, and every other web application works. But, of course, we have a lot more to learn before we could build, for example, a social network.

    What are we still missing? What are you most curious to learn next?



