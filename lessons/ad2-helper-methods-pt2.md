# AD2 Helper Methods Pt 2

**BENP: Document based on descript transcription of AD2 WS 2023 Helper Methods Part 2 Video.**

## `form_with` 00:00:00 to 00:12:00

We're continuing to work in our same [Helper Methods](https://github.com/appdev-projects/helper-methods) Gitpod project. We'll start where we left off with the `link_to` helper method. Hopefully all of your `<a>` elements are now `link_to` helper methods instead. 

It's time to work on our `<form>`s and turn those into helper methods also. This is going to pay big dividends for us down the line.

Let's start with the form in `app/views/movies/new.html.erb`. The new helper method we'll use to replace this whole form is `form_with`. Let's begin:

```html
<!-- app/views/movies/new.html.erb -->

<h1>New movie</h1>

<% @the_movie.errors.full_messages.each do |message| %>
  <p style="color: red;"><%= message %></p>
<% end %>

<%= form_with(url: movie_path(@the_movie)) do %>
  
<% end %>

<form action="<%= movie_path(@the_movie))%>" method="post">
  <input name="authenticity_token" value="<%= form_authenticity_token %>" type="hidden">
  ...
```
{: mark_lines="9-11" }

As you can see, the method takes arguments. In this case we pass the option `url:` the output of our route helper `movie_path(@the_movie)) (which we know is just `"/movies"`). We also put this helper in a `do`-`end` block, because it's going to write a form for us in this block!

In the live app, refresh the **/movies/new** page and "view source". You should see that `form_with` has produced:

```html
<form action="/movies" accept-charset="UTF-8" method="post"><input type="hidden" name="authenticity_token" value="some-long-token">

</form>
```

Compare that with the form that we wrote by hand. Pretty similar right? 

The `form_with` helper not only added an attribute with the accepted characterset (UTF-8), but also automatically created an authenticity token to protect our form against CSRF attacks. We don't need to worry about remembering this step with the `form_with` helper. 

Let's move all of our previous inputs and tags into this block now (removing our old `<form>` opening and closing tags):

```html
<!-- app/views/movies/new.html.erb -->

<h1>New movie</h1>

<% @the_movie.errors.full_messages.each do |message| %>
  <p style="color: red;"><%= message %></p>
<% end %>

<%= form_with(url: movie_path(@the_movie)) do %>
  <div>
    <label for="title_box">
      Title
    </label>

    <input type="text" id="title_box" name="query_title" value="<%= @the_movie.title %>">
  </div>

  <div>
    <label for="description_box">
      Description
    </label>

    <textarea id="description_box" name="query_description" rows="3"><%= @the_movie.description %></textarea>
  </div>

  <button>
    Create Movie
  </button>
<% end %>
```

Now what else can we do here?

For `<labels>`, we can use `label_tag`:

```html
...
<%= form_with(url: movie_path(@the_movie)) do %>
  <div>
    <%= label_tag :title_box, "Title" %>

    <input type="text" id="title_box" name="query_title" value="<%= @the_movie.title %>">
  </div>
...
```
{: mark_lines="4"}

The first argument to `label_tag` is the `for=""` attribute that connects the label with the input (by the input `id=""`), and the second argument is the copy we want shown. As usual, refresh and view source on the live app, and you should see a `<label>` tag rendered by this helper method. Same as before!

We can actually leave out the first argument `:title_box`, and just write `<%= label_tag "Title" %>`. What does that do on the page? View source and see for yourself.

The `for=""` attribute is now populated with the copy (`for="Title"`). That's nice, but in this case, we want to make sure our `for` and `id` attribute values matchup, so let's leave it as `<%= label_tag :title_box, "Title" %>`.

We also have helper methods for our `<input>`s. You might expect it to be `input_tag`, if we're following the same kind of pattern, but it's actually not because we have a separate helper method for each type of input: 

```html
...
<%= form_with(url: movies_path) do %>
  <div>
    <%= label_tag :title_box, "Title" %>

    <%= text_field_tag :query_title, @the_movie.title %>
    <!-- <input type="text" id="title_box" name="query_title" value="<%= @the_movie.title %>"> -->
  </div>
