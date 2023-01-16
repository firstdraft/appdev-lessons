# Cookies Intro

- Notes:

  - [Cookies Intro video](https://canvas.uchicago.edu/courses/41147/pages/video-cookies-intro){target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/cookies-with-video.md){target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/cookies-intro](https://github.com/appdev-projects/cookies-intro){target="_blank"}

  - Target: [https://cookies-intro.matchthetarget.com/](https://cookies-intro.matchthetarget.com/){target="_blank"}

  - Useful chapters:
    - [`cookies.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/cookies.md){target="_blank"}
    - [`cookies-vs-session.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/cookies-vs-session.md){target="_blank"}

**BENP: note that this assignment is not manadatory, so is there even a rails grade? May need to doublde check this in other optional assignments as well**

## Video Segment: Exploring Browser Cookies

- Notes:

  - time stamp 00:00:25 to 00:03:30
  - in Chrome, visit [target](https://cookies-intro.matchthetarget.com/), "Inspect" > "Application" > "Cookies", Name/Value pairs

This is much like Omnicalc, but the difference is, when we type in some values and go back to previous pages, it remembers my previous inputs. Somehow this application is storing information between requests. 

We could have done that with a database and tables, storing the information that was put in the forms. But if we open another browser, navigate to the [target](https://cookies-intro.matchthetarget.com/){target="_blank"}, and enter some new calculations, then we can see that it remembers the information only from the current browser. So we are not just storing information in a database and retrieving the most recent record to show to everyone.

Each individual user is seeing their own previous calculation. Now with cookies we have the tools to do this.

**BENP: below is transcription, but really needs a GIF showing it**

If you open your developer tools in Chrome by right-clicking on an element and selecting "Inspect", you will will see a tab in the toolbar called "Application".

The "Application" tab has a navigation menu on the left side, where you can find a section called "Cookies". The cookies are grouped by domain, and you can see all of the cookies that are being stored by the current domain of the target. These values are being stored by Chrome on your own laptop, so they are unique to each of us on different computers!

We can see the "Name" column and the "Value" column with things related to our addition, subtraction, multiplication, and division. These are key/value pairs, just like the hashes that we are used to.

Each domain is able to store about 50 key/value pairs, with some slight variation in the amount by browser (e.g., Chrome vs. Firefox), and use about 4 kb of space. That's not much space, but plenty for some basic text information.

What if I select a row from my cookies table and delete it? When I go back to the form associated with that cookie, the memory of the key/value pair I entered will be erased. It resets the memory. Useful if you ever want to force signout of a website (using the "Clear all cookies" button).



### Text Companion: Exploring Browser Cookies

## Video Segment: `cookies` Object

- Notes:

  - time stamp 00:03:30 to 00:10:23
  - explore `<%= cookies %>` on `app/views/calculation_templates/addition_form.html.erb`
  - `cookies.store()` in `add` action and show in view template

Let's see how to implement this in our Rails app. If we open our app browser and try some of the calculation forms and go back, we will see there is no memory of my previous interaction being shown.

First, let's find the form we want to work on. How about addition? We can begin by embedding a variable called `cookies`, that we haven't discussed yet. Rails creates this and gives it to us, just like `params`. It comes pre-defined for us and puts it into this hash-like object:

```html
<!--- app/views/calculation_templates/addition_form.html.erb --->

<h1>New addition</h1>

<form action="/wizard_add">
  <label for="first_field">Add this:</label>
  <input type="text" id="first_field" name="first_num">

  <label for="second_field">to this:</label>
  <input type="text" id="second_field" name="second_num">

  <button>Add!</button>
</form>

<%= cookies %>
```
{: mark_lines="15"}

Now we can refresh the "Add" page (at the URL path **/muggle_add**), and we will see that where we embedded `cookies` there is a an `ActionDispatch::Cookies::CookieJar` class.

This object behaves just like a hash. So we can do things like `.fetch()` and `.store()` key/value pairs in it. If we wanted to store some random pair like `apple` (key) and `banana` (value), we could write `<%= cookies.store(:apple, "banana") %>`.

If we refresh **/muggle_add**, then open the dev tools and go to our "Application" tab and then the cookies for the current domain, we will see the "Name" and "Value" column have been added to with "apple" and "banana", respectively. So this information is now stored in the browser on my laptop. And we could go and `.fetch` it from `cookies` elsewhere in the app!

But let's do something more interesting. Let's store the results of each addition. We know from our addition form, that the `action="/wizard_add"` is telling us that this is the route the form will send the input to. That route goes to the `app/controllers/calculations_controller.rb` action called `add` (check the `config/routes.rb` file to see that). This is the action that actually parses information from the query string (supplied by the form), does the calculation and renders a template showing the result. Let's improve this action by also storing the results in our `cookies` object:

```ruby
# app/controllers/calculations_controller.rb

class CalculationsController < ApplicationController
...
  def add
    @first_number = params.fetch("first_num").to_f
    @second_number = params.fetch("second_num").to_f

    @result = @first_number.to_f + @second_number.to_f

    cookies.store(:addition_result, @result)

    render({ :template => "calculation_templates/add_results.html.erb" })
  end
...
```
{:mark_lines="11"}

Now that we stored it in the `cookies` hash, if we go back to **/muggle_add**, and (with our dev tools cookies tab open!) input some data and click "Add!", then we will see a new "Name"/"Value" pair appear in our table, the "addition_result" with our `@result` value from the action.

And now, back in the form, we can embed the new `cookies` value using the key that we assigned to it in the action:

```html
<!--- app/views/calculation_templates/addition_form.html.erb --->

<h1>New addition</h1>

<form action="/wizard_add">
  <label for="first_field">Add this:</label>
  <input type="text" id="first_field" name="first_num">

  <label for="second_field">to this:</label>
  <input type="text" id="second_field" name="second_num">

  <button>Add!</button>
</form>

<p>Your previous addition was: <%= cookies.fetch(:addition_result) %></p>
```
{: mark_lines="15"}

And now if we enter data in the form, click "Add!", view the results, and then return to **/muggle_add**, we will see the result of our previous calculation being displayed.

We can expand this to match the target by storing the other two numbers and displaying the full calculation string on the addition page:

```ruby
# app/controllers/calculations_controller.rb

class CalculationsController < ApplicationController
...
  def add
    @first_number = params.fetch("first_num").to_f
    @second_number = params.fetch("second_num").to_f

    @result = @first_number.to_f + @second_number.to_f

    cookies.store(:addition_result, @result)
    cookies.store(:addition_first, @first_number)
    cookies.store(:addition_second, @second_number)

    render({ :template => "calculation_templates/add_results.html.erb" })
  end
...
```
{:mark_lines="12-13"}

```html
<!--- app/views/calculation_templates/addition_form.html.erb --->

<h1>New addition</h1>

<form action="/wizard_add">
  <label for="first_field">Add this:</label>
  <input type="text" id="first_field" name="first_num">

  <label for="second_field">to this:</label>
  <input type="text" id="second_field" name="second_num">

  <button>Add!</button>
</form>

<p>
  Your previous addition was: 
  <%= cookies.fetch(:addition_first) %> + 
  <%= cookies.fetch(:addition_second) %> = 
  <%= cookies.fetch(:addition_result) %>
</p>
```
{: mark_lines="15-20"}

Now the page **/muggle_add** should match the target.

That's fundamentally it for cookies! Just a simple key/value object called `cookies` that we can add to and pull values out of in *any* action and *any* view template.

The cookies that a user stores on their computer will come back to us everytime they visit our app from the same browser and we can fetch to show the user tailored content. Until they clear their cookies, use a new browser, or use a new computer.


### Text Companion: `cookies` Object

## Finish and Submit Cookies Intro

  - see `cookies.md` for requirements