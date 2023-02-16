# Omnicalc 1 (Forms and Query Strings)

- Notes:

  - Forms and Query Strings

  - [Original video](https://canvas.uchicago.edu/courses/41147/pages/video-omnicalc-1-forms-and-query-strings){target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/forms-query-strings-and-params-Omnicalc-Part1.md){target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/omnicalc-1](https://github.com/appdev-projects/omnicalc-1){target="_blank"}

  - Target: [https://omnicalc-1.matchthetarget.com/](https://omnicalc-1.matchthetarget.com/){target="_blank"}

  - Useful chapters:

    - [Forms, Query Strings, and Params][Forms, Query Strings, and Params]

**BENP: Would be useful here to show the "layouts" folder that is providing the wrapper with the table of buttons. But I am confused because now the wrapper is not pointed out in the application_controller.rb file as in RPS RCAV. In any case, the layouts/application.html.erb is finally brought up in relation to the nav bar in the Day 4 video @ 28'30" for the fortune teller app. Probably good to bring this up earlier. Also because this is where all the html header stuff went that is missing from our .html.erb view templates.**

## Video Segment: Intro to Forms and Exploring the Target

- Notes:

  - time stamp 00:00:00 to 00:02:26
  - we want forms to get information
  - what is a query string
  - open gitpod
  - explore the target

Our users don't want to type input into the address bar; they want to type into forms! 

Let's practice building forms. Forms are incredibly important to us. That is the primary way in which users give us information that we will eventually be storing in our *databases*, the heart of our applications as we have talked about since day 1. For now we don't have a database, but we will be doing some calculations, sending text messages, even doing some pretty cool API work with that information. Geocoding it, machine learning, all kinds of stuff. Next week we will have databases to store that information as well. We have a project called Omnicalc Part 1 to work on this, so we'll create a GitPod workspace for it.

**BENP: Starting Our GitPod Workspace, 00:00:44 to 00:01:05**

**BENP: this setup is also occurring some more around 4 minutes in the midst of the first RCAV**

[Here is the assignment](https://github.com/appdev-projects/omnicalc-1){target="_blank"}. As usual:

1. Start the web server by running `bin/server`.
2. Navigate to your live application preview.
3. As you work, remember to navigate to **/git** and *Always Be Committing (ABC)*.
4. Organize your workspace tabs.
5. Run `rails grade` as often as you like to see how you are doing, but make sure you **test your app manually first** to make sure it matches the target's behavior.

**BENP: possible image(s) (better, GIFs?) of starting a workspace, opening /git, organizing tabs, noting the target favicon. But these are probably in a different chapter.**

The target for this project is [here](https://omnicalc-1.matchthetarget.com/){target="_blank"}. 

**BENP: Exploring the Target, 00:01:05 to 00:02:26**

This is a very simple application we will build today, to get our feet wet with forms. There are four forms that users can type into. This first one at the URL path **/square/new** there is a very simple single input form, where I can type in a number where I can type in a number like "42", click the button and it gives me the square. The second URL **/square_root/new** let's me enter a number, again "42", and then I end up at the URL **/square_root/results?user_number=42**. There's a query string starting at the **?** there: **?user_number=42**. There is also the URL path **/payment/new** with three inputs, and finally there is **/random/new** with two inputs. 

So let's make these four links (URL paths) work. In doing so, we'll see the fundamental pieces in making all forms work, and that is fundamentally how we get all of our user input.

### Text Companion: Intro to Forms and Exploring the Target

## Video Segment: /square/new RCAV

- Notes:

  - time stamp 00:02:26 to 00:11:25
  - RCAV with RTEM for **/square/new**
  - debugging

Okay, so here is how this is gonna go. First and foremost, as always, it's going to be a question of RCAV: Route, Controller, Action, View. That comes first, before anything. We need to identify the URLs users can visit, make up a route, and then first of all just make the page say something (anything) just to make sure we connected the RCAV dots correctly. Then we can figure out what do we actually need to show them, what, if any, Ruby do we need to write to make the page dynamic and all that other stuff.

So let us first begin with let's say the form at **/square/new**. We need to define this URL and then make it display a form to match the target. Pretty simple, there is nothing dynamic going on here, it's just a static HTML page. Actually we could probably achieve this in the `/public` folder, but from now on we won't do anything in there, we will always do RCAV, just to give us the flexibility of later embedding Ruby if we want to.

My workflow is: pretend I'm a user, navigate to a URL I want to start supporting, and start debugging it one step at a time.

Let's begin by navigating (typing into the address bar) in our new Rails app **http://[YOUR APP DOMAIN]/square/new**. And in my staring point I will see:

```
Routing Error
No route matches [GET] "/square/new"
```
**BENP: in RPS-RCAV I added screenshots for error messages, probably fine to just do as here with code blocks**

So step one is opening `config/routes.rb` in our GitPod workspace, and add some code to it:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/square/new", { :controller => "application", :action => "blank_square_form" })

end
```
{: mark_lines="5" }

**BENP: in the video at 00:05:14, the routes.rb file has some additional content not on the GitHub starting point. `devise_for` blah blah blah. We can maybe leave this code out from above?**

The first argument is the `String` defining the path that the user can visit, and the second argument defines the class (`:controller`) and method (`:action`) that are activated when someone visits the path. We decided on a method name called `"blank_square_form"`, since the job of it is just to show a form for the user to type into when the user wants to calculate the square of a number. We decided we will put this method in the controller that comes with Rails out of the box: `"application"`, which is found in the `app/controllers/application_controller.rb` file and has the class name `ApplicationController` when we open that file:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base

end
```

In our `config/routes.rb`, we tell Rails to look in this controller for our method whenever someone visits the route **/square/new**. Later when we have larger applications, and we begin having more actions, we'll break it into multiple controllers. Now if pretend to be users in our running application and try to visit that route we get a new error:

```
The action 'blank_square_form' could not be found for ApplicationController
```

The routing error is gone, which tells me I put the route in the right place, and didn't have any typos. The new error message is saying that it found the route and controller, but the method (action) is missing. We still need to add our method to the `app/controllers/application_controller.rb` controller file:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def blank_square_form
    
    render({ :template => "calculation_templates/square_form.html.erb" })
  end
end
```
{: mark_lines="4-7" }

I made up a name for a folder to but the templates in to keep things organized and I named the file. So we now need to go into our `app/views/` folder, create a new folder called `calculation_templates` (do not create this folder or file in the `layouts/` subfolder!) and then create a new file in that folder called `square_form.html.erb`. We can right away add something to that file, just to make sure that it works:

```html
<!-- app/views/calculation_templates/square_form.html.erb -->

<h1>howdy!</h1>
```

Now we can go back to our Rails app browser tab and refresh the **/square/new** URL. When we refresh, we see "howdy" and know that our RCAV is complete. 

Note that I don't try to type everything at once, work in very small steps and give yourself feedback (view) as early as you possibly can to make sure the code that you typed is doing what you think it is. 

If you see an error message up to this point then go back and be sure to RTEM! Let the error message help you. If it says "No route matches", you might have typed in the URL in the address bar wrong (try to visit **/squarre/new** and see that happen), or you might have a typo in your `config/routes.rb` file in the `get()` call. 

Use the error messages and **debug**. It is very **deterministic** and will do exactly what you tell it to do. Rails is looking at this in a clear order. You visit a route, then it looks for the controller in the `app/controllers/` folder and if that file is found, then it looks inside the file and looks for a class with the same name as the file (but capitalized and with underscores removed), then it looks for the action (method) in that class called whatever we defined it as in `get()`, then it will run that method. 

At every step, if something isn't found, you will get a clear error message pointing out where the problem occurred and it is up to you to go back and correct. If you can't spot the problem often the easiest thing to do is comment out your code and start from scratch typing everything. It's quicker sometimes to pave over the typo, when they are hard to spot.


### Text Companion: /square/new RCAV

## Video Segment: /square/new Form

- Notes:

  - time stamp 00:11:25 to 00:14:12
  - building a form in the **/square/new** view template
  - `<form></form>`, `<label></label>`, `<input>`, `<button></button>`
  - valid forms with `for=""` and `id=""`

Now that we have the **/square/new** form saying something, we need to think about what it should actually do. It needs to have a form with a label and one text input and a button. Alright, if we refresh our memories and go back to the slides from the essential HTML review, there is a slide about forms, which we looked at in class. **BENP: link here? Probably not necessary. I could not find this slide. Better to just link form chapter content.**

We can go into our view template for the current form and do the following:

```html
<!-- app/views/calculation_templates/square_form.html.erb -->

<h1>howdy!</h1>

<form>
  <label></label>
  <input>

  <button></button>
</form>
```
{: mark_lines="5-10"}

We have an opening and closing tag (`<form></form>`) to bracket the form, then a label tag (`<label></label>`), then an input tag (`<input>`, no closing necessary), then a button tag (`<button></button>`). These are the essential form elements.

Now what about the copy? Let's have a look at our [target URL](https://omnicalc-1.matchthetarget.com/square/new){target="_blank"} so we can get the copy right, because `rails grade` will be looking for it -- you have to build to the spec that you've been "hired" to build. You can just make up your own copy willy nilly. Once we have the copy, we go back to our view template and add some more:

```html
<!-- app/views/calculation_templates/square_form.html.erb -->

<h1>howdy!</h1>

<form>
  <label>Enter a number</label>
  <input>

  <button>Calculate square</button>
</form>
```
{: mark_lines="6 9"}

Now that we have the copy, we need to make this form proper by adding the following:


```html
<!-- app/views/calculation_templates/square_form.html.erb -->

<h1>howdy!</h1>

<form>
  <label for="giraffe">Enter a number</label>
  <input id="giraffe" type="text" placeholder="What number do you want to square?">

  <button>Calculate square</button>
</form>
```
{: mark_lines="6-7"}

We always need to associate `input`s and `label`s with an `id` and a `for`. Every form control must always have an `id` and be labelled with a unique string. It doesn't matter what the value is, it just needs to match for accessibility and for machines to understand the form. We just picked something random. It doesn't matter so we just used `"giraffe"` for both. **BENP: this use of random id and for is a little confusing because it's not how we would do it later in the course or in reality. I'm in favor of using realistic form associations from this point already** In addition, we added the `type` as `"text"` for the input, which is the default and would be used anyway even if we left it out. We also added a `placeholder` to add the gray text from our target: `"What number do you want to square?"`.

We can return to our Rails app and refresh **/square/new** to see our form. Great!

### Text Companion: /square/new Form

## Video Segment: Query String and Parameters Hash

- Notes:

  - time stamp 00:14:12 to 00:16:36
  - everything after **?** from **/square/new** form and the Parameters `Hash`

If I type in "42" and hit calculate, my form is terrible, it doesn't really do anything. At least when I click the `label` "Enter a number" it puts the focus on the `input` box, so my association is wired up correctly. But when I click the button it doesn't take me anywhere. Forms are like links, when you click on them they are supposed to take you to another URL, not keep you on the same page. The form is also supposed to put whatever I typed into the address bar after the **?** symbol.

One of the key problems I have is not naming my `input`, so let's do that in our form:

```html
<!-- app/views/calculation_templates/square_form.html.erb -->

<h1>howdy!</h1>

<form>
  <label for="giraffe">Enter a number</label>
  <input id="giraffe" type="text" placeholder="What number do you want to square?" name="elephant">

  <button>Calculate square</button>
</form>
```
{: mark_lines="7"}

Just to be silly **BENP: again, maybe use realistic for, id, name from this point already** we named the `input` `"elephant"`. And now when I **refresh** (the **back** arrow won't change anything) the form at **/square/new**, and enter in 42 again then hit the calculate button, I will see a new URL string: **/square/new?elephant=42**.

Now even though the form isn't taking me to another place, at least the value I typed is getting preserved in the *query string* in the URL. And because of the way that Rails work, that value, if it's in a query string, Rails is going to parse it and put it in a very special `Hash`. We can view that `Hash` in our GitPod terminal (<kbd>Ctrl</kbd> + <kbd>J</kbd>: to open or close it):

![](assets/omnicalc-1/params-elephant-gitpod-terminal.png)

This `Hash` with the name `Parameters` is now available in our entire app: in the view template, the action, we can use it anywhere. That is the crux of how we get information out of forms. All we need to do is `name` an `input` in the form, and that will capture the variable in our query string and Rails will put it in a hash that we can access. After all the API work that we've done **BENP: wait, did we do API work up to this point?** we are pros at capturing things out of hashes.

Time for a **/git** commit (perhaps with the title message "Square form looking pretty good, doesn't work yet" or something along those lines), and maybe even a `rails grade` to see what's left to do.

### Text Companion: Query String and Parameters Hash

## Video Segment: /square/results RCAV

- Notes:

  - time stamp 00:16:36 to 00:23:48
  - building the **/square/results** RCAV and form
  - more on query strings

If we look at how the target works, when we enter a number (why not..."42"?) to square and click calculate, then we end up at another URL **/square/results?number=42**. I started at **/square/new** and when I click, it takes me to **/square/results**, a page with different markup and different content from the starting point. Let's send the user there in our app. 

We will need to start by going through our RCAV steps. Remember to work in small steps and refresh the view often. Keep Reading the Error Message and slowly debugging. Get used to this process, we will be doing it over and over again! Route, Controller, Action, View!

First, the route. Go to your app's browser and manually navigate to **/square/new**. RTEM. Time to add a route:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/square/new", { :controller => "application", :action => "blank_square_form" })

  get("/square/results", { :controller => "application", :action => "calculate_square" })

end
```
{: mark_lines="7" }

Since this is when the user is actually calculating (as opposed to requesting a blank form with `"blank_square_form"`), we call the action `"calculate_square"`. 

Now refresh the browser again and RTEM. The route should be set, and it's time to add an action (method) in our controller (class):

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def blank_square_form
    
    render({ :template => "calculation_templates/square_form.html.erb" })
  end

  def calculate_square
    
    render({ :template => "calculation_templates/square_results.html.erb" })
  end
end
```
{: mark_lines="9-12" }

We keep using the same `calculation_templates/` folder. 

Now if we refresh again and RTEM, we see the action was found, but now we need to make a new file in `app/views/calculation_templates/` called `square_results.html.erb`. Once we create that file and enter some quick copy to view (why not...`<h1>hi</h1>`?), we refresh once more to see our completed, error-free RCAV cylce (assuming you don't have any typos).

Now let's get the result page doing what we actually want.

We begin by adding some formatting and HTML to our view template in `app/views/calculation_templates/square_results.html.erb`:

```html
<!-- app/views/calculation_templates/square_results.html.erb -->

<h1>Square Results</h1>

<dl>
  <dt>Number</dt>
  <dd>something</dd>

  <dt>Square</dt>
  <dd>something squared</dd>
</dl>
```
{: mark_lines="3-11"}

We use a description list (`<dl>`) containing description terms (`<dt>`) and data (`<dd>`), as per the copy (remember to right click and "View Source") in the [target](https://omnicalc-1.matchthetarget.com/square/results?number=42){target="_blank"}.

Refresh out app, and everything should look okay on this page. But we just put in some placeholders for the result. Let's actually make it dynamic. We need to put the original number in the first `something` and calculate the square to put the result in `something squared`.

If I add a query string on the end of any URL in Rails (e.g., I can go to my app and add **/square/results?user_number=42**), and then I hit return, it doesn't change anything. For the purposes of routing anything after the **?** in a query string is ignored, but in the server log (GitPod terminal where we ran `bin/server`), we saw previously that everything after the **?** is added as key/value pairs in the `Parameters` `Hash`:

```
Parameters: {"user_number" => "42"}
```

We could add a bunch of variables to our query string with **&** and all of them would be separated in the `Parameters`. If we typed into our address bar  **/square/results?user_number=42&zebra=12&giraffe=82**, hit enter, and return to our server log on GitPod, we would find:

```
Parameters: {"user_number" => "42", "zebra" => "12", "giraffe" => "82"}
```

So the *query string* is just a `Hash`!

### Text Companion: /square/results RCAV

## Video Segment: Form Action and `params`

- Notes:

  - time stamp 00:23:48 to 00:31:46
  - adding `action="/square/results"` to the **/square/new** form 
  - using `params` Hash in the **/square/results** action to fetch from query string, calculate, and display



Now if we go back to our form in our app at **/square/new**, enter "42", and hit calculate, then it puts the query string together, but stays in the same place: **/square/new?elephant=42**. Remember we defined the `name` of the variable in our view template form as `elephant`. A bit silly, but we can roll with it. **BENP: See what I mean? If we eliminate elephant above then we save on the awkward name here**

So this means we need to add a redirect action to our form, pull out the query string data, and do a calculation. So here's the magic. 

Let's open the view template at `app/views/calculation_templates/square_form.html.erb`:

```html
<!-- app/views/calculation_templates/square_form.html.erb -->

<h1>howdy!</h1>

<form action="/square/results">
  <label for="giraffe">Enter a number</label>
  <input id="giraffe" type="text" placeholder="What number do you want to square?" name="elephant">

  <button>Calculate square</button>
</form>
```
{: mark_lines="5"}

The `action` attribute to the `<form>` is equivalent to the `href` in a link like `<a href="https://www.wikipedia.org">Go to wikipedia</a>`. Putting `"https://www.wikipedia.org"` after `action=` would cause the form to redirect to WikiPedia after we click the button, you can try it yourself. **Be sure to refresh the page, back buttons will not reload the code and the action will not work**. 

Instead of redirecting away from our app though, we want our button click to send the user to **/square/results**, and that is what we specified above, and where the form will now go. Refresh **/square/new**, enter a number, click the button, and see for yourself. **Again, if you tried the WikiPedia example, remember to *refresh* the page or your new action will not take effect**.

What happened? We entered "42", we hit calculate, the form routed us to **/square/results**, Rails called the `get()` for this route, which used the controller and action to render our view template for this page, and on the end of our URL we have our input preserved: **/square/results?elephant=42**. And this input is also preserved in our `Parameters` `Hash`.

Let's pull out this data from the hash and use it in our action (contained in our controller) that was triggered when we were routed to the URL **/square/results** by our form:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def blank_square_form
    
    render({ :template => "calculation_templates/square_form.html.erb" })
  end

  def calculate_square
    # params = {"elephant"=>"42"}
    
    @num = params.fetch("elephant")
    @square_of_num = @num * @num

    render({ :template => "calculation_templates/square_results.html.erb" })
  end
end
```
{: mark_lines="10-13" }

From our server log, we copy-pasted in our hash and put this in a comment with the assigned variable `params`. This is for our own reference (it is in a comment `#`), but the variable `params` exists in every Rails app to store this hash. Hence we use it in the subsequent lines with our familiar `Hash` method `.fetch()` to pull out the key/value pair of interest. In this case we pull the user input (which we named `elephant` in our form) to an instance variable `@num` (because an instance variable will be accessible in our rendered view template `"calculation_templates/square_results.html.erb"`), and we calculate another instance variable `@square_of_num` to store our result for rendering.

Let's put these instance variables into that view template with embedded Ruby tags:

```html
<!-- app/views/calculation_templates/square_results.html.erb -->

<h1>Square Results</h1>

<dl>
  <dt>Number</dt>
  <dd><%= @num %></dd>

  <dt>Square</dt>
  <dd><%= @square_of_num %></dd>
</dl>

<a href="/square/new">Calculate another square</a>
```
{: mark_lines="7 10 13"}

Note that we also added a link at the bottom (as per the target app) to return to the form and make another calculation. Now we can refresh the **/square/new**, enter data, and submit again... but wait! Another error message:

```
undefined method `**' for "42":String
```

Oops, the query string puts the data into the `params` `Hash` as a `String` object, but we need it as a `float` or `integer` to do math on it. Let's return to our controller action and:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def blank_square_form
    
    render({ :template => "calculation_templates/square_form.html.erb" })
  end

  def calculate_square
    # params = {"elephant"=>"42"}
    
    @num = params.fetch("elephant").to_f
    @square_of_num = @num * @num

    render({ :template => "calculation_templates/square_results.html.erb" })
  end
end
```
{: mark_lines="12" }

We use a `.to_f`, since we want a `float` so the user can enter a decimal number (like "42.01") and get the exact (not integer rounded) result. Now we can try once more, and everything should be up and running.

Time for a **/git** commit (perhaps with the title message "Square form and calculation done" or something along those lines), and a `rails grade` to see what's left to do. **Do not use `rails grade` to debug, always test your app manually before running `rails grade` as the last check.**

### Text Companion: Form Action and `params`

## Video Segment: Independence of Routes

- Notes:

  - time stamp 00:31:46 to 00:43:13
  - use **/random/results** RCAV developed *before* **/random/new** to highlight independence of routes

You will complete most of the rest of the assignment on your own, but let's talk about one more thing using the **/random/new** URL path. We can have a look at the [target](https://omnicalc-1.matchthetarget.com/random/new){target="_blank"} and see that when we type in the "Minimum" using "1.5" and "Maximum" using "4.5" and click the button, we are routed to **/random/results?user_min=1.5&user_max=4.5**. So this is the route we want to work.

I want to point out here that in theory the **/random/new** page with the form and the **/random/results** page with the result are entirely independent. I could just build **/random/results** without **/random/new**, but then the user would need to manually type into the address bar their inputs after a query string: **?user_min=1.5&user_max=4.5**. 

Try and just change the URL to **/random/results?user_min=0&user_max=2**. The page will change when you hit enter and we never used the form page. 

The point is, **every RCAV is independent of every other RCAV**. Clicking the button on our previous form for **/square/new** triggered a new and independent RCAV. We need to think of these things as independent, we are just cleverly arranging things such that there is a cause and effect, but this does not exist without our clever arrangement. So you can choose whatever names you want for inputs, parameters, or anything else. You just need to make sure whatever names you choose, that everything matches up so that at the end of the day you can retrieve the information you need. Don't expect Rails to guess your intention, you need to instruct Rails what you want to do and it will follow your instructions *to the letter*.

Let's start the task of getting **/random/new** and **/random/results** to actually work. But let's begin the other way around from before, by getting **/random/results** going first.

So first step is to manually in my app enter the URL **/random/results**, get my familiar "No route matches" error and begin the RCAV cycle.

First we add the route:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/square/new", { :controller => "application", :action => "blank_square_form" })

  get("/square/results", { :controller => "application", :action => "calculate_square" })

  get("/random/results", { :controller => "application", :action => "calculate_random" })

end
```
{: mark_lines="9" }

Now we refresh our browser, RTEM, and add the action that we named in our controller:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def blank_square_form
    
    render({ :template => "calculation_templates/square_form.html.erb" })
  end

  def calculate_square
    # params = {"elephant"=>"42"}
    
    @num = params.fetch("elephant").to_f
    @square_of_num = @num * @num

    render({ :template => "calculation_templates/square_results.html.erb" })
  end

  def calculate_random
    
    render({ :template => "calculation_templates/random_results.html.erb" })
  end
end
```
{: mark_lines="18-21" }

Now we refresh our browser, RTEM, and add the new view template that we named and put some copy in it:

```html
<!-- app/views/calculation_templates/random_results.html.erb -->

<h1>howdy</h1>
```

And if we refresh and get no error message, our RCAV is complete and now we just need to get the view template to actually render what we want. 

Try to manually navigate the URL to **/random/results?user_min=1.5&user_max=4.5**. Now go to the GitPod server terminal (as usual <kbd>Ctrl</kbd> + <kbd>J</kbd>: to open or close it, and <kbd>Ctrl</kbd> + <kbd>K</kbd>: to clear the log for a better view) and you will see the query string transcribed in the `Parameters` `Hash`, which we know is accessible anywhere in our Rails app by `params = { key => value}`, or, in this case: `params = { "user_min" => "1.5", "user_max" => "4.5" }`. 

Okay so let's get this out in our action:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def blank_square_form
    
    render({ :template => "calculation_templates/square_form.html.erb" })
  end

  def calculate_square
    # params = {"elephant"=>"42"}
    
    @num = params.fetch("elephant").to_f
    @square_of_num = @num * @num

    render({ :template => "calculation_templates/square_results.html.erb" })
  end

  def calculate_random
    # params = {"user_min"=>"1.5", "user_max"=>"4.5"}

    @lower = params.fetch("user_min").to_f
    @upper = params.fetch("user_max").to_f
    
    render({ :template => "calculation_templates/random_results.html.erb" })
  end
end
```
{: mark_lines="19-22" }

And then add these instance variables in the rendered view template:

```html
<!-- app/views/calculation_templates/random_results.html.erb -->

<h1>howdy</h1>

<dl>
  <dt>Minimum</dt>
  <dd><%= @lower %></dd>

  <dt>Maximum</dt>
  <dd><%= @upper %></dd>

  <dt>Random Number</dt>
  <dd>Something</dd>
</dl>
```
{: mark_lines="5-14" }

`Something` above is just a placeholder. I leave that to you to calculate in the action and place in the view template. 

But let's refresh our new **/random/results?user_min=1.5&user_max=4.5** page. We see that indeed the URL query string has been parsed and turned into the instance variables which were then embedded in my view template. 

Try and just manually change the URL to **/random/results?user_min=0&user_max=2**. The page will change when you hit enter and we **never used the form page**. 

So the two routes are **independent**. In theory, the savvy user could manually change the URL to get new results, but this isn't so nice and we can't expect our users to know how to do this. That's why we use forms and wire things together. But remember: **during the lifecycle of a given RCAV, only that route, action, and view template exist**.

Time for a **/git** commit, and a `rails grade` to see what's left for you to do.

### Text Companion: Independence of Routes

## Finish and Submit Omnicalc 1

- Notes:

  - Below are relevant notes for the rest of the project taken from the README

### The Target

The way the assignment should work is:

 - If I visit the ROUTE **/square/new**, I should see a form with a label and an input to enter a number.
    - If I submit that form, I should see the square of the number that I entered.
 - If I visit the ROUTE **/square_root/new**, I should see a form with a label and an input to enter a number.
    - If I submit that form, I should see the square root of the number that I entered.
 - If I visit the ROUTE **/payment/new**, I should see a form with labels and inputs to enter three values:
    - The APR (annual percentage rate).
    - The number of _years_ remaining.
    - The present value.
    - If I submit that form, I should see the **monthly** payment due given the values that I entered.
    - Mind your units! Use this formula:

        ![Payment formula](assets/omnical-1/payment_formula.gif)

    - Hint 1: The number of periods, `n`, that we receive from the user is in years. Since we're calculating monthly payment we multiply it by 12.
    - Hint 2: `apr` comes in as a string. We should turn it into a float and divide the number by 100 to get the percentage.
    - Hint 3: `r` in the formula is a percentage per period.  One period is equal to one month.  The `apr` we receive from the user is yearly.
    - Hint 4: Create a variable for the numerator and another one for the denominator.  If they are instance variables, you can view them within your view page. If your output does not match the target, having done this  will make debugging much more manageable.

 - If I visit the ROUTE **/random/new**, I should see a form with labels and inputs to enter two numbers, a minimum and a maximum.
    - If I submit that form, I should see a random number that falls between the numbers that I entered.

You can compare your app against the [target](http://omnicalc-1.matchthetarget.com/){target="_blank"}, including doing "View Source" to look at some of the static HTML.


### Valid, Accessible Forms

**In order for your tests to pass**, you must build _valid_ forms (your Chrome browser _may_ tolerate invalid forms while you are manually testing, but automated test suites reject invalid forms):

 - Each `<input>` in the form must have a unique `id=""` attribute.
 - The `<label>` associated with the `<input>` should have a `for=""` attribute that matches the value of the `<input>`'s `id`.
 - The copy within the `<label>` must exactly match the target — spelling, capitalization, and punctuation matter for labels.
 - The same goes for the copy on the button to submit the form.
 - Any invalid HTML within a form will cause the test to fail, e.g. an orphaned closing `</div>` tag. Keep your code neatly indented to help avoid this.

An example of a valid form; in particular, notice the `id=""` and `for=""` attributes:

```html
<form action="/random/results">
  <div>
    <label for="min_input">
      Minimum
    </label>

    <input id="min_input" type="text" name="user_min" placeholder="E.g. 1.5">
  </div>

  <div>
    <label for="max_input">
      Maximum
    </label>

    <input id="max_input" type="text" name="user_max" placeholder="E.g. 4.5">
  </div>

  <button>
    Pick random number
  </button>
</form>
```

### Additional Hints

The `to_s` method can format `Floats` [in more specific ways](https://chapters.firstdraft.com/chapters/853) that help us easily display data in a variety of ways.

In particular these two:

- [`.to_s(:currency)`](https://chapters.firstdraft.com/chapters/853#currency)
- [`.to_s(:percentage)`](https://chapters.firstdraft.com/chapters/853#percentage)

could be useful when formating the output of the payment form.