...
```
{: mark_lines="6-7"}

The `text_field_tag` that's replacing our `<input type="text"...>` HTML element is taking the `name=""` attribute as the first argument. This `name=""` is how the input will be registered in the `params` hash (in this case, as `query_string`), so that's a very important argument. After that, we have the `value=""` attribute that we want to prepopulate our form with. We spent awhile getting those prepoulation values working, to improve the form filling experience.

Refresh the live app and view source again. What do you notice about the `id=""` attribute with this input helper method?

It is just using the `name=""` attribute `query_string`, that we supplied the method! Similar to leaving out the `for=""` attribute on the `label_tag` helper. Rails will try to fill these in for us. We'll see how useful this is soon.

But for now, let's note that the final argument to our `text_field_tag` can be a hash of additional options that I want:

```html
...
<%= form_with(url: movies_path) do %>
  <div>
    <%= label_tag :title_box, "Title" %>

    <%= text_field_tag :query_title, @the_movie.title, {id: "title_box" } %>
    <!-- <input type="text" id="title_box" name="query_title" value="<%= @the_movie.title %>"> -->
  </div>
...
```
{: mark_lines="6"}

And refreshing our **/movies/new** then viewing source, we can see that added an `id="title_box"` to our `<input>` HTML element.

Do the same for the movie description as well. This is a `<textarea>` input, so we need to use the helper `text_area_tag`. Also, we had a `rows="3"` attribute, so we need to add that to our optional hash. Otherwise, the rest is similar to the "Title", so the whole form should end up like:

```html
<!-- app/views/movies/new.html.erb -->

<h1>New movie</h1>

<% @the_movie.errors.full_messages.each do |message| %>
  <p style="color: red;"><%= message %></p>
<% end %>

<%= form_with(url: movie_path(@the_movie)) do %>
  <div>
    <%= label_tag :title_box, "Title" %>

    <%= text_field_tag :query_title, @the_movie.title, {id: "title_box" } %>
  </div>

  <div>
    <%= label_tag :description_box, "Description" %>

    <%= text_area_tag :query_description, @the_movie.description, {id: "description_box", rows: 3 } %>
  </div>

  <button>
    Create Movie
  </button>
<% end %>
```
{: mark_lines="17 19"}

Check out the live app. Everything looking good? Great!

The last thing is the `<button>`. Even for this, we have a `button_tag` helper method:

```html
...
  <!-- <button>
    Create Movie
  </button> -->
  <%= button_tag "Create Movie" %>
<% end %>
```

All right, so now we've replaced all of the essential parts of this form, other than `<div>`s that we use to organize it, with helper methods. Ultimately, the output is the _exact_ same HTML as before, but it's better in many ways.

The most concrete way in this example is that we didn't have to generate the CSRF token manually. That's going to save us a lot of work over the hundreds of forms that we're going to make! 

Make a **/git** commit now.

## Update Edit Form 00:12:00 to 00:16:00

Let's take our new helper methods and do the same update on our edit page. Try to type out the new form to build some muscle memory. It's almost identical to our `new.html.erb` form. However, we can see a few key differences that need to be incorporated:

```html
<!-- app/views/movies/new.html.erb -->

<h1>Edit movie</h1>

<% @the_movie.errors.full_messages.each do |message| %>
  <p style="color: red;"><%= message %></p>
<% end %>

<%= form_with(url: movie_path(@the_movie), method: :patch) do %>
  <div>
    <%= label_tag :title_box, "Title" %>

    <%= text_field_tag :query_title, @the_movie.title, {id: "title_box" } %>
  </div>

  <div>
    <%= label_tag :description_box, "Description" %>

    <%= text_area_tag :query_description, @the_movie.description, {id: "description_box", rows: 3 } %>
  </div>

  <%= button_tag "Update Movie" %>
<% end %>
```
{: mark_lines="9"}

The default method that HTML forms use is `get`. But Rails is smart, and it knows that many of our forms use `post`. So by default, the `form_with` method on our `new.html.erb` form added the `method="post"` attribute _and_ the authenticity token. 

Similarly, we can tell `form_with` exactly which method (HTTP verb) we want to use. In the case of our `edit.html.erb` form, we actually want the `method: :patch`, which we pass in as an argument above.

If you view source on the new edit form, you will see that adding this argument to the helper method produced that odd bit of HTML to "trick" the form into making a patch request:

```html
<input name="_method" value="patch" type="hidden">
```

We never need to remember to add that again, because `form_with(..., method: :patch)` does it for us. Nifty!

Does the edit form work like before we refactored? If yes, then make another **/git** commit!

## Refactoring `MoviesController` 00:16:00 to 00:24:30

Our views are now much more concise. We're using Ruby helper methods embedded in the view templates to generate HTML in a more secure way, and in a more reusable way using route helper methods.

Now it's time to spend some time refactoring our `app/controllers/movies_controller.rb` file. If you haven't already, go through and make all the syntax changes. For instance, a line like:

```ruby
matching_movies = Movie.where({ :id => the_id })
```

should end up like:

```ruby
matching_movies = Movie.where(id: the_id)
```

In AD1, we were very deliberate in the three steps to get an `ActiveRecord` instance (a single row of a table) compared to an `ActiveRecord:Relation` (many rows of a table):

```ruby
  ...
  def show
    the_id = params.fetch(:id) # FIRST we get the ID

    matching_movies = Movie.where(id: the_id) # THEN we get the set of matching rows (ActiveRecord:Relation)

    @the_movie = matching_movies.first # FINALLY we get one instance of ActiveRecord, or one row
  end
  ...
