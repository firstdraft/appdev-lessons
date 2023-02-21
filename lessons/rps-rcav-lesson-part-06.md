# RPS RCAV Part 6

That was a lot of information! RCAV, embedded Ruby, instance variables, layouts. Don't worry, you'll be getting a lot of practice with all of it. Starting now.

## Finish and Submit RPS RCAV

The rest of the project is up to you to finish. Continue working on Gitpod, keeping in mind the [target](https://rps-rcav.matchthetarget.com){:target="_blank"}.

Visit the **specs** (URLs) and wire them all up. You have all the tools now. Use the resources in the previous sections. There is also an RCAV cheatsheet flowchart below that may help.

Remember to use `rails grade` and **/git** commit, and if you need help, you can always share a Gitpod snapshot along the way.

There are also two additional addendums below regarding custom controller files and rendering JSON, which you're welcome to *optionally* read through and play with.

## Addendum: RCAV Flowchart

Our apps are nothing more than a collection of URLs that we decide to allow users to access:

 - **mydomain.com/products**
 - **mydomain.com/photos/193**
 - **mydomain.com/signin**

So remember: everything always starts with a *route* between an *address* we want users to be able to visit and a *Ruby method* that will be responsible for generating a response to the user's browser.

In order to support a URL in your app such as **https\://3000-your-gitpod-workspace.gitpod.io/home**, there are a lot of dots to connect!

<!-- ![](assets/rps-rcav/rcav-chart.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1676658023/rcav-chart_w4osbj.png)
{: .bleed-full }

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

