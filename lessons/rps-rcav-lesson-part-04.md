# RPS RCAV Part 4

Now that we've seen the power of embedded Ruby, let's reinforce the RCAV steps a few times!

## Reinforce RCAV with /

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

<!-- ![](assets/rps-rcav/err-action-not-in-contoller.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1676657214/err-action-not-in-contoller_g2tpbg.png)

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

Now refresh **/**. There is no error and our HTML template is rendered. And we did not put any HTML in the `public/` folder! You will almost always want some kind of dynamic behavior on every page. So our new workflow is *always RCAV*: 

  - Define a *route*, 
  - assign a *controller*, 
  - create an *action* in that controller, 
  - and *view* the result.

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

<!-- ![](assets/rps-rcav/err-missing-view-template.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1676657230/err-missing-view-template_xennnd.png)

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