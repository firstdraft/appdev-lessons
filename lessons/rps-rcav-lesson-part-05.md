# RPS RCAV Part 5

Before you're left to finish the rest of the project with the instructions in the next part of the lesson, let's go through two very important items here.

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

---

<p style="height: 150px"></p>

--- 

We have removed all of the embedded Ruby tags (`<% %>` and `<%= %>`) from the code we had in the `user_rock.html.erb` view template and added a new `outcome` variable to hold a `String` that depends on the control flow associated with the random computer move `comp_move`. 

Now, when a user visits the route **/paper**, the action `play_paper` in the controller `ApplicationController` will be triggered, and the code will be run *before* the template is rendered. 

So let's try to visit **/paper** again. Oops, we get this error:

```
undefined local variable or method `comp_move' for #<#Class...
```

<!-- ![](assets/rps-rcav/err-undefined-local-var-or-meth.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1676657545/err-undefined-local-var-or-meth_f58lll.png)

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

#### Quiz Question

- What is the difference between a local variable and an instance variable?
- There is no difference, we just name them differently because they are in different files of the `app/` folder
    - No, please carefully read the previous section. This is important!
- An instance variable is only used one time and local variables are re-used.
    - No, please carefully read the previous section. This is important!
- Instance variables are available as long as the object they are called from exists. Local variables only exist in the scope that they are defined.
    - Yes, and we define instance variables by pre-prending the name with an `@`-symbol.
- Local variables are available as long as the object they are called from exists. Instance variables only exist in the scope that they are defined.
    - No, please carefully read the previous section. This is important!
{: .choose_best #instance_vs_local points="10" answer="3" }

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

#### Quiz Question

- What does the keyword `yield` in an embedded Ruby template mean, and where do we normally find it?
- This is an object that is only available to files in the `public/` folder.
    - No, we're pretty much done thinking about the `public/` folder. Try again, and maybe re-read the previous section.
- This keyword can be used in the `.html.erb` layout file that wraps our other pages. When we see the keyword, it means "put the page content right here".
    - Yes!
- This keyword is used in our `.rb` controller files, and it means "slow down".
    - No, please carefully read the previous section.
{: .choose_best #yield points="10" answer="2" }

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