```

As you might expect, professional Rails, developers do not do this. Instead, you will often see:

```ruby
  ...
  def show
    @the_movie = Movie.where(id: params.fetch(:id)).first
  end
  ...
```

There's actually a succinct method that is designed to do exactly that. It's called `find_by`, and it's exactly the same thing as `.where`, except that if automatically returns just the `.first` record given a collection:

```ruby
  ...
  def show
    @the_movie = Movie.find_by(id: params.fetch(:id))
  end
  ...
```

That method will return a `nil` if the `id` isn't found. (Try it in the `rails console` to see for yourself.)

And we can actually go one step farther and use another method:

```ruby
  ...
  def show
    @the_movie = Movie.find(params.fetch(:id))
  end
  ...
```

The `find` method, only takes an integer argument, and it assumes that you are searching on the table's ID column. No need to tell it which column as we did with `.where`. 

As opposed to `find_by`, which returns `nil` if the record with the given ID doesn't exist, `find` throws an error exception of class `ActiveRecord::RecordNotFound`. (Again, use the `rails console` to experiment with both methods on the `Movie` model.)

Once I push this my app to Heroku, if I'm using the `find` method, then this error message shows up as a 404 page, which is the correct behavior when someone tries to visit a resource that doesn't exist (like **/movies/890909820**, or some ID number we don't have in our table). If we used `find_by` and the query returned a `nil`, then a 500 page would be shown ("Something went wrong"), which is not the experience we want for our users.

And another thing while we're talking about this `show` method. Conventionally, Rails developers don't say `the` underscore `movie`. We did that in AD1 to be very explicit. The convention is to name these variables the same thing as the class name and the controller name!

```ruby
  ...
  def show
    @movie = Movie.find(params.fetch(:id))
  end
  ...
```

You _can_ name your variables whatever you want to, but it's just a convention and you'll see this done a lot.

Similarly, we should rename all of our `list_of_movies` variables to just `movies` (the resource plural). 

For instance, the `index` action should end up like:

```ruby
  ...
  def index
    @movies = Movie.order(created_at: :desc)

    respond_to do |format|
      format.json do
        render json: @movies
      end

      format.html
    end
  end
  ...
```

## Query String Naming and View Refactoring 00:24:30 to 00:30:00

Now what about those query strings? 

```ruby
  ...
  def create
    @movie = Movie.new
    @movie.title = params.fetch("query_title")
    @movie.description = params.fetch("query_description")

    if @movie.valid?
      @movie.save
      redirect_to movies_path, notice: "Movie created successfully."
    else
      render template: "movies/new.html.erb"
    end
  end
  ...
```
{: mark_lines="4-5"}

Recall, `"query_title"` is the `name` we gave to the input in our form, which goes into query string, and then into the `params` hash that we're fetching from. But we don't need the `"query_"` construction, it was just there to remind us. 

If we want to be more professional, we would just change those to the name of the column we are getting inputs for:

```ruby
  ...
  def create
    @movie = Movie.new
    @movie.title = params.fetch("title")
    @movie.description = params.fetch("description")

    if @movie.valid?
      @movie.save
      redirect_to movies_path, notice: "Movie created successfully."
    else
      render template: "new"
    end
  end
  ...
```
{: mark_lines="4-5"}

And, also, in the `params` hash, we typically fetch on symbols, rather than strings. We can only use strings and symbols interchangably in `params` because it is a special subclass of `Hash`:

```ruby
  ...
  def create
    @movie = Movie.new
    @movie.title = params.fetch(:title)
    @movie.description = params.fetch(:description)

    if @movie.valid?
      @movie.save
      redirect_to movies_path, notice: "Movie created successfully."
    else
      render template: "new"
    end
  end
  ...
```
{: mark_lines="4-5"}

Now, what that `params` key has to match is the `name` that we assigned that input back on our form. Let's take a peek back there on the `new.html.erb` form:

```html
<!-- app/views/movies/new.html.erb -->

...
<%= form_with(url: movie_path(@movie)) do %>
  <div>
    <%= label_tag :title_box, "Title" %>

    <%= text_field_tag :query_title, @movie.title, {id: "title_box" } %>
  </div>

  <div>
    <%= label_tag :description_box, "Description" %>

    <%= text_area_tag :query_description, @movie.description, {id: "description_box", rows: 3 } %>
  </div>
...
```
{: mark_lines="4 8 14"}

First of all, note that we changed `@the_movie` to `@movie`, because we changed the name of that instance variable in the controller. Now, look at these changes to align our view template with our controller `params` fetching:

```html
<!-- app/views/movies/new.html.erb -->

...
<%= form_with(url: movie_path(@movie)) do %>
  <div>
    <%= label_tag :title, "Title" %>

    <%= text_field_tag :title, @movie.title, {id: "title" } %>
  </div>

  <div>
    <%= label_tag :description, "Description" %>

    <%= text_area_tag :description, @movie.description, {id: "description", rows: 3 } %>
  </div>
...
```
{: mark_lines="6 8 12 14"}

We don't need the `query_` and we don't need the `_box`. Those are names we made up to help use keep track of things, but they aren't used in a professional code base.

Also, we can remove some more things here and let Rails automatically: 
 
 - set the label copy (by calling `.capitalize` on the `:title` or `:description`) 
 - and set the `for=""` / `id=""` attributes (which are just going to default to `"title"` and `"description"`):

```html
<!-- app/views/movies/new.html.erb -->

...
<%= form_with(url: movie_path(@movie)) do %>
  <div>
    <%= label_tag :title %>

    <%= text_field_tag :title, @movie.title %>
  </div>

  <div>
    <%= label_tag :description %>

    <%= text_area_tag :description, @movie.description, { rows: 3 } %>
  </div>
...
```
{: mark_lines="6 8 12 14"}

Spend a few minutes now manually testing your app and chasing down any error messages caused by the controller refactoring. This comes down to changing the `list_of_movies` to `movies` (plural) and any variable that includes `the_movie` or `a_movie` (see the `index.html.erb` loop!) to just be `movie`. 

In AD1, we named every variable differently to be very explicit about the connections between our pages and actions. But, now that we understand the conventions, which is to just name the variable after the resource (`movie` or `movies`), we don't have to think about making up different names.

That was a lot of refactoring. Let's make a **/git** commit. 

## 00:30:00

Let's do some more work on our forms. We can demonstrate something with some dummy code, maybe in the `index` page:

```html
<!-- app/views/movies/index.html.erb -->

<h1>
  List of all movies
</h1>

<form>
  <input name="zebra">
  <button>Submit</button>
</form>
...
```
{: mark_lines="7-10"}

Now, if we refresh **/movies**, we should see our blank form with just one, un-labelled input box. If we type "hi" into the form and click "Submit", then go to our server log in the terminal (the terminal that we ran `bin/server` in that's connected to the live app), we should be able to find the `params` hash and see:

```bash
Parameters: {"zebra"=>"hi"}
```

What happens if I change my form slightly to add some square brackets next to `"zebra"`:

```html
<!-- app/views/movies/index.html.erb -->

<h1>
  List of all movies
</h1>

<form>
  <input name="zebra[]">
  <button>Submit</button>
</form>
...
```
{: mark_lines="8"}

Again, refresh **/movies** and submit something to the blank form again. How do the `params` look? You should see something like:

```bash
Parameters: {"zebra"=>["hi"]}
```

The key is still `"zebra"`, but now it put the value into an array. Interesting. Let me put in another one of these inputs:

```html
<!-- app/views/movies/index.html.erb -->

<h1>
  List of all movies
</h1>

<form>
  <input name="zebra[]">
  <input name="zebra[]">
  <button>Submit</button>
</form>
...
```
{: mark_lines="9"}

And on the form put something different in both input boxes then submit, and view the `params` in the server log. You should see something like:

```bash
Parameters: {"zebra"=>["hi", "there"]}
```

Rails put the two values for the two different inputs on the same `name`d input fields into an array. So now, we could do `params.fetch("zebra")` and that would return an array that we could do `.each` on to loop through. In other words, we have created nested structures in our `params`.

This gives you a lot of different power and flexibility. A classic use case here is creating check boxes. For instance with code like this:

```html
...
<form>
  <label>Red</label>
  <input type="checkbox" name="zebra[]" value="red">
  
  <label>Blue</label>
  <input type="checkbox" name="zebra[]" value="blue">

  <button>Submit</button>
</form>
...
```
{: mark_lines="9"}


What else? Well, other than the classic many to many checkbox situation, I go back to type text and I want to do something else I'm going to do, we'll just leave those values in there to save me some typing. But they're type text [00:36:00] now. Watch if I do giraffe, what if I put a value in there? Now what's going to happen?

So I now have this form. Zebra, zebra. I put the square brackets, but now I put something else inside the square brackets and I type in some stuff. 1, 2, 3, 4, 5, 6. Imagine I just typed in some values. What do you think the peram hash is going to look like? Now, take [00:36:30] a guess. Is it going to be an array again with values, giraffe and elephant in it?

If so, what? It's going to happen to red one, two, and three blue. Where is this food going to go? Is it going to be nested arrays? Two levels deep. So the key will be the top level key will be zebra and the peram slash then the value will be an array. Is it an array of arrays? Let's, let's see. [00:37:00] So as, as always, top level key in the prams hash, we got zebra, but now the value is a hash, so nested hash.

And the first key for this input is giraffe, and it's got a value of whatever I typed. The second key is elephant, and it's got a value of what I write typed. So this is a very handy way of bundling [00:37:30] together related inputs in a form into a subhash. So they're not all in an array. They're labeled in a subhash, which is really handy as well.

And this is actually the technique that we use more often. The first technique I showed you is useful mainly for check boxes, which are not that common, but this is super common. In fact, this is the technique we use for 95% of our forms is. All of the inputs that are [00:38:00] related to one model type object, a movie or a director, anything related to one database record.

We want to bundle them all together into one subha and store them in a key movie or director or event or whatever. We want that to be a top level key in the pram slash and then the subhash should ha have all of the attributes for that top level key in that way if we want to. It's very easy to have attributes for multiple different objects [00:38:30] in the same form if we need to.

Alright, so let's re, given this principle, I want to reorganize our form a little bit. So I'm going to go back here. I'm going to bring this back here. And given this, I want to think about our new form and what I want to do. Is put all of these [00:39:00] into a, in the prams hash. I want them all to be in a subha under a key called movie.

So what I'm saying here is I want the prams hash to end up looking like movie. And then I want title, some whatever I type. And then description.

This is, this is my goal. I want the prams hash [00:39:30] to look like this. So I need to name my inputs in, in a particular way. Okay, cool, cool, cool. That means, so this is, what is the name of the inputs? So I'm, I had 'em a very concise form here. Now I have to make it like less concise, but that's cool. I'm going to do, I'm going to use strings here, cuz now you have to use those square brackets.

And I'm not sure if I can use square brackets and symbols, but, If I want the top level key, that means they have [00:40:00] to say movie and then title and movie, and then the description, and we'll worry about these labels in later on. We'll get all that to match up the labels and the IDs and the forests. We'll get that all tidied up later.

Let's just get this to work first. So I'm going to go check out my form, view source, [00:40:30] see if this did what I wanted. So the input now has a name movie, Squareback title movie, Squareback description. So I think this is going to do what I want when I submit this form, say sum title, some description. Of course, my controller actions are now going to have to be updated, so I'm getting a missing parameter error.

But in the server log, [00:41:00] I got what I wanted in terms of the structure. I have a top level key movie and all of the movie related attributes, which could be like 30 of them, are nicely bundled into the subhash. Excellent. Now let's update our controller code to take advantage of this in the create action. I have to, well, it's going to be a little bit more verbose now because I'm going to do prams [00:41:30] fetch first.

I'm going to fetch the key of movie. Then I'm going to fetch, oops, I did thought I had multiple controllers here. Multiple cursors rather. So first I'm going to fetch the Kiev movie, and then I'm going to fetch. The next key, right? So you have to go two levels in. Okay, now this should work. And there we go. We're back to [00:42:00] having it work Like before now, you might be like, oh, wow, you just made extra work for yourself.

But trust me, we're, we're getting, we're getting there slowly, step by step. Okay? Here's another thing to realize. Let me make a good commit. So far, so good.

In my Rails console, I want to look at a nice [00:42:30] technique. Let me just make this commit before I mess anything up. New movie form. Now, Nasts movie attributes subha within prams.

Here is what we usually do when we want to create a new movie. Movie can movie our new M title equals high M description equals bye m save. [00:43:00] Right. Great. There's a slightly more concise way of doing this sort of suppose you happen to have a hash laying around that happens to have keys in it

that exactly match your column names. Exactly right. So the hash has exactly the [00:43:30] same column names as the movie table. Well, I can say movie.new and I can give the new method, the hash as an argument. and the new method will iterate through the key value pairs and it will assign this value to the column that has this name and this value to the column that has this name.

So that just like that X is initialized with those values. [00:44:00] Mm-hmm. , maybe you can see where I'm going with this now. Right?

Uh, look at that hash and then look at the hash that came into our server log. I already cleared it, but perms fetch. So like the movie attributes are in a subhash [00:44:30] called movie, which means I can just pass them as an argument. to.new and imagine in your head if there was 30 of those. So there, there was in, in APTA one code, there's 30 lines of code of of assignments here happening every single time, right?

We don't have to do that. This is called mass assignment. the.new method is capable of receiving a hash containing all of the attribute value [00:45:00] pairs and it'll mass assign them to all of the columns for us.

Is this going to work? Unfortunately, it's not going to work. It's not that easy. My friends, if I say Alice, Bob and I create, I get this forbidden attributes error. What is this? This is Rails doing more fancy pants security on our behalf without us even realizing it. [00:45:30] This is protecting us against another type of attack, not a CSR attack, but a different type of attack.

Where if people know Rails does this and people know that Rails developers are blindly passing whatever parameters are in the form there, there's an attack where people manipulate the form, which already has that C S R F authenticity token in it. So they're going to, in Chrome, they're going to inspect the form that already has the [00:46:00] authenticity token.

Then they manipulate what inputs are in there to put inputs that are not supposed to be in there, and they'll modify columns that are not supposed to be modified like admin, and they'll switch it to true. So what you have to do is you have to say which attributes are allowed to be mass assigned like this.

You have to whitelist which columns you, you allow to be assigned in this manner. Because there are sneaky users. And that funny, it [00:46:30] was funny because the, the security researcher who discovered this hack, and we don't know how many times the hack was abused before this, but the person who publicized this hack, the way that he got attention, he, he's, he claims he reported it, but it, he didn't get enough attention from the Rails team.

So he hacked GitHub, made himself uh, an admin on the Rails repository, and then he made a commit to Rails itself. And then that got David's attention and then they made this change. So, [00:47:00] alright, we, what we need to do here is we say prams dot require instead of fetch and prams because prams isn't actually just a plain hash, peram is a very complicated and powerful other class.

It has a method called Require, which returns an object of another class, which has a method called Permit. Then you list, which, Attributes you will allow through for mass [00:47:30] assignment. So now if I try this, I noticed that I didn't allow description through, I only allowed title through. So description ran into that wall, title, got through, description, didn't, and now we get this red error in the server log.

That's really easy to spot. This is a super common thing. Whenever you add a new column, whenever I add a new column, I always forget that. I also have to whitelist it in my, what's called [00:48:00] strong parameters list. And then I look at my server log and I see this error message. I'm like, have strong parameters.

I forgot about the GitHub hack. And then I have to go in here and I have to do this. And then it'll work,

create, and now it works. Yay. Okay, so this is awesome. Oh my gosh, this my friends is the biggest code savings of all. Think about. How many columns we usually have in all of our, in our tables, usually not just two. And [00:48:30] then for, we have one of these, we have like huge chunks of code for all of these assignments in all of our controllers.

All of that goes away now with this mass assignment technique. So amazing. We can do the same thing. Uh, for update. I'm going to allow you to do the update action yourself, but let me make this even more concise. Let me make this a, let me get, commit this first. [00:49:00] Now, one last thing

for this video. This is looking great. Love this. This is looking awesome, this form. This is the, this is the only thing that, and we have to make the IDs match up, and that's the thing that we have to do. Like I feel like I went a little bit backwards here. It was [00:49:30] nice, and then I made it less nice and it's going to get even less nice once I fix these label tags to match up.

And then I have to add the ID back over here to both of these things, so I may, there's a better way here if we want this nested behavior. Essentially what's happening is when you're making forms, generally this is the right technique. When you're making a sign-in form or when you're making a search form, this is what you have to [00:50:00] do form with url label tag, text field tag.

These are the helper methods that you use when you're making a form for the specific purpose of creating a record in your database table using an active record instance or updating a record. That's a very specific job and there's a, a more specific method for that, and that will save us even more code.

It's actually the same [00:50:30] method. It's just a different way of using the method. It used to be a different method, but then they unified the two methods in rail six. So we're going to use that. And as you know, most of what our applications do is crud. So actually 99% of our forms, the purpose of them is to just create or update one record.

So it's really handy that there's this other way of using it. Here's how it works. Instead of saying form with url, you say form with model. [00:51:00] And the argument for this now should be the object that itself, that you're trying to build a form for. Now, what the heck is this object? Oh, this was, remember, think.

Remember how we created a new movie Object. in the new action. Now we did that only because we were going to draw this errors collection and if we did this and we didn't have any object there on the very first time somebody visited slash new before they even filled anything out, so there was no [00:51:30] errors, we would get a undefined method errors for nil.

So we're like, okay, we're just going to create a blank object just to satisfy that so that when we re-render the page later from a different action, we can use the reuse the same template. So this object will have an errors collection in this case, and it allowed us to be lazy and reuse the same template from two different actions instead of creating two different templates that have 99% of the same code.

But hey, it's going to come in handy for us [00:52:00] that we have a movie object, cuz now I'm going to say, give me a form. And the purpose of this form is to create this new record in the movies table. Okay, with only that change, I just switched it from form with URL to form with model. What's going to happen to the action attribute?

Let's take a look here. So if I go to add a new movie, look at the source code of this form,[00:52:30] 

it did the same exact thing. Let me prove to you that it did the same exact thing. I'm going to put an end in here and switch it back to URL and movies path. So now there's two. And let's take a look at the source code of this and prove that actually. So here's the form with url [00:53:00] and here's the new form with model.

And the opening tags are exactly the same with a slightly different authenticity token of course. , but they do the same exact thing. So this is another one of these so-called magical instances where Rails knows or assumes that if you're trying to create a record and this record is [00:53:30] class is, so Rails calls a dot class on this and Rails understands, okay, this is a class instance of class movie.

And if you are going to be, if you're following all the conventions, then that means you probably have a route called movies and that's probably alias as movies. So there must be a movie's URL helper Method, and Rails itself is going to call that helper method in order to generate the URL for the action of the form.[00:54:00] 

I know Madness, right? If you don't believe me, I'm going to comment this out. And this out. So that means there's no movies help Path Route Helper anymore, which means we're going to get undefined local VRBO method movies, path Online Seven. It's like, oh, actually wait. I did explicitly call Movies Path there.

Hang on a second, [00:54:30] go back here, I'll comment these out. So now it's a form with Online 12. Look at that. Now. On line 12 it says, undefined Method Movies, path Online. 12. We didn't call Movies Path. Who called Movies Path. The Form with Method saw that this is an instance of class movie and it called Movies Path, assuming that you were going to re name your Routes Restfully.

But, so if you don't have Restful Routes, then you can't [00:55:00] use this form with Model Trick. So this is why Restful Routes and generally conventions and Rails. , the dividends just compound and compound and compound and compound and compound on each other. Alright, so let's go back and I want my restful routes again.

So put that back, put that back. Now that this method exists, now I can use this method. I've got this going and I can get rid of this. [00:55:30] Awesome. I can get rid of this. Now that we get that idea. Alright, cool. So I've exactly replicated the previous behavior with this form with, but the benefit of using form with model is there's now a block variable.

Provided this method now produces a block variable known as a form builder object. And you can call it anything you want to, the convention is to call it [00:56:00] form, but again, it's, it's just a block variable. So you can call it whatever. Now the Form Object has methods called label. Basically it's the same thing, but take off the tag and it has labels called that form label, form text field.

And I'm going to switch this back to just movie. And I'm going to take [00:56:30] out this, or sorry, title rather. So we'll put it back to how it was before I took out that, uh, at movie title, the second argument. And let's just take a look at what happens to the source code here. For this first section, we're going to refresh and it created a label.

It correctly created the content for the label by capitalizing what we put in as the argument. It created a four attribute of [00:57:00] movie underscore title, which is interesting, and it matched that up with the input correctly, which is great input type text and look at the name of this, it correctly did exactly what we wanted, which was create that nested structure cuz it knows that we're trying to create a form for a model.

Excellent. Well what about this though, like previously we had at movie title, this was the, this was to be [00:57:30] used as the value attribute in case of form validation failures and we lost that, right? Let's, let's check out what happens here. If I say description. So, okay, so if I leave everything blank validations fail, put in this.

Wait a second. It works. It still works. Just like before, if I put this in, do that, look at the source code. We still have, [00:58:00] uh, this is the wrong source code.

Hmm, I see It's giving me the source code of the index page because this is after a validation failure. So it's rendering the new template, but it's on the route. Looks like slash movies cuz we did a post to slash movie. [00:58:30] So it's doing a get of the source code of slash movies. But I need this. But in any case, you can see here, if I inspect element, that'll be a better way of doing it.

It did a value attribute and it populated it with what it, what it had before, so it's correctly pre-populating. This box Rails does it automatically when we use the form with helper for a model, give it a form block [00:59:00] variable. These methods automatically do the right thing of using whatever attributes this object already has.

So if I previously, let's just oppose this object, if I do at movie dot title equals preexisting value, so I'm assigning a value to it and then I rendered this form when the title method here [00:59:30] is called with Tex Field. It's going to be smart enough to prepopulate. Whatever value's already on that object. So it makes edit forms super easy.

It makes this re rendering super easy after validation. Failure methods, me messages. Okay. Whew. So now this form becomes really elegant. Form dot description. Oops. And this just [01:00:00] becomes description. We can get rid of this, it takes care of automatically. We can put in any other customizations that we want and we can even do form dot button, and we can even get rid of this copy.

And because this is a smart, smart method and it knows that this is a new instance that we created over here, it's a, it still hasn't been persisted to the database. It doesn't have an id. It knows that, oh, oh, I [01:00:30] shouldn't use the dot tag. I need to get rid of dot underscore tag on these two.

It knows to put Create movie on here because that's a brand new record. If I had already saved that object, let's just for kicks, do movie, do new save. Although that won't work because it needs some attributes. So I'm going to say title dot, hi prescription [01:01:00] as you can mass signing these and saving it.

Oops. And then I'm going to go to add a new movie,

undefined. Oops. Okay, so let me, I did that too much in one line. Do this@movie.save and then let's see what it says. Okay, so it's going to prefill [01:01:30] and notice. That because this object already exists. The button copy changed to update. This is a smart helper. It's such a smart helper because I'm calling it on this object.

This object is coming from here. This is an argument. It knows that this has already been persisted to the database. So it writes this copy for us. Of course we can change it and say howdy and put whatever copy we want to [01:02:00] if necessary, we can override it. As always, default behavior that is override is Rails.

His philosophy in life, we're going to save you a bunch of time with defaults, but then you can then override it. That's the whole resin detra for Rails. All right, so I'm going to go back here, get this out, get this out, and we now have an amazingly concise new and create [01:02:30] action. And my challenge to you. Is use this technique to update the edit form and update action and get it as concise as you possibly can and ask lots of questions as you're doing so, and then generate a new model.

So head over to a terminal, generate a [01:03:00] new model, not a, not a draft resource, only a model Rails, generate model. Pick anything you want. Director name string is the default date of birth. Okay? Whatever you want to pick. Pick a model. Some columns starting from just the model and the database table. Build up the entire resource, all the routes controller, and then.[01:03:30] 

The seven golden actions that we did here, but do it in this modern way and get practice at doing it in this modern way for all seven of these actions. One last thing I want to tell you to get you on your way for doing that is for these seven routes, there's a shortcut. Because these seven routes are the standard restful routes, this name naming, convention id, the these names, [01:04:00] this is completely standard for every restful resource.

Therefore, if I, let me pull up my rail slash info again.

So if I go here, let's search for movies again. So we got all my movie stuff, right? If I comment these out now I've got no routes,

right? So now I've got no movies, routes.[01:04:30] 

Resource movies. That's it. One line gives you all seven of these routes. Go back here, refresh, search for movies. You've got it all back. So when you're starting on your next resource, if it's director, whatever, whatever table, whatever [01:05:00] model you generate, do resources, directors,

go check it out. You've got all seven ready to go. Then add your director's controller and then implement your seven routes and, and then your four view templates, and try to use everything you learned for every link. Write it using a link to helper method for every [01:05:30] URL in the controller and in the view time every, for every url, write it using a route helper every A element.

Write it using a link to helper every form. Use the form with helper and practice that at least once. All right. See you on Piazza.

