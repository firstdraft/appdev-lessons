# Omnicalc 2 (Forms, Params, APIs)

- Notes:

  - [Original video](https://uchicago.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=8c2e54f8-4bed-47d2-82b2-aeca0102f92c){target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/Omnicalc-Part2.md){target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/omnicalc-2](https://github.com/appdev-projects/omnicalc-2){target="_blank"}

  - Target: [https://omnicalc-2.matchthetarget.com/](https://omnicalc-2.matchthetarget.com/){target="_blank"}
    - username: appdev
    - password: fullstack

  - Useful chapters:

    - [Forms, Query Strings, and Params][Forms, Query Strings, and Params]
    - [Omnicalc API][Omnicalc API]
    - [Storing credentials securely][Storing credentials securely]
    - [Meteorologist (Intro to APIs)][Meteorologist (Intro to APIs)]
    - **Right now a bunch of API stuff is found much later in the Day 5 material on Canvas. See my notes below, APIs might need devoted video.**

## Video Segment: Exploring the Target 

- Notes:

  - time stamp 00:38:36 to 00:42:54
  - doing math, intro to APIs
  - Street to Coordinates
  - Translate with SMS

Forms are incredibley important to us. The first layer of building a dynamic application is connecting the Route, Controller, Action, View. Having some variables displayed on the page so it is dynamic and not static HTML.

The second thing we need to do is accept information from our users because just generating random stuff on a page is boring, so we'll be building tons and tons of forms for the rest of the quarter. 

Omnicalc 2 is very similar to Omnicalc 1, where you began to learn forms in that homework. In this case, if I have a look at `config/routes.rb`, the file is empty:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```

So will need to build up the [target](https://omnicalc-2.matchthetarget.com/){target="_blank"} step-by-step. When you open this app, you need to enter a username (*appdev*) and password (*fullstack*). The reason for this, is because, if we have time, we're going to do some more fun things than we've done so far. Instead of just getting numbers and doing some math, we'll be doing some more fun things.

For example if we look in the target, there's a "Street to Coordinates" calculator. If you type in and address here, like "5807 S Woodlawn Ave" and click "Lookup Coordinates", then it displays latitude and longitude. So all the form entry steps are the same as what you've already done, but the application does much more here. How did we get from a street address to these coordinates? What's the Ruby for that? Well, we're going to learn how to do that.

Even more cool, there's a link in the target called "Translate". Ff we fill out this form, maybe with "Ruby is the best!" in the first box, and then select a language from the second drop down menu (e.g., Chinese (simplified)), and put in a phone number in the last box with the country code (e.g., +1 for USA), and finally hit translate, then the text gets translated and the number we entered gets a text message with that translation!

It's still all about entering in forms, but the way we achieve these responses is very empowering. This is known as *Application Programming Interface*, or *API*, programming. This means that other companies, like Google, will allow us to Create, Read, Update, and Delete information in *their* databases, and they will send back information that they have. We don't need to create their data, we can use their resources. Both the street to coordinates and translation service above is provided by Google (actually the text messaging part is another company called Twilio).

We also have link to "Street to Weather" or "Coordinates to Weather". These use two APIs, one for Google to get the location, and the second is the DarkSky API to get back a detailed weather forecast.



### Text Companion: Exploring the Target 

## Video Segment: Reviewing Query Strings

- Notes:

  - time stamp 00:42:54 to 00:50:45
  - examine target **/wizard_add** and implement using query string and `params`

All that said, the important goal of this project (and the required part) is building forms, so let's do one of the four forms together now: Add, Subtract, Multiply, Divide.

We will focus on the "Add" form. Let's visit **/add** in our Rails app browser. As expected we get a "No route matches" error. So we will need to build this up step-by-step.

But first, observe the target app. In each calculator there are two actions. There is one action that just displays the form. Then when I fill out the form and press the button, it takes me to a different URL. If we fill out "Add" with "4" in the first number and "10" in the second, then press the button, the resulting URL on the "Addition" page looks like **/wizard_add?first_num=4&second_num=10**. 

Any of the other forms on our target works this same way: the information we put in the form is placed as variables in the URL *query string* preceded by the **?** character. If I know how this form works, I can just type directly into the URL with new variable values, and I will get a new result. I never even need to visit the form page. I want to emphasize here, the form and second action that does the work are two totally separate independent actions. We use forms because we want a nice interface for our users. It is polite to add a form for our users, who are not developers like us.

We'll implement **/add** now, but we will go backwards. First, I'm going to implement the second step **/wizard_add**:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  
  get("/wizard_add", { :controller => "math", :action => "add_results" })

  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```
{: mark_lines="5"}

My selection for the `:controller` and `:action` names above, mean I'll need to create these in out app. So in the `app/controllers/` folder we need to make a new file `math_controller.rb` and fill it in with our inherited `ApplicationController` functionality and our new action:

```ruby
# app/controllers/math_controller.rb

class MathController < ApplicationController
  def add_results
    render({ :template => "math_templates/add_results.html.erb" })
  end 
end
```

And our selection to just render some HTML, means that we also need to create the view template. So in the `app/views/` folder we need to first make a new folder `math_templates/` and then a new file in that folder called `add_results.html.erb`. And in this file we can put some placeholder text to render:

```html
<!-- app/views/math_templates/add_results.html.erb -->

hi
```

Now if we didn't make any typos and visit or refresh **/wizard_add**, we will see our rendered HTML. You will also already see a navbar, that we included in the app, and this, as you have already seen, is in the `app/views/layout/application.html.erb` file that is applied to every page.

Now if a user includes a query string in the URL, like **/wizard_add?zebra=bob**, there is no effect on the routing when we press enter. But if we look into our server log in the GitPod terminal tab running your server ([Cmd-K or Ctrl-K to clear it out](https://chapters.firstdraft.com/chapters/834#clear-terminal)), we can find:

```
...
HTML
  Parameters: {"zebra"=>"bob"}
  Rendering math_templates/add_results.html.erb
  Rendered math_templates/add_results.html.erb within layouts/application
...
```

Our query string that is automatically split, parsed, and added to `params`. All before I have built the form. Let's use the expected query string: **/wizard_add?first_num=4&second_num=10**. And observe now in the server log:

```
...
HTML
  Parameters: {"first_num"=>"4", "second_num"=>"10"}
  Rendering math_templates/add_results.html.erb
  Rendered math_templates/add_results.html.erb within layouts/application
...
```
{: mark_lines="3"}

We can now pull out this information in our action:

```ruby
# app/controllers/math_controller.rb

class MathController < ApplicationController
  def add_result
    @first = params.fetch("first_num")

    @second = params.fetch("second_num")

    @result = @first + @second

    render({ :template => "math_templates/add_results.html.erb" })
  end 
end
```
{: mark_lines="5-9"}

And display the *instance variables* on our view template:

```html
<!-- app/views/math_templates/add_results.html.erb -->

<%= @result %>
```
{: mark_lines="3"}

And if we now refresh **/wizard_add?first_num=4&second_num=10**, we see the result displayed as "410". Why? Because we are adding two strings in our action! We need to remember to convert them to floats or integers to do math on them:

```ruby
# app/controllers/math_controller.rb

class MathController < ApplicationController
  def add_results
    @first = params.fetch("first_num").to_f

    @second = params.fetch("second_num").to_f

    @result = @first + @second

    render({ :template => "math_templates/add_results.html.erb" })
  end 
end
```
{: mark_lines="5 7"}

And now we should get "14.0" on our page. We won't flesh out all the copy and formatting to get our HTML view template to match the target page, but this should be straightforward. 



### Text Companion: Reviewing Query Strings

## Video Segment: Reviewing Forms

- Notes:

  - time stamp 00:50:45 to 00:58:00
  - examine target **/add** and implement using forms

Our results page works, but it's a pain for our users to type in the URL query string. If they make any mistake like typing "first_number" instead of "first_num", like **/wizard_add?first_number=4&second_num=10**, they would get the error:

```
param is missing or the value is empty: first_num
```

because in our `add_result` action in our `MathController`, we have `@first = params.fetch("first_num").to_f`. But `"first_num"` does not exist in our `params` variable, because the user accidentally named it `first_number` in the URL.

Hence, we need a form for the user to type into. So the usual RCAV here:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  
  get("/add", { :controller => "math", :action => "add_form" })
  
  get("/wizard_add", { :controller => "math", :action => "add_results" })

  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```
{: mark_lines="5"}

Then:

```ruby
# app/controllers/math_controller.rb

class MathController < ApplicationController
  def add_form
    render({ :template => "math_templates/add_form.html.erb" })
  end

  def add_results
    @first = params.fetch("first_num").to_f

    @second = params.fetch("second_num").to_f

    @result = @first + @second

    render({ :template => "math_templates/add_results.html.erb" })
  end 
end
```
{: mark_lines="4-6"}

Put some copy in the new view template we create:

```html
<!-- app/views/math_templates/add_form.html.erb -->

hi
```

And when we see our URL **/add** loads with no error, we can put together our form in the view template to finish things off:

```html
<!-- app/views/math_templates/add_form.html.erb -->

<form action="/wizard_add">
  <input name="first_num">

  <input name="second_num">
  
  <button>
    Add
  </button>
</form>
```
{: mark_lines="3-11"}

The all important `action="/wizard_add"` attribute in the opening `<form>` tag, tells the form that when we click the `<button>`, then route to **/wizard_add**, which activates the first RCAV we built to do the computation. This is the most basic, working version of the form, but you will need to add a lot more like the input labels. Of course, we want a valid form, so you will need to include the matching `for=""` and `id=""` attributes for each `<label>` and associated `<input>`, and make sure everything matches the target. **BENP: could link to forms-query-strings-and-params.md chapter or whatever that content becomes**

Complete the rest of the assignment on your own and make sure to be **/git** committing anytime you get something working with `rails grade`.

You will need to wire up all RCAVs and the associated forms for "Add", "Subtract", "Divide", and "Mulitply".


**BENP: From below, I think a new chapter /recording / chapter is in order.**


### Text Companion: Reviewing Forms

## Video Segment: Intro to APIs with Street to Coordinates

- Notes:

  - time stamp 01:00:00 to 01:21:00
  - there is a bunch of explanation here about APIs
  - implementing **/experiment** for "Street to Coordinates"
  - API keys
  - JSON
  - Google Maps API
  - JSON to Hash with `JSON.parse(open(@url).read)`

Let's begin to experiment with APIs in our app. One of the homework videos for next week includes some API work, but we will get a taste here. 

First we will add a route to experiment with:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  
  get("/add", { :controller => "math", :action => "add_form" })
  
  get("/wizard_add", { :controller => "math", :action => "add_results" })

  get("/experiment", { :controller => "application", :action => "experiment" })

  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```
{: mark_lines="9"}

We are just going to use the `application_controller.rb` file as our controller and add an action there `experiment`.

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def experiment

    render({ :template => "math_templates/experiment.html.erb" })
  end
end
```
{: mark_lines="3-6"}

We just put the new template again in the `app/views/math_templates/` folder, just to `experiment.html.erb`.

And here is a bunch of handy links (**BENP: originally from README, can we remove some links? yes definitely**) with information on APIs:

 - [JSONView Chrome extension](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en){target="_blank"}
 - [Dark Sky forecast at the Merchandise Mart for humans](https://darksky.net/forecast/41.8887,-87.6355/us12/en){target="_blank"}
 - Dark Sky forecast at the Merchandise Mart for machines:
 
     
     **https://api.darksky.net/forecast/REPLACE_THIS_PATH_SEGMENT_WITH_YOUR_API_TOKEN/41.8887,-87.6355**

 - [Dark Sky API docs](https://darksky.net/dev/docs){target="_blank"}
 - [Map of Merchandise Mart for humans](https://goo.gl/maps/2mXdvBnHSGuMq98m6){target="_blank"}
 - Map of Merchandise Mart for machines:

    **https://maps.googleapis.com/maps/api/geocode/json?address=Merchandise%20Mart%20Chicago&key=REPLACE_THIS_QUERY_STRING_PARAMETER_WITH_YOUR_API_TOKEN**

 - [Google Geocoding API docs](https://developers.google.com/maps/documentation/geocoding/start){target="_blank"}
 - [How to store secrets securely on Gitpod](https://chapters.firstdraft.com/chapters/792){target="_blank"}


If we look at the [target](https://omnicalc-2.matchthetarget.com/){target="_blank"} and navigate to "Street to Coordinates", **BENP: video cuts out** ... the reason for that is, it costs money. Each time we're making an API call, they are tracking our use and charging us if we are above some limit. GoogleMaps has a very high limit of API calls before charging begins, but the text messaging in the "Translate" page costs money for every message. That is why we have password secured the target in this case. So this is something to keep in mind: if you start to play around with APIs and sign up for an account with a credit card, then be careful with your API credentials!

In this project any necessary API credentials are made available to you **BENP: these are from Canvas and probably should not be / or should be changed in the final material. ALL API KEYS LABELLED AS `TODO`**:

 - `TWILIO_ACCOUNT_SID` : `TODO`
 - `TWILIO_AUTH_TOKEN` : `TODO`
 - `TWILIO_SENDING_PHONE_NUMBER` : `TODO`
 - `MAILGUN_API_KEY` : `TODO`
 - `MAILGUN_SENDING_DOMAIN` : `TODO`
 - `GMAPS_KEY` : `TODO`
 - `DARK_SKY_KEY` : `TODO`
 - `TRANSLATE_PROJECT` : `TODO`
 - `TRANSLATE_CREDENTIALS` :

     ```
     { TODO } 
     ```

So you can feel free to play around. But with your own credentials, be careful and protect them. **BENP: could link to [Storing credentials securely][Storing credentials securely] content here**

How do I begin to think about tackling "Street to Coordinates"?

I have an address and I want the latitude and longitude. I don't want to use my company resources to building up a huge database of this information that I can lookup in. So let's use [Google's Geocoding API](https://developers.google.com/maps/documentation/geocoding/start){target="_blank"}.

The first step of any API work is doing some homework. Search around on the internet for different options and read through some of the documentation. If we look around in the Google documentation, we would find a URL:

**https://maps.googleapis.com/maps/api/geocode/json?address=1600+Amphitheatre+Parkway,+Mountain+View,+CA&key=YOUR_API_KEY**

What do we see? We have an address: **https://maps.googleapis.com/maps/api/geocode/json** and a query string: **?address=1600+Amphitheatre+Parkway,+Mountain+View,+CA&key=YOUR_API_KEY**. And we can see the query string includes an **address=** variable, and a **key=** variable. If we try to visit the URL as it is, we would see a page like:

```json
// 20221217132605
// https://maps.googleapis.com/maps/api/geocode/json?address=1600+Amphitheatre+Parkway,+Mountain+View,+CA&key=YOUR_API_KEY

{
  "error_message": "The provided API key is invalid. ",
  "results": [
    
  ],
  "status": "REQUEST_DENIED"
}
```

We see an error message. Because we need to replace **YOUR_API_KEY**, with our API key!

So we can go into a new tab and try to do that with our `GMAPS_KEY` **BENP: this key is expired and needs to be changed everywhere above and below**:

**https://maps.googleapis.com/maps/api/geocode/json?address=1600+Amphitheatre+Parkway,+Mountain+View,+CA&key=TODO**

And when we enter this address in the tab, we should see a very long JSON file displayed in our browser, something like:

```json
// 20221217131844
// https://maps.googleapis.com/maps/api/geocode/json?address=1600+Amphitheatre+Parkway,+Mountain+View,+CA&key=TODO

{
  "results": [
    {
        "address_components":
        ...
    }
    ...
  ]
}     
```

There may be several hundred lines displayed and it may not be broken into readable lines if you don't have a third party extension like [JSON Viewer for Chrome](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh){target="_blank"}.

If you examine the page, you will see lots of information about the address we entered. *JSON*, or *Javascript Object Notation*, is not the same format as HTML. JSON is somewhat similar to CSV, and there is another format called XML that many APIs use. These are all just different data formats that are much easier to parse programmatically compared to HTML.

If I change the query string in my URL to whatever I want (even with spaces):

**https://maps.googleapis.com/maps/api/geocode/json?address=5807 S Woodlawn Ave&key=TODO**

Then the JSON information will change to give me information on that address `5807 S Woodlawn Ave`. If I look carefully and scroll down, I could even find the following:

```json
...
"location": {
          "lat": 41.7891387,
          "lng": -87.5954555
        },
...
```

Ahh, just what we needed to display on our "Street to Coordinates" result page! Wow, APIs seem intimidating, but in reality it's just a URL that we provide and we get back information from a database owned by some company. Once we get to the stage of entering a URL with some form data and receiving a response, then it's actually pretty simple to finish our app.

Now it's time to actually get our form and results working. We'll start by just copying our working URL into the `experiment` action in our GitPod app:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def experiment
    @url = "https://maps.googleapis.com/maps/api/geocode/json?address=5807 S Woodlawn Ave&key=TODO"

    render({ :template => "math_templates/experiment.html.erb" })
  end
end
```
{: mark_lines="5"}

(You may see `%20` characters in the place of the URL spaces we put in, like `5807%20S%20Woodlawn%20Ave`. You can copy those in too, they just mean "space".)

And now we can use some cool methods for opening (`open` built into Ruby):

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def experiment
    @url = "https://maps.googleapis.com/maps/api/geocode/json?address=5807 S Woodlawn Ave&key=TODO"

    @raw = open(@url)

    render({ :template => "math_templates/experiment.html.erb" })
  end
end
```
{: mark_lines="7"}

Now if we open our view template and inject this instance variable in:

```html
<!-- app/views/math_templates/experiment.html.erb -->

<%= @raw %>
```
{: mark_lines="3"}

then load the URL **/experiment** in our app browser, we will see "#<StringIO:0x00007f623b0d66b0>" or something similar. This is an object of class `String`, which contains that page. We can call another method on this in the view template:

```html
<!-- app/views/math_templates/experiment.html.erb -->

<%= @raw.read %>
```
{: mark_lines="3"}

which will get the body of the page and return is as a string when we refresh the browser. This will be the entire (long) JSON string.

We can put all this into the action:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def experiment
    @url = "https://maps.googleapis.com/maps/api/geocode/json?address=5807 S Woodlawn Ave&key=TODO"

    @raw = open(@url).read

    render({ :template => "math_templates/experiment.html.erb" })
  end
end
```
{: mark_lines="7"}

We could now remove the `.read` from our HTML view template. We can go into our action and change `address=5807 S Woodlawn Ave` in the URL to whatever we want (e.g., `address=Miami FL`), and if we refresh **/experiment** then we will see the JSON changing. The page now dynamically reacts using information from the Google API. 

Now, we can also parse the JSON (which is currently just a long `String` variable) to get just the information we want. We don't want to directly parse the string (e.g., with `.split()`). There is a much better way: we can convert it into a `Hash` using the built in class `JSON` and one of its methods, `parse()`, to convert it to a `Hash`. Then we can take our `Hash`, bury through the key/value pairs (there are `Hash`es within the `Hash`!), and figure out where the latitude and longitude values are to then pull out (`.fetch()`) as instance variables and put on our webpage.

Alltogether that looks like:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def experiment
    @url = "https://maps.googleapis.com/maps/api/geocode/json?address=5807 S Woodlawn Ave&key=TODO"

    @raw = open(@url).read

    @parsed = JSON.parse(@raw) # parsed is now a Hash class

    # and we bury down into the hash with the key/value pairs
    # to get what we want
    @results = @parsed.fetch("results")
    @geom = @results.fetch("geometry")
    @loc = @geom.fetch("location")
    @lat = @loc.fetch("lat")
    @lng = @loc.fetch("lng")

    render({ :template => "math_templates/experiment.html.erb" })
  end
end
```
{: mark_lines="9-17"}

And display that in our experiment template:

```html
<!-- app/views/math_templates/experiment.html.erb -->

Latitude <%= @lat %>, Longitude <%= @lng %>
```
{: mark_lines="3"}

Now, we hard-coded an address `5807 S Woodlawn Ave` into our `experiment` action in the `@url` variable, so we would need this to come from an associated input form so the user could change this string. That is not required, but is good practice if you implement it.


### Text Companion: Intro to APIs with Street to Coordinates

## Finish and Submit Omnicalc 2

- Notes:

  - Below are relevant notes for the rest of the project taken from the README
  - API stretch goal should maybe go in a separate place?


**BENP: I think all of this additional API stuff needs to go in a separate document with links to [Google Cloud Translate][Google Cloud Translate] and [Sending emails and text messages][Sending emails and text messages] documents that right now are just linked as optional exercises on the Day 5 material on Canvas**


### Your tasks

 - **Street to Coordinates:** Figure out how to turn an arbitrary street address (find a place that is [sort of rainy](https://www.rainviewer.com/) right now to test with) into a latitude/longitude using the Geocoding API.
 - **Coordinates to weather:** Figure out how to turn a latitude/longitude pair into a weather forecast using the Dark Sky API Show the information displayed in the target:
    - Current Temperature
    - Current summaray
    - Outlooks for next sixy minutes, several hours, several days
 - **Street to Weather:** Put the above two together — given an arbitrary street address, display the forecast.


### Stretch goal
   
   - Stretch goal: check whether there is a >50% chance of precipitation at any point during the next 12 hours. If so, we will print "You should take an umbrella!"
   - Explore [the API documentation](https://darksky.net/dev/docs#forecast-request) to see what information is available to help you check this.
   - Something that might or might not be useful: [the `Time.at` method](https://apidock.com/ruby/Time/at/class).

        (Humans have [many, many different ways of representing dates](https://en.wikipedia.org/wiki/List_of_calendars). For the purposes of different pieces of software being able to agree on dates and times, most systems when talking to each other use [Epoch time](https://en.wikipedia.org/wiki/Unix_time) notation, or the number of seconds that have passed since midnight UTC on January 1st (minus leap seconds). Dark Sky, for example, includes times in this format. You can use `Time.at()` to convert to something more familiar, if you want to.)
 - Put all of the pieces together; given an arbitrary address:
    - print the current temperature
    - print outlook for the next hour
    - print whether a person should carry an umbrella.

### Using gems to interact with APIs

- Notes:

  - from [https://github.com/appdev-targets/omnicalc-2-api-starting-point#using-gems-to-interact-with-apis](https://github.com/appdev-targets/omnicalc-2-api-starting-point#using-gems-to-interact-with-apis){target="_blank"}

Interacting with APIs can be easier if someone has written a Ruby library (or "gem") with methods that already know the URLs, parse the JSON, and return exactly the values we want.

#### Twilio

In your `Gemfile`, add:

```ruby
gem "twilio-ruby"
```

Then, at a Terminal prompt:

```bash
bundle install
```

You will then have access to the `Twilio::REST::Client` class. It is used like this:

```ruby
# Retrieve your credentials from secure storage
twilio_sid = ENV.fetch("TWILIO_ACCOUNT_SID")
twilio_token = ENV.fetch("TWILIO_AUTH_TOKEN")
twilio_sending_number = ENV.fetch("TWILIO_SENDING_PHONE_NUMBER")

# Create an instance of the Twilio Client and authenticate with your API key
twilio_client = Twilio::REST::Client.new(twilio_sid, twilio_token)

# Craft your SMS as a Hash with three keys
sms_parameters = {
  :from => twilio_sending_number,
  :to => "+19876543210", # Put your own phone number here if you want to see it in action
  :body => "It's going to rain today — take an umbrella!"
}

# Send your SMS!
twilio_client.api.account.messages.create(sms_parameters)
```

 - Sign up for your own Twilio account — [if use this referral link you'll $10 in credit](https://www.twilio.com/referral/86ykDX), and so will our class account.
 - [Twilio Ruby Quickstarts](https://www.twilio.com/docs/quickstart/ruby)

#### Google Cloud Translate

 - [Google Cloud Translation](https://cloud.google.com/translate)

Here's the crux of using the official Google Translate gem.

Add the gem to your Gemfile:

```ruby
# /Gemfile
gem "google-cloud-translate", "2.3.0"
```

Then `bundle install` and restart your web server.

You now have access to the `Google::Cloud::Translate` class. To use it:

```ruby
require "google/cloud/translate"
gt_client = Google::Cloud::Translate.new({ :version => :v2 })
translation = gt_client.translate("Hello, world!", { :to => "es" })
```

Amazing! (If that didn't work, ensure that you've added my API credentials [as environment variables on Gitpod](https://chapters.firstdraft.com/chapters/792). You can find them in Canvas.)

To list all available languages,

```ruby
languages = gt_client.languages("en") # The argument determines what language to list the other language names in
languages.size #=> 104
languages[0].code #=> "af"
languages[0].name #=> "Afrikaans"
```

**Stretch goal:** Make your app behave like the target 

Read more at the gem docs:

 - [Ruby gem documentation](https://googleapis.dev/ruby/google-cloud-translate/latest/index.html#Using_the_legacy_v2_client)
