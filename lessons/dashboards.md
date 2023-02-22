# Dashboards (Dynamic Route Segments)

- Notes:

  - [Original video](https://canvas.uchicago.edu/courses/41147/pages/video-dashboards-dynamic-route-segments){:target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/dashboards.md){:target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/dashboards](https://github.com/appdev-projects/dashboards){:target="_blank"}
    - And [here](https://gitpod.io/#snapshot/f960df8d-c502-40c4-a9bb-f224196aa028){:target="_blank"} is a snapshot of the Omnicalc 2 workspace, which may be useful as reference.

  - Target: [http://dashboards.matchthetarget.com/](http://dashboards.matchthetarget.com/){:target="_blank"}

  - Useful chapters:

    - [Refactoring Fortune Teller with Dynamic Routes][Refactoring Fortune Teller with Dynamic Routes]

## Video Segment: URLs and Dynamic Routes

- Notes:

  - time stamp 00:00:00 to 00:02:00
  - dynamic route segments in `params`. sometimes we call these flexible routes.
  - using **/chapters/841** as example
  - wildcards

The modern world revolves around the humble URL. And now I hope you're staring to notice these and understand them a little bit better. For example the [refactoring Fortune Teller chapter](https://chapters.firstdraft.com/chapters/841){:target="_blank"}:

**https://chapters.firstdraft.com/chapters/841**

You've got a path **/chapters/841** with two segments, **chapters** and **841**, just like in our dice rolls from refactoring: **https://refactoring-fortune-teller.matchthetarget.com/roll/42/1337**.

We know how to connect a visit to the full path to a Ruby method that can generate dynamic content rather than just having static pages in the `public/` folder. 

After your experience refactoring, you now also know that you can have parts of the path that are *dynamic*. So we don't need to write a route for every single URL that we want to support. We can allow pieces of the path to be *wildcards* (like **841** in our chapter example), and in doing so we can support an infinite number of URLs because anything that matches a certain pattern will be recognized and routed to a single action that knows how to handle all requests of that variety.
  
So this is a second form of user input. The first form was *query stings* in the URL, and these are the *dynamic route segments*, which is how users tell us which resource they want. And that's it for user input! Both of them end up in our `params` hash, which we can `.fetch()` from.

### Text Companion: URLs and Dynamic Routes

## Video Segment: Exchange Rate API Intro

- Notes:

  - time stamp 00:02:10 to 00:03:56
  - explore https://api.exchangerate.host/symbols
  - discuss JSON format
  - using **/symbols** and **/convert**

In this next project, let's finally use some more realistic data. Enough with random numbers and rock, paper, scissors. Let's get some actual data from APIs like we did with the umbrella project. **BENP: did they do this project?**

The first API that we're going to use is called [**https://api.exchangerate.host/symbols**](https://api.exchangerate.host/symbols){:target="_blank"}. It gives us back JSON that looks like this:

```json
// 20221219122429
// https://api.exchangerate.host/symbols

{
  "motd": {
    "msg": "If you or your company use this project or like what we doing, please consider backing us so we can continue maintaining and evolving this project.",
    "url": "https://exchangerate.host/#/donate"
  },
  "success": true,
  "symbols": {
    "AED": {
      "description": "United Arab Emirates Dirham",
      "code": "AED"
    },
    "AFN": {
      "description": "Afghan Afghani",
      "code": "AFN"
    },
    
    // ...
```

Where we can see many currencies (even crypto!). This is a free API. If you put in any of their supported symbols, it will instantaneously and for free give you back the current exchange rate. For example if we use the URL to go from USD to Euros:

**https://api.exchangerate.host/convert?from=USD&to=EUR**

Then we get back:

```json
// 20221219123153
// https://api.exchangerate.host/convert?from=USD&to=EUR

{
  "motd": {
    "msg": "If you or your company use this project or like what we doing, please consider backing us so we can continue maintaining and evolving this project.",
    "url": "https://exchangerate.host/#/donate"
  },
  "success": true,
  "query": {
    "from": "USD",
    "to": "EUR",
    "amount": 1
  },
  "info": {
    "rate": 0.942959
  },
  "historical": false,
  "date": "2022-12-19",
  "result": 0.942959
}
```

This is great for us to practice our dynamic routes and APIs.

We'll use the two **api.exchangerate.host** endpoints for listing symbols **/symbols** and converting currencies **/convert** to build our [target](https://dashboards.matchthetarget.com){:target="_blank"}. Full documentation for the API can be found [here](https://exchangerate.host/#/#docs){:target="_blank"}

### Text Companion: Exchange Rate API Intro

## Video Segment: Building /forex

- Notes:

  - time stamp 00:03:56 to 00:22:39
  - RCAV **/forex** URL that lists all available currency symbols from JSON keys at https://api.exchangerate.host/symbols

The first thing we're going to build and the required part of this homework is a route that looks like **/forex** ([**https://dashboards.matchthetarget.com/forex**](https://dashboards.matchthetarget.com){:target="_blank"} in our target). 

This URL should list all of the available symbols, and if I click on one of the links it should take me to a page with the path: [**/forex/EUR**](http://dashboards.matchthetarget.com/forex/EUR){:target="_blank"}, where the second segment is the currency I clicked. And on that page it should give me all of the symbols, including the current symbol itself. Clicking on a given link there (like "Convert 1 EUR to USD..."), will take me to the URL: [**/forex/EUR/USD**](http://dashboards.matchthetarget.com/forex/EUR/USD){:target="_blank"}, where I will see the conversion rate.

Of course I could type in manually, like:

**/forex/EUR/MWK**

if I know the what these URLs look like and how what symbol corresponds to what currency.

So you're job is to build all of that. It should be doable with what you know about dynamic route segments and reading APIs **BENP link to dynamic route and reading API content**. If you feel up to the challenge, pause the video now and try to build the routes yourself!

**BENP: suggested pause point at 00:06:00**

I'm going to do my usual thing. Start up Gitpod, start the server, type in the URL I want to build as a user in the browser, and just start debugging the error messages.

Let's visit `config/routes.rb`, and we will see it is a completely blank Rails app that we are dealing with. We will start by building **/forex**. So let's add the route:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/forex", { :controller => "currencies", :action => "first_currency" })

end
```
{: mark_lines="5"}

From now on, we are not putting our actions in `ApplicationController`, so I made up a name called `"currencies"` for the controller and an action within that called `"first_currency"` (because this action will list the first currency in the exchange rate calculation).

(As usual, between every step I refresh my browser **/forex** path, and RTEM.)

So now in `app/controllers/`, I can make a new controller file called `currencies_controller.rb`, and fill that in with my inheritence from `ApplicationController` and my action:

```ruby
# app/controllers/currencies_controller.rb

class CurrenciesController < ApplicationController
  def first_currency

    render({ :template => "currency_templates/step_one.html.erb" })
  end
end
```

We made up names for our view templates folder (`"currency_templates/"`) and file (`"step_one.html.erb"`), so we need to create both of these in `app/views/`, and fill in some dummy copy:

```html
<!-- app/views/currency_templates/step_one.html.erb -->

hi
```

Now everything should be wired up correctly and we can think about the actual work to be done. It can be helpful to start by just mocking up the document with some static HTML to form an outline. We can right-click and "View Source" on the [target](http://dashboards.matchthetarget.com/forex){:target="_blank"} to help us with the proper HTML tags. We can just copy-paste in the first lines of the body in this case and clean it up a bit. 

```html
<!-- app/views/currency_templates/step_one.html.erb -->

<h1>Currency pairs</h1>

<p>Go <a href="/">back<a>.</p>

<ul>
  <li>
    <a href="/forex/AED">
      Convert 1 AED to...
    </a>
  </li>
</ul>
```
{: mark_lines="3-13"}

So now we have a starting point. What we need is to get a list of all the symbols like `AED` above from the API, and print them out in an unordered list of links. We don't want to hard code the list, we want to get it fresh everytime in case the list of symbols (currencies) changes. 

From our API endpoint [**https://api.exchangerate.host/symbols**](https://api.exchangerate.host/symbols){:target="_blank"}, we just need the currency symbols from the JSON. It might be nice to show the currency name (`description`):

```json
...
  - AED: {
    description: "United Arab Emirates Dirham",
    code: "AED"
  }
...
```

but the target doesn't do that, so we really just need the keys from the sub-hash.

Let's return to our view template and write in some pseudo-code for what we wish that we had:

```html
<!-- app/views/currency_templates/step_one.html.erb -->

<h1>Currency pairs</h1>

<p>Go <a href="/">back<a>.</p>

<ul>
  <% @array_of_symbols.each do |a_symbol| >
    <li>
      <a href="/forex/AED">
        Convert 1 AED to...
      </a>
    </li>
  <% end %>
</ul>
```
{: mark_lines="8 14"}

If we had an `@array_of_symbols` containing all of our currency symbols, we could loop over it with `.each`, take each `a_symbol` variable, and replace `AED` with that symbol, thus building up a long unordered list.

Okay, we need to create our desired instance variable in the controller action now:

```ruby
# app/controllers/currencies_controller.rb

class CurrenciesController < ApplicationController
  def first_currency
    
    @raw_data = open("https://api.exchangerate.host/symbols").read

    render({ :template => "currency_templates/step_one.html.erb" })
  end
end
```
{: mark_lines="6"}

We need the URL that has the data (**https://api.exchangerate.host/symbols**), then we need to use the method `open()` on that string, and finally we need to call the `read` method on the opened file, which will return the file as a long string. 

(Normally, we would need a line `require "open-uri"` to allow Ruby to read files across the internet, but we don't have to do that in Rails, because Rails has already done that for its own operation.)

Once we have the file opened as a string with `read` in the `@raw_data` variable, we can convert it to a hash using `JSON.parse()`:

```ruby
# app/controllers/currencies_controller.rb

class CurrenciesController < ApplicationController
  def first_currency
    
    @raw_data = open("https://api.exchangerate.host/symbols").read
    @parsed_data = JSON.parse(@raw_data)

    render({ :template => "currency_templates/step_one.html.erb" })
  end
end
```
{: mark_lines="7"}  


Now if we view the `@parsed_data` in our view template (by adding `<%= @parsed_data %>`), we will see our full hash. And at this point it's just a matter of peeling off each layer of the onion, and burying into the hash to pull out the symbols:

```ruby
# app/controllers/currencies_controller.rb

class CurrenciesController < ApplicationController
  def first_currency
    
    @raw_data = open("https://api.exchangerate.host/symbols").read
    @parsed_data = JSON.parse(@raw_data)
    @symbols_hash = @parsed_data.fetch("symbols")
    @array_of_symbols = @symbols.keys

    render({ :template => "currency_templates/step_one.html.erb" })
  end
end
```
{: mark_lines="8-9"}  

We used the handy [`.keys`](https://chapters.firstdraft.com/chapters/767#use-keys-to-explore) method on our sub-hash (that we `.fetch()`ed from the full hash), because the list of symbols is actually contained in the key names. No need to use a second `.fetch()` in this case.

Now we should be good to go in our template, by replacing the `AED` (in the copy and `href` link!) with our embedded Ruby tags for each symbol in the array:

```html
<!-- app/views/currency_templates/step_one.html.erb -->

<h1>Currency pairs</h1>

<p>Go <a href="/">back<a>.</p>

<ul>
  <% @array_of_symbols.each do |a_symbol| %>
    <li>
      <a href="/forex/<%= a_symbol %>">
        Convert 1 <%= a_symbol %> to...
      </a>
    </li>
  <% end %>
</ul>
```
{: mark_lines="10-11"}

In the above, we included embedded Ruby in our HTML tag attribute (`href=""`). This is very common! We often need to include dynamic responses in the attributes to HTML to get our pages to behave correctly.

And now the page **/forex** should behave like the target.

Time for a `rails grade` and **/git** commit.

Try to tackle the next route **/forex/SYMBOL**, and maybe even **/forex/SYMBOL/SYMBOL**, on your own. How can you build a *dynamic route* to support every possibility here, so you don't need to hard-code hundreds of individual routes?

### Text Companion: Building /forex

## Video Segment: Building /forex/SYMBOL/SYMBOL

- Notes:

  - time stamp 00:22:39 to 00:33:01
  - RCAV **/forex/SYMBOL/SYMBOL** URL with dynamic route segments that lists all available currency exchange rates from JSON at https://api.exchangerate.host/convert with query strings like **?from=USD&to=EUR**

Let's start with the next step, where a user can select a currrency on **/forex**, which brings them to **/forex/SYMBOL**, where they can select a second currency bringing them to the exchange rate on **/forex/SYMBOL/SYMBOL**.

We begin by simulating what we want to work by navigating our browser to **/forex/AWG**, RTEM, and starting the RCAV:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/forex", { :controller => "currencies", :action => "first_currency" })

  get("/forex/...", { :controller => "currencies", :action => "second_currency" })

end
```
{: mark_lines="7"}

Where we have `/...` above, we want a dynamic route wildcard that can be pulled out in the `params`, otherwise, we have the usual controller (same as our previous) and a new action we will make in that controller (`"second_currency"`).

We don't want to type `/AWG`, because that is just one of our many currencies. But, if we remember our dynamic routes **BENP: link to dice here**, we know we can use a symbol to make it flexible, like so:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/forex", { :controller => "currencies", :action => "first_currency" })

  get("/forex/:from_currency", { :controller => "currencies", :action => "second_currency" })

end
```
{: mark_lines="7"}

Now our routing error in the browser should be gone and we can move on to making the action in our controller:

```ruby
# app/controllers/currencies_controller.rb

class CurrenciesController < ApplicationController
  def first_currency
    
    @raw_data = open("https://api.exchangerate.host/symbols").read
    @parsed_data = JSON.parse(@raw_data)
    @symbols_hash = @parsed_data.fetch("symbols")
    @array_of_symbols = @symbols.keys

    render({ :template => "currency_templates/step_one.html.erb" })
  end

  def second_currency
    
    render({ :template => "currency_templates/step_two.html.erb" })
  end
end
```
{: mark_lines="14-17"}  

And we will right away add some static markup from the target ("View Source") into our view template:

```html
<!-- app/views/currency_templates/step_two.html.erb -->

<h1>Convert AWG</h1>

<p>Go <a href="/forex">back<a>.</p>

<ul>
  <li>
    <a href="/forex/AWG/INR">
      Convert 1 AWG to INR...
    </a>
  </li>

  <li>
    <a href="/AWG/EUR">
      Convert 1 AWG to EUR...
    </a>
  </li>
</ul>
```

This pattern of list items would need to be repeated over and over. So let's make the static mockup dynamic by looping over the symbols array:

```html
<!-- app/views/currency_templates/step_two.html.erb -->

<h1>Convert AWG</h1>

<p>Go <a href="/forex">back<a>.</p>

<ul>
  <% @array_of_symbols.each do |a_symbol| %>
    <li>
      <a href="/forex/AWG/<%= a_symbol %>">
        Convert 1 AWG to <%= a_symbol %>...
      </a>
    </li>
  <% end %>
</ul>
```
{: mark_lines="8-14"}

And now back into our controller, just copy and pasting from our previous action:

```ruby
# app/controllers/currencies_controller.rb

class CurrenciesController < ApplicationController
  def first_currency
    
    @raw_data = open("https://api.exchangerate.host/symbols").read
    @parsed_data = JSON.parse(@raw_data)
    @symbols_hash = @parsed_data.fetch("symbols")
    @array_of_symbols = @symbols.keys

    render({ :template => "currency_templates/step_one.html.erb" })
  end

  def second_currency

    @raw_data = open("https://api.exchangerate.host/symbols").read
    @parsed_data = JSON.parse(@raw_data)
    @symbols_hash = @parsed_data.fetch("symbols")
    @array_of_symbols = @symbols.keys
    
    render({ :template => "currency_templates/step_two.html.erb" })
  end
end
```
{: mark_lines="16-19"}

Okay, it looks close. But we need to get the information out of our dynamic route **/forex/SYMBOL** to make our page change with each currency. 

Well everytime we visit a given route (by typing or clicking a link) like **/forex/AWG**, or **/forex/INR**, or **/forex/EUR**, because I defined my route dynamically in `config/routes.rb` as `"/forex/:from_currency"`, if we view our server log in the Gitpod terminal window when we visit the page, then we will see:

```
Parameters: {"from_currency"=>"EUR"}
```

So we have the currency symbol in the hash, and we can pull it out and use it in our controller:

```ruby
# app/controllers/currencies_controller.rb

class CurrenciesController < ApplicationController
  def first_currency
    
    @raw_data = open("https://api.exchangerate.host/symbols").read
    @parsed_data = JSON.parse(@raw_data)
    @symbols_hash = @parsed_data.fetch("symbols")
    @array_of_symbols = @symbols.keys

    render({ :template => "currency_templates/step_one.html.erb" })
  end

  def second_currency

    @raw_data = open("https://api.exchangerate.host/symbols").read
    @parsed_data = JSON.parse(@raw_data)
    @symbols_hash = @parsed_data.fetch("symbols")
    @array_of_symbols = @symbols.keys
    
    # params are
    # Parameters: {"from_currency"=>"EUR"}
    @from_symbol = params.fetch("from_currency")
    
    render({ :template => "currency_templates/step_two.html.erb" })
  end
end
```
{: mark_lines="16-19"}

And back on our template we embed the new instance variable in our previous `AWG` static mockup (it's as easy as replacing every instance with `<%= @from_symbol %>`):

```html
<!-- app/views/currency_templates/step_two.html.erb -->

<h1>Convert <%= @from_symbol %></h1>

<p>Go <a href="/forex">back<a>.</p>

<ul>
  <% @array_of_symbols.each do |a_symbol| %>
    <li>
      <a href="/forex/<%= @from_symbol %>/<%= a_symbol %>">
        Convert 1 <%= @from_symbol %> to <%= a_symbol %>...
      </a>
    </li>
  <% end %>
</ul>
```
{: mark_lines="3 10-11"}

And we have a dynamic route setup for the list of currency conversions! Test it manually, do a `rails grade`, and be sure to **/git** commit if everything looks good.

The last step is to build the second currency symbol route, like **/forex/AWG/USD**. So you need to get two pieces of data out. You need to write a route that can accept two dynamic segments, fetch both of those segments from the params hash, and then use that to call the API: **https://api.exchangerate.host/convert?from=AWG&to=EUR**, and finally extract the exchange rate from the JSON returned. 

### Text Companion: Building /forex/SYMBOL/SYMBOL

## Finish and Submit Dashboards

- Notes:

  - covid tracking README text at bottom of [https://github.com/appdev-projects/dashboards](https://github.com/appdev-projects/dashboards){:target="_blank"}

### The COVID Tracking Project

- API endpoint for a single state (Illinois): [**https://api.covidtracking.com/v1/states/ca/current.json**](https://api.covidtracking.com/v1/states/ca/current.json){:target="_blank"}
- [Full documentation](https://covidtracking.com/data/api){:target="_blank"}