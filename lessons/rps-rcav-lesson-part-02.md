# RPS RCAV Part 2

Let's start working in our Gitpod workspace to reinforce some of the theory in Part 1.

## Our First RCAV

Our workflow for a ***dynamic web application*** is always the same: Route, Controller, Action, View (RCAV). *The world is ruled by URLs*, so we will always start with what URL we want to build and get it to work.

Navigate to the route **/rock** in your Rails browser. 

<div class="experiment" markdown="1">
  
  *We will no longer write out the entire URL path* with **http\://[APP DOMAIN]** preceeding the route of interest. A lone **/** signifies the homepage and anything else is another route (page) in the app.
</div>

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

### Completed Code

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