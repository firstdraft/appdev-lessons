# AD2 Helper Methods Pt 3

**BENP: Document based on descript transcription of AD2 WS 2023 Day 3 Recording.**

## Getting Started 00:00:00 to 00:09:00

Please start the Gitpod workspace for [Helper Methods (Part 3)](https://github.com/appdev-projects/helper-methods-3). As usual, run `bin/setup` and get the server started as well. 

Have a look through the code. It is a solution Parts 1 and 2 of the Helper Methods project, with all of our professional refactoring. Refresh anything that looks unfamiliar by glancing back to your notes.

As long as your looking through notes, now might also be a great time to have a look at Ruby Weekly from this week. Did you see anything interesting? Could you begin to make some sense of some of the news with all your AD1 and beginning AD2 knowledge? Hopefully yes!

Now let's keep going with our helper methods and learn about four more Rails shortcuts.

## Bootstrap CSS Navbar 00:09:00 to 00:15:30

I want to start getting in the habit of making our apps look better. That means pulling in Bootstrap CSS and Font Awesome. 

Rather than us downloading and then uploading the files into our workspace, the quickest way of getting those is using some design resources from AD1:

```html
<!-- Expand the number of characters we can use in the document beyond basic ASCII 🎉 -->
<meta charset="utf-8">

<!-- Make it responsive -->
<meta name="viewport" content="width=device-width, initial-scale=1">

<!-- Connect Bootstrap CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">

<!-- Connect Bootstrap JavaScript and its dependencies -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.min.js" integrity="sha384-QJHtvGhmr9XOIpI6YVutG+2QOK9T+ZnN4kzFN1RtK3zEFEIsxhlmWl5/YESvpZ13" crossorigin="anonymous"></script>

<!-- Connect Font Awesome -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/js/all.min.js"></script>
```

Specifically, we want the CDN links in your HTML application layout view template. And if it's not already there, we also want the UTF-8 character set and the responsive viewport for different screen sizes.

Take those HTML elements and copy-paste into `app/views/layouts/application.html.erb`, our wrapper file for all of the pages we are `yield`ing into the `<body>` of:

```html
<!-- app/views/layouts/application.html.erb -->

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>VanillaRails</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>

    <!-- Connect Bootstrap CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">

    <!-- Connect Bootstrap JavaScript and its dependencies -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.min.js" integrity="sha384-QJHtvGhmr9XOIpI6YVutG+2QOK9T+ZnN4kzFN1RtK3zEFEIsxhlmWl5/YESvpZ13" crossorigin="anonymous"></script>

    <!-- Connect Font Awesome -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/js/all.min.js"></script>
  </head>
  ...
```
{: mark_lines="6 8 15-16 18-19 21-22"}

Note that we put the UTF-8 character set at the _top_ of the `<head>` because we want those characters available throughout our application, including in the `<title>` of the page.

<aside markdown="1">
When copy-pasting code into HTML documents, you can auto-format the indentation so that the elements are properly nested using <kbd>Cmd</kbd>(Mac) or <kbd>Cntrl</kbd>(PC) + <kbd>shift</kbd> + <kbd>P</kbd> to open the command pallet on Gitpod's VS Code editor. With the `>` command pallet prompt open, you can search "Format" and find the command. (You can search for any command in this prompt.) You will also see a direct keyboard shortcut to that formatting command that might be useful to you. Become a keyboard ninja!
</aside> 

Now refresh a page in your app (**/**, the root should be set to the movies `index` page) and see the change. If the fonts look a little better, you know you you connected the assets correctly.

Let's start putting it to use. Visit the [Bootstrap docs](https://getbootstrap.com/docs/5.1/getting-started/introduction/) (we are using v5.1), specifically the docs for implementing a [navbar](https://getbootstrap.com/docs/5.1/components/navbar/).

Near the top of the page you can copy the "kitchen sink" example, with everything in it, and click the "Copy" button:

![](/assets/navbar-bootstrap-gif.gif)

There's a lot here, but we just want to take it all and then remove what we don't need:

```html
<!-- app/views/layouts/application.html.erb -->

...
    <!-- Connect Font Awesome -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/js/all.min.js"></script>
  </head>

  <body>

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Link</a>
            </li>
            <li class="nav-item dropdown">
              <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                Dropdown
              </a>
              <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                <li><a class="dropdown-item" href="#">Action</a></li>
                <li><a class="dropdown-item" href="#">Another action</a></li>
                <li><hr class="dropdown-divider"></li>
                <li><a class="dropdown-item" href="#">Something else here</a></li>
              </ul>
            </li>
            <li class="nav-item">
              <a class="nav-link disabled">Disabled</a>
            </li>
          </ul>
          <form class="d-flex">
            <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
            <button class="btn btn-outline-success" type="submit">Search</button>
          </form>
        </div>
      </div>
    </nav>
    
    <div style="color: green;">
      <%= notice %>
    </div>

    <div style="color: red;">
      <%= alert %>
    </div>
    
    <%= yield %>
  </body>
</html>
```
{: mark_lines="10"}

This is a good example of something that would go in the application layout file in the `<body>` above our `<%= yield %>` statement, because we want the navar to appear on every page.

After this copy-paste, check on your live app that the navbar showed up.

Now would be a good time for **/git** commit.

Let's start modifying the navbar to suit our purposes, starting with the homepage link:

```html
...
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        
        <!-- <a class="navbar-brand" href="#">Navbar</a> -->
        <a class="navbar-brand" href="/">Helper Methods 3</a>
        
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
       ...
```
{: mark_lines="5-6"}

Okay, we have a link to our **/** root page now. But actually, we should use our new helper methods! Remember, we have `link_to` now, which will draw `<a>` elements for us:

```html
...
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        
        <!-- <a class="navbar-brand" href="#">Navbar</a> -->
        <a class="navbar-brand" href="/">Helper Methods 3</a>
        <%= link_to "Helper Methods 3", root_path, class: "navbar-brand" %>
        
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
...
```
{: mark_lines="5-7"}

We added another argument to `link_to` besides the copy (first position), and the path (second position). We can also pass additional arguments as a hash on the end of the method, noting that we dropped the curly braces since this hash is the last argument to the method. And in that hash, we are just noting that the `class` of the link should be `"navbar-brand"`, as it was in the original `<a>` element.

Confirm that the new `link_to` method works exactly as expected (and looks good with bootstrap). Then feel free to delete the old HTML element.

What next? Just below the `"navbar-brand"` root link, there is code for the "hamburger" menu for smaller screens, so we don't want to modify that at all. But, a bit farther down is the actual nav links:

```html
...
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Link</a>
          </li>
...
```
{: mark_lines="3-6"}

We have a list beginning with `<ul>`, then each `<li>` with a `class="nav-item"` followed by an `<a>` link of `class="nav-link"`. Well, we can replace those with `link_to`s and put in the paths we want links to:

```html
...
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <!-- <a class="nav-link active" aria-current="page" href="#">Home</a> -->
            <%= link_to "Movies", movies_path, class: "nav-link" %>
          </li>
          <!-- <li class="nav-item">
            <a class="nav-link" href="#">Link</a>
          </li> -->
...
```
{: mark_lines="6-7"}

We could add more links to things like **/movies/new**, but we'll just keep it simple for now. 

Lastly, let's delete the the `<li>` defining the dropdown menu, so that our final navbar code in the `<body>` of `app/views/layouts/application.html.erb` looks like:

```html
...
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
          <%= link_to "Helper Methods 3", root_path, class: "navbar-brand" %>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <%= link_to "Movies", movies_path, class: "nav-link" %>
              </li>
            </ul>
            <form class="d-flex">
              <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
              <button class="btn btn-outline-success" type="submit">Search</button>
            </form>
          </div>
        </div>
      </nav>
...
```

Now's a good time for another **/git** commit. 

**BENP: CLI `git` 00:15:30 to 00:19:30 using chapters. Maybe better to wait to show in a separate subsequent lesson**

## Bootstrap Alerts 00:19:30 to 00:23:30

Let's add some more bootstrap. Right now, when we add a movie at **/movies/new** there is a green sentence that comes up, which is the `:notice` message we set in our `create` action in the controller being rendered in the application layout:

```html
<!-- app/views/layouts/application.html.erb -->

...
  <body>

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      ...
    </nav>
    
    <div style="color: green;">
      <%= notice %>
    </div>

    <div style="color: red;">
      <%= alert %>
    </div>
    
    <%= yield %>
  </body>
</html>
```
{: mark_lines="10-12 14-16"}

We can improve that simple green text with [bootstrap alerts](https://getbootstrap.com/docs/5.1/components/alerts/). Again, we can just copy and paste the examples we want (perhaps the green "success" and red "danger" boxes):

```html
<!-- app/views/layouts/application.html.erb -->

...
  <body>

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      ...
    </nav>
    
    <div class="alert alert-success" role="alert">
      <%= notice %>
    </div>

    <div class="alert alert-danger" role="alert">
      <%= alert %>
    </div>
    
    <%= yield %>
  </body>
</html>
```
{: mark_lines="10 14"}

And now try to refresh the **/movies** page. 

We have an issue. If there is no notice or alert, a red and a green box still appear. So what should we do? How about some `if` control flow? There's a nice method for this, which will check if the message is undefined or `nil` and return true or false: `.present?`

```html
<!-- app/views/layouts/application.html.erb -->

...
  <body>

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      ...
    </nav>
    
    <% if notice.present? %>
      <div class="alert alert-success" role="alert">
        <%= notice %>
      </div>
    <% end %>

    <% if alert.present? %>
      <div class="alert alert-danger" role="alert">
        <%= alert %>
      </div>
    <% end %>

    <%= yield %>
  </body>
</html>
```
{: mark_lines="10 14 16 20"}

Test out adding movies and also filling out forms correctly and incorrectly. Do the messages appear and disappear as expected? Good! Time for another commit.

## Bootstrap Containers for Padding 00:23:30 to 00:27:00

Okay, what else? Wouldn't it be nice if everything in the app wasn't pushed all the way to the edges? We would like some padding around the content. This is the perfect use case for [bootstrap `container` class](https://getbootstrap.com/docs/5.2/layout/containers/). 

And since we want padding on every page, why not put it in the application layout again!

```html
<!-- app/views/layouts/application.html.erb -->

...
  <body>

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      ...
    </nav>
    
    <div class="container">
      <% if notice.present? %>
        <div class="alert alert-success" role="alert">
          <%= notice %>
        </div>
      <% end %>

      <% if alert.present? %>
        <div class="alert alert-danger" role="alert">
          <%= alert %>
        </div>
      <% end %>

      <%= yield %>
    </div>
  </body>
</html>
```
{: mark_lines="10 "}

<aside markdown="1">
When I'm actually writing code, to speed things up, I use the "Emmet" abbreviation to generate tags for a given class in HTML. For instance, you can just type `div.container` in the code editor, and you should see an option come up to press <kbd>tab</kbd>, which will generate `<div class="container"></div>`.
</aside>

We put the container around our alerts and our `yield` (where all the rest of each page goes), but under the navbar, so the navbar will still stretch across the top of the screen.

If we test this, it looks pretty good. But there's not a lot of space between flash messages and the navbar. We can shift everything down a little by adding to the `class` attribute in the container and making it: `class="container mt-4"`. MT for margin top and "4" for the spacing. 

Looks good? Great! Commit again.

I want to note: there's an open [pull request for this project](https://github.com/appdev-projects/helper-methods-3/pull/1/files) on Github, that contains all of the changes we will be incrementally making in this lesson. That's a nice resource to occassionally glance at as we go throught the project to see a summary of changes on each file.

**BENP 00:27:00 to 00:33:30 is Q/A**

## Reviewing Form Builder 00:33:30 to 00:51:30 

Sometimes we have code that we want to reuse, but not in every single template, but in _some_ templates. And it would be really nice to avoid duplication. Also, look how long our application layout has become with all of the bootstrap additions we made. Wouldn't it be great if we could put some of that code in separate files to make it all more readable?

We're headed towards partial view templates. Let's get our first feel for things with our `new.html.erb` and `edit.html.erb` forms. Open those files. What to do you notice? Where are the differences?

It turns out, because we switched to `form_with` helpers, the two forms are identical besides the copy in the `<h1>` tag at the top of each page! ("New" vs. "Edit".)

`form_with` does a lot for us. Let's review it before we go on to partial view templates. 

It knows whether the object is persisted in the database or not, and how to fill in placeholder values for partially filled out forms or objects that already have column values. So everything is basically the same! 

Now, what if we add a new column? Let's see how we would change our code to allow that. How about an image URL for the movie?

Start by running the terminal command:

```bash
rails g migration AddImageUrlToMovies image_url:string
```

Then migrate the change to the database:

```bash
rails db:migrate
```

And you can check the `db/schema.rb` file to see that the table `movies` now has this additional column.

What if I want to add it to my form so people can actually use that column? 

We can do that with the `form_with` construction easily:

```html
<!-- app/views/movies/new.html.erb -->

<h1>New movie</h1>

<% @movie.errors.full_messages.each do |message| %>
  <p style="color: red;"><%= message %></p>
<% end %>

<%= form_with model: @movie do |form| %>
  <div>
    <%= form.label :title %>
    <%= form.text_field :title %>
  </div>

  <div>
    <%= form.label :description %>
    <%= form.text_area :description %>
  </div>

  <div>
    <%= form.label :image_url %>
    <%= form.text_field :image_url %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```
{: mark_lines="20-23"}

But what if I try that out in the **/movies/new** page? It won't actually work yet. Why?

Because we also need to remember to whitelist this new column to allow for mass assignment to take place!

```ruby
# app/controllers/movies_controller.rb

  ...
  def create
    movie_params = params.require(:movie).permit(:title, :description, :image_url)
    
    @movie = Movie.new(movie_params)
  
  ...
  
  def update
    @movie = Movie.find(params.fetch(:id))

    movie_params = params.require(:movie).permit(:title, :description, :image_url)

    if @movie.update(movie_params)
    ...
```
{: mark_lines="5 14"}

And we whitelisted in both the `create` and `update` action so we can save new recrods and edit them later.

Okay, that aside was just to remind us how `form_with model` works with mass assignment. But back to the point. We have these two forms `edit` and `new` and we would like to just reuse the code in them and not need to make changes in two places ever.

First of all, where we are creating that variable `movie_params` twice in our controller, we can dry that up. We can do that by defining a new method in the bottom of the controller:

```ruby
# app/controllers/movies_controller.rb

...

  private

  def movie_params
    params.require(:movie).permit(:title, :description, :image_url)
  end
end
```
{: mark_lines="5 7-9"}

We put a new keyword `private` and below this, we defined our helper method. We put any methods that are just helpers for the actions below `private` in the controller.

Then passing that _method_ to the `create` and `update` actions!

```ruby
# app/controllers/movies_controller.rb

  ...
  def create
    # movie_params = params.require(:movie).permit(:title, :description, :image_url)
    
    @movie = Movie.new(movie_params)
  
  ...
  
  def update
    @movie = Movie.find(params.fetch(:id))

    # movie_params = params.require(:movie).permit(:title, :description, :image_url)

    if @movie.update(movie_params)
    ...
```
{: mark_lines="5 14"}

When these actions are triggered, Rails will reach that `movie_params` argument, which we didn't define in the action, and instead of throwing an error, it will search the controller for a method that matches that argument and call that method. We could write `self.movie_params`, as the longhand for what this step is doing!

So now all of our whitelisted columns are in one place and we don't need to repeat our code when we make changes to the database.

## Partial View Templates 00:51:30

Now that we can add to the forms, how can we get the forms in one place so we can reuse them for different purposes (`create` and `update`) on different pages? The answer is partial view templates.

Partial view templates (or just "partials", for short) are an extremely powerful tool to help us modularize and organize our view templates. Especially once we start adding in styling with Bootstrap, etc, our view files will grow to be hundreds or thousands of lines long, so it becomes increasingly helpful to break them up into partials.

Here is the [official article in the Rails API reference](https://edgeapi.rubyonrails.org/classes/ActionView/PartialRenderer.html) describing all the ways you can use partials. There are lots of powerful options available, but for now we're going to focus on the most frequently used ones.

Let's get our first feel for partials, then see about our `new.html.erb` and `edit.html.erb` forms. 

### Static HTML Partials 00:52:00 to 01:00:00

Create a partial view template in the same way that you create a regular view template, except that the first letter in the file name must be an underscore. This is how we (and Rails) distinguish partial view templates from full view templates.

For example, create a folder (`app/views/zebra/`) and file within it called `_giraffe.html.erb`. Within the file, write the following:

```html
<!-- app/views/zebra/_giraffe.html.erb -->

<h1>Hello from the giraffe partial!</h1>
```

Then, in any of your other view templates, e.g. `movies/index.html.erb`, add:

```html
<!-- app/views/movies/index.html.erb -->

<h1>
  List of all movies
</h1>

<%= render partial: "zebra/giraffe" %>
...
```
{: mark_lines="7"}

Notice that we don't include the underscore when referencing the `partial:` in the `render` method, even though the underscore _must_ be present in the actual filename.

You can render the partial as many times as you want:

```html
<!-- app/views/movies/index.html.erb -->

<h1>
  List of all movies
</h1>

<%= render partial: "zebra/giraffe" %>

<hr>

<%= render partial: "zebra/giraffe" %>
...
```
{: mark_lines="11"}

A more realistic example of putting some static HTML into a partial is extracting the long Bootstrap navbar into `app/views/shared/_navbar.html.erb` and then `render`ing it from within the application layout. This will make our very long view templates much easier to navigate and make sense of. Try doing that now!

First create the folder `shared` in `app/views/`, then create the `_navbar.html.erb` file within that. Now, cut and paste the entire `<nav></nav>` element from the `app/views/layouts/application.html.erb` file to the new `_navbar.html.erb` file:

```html
<!-- app/views/shared/_navbar.html.erb -->

<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <%= link_to "Helper Methods 3", root_path, class: "navbar-brand" %>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <%= link_to "Movies", movies_path, class: "nav-link" %>
        </li>
      </ul>
      <form class="d-flex">
        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success" type="submit">Search</button>
      </form>
    </div>
  </div>
</nav>
```

And back in the layout:

```html
<!-- app/views/layouts/application.html.erb -->

...
  <body>

    <%= render partial: "shared/navbar" %>
    
    <div class="container">
      <% if notice.present? %>
        <div class="alert alert-success" role="alert">
          <%= notice %>
        </div>
      <% end %>

      <% if alert.present? %>
        <div class="alert alert-danger" role="alert">
          <%= alert %>
        </div>
      <% end %>

      <%= yield %>
    </div>
  </body>
</html>
```
{: mark_lines="6"}

Much more organized! And why not do the same with the alert messages? Put the whole content of the `if ...present?` statements into a file `app/views/shared/_flash_messages.html.erb` and render that in the layout file. And while we're at it: the bootstrap and font awesome stuff can also go in another static view template called `app/views/shared/_cdn_assets.html.erb`.

Now our application layout file should look much, much cleaner:

```html
<!-- app/views/layouts/application.html.erb -->

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>VanillaRails</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>

    <%= render partial: "shared/cdn_assets" %>
  <body>

    <%= render partial: "shared/navbar" %>

    <div class="container mt-4">

      <%= render partial: "shared/flash_messages" %>

      <%= yield %>

    </div>
  </body>
</html>
```
{: mark_lines="15 18 21"}

Partials make our code more modular, easier to read, and they will enable us to get to AJAX in a few more lessons.

### Partials with Inputs 01:02:30 to

Partials get even more powerful when you can send data into them to be automatically used in the output of the partial. 

Create another file called `app/views/zebra/_elephant.html.erb`, and add the following code there:

```html
<h1>Hello, <%= person %>!</h1>
```

Then, in `movies/index`, try:

```html
<%= render partial: "zebra/elephant" %>
```

When you test it, it will break and complain about an undefined local variable person. To fix it, try:

```html
<%= render partial: "zebra/elephant", locals: { person: "Alice" } %>
```

Now it becomes more clear why it can be useful to render the same partial multiple times:

```html
<%= render partial: "zebra/elephant", locals: { person: "Alice" } %>

<hr>

<%= render partial: "zebra/elephant", locals: { person: "Bob" } %>
```

If we think of rendering partials as _calling methods that return HTML_, then the `:locals` option is how we pass in arguments to those methods. This allows us to create powerful, reusable HTML components.

The arguments that we pass with the option `:locals` take the form of a hash with key/value pairs. The keys correspond to the name of the variables in the the partial, and the value is whatever we want the variable to be.

We're finally at the point where we can move our form into a partial to reuse on the `new` and `edit` pages!

Make a new file in `app/views/movies/` called `_form.html.erb`, and cut-paste the content of our form there (changing all of the `@movie` instance variables to just local variables called `movie`):

```html
<!-- app/views/movies/new.html.erb -->

<% movie.errors.full_messages.each do |message| %>
  <p style="color: red;"><%= message %></p>
<% end %>

<%= form_with model: movie do |form| %>
  <div>
    <%= form.label :title %>
    <%= form.text_field :title %>
  </div>

  <div>
    <%= form.label :description %>
    <%= form.text_area :description %>
  </div>

  <div>
    <%= form.label :image_url %>
    <%= form.text_field :image_url %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```
{: mark_lines="3 7"}

<aside markdown="1">
Note that we could have still used `@movie` in this partial, because instance variables that are defined in the actions will be available in the partial, and the instance variable is the same in both actions using this form. But if the name was different in the two actions (e.g., `@the_movie` vs. `@new_movie`), then we would want to use `:locals` as we do in the example.
</aside>

And now, we can just render this partial on both of our view templates, passing the `@movie` instance variable from the `create` and `update` actions to the partial as the local variable `movie`:

```html
<!-- app/views/movies/new.html.erb -->

<h1>New movie</h1>

<%= render partial: "movies/form", locals: { movie: @movie } %>
```

```html
<!-- app/views/movies/edit.html.erb -->

<h1>Edit movie</h1>

<%= render partial: "movies/form", locals: { movie: @movie } %>
```

And in our partial, everywhere that we put `movie` will be replaced with the instance variable and everything will work like before.

Actually, we can shorten things a bit. If you are rendering a partial with some local variables, we could just drop the `partial:` and `locals:` keyword, and Rails will figure it all out:

```html
<%= render "movies/form", movie: @movie %>
```

That's optional though, and I prefer typing out the long way with `partials:` and `locals:` so you can tell exactly what's going on.

### Adding Another Column 01:17:00 to 01:19:18

Let's see the power of our new form partials by adding another column to the database and then to our forms.

The first step is generating the migration and running it:

```bash
rails g migration AddReleasedOnToMovies released_on:date
```

```bash
rails db:migrate
```

Then we need to whitelist the new column in our strong parameters to allow mass assignment:

```ruby
# app/controllers/movies_controller.rb

...
  private

  def movie_params
    params.require(:movie).permit(:title, :description, :image_url, :released_on)
  end
end
```
{: mark_lines="7"}

And finally, we can just pop that into the `movies/_form.html.erb` file (using the `.date_select` method to create a nice selection menu on the form):

```html
...
  <div>
    <%= form.label :image_url %>
    <%= form.text_field :image_url %>
  </div>

  <div>
    <%= form.label :released_on %>
    <%= form.date_select :released_on %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```
{: mark_lines="7-10"}

And it will appear (and work) in both of our new and edit forms!

## `ActiveRecord` Object Partials 01:25:00 to

So I wanna make the show page of [01:25:00] a movie look a little bit better first. So we over to the details page of a movie. Right now it looks pretty terrible and it's, I want this to be in like the header of the card. Not, uh, in this case, I think, I don't really wanna spend time building up the bootstrap stuff, like a tab.

The code in here, I'm just gonna copy it in and then we'll see what it looks like and then we'll talk about it. [01:25:30] So let's go to show a sign. Oh, here. Cool. This is the output. So it's a bootstrap card. I've got the card header, card footer, and a card body in the card body. I have a description list with the attributes and then I have these buttons, right, and delete, and I'm using font awesome icons for those fonts.

So you should be able to stop, paste the example out of the README and have it look [01:26:00] like this. Now let's read code and make sureand going here. So we got, that's the outer container that has a board around it. Then you have the, the body and the footer. When I'm, I use bootstrap card a lot and I think of it almost like as contain,

you have a head, a bonder as like children of [01:26:30] card. Just gives that kind of great background. So usually you just have some text in there, similarly with the footer, but then the body, you're gonna have a whole bunch of markup inside, including starting on line 23. All of this is what I needed to achieve, these two side by side buttons that take up the full width of their bootstrap row.

Okay, so it's bootstrap there. [01:27:00] Any

boots?

Um, the card is centered in, uh, in the middle of the screen. Mm-hmm. and, uh, is, was that done by creating empty columns on either side or is there a class that just has it centered in the middle? So actually centered it width, [01:27:30] that's a container. That's right. It's just taking up the whole diviv dot container right now.

So you're, I don't actually like that. I want to center it. Let's do that now. So here's my card. I want that to be like, let's, in half or two-thirds or one-third of the page, I'm gonna do a bootstrap row, right? Cuz we already have the diviv dot container from the so not strap row. I want to have like a, let's say call dash MD dash four.

So one third of the [01:28:00] page. I'll put that here.

And now, now this whole card is inside this cell. Now it's like, okay, it's on one third of the page, but I want it centered. So I need to either put an empty cell over here just to push it over.

You can achieve the same effect with the offset MD four class. That's like the same as [01:28:30] having an empty cell to the left.

Six by three,

and then on the phone it just pops to being full width again. So why would you create a diviv that contains the card instead of just adding another class, which would be call empty six within the card question? [01:29:00] Uh, if I have another one here, right? So let's say I'm actually using all 12 of mine or two.

Uh,

okay, so now I've got six and six, right? See this six in the middle? Where is that space coming from? Well, it's because the, each, the, the cells, think of it [01:29:30] like the table cells, right? Solid gutter between each of the cells, which usually we want or, and, and, and, sorry. It's, I think it achieves that using padding.

If I just put the class like this, just try it reasonable. I think it's right. So the [01:30:00] philosophy is, Should be sub separate from the content. So just build out your whole grid and only have grid classes on the data that are meant to be used for the structure of the page. And then within your cells, you and then bootstrap will take care of responsiveness and spacing and gutters and everything else.

Right? So usually when I'm building a page out, I [01:30:30] write the grid,

actually equip tag, then I put content into each cell

and I wanted this to be

one.[01:31:00] 

Alright, cool.

Gives you the option, you gallery mode,

template layout that we have there and then red when they clicked it, trailers the next plate. Yeah. Think there a bunch of ways to do that. Like you could, for example, perhaps out here for like [01:31:30] you. Like gallery or whatever, and then, and see what, and then I might select it,

maybe have a cookie, and then just for every page to visit after that. All right, great. Now that we have, or now that we have the show, [01:32:00] what if I want on my movies index page, what if I want cards for all the movies instead of this? Yep. Should we put all that HDL for the card, the actual show file? Yes. We have partial.

That's a great idea. Because what, like the problem in front of me right now is in another place. [01:32:30] I want those cards, right? Copy, paste it, go here, copy paste this card, go to my index and,

and I'm gonna,

so let's

can keep the loop, but then inside the loop for each movie. I [01:33:00] want a card and this I just copy pasted. So this instance variable at movie needs to change to

here, but now it works. No, I think cards doesn't look great cuz it's like too wide. But we'll get there. So I can [01:33:30] start a dim and then,

and then put each of these cards again in a call and be, let's say three this time.

Now I've got like sort of nice cards wrapping pretty good. [01:34:00] But we have this problem now that we start, as you can see now that we start going down the bootstrap road. This 37, this sort of like the representation of one movie. And those are gonna grow to be like hundreds of lines long once you get really deep with styling.

The HTML repre representation of a record from . So let's not exactly the same and we wanna render it on different.[01:34:30] 

Create a new partial call card, put all in. And again, we don'ts. So that's good. This is just like a self-contained partial now with partial a local movie. And that's what it's gonna use to populate this thing. If I [01:35:00] to my index and here render Marshall movies movie card, and if I just leave it there, it's gonna crash because in the, in the partial once the variable called movie, which we haven't sent, so we'll do local, and this is where it starts to get a little confusing.

But we have movie, movie, movie, movie, [01:35:30] movie, movie,

Movie, movie, movie, movie, movie. Imagine if I called this partial movie too, which is usually what they call it. But I'm trying to keep things a little bit separate. But here, this is the, the value that we're passing in. So I could just do like movie dot last here and it's gonna draw that point. Data, this, the value that.

This is the [01:36:00] variable that the part seconding us to send in. So here, and it usually ends up being that this is the same as this because there's a singular version of this. But now I can go to my, I'll render this partial, and here in the sun it's atmo is the how we get the value. Now this should work.

Click on, [01:36:30] go to the show page. Both the show page and the index page are working and they have the same

page. The styling of it. Nope, I guess that's not the class. But

point being like that partial is being used here and here, I can just continue to refine the styling of what a card, what a movie looks like, and the whole, my whole app [01:37:00] doesn't have to know about the code for it. So this is,

I would say like I use partials a lot heavily for so many reasons. Like I said, first of all, it helps me break up my huge templates into smaller and more manageable chunks. Another thing that's really nice, imagine if I want to add a link to the nav bar. I need to go to the application. I need to [01:37:30] find it in application layout, right?

Here's what I want you all to. So you go over here and you like dig through your stuff and then click on this. Scroll more and more become professional developers, less and less on our mouse. Wanna try to learn more and more keyboard from us, because that really does dramatically change your productivity.

So instead of clicking on a file in the sidebar from now on, [01:38:00] do command shift P, sorry, no, that's for the pallet. Just command P. So just command P brings up the file search and, and then you guys start to just type a few letters. Let's say I want that movie card. I'll be like Mv C D. And it almost always finds it.

And you don't even have to, it's not, you don't have to like a literal match either. Just type a few significant characters and it's really good at ly finding it and then hit return [01:38:30] and it jumps you right in there. So you notice, like I rarely dig around the sidebar routes. Oh, or ut boom movie boom. It's incredibly easier to get around Now that you, I mean, of course it relies upon you knowing what file you want to go to, but now that you start to know which one that is another.

To break up your gigantic view templates into partners. Cause [01:39:00] now I need to add lead to the nav bar. I can just go nav bar cause I create a partial called Nav bar and I'm, I just have what I care about here. So it makes it a lot easier to get it on your code base as well if you create smaller, more modern files, gigantic view templates.

So that's a huge benefit is the ability to just break up your big view templates. Another benefit of part of partials is something like a form here where you can pass [01:39:30] in input, mostly the same but has slight differences. But I would say that's biggest benefit is most of what we do as crud web developers, is we're getting data out of our database and then putting HTML around each record.

The ability to use a partial to represent a particular database record and then reuse that across our app is [01:40:00] the biggest win. I think I, I hesitate to even show this part, but I'm gonna show it to you because you're gonna start to see it when you read Stack Overflow answers and other documentation. So here is the cool thing, don't, I don't, maybe don't even try to replicate this.

Just when you have an active record object m. All active record objects inherit a method from application record, active record base called two [01:40:30] Partial Path, right? So all active record objects have a method included already outta the box and it returns by default the table slash the singular version of the object.

So plural, singular, we go right? Watch it. So I could go into my movie model if I wanted to and add a method def to partial [01:41:00] and say movie slash movie card. Basically, you're able to announce the active record object using this method. What is the name of the functioning that I should use to render you?

And the active record object will respond. That means that, that when I'm rendering it, like in the show page, [01:41:30] there's a shortcut as you might expect. I can

describe the object.

The render method. You give the render method an active record object. It's like, oh, okay, you want me to draw some H M L, the H M L representation of this active record object. So what the render method does is it implicitly calls two partial path on this, [01:42:00] and let's see if this works. Is this gonna work?

No, because the partial wants the local variable movie, which we have here. So the, I dunno if that's gonna work. There's that correct. Okay. Now let's suppose I did the conventional thing. So I, I kind of on [01:42:30] purpose named this movie underscore card. The conventional name for an active record object is singular underscore singular object name.

So at underscore at movie. So now that means that I don't have to overwrite this because the default method returns movie slash movie and I'm ready here. I don't have to pass this object in [01:43:00] either, because it will automatically assume. That the ver, the local variable name that we're using in that partial matches up with the class name, which is the case 99.999% of the time.

So now literally in order to render that partial, you just say render, give it the object. Kind of like how there's the ultimate short form of link to movie and it like figures out using the class name and the named routes and then [01:43:30] brows file. As long as everything matches up just right, you can send link to Mo and it figures out to create the whole A element.

But then this is like a lot more elaborate than that. But I do use this in my actual Real Rails apps. I style all the time. I want you to see it. You willing capture this on the internet. You can start using it if you want, or kind of write out the partial name and the logo passing in until you feel very comfortable with what's going on.

[01:44:00] Another cool is also this kind of situation. Uh, you can just say render at movies

because this is an active record relation. If you give it a relation, it'll do the dot each, and for each object it'll render the object. And if there's a partial that matches the name of the [01:44:30] object, it all figures it out and it works. So if you just have a collection of things like comments, And the comment is a self-contained partial, you can render the collection and it'll work.

Now, I lost my grid classes, so in this case I probably won't because I want these grid, like I need this in here to make it work, right? This, I'm not just rendering the partial over and over. There's other markup that I'm rendering. So you don't always, [01:45:00] but if you read, um, in the, uh, in the notes for the project, in the official docs, if you're curious, you can read through and there's like so many super short ways of doing this and render a collection.

And you can actually specify a separate template to use as a spacer between each one and put that so they each object and then a spacer and then a the object. So lots of super [01:45:30] ways can be concise. This documentation describes them all if you're interested,

but we'll leave it there for now. Uh, okay, what's next?

Okay, so we did cards in the index. Jump to file. Start using, jump to file more. Copy. [01:46:00] Okay, now I wanna switch gears and talk about something else that we about very briefly in Optiv one, when we talking about siren I out, but I wanna remind you about it. There's another feature in Rails called filters or, uh, uh, before action here, how this works.

If I have a controller and I want to just random method here,[01:46:30] 

and

so I'm printing, if I call this method

and action Action and I look at my server log,

so when you print in [01:47:00] the controller, the output is in the server log. But the key here is that I'm able to call this method here and then maybe let's say if I, if I, if I had a method that I wanted to call,

it's nice for me to, if you have some repeated logic, the exact same code happening in multiple actions. Well, you can extract that log into a single method and then call it as the first thing that you're doing each of those [01:47:30] methods. And if you're doing that a lot, then Rails has a syntax say before, give it the name of a method and then you don't have to even call it, it's now gonna automatically run this before every action in this controller.

Let me clear my server log. Is it like movies index and, oh, what's this missing Partials movie [01:48:00] card.

Yeah.

Okay, so let me clear this. Press this server log. So like it that that method ran before Index and

method ran before edit. It's just [01:48:30] gonna run before every single action in this controller now.

And I wanna be a little bit more surgical with it. I can say. Okay. And maybe not everyone. Maybe we'll just do the show and destroy actions so you can specific actions or you can accept specific actions. Really nice. And the place that we saw it before [01:49:00] was when we wanted to have like a signed in user them.

We didn't want them to do anything until they signed in. So if, and back then we were using exception use. This doesn't exist in this app, but I'm just saying as an example, if this is present, then we'll let them in. If not redirect them to the sign in page,

remember [01:49:30] this. Then we would have to basically need this code as the first three lines of every single action on our app of, there could be thousands of the actions in our app and if we want the same code to run, that would be extremely tedious. So instead we would put that into a method. We'd call it something like force user sign in and put it in here and then we would before.

Right? Great. Now [01:50:00] we would call that call, it would be

now every runs literally before every actually app. Okay. Okay. So we did this really quickly when digital generator, but we didn't really touch it after that. I just wanted to remind you that it exists because you are gonna, again, you're gonna see it when you start to read [01:50:30] Rails. Documentation. For example, in this app, we have some repetitive code in No index is pretty fine.

But here is, we have movie, we're we're taking prams of Id looking up and creating that movie, and we're doing that here. Exact same thing we're doing here. We're doing it here and we're doing it here for show, edit, update, and destroy. The first [01:51:00] thing that we need to do is find the movie and then put into a variable, right?

It's not that bad, but if I wanted to be very lazy, I could take this out, define a method, let's call it, uh, find movie or something, set movie

code there, and then use action to execute it. [01:51:30] But I don't want to do it for all my actions, like I don't need it in new and edit. I need it.

Update and destroy

actions. That's that. Now. Because we're not rendering either. Take it out here and also start [01:52:00] action. Cause I, this is again, whenever you're reusing code in different places, you're kind of constraining yourself. Cause you now have to use the same variable name everywhere. So I don't have the ability to rename this sound.

Yes. Switch this back to at moving. But this now runs, uh, before I reaction, let me see if it works. So edit seems to be working. Show seems to be working. [01:52:30] Update seems to be working and destroy seems working. So it's still working and we've dried up our code just a little bit more. I don't know if I like this.

I just wanna show it you cause you're gonna capture it. I don't, I wouldn't do this in my own code because when my team members are debugging the show action, I don't want them to like go here and be like, oh right. It's not very clear. They have to go and look at the view template and see that, oh, actually there is visitor.

Where's that coming from? And then [01:53:00] remember, oh, the one done is, there might be a before action and it might not even be in here, it might be in the application controller. So there's a lot of stuff that you have to backtrack and check. And I like being very explicit, so I might not use it a lot. Context, but plug users not in, or making sure that the sign user has the permission is like supposed to be able to execute that action.

Those are purpose for candidates for actions[01:53:30] 

and read.

With all that said, now I want us to press together open

and you can use any table name. I give director, actor. Let's do a [01:54:00] name and a date of birth, which is a date and a bio to the text. So you're using the rails, generating the built-in scaffold generator that I talked about, last class generating, and then read all the code that are generated. So we'll generate, gonna do a whole bunch of stuff, model migration, and create some tests.

File source, it puts resources in the routes for us. There's the controller, so you can skip reading the test files for now, and [01:54:30] the helpers and the jbo. There's, you can skip all that, but read through. Read through the routes. Read through the controller that was generated. And read through all of the templates that were generated and try to think of anything that doesn't make sense out.

Cause I think we have not touched upon everything that the Scaffold generator uses. And that's kind of the baseline minimum amount of [01:55:00] knowledge that Rails developers are assumed to have on Stack Overflow and blog posts when people are writing things. So it's very crucial to understand everything that's going on.

Scaffold the controllers, so the one controller, the view templates. Make sure you understand everything that's going on[01:55:30] 

my snapshot. So you're gonna have to,

whatever reason, doesn't

fix it.[01:56:00] 

I send them so you can read my code but not really work in them.[01:56:30] 

The whole question you said has questions or question. Um, yeah, let's start taking questions. What do you think? What do you see? So notice in the controller, its the default blank. [01:57:00] Do you, do you normally add that back in control? In the control of the act? Uh, sorry, the show, uh, uh, functions, please. So you add that back in for clarity.

The reason I just showed you, it's

here, here. And then this is the open scaffold. Everybody, basically, every Rails developer kind of [01:57:30] expects. So like, put it in. I'll, I just like, I, I let that be. Yeah, but I don't do cell like that myself. I'm writing.

Yeah. I changed it. Be good. Great. This is the shortcut. So look at, so when I wrote it, the square bracket and then it's an array of symbols. So for, this is a quick way, just a ruby. This is a ruby thing, not a rails thing.[01:58:00] 

Or I guess just do that in IRB too. But it's just like a quick literal syntax for creating an array of symbols. So you have a column, the colons, and there's a way to do that with strings. Two, I think it's w Um, so if you need an array of strings real quick, and if there's no spaces in any of the strings, you can use this shorthand syntex.[01:58:30] 

Okay. Anything

looks like instead of a button, like a class actions thing, you said button. Something else I used Submit, didn't I?[01:59:00] 

Okay. But I guess

Somem to get you started, Mr. Class, write up Style Rule four if you want.

Yep. Matt, the controllers. What is going on with the,[01:59:30] 

um, ? So one of the things I don't, let me, let me show it to you in the context of movies. So we have the movies. Oh, actually we had it here too. That's good. When you want from that action to be able to send out either JSON or H or depending pdf, [02:00:00] if you want that same resource to be able to request, in other words, you're building an api, not just html.

Then we add the Respond two block. And the way you interpret the respond two is almost like an if statement. Kind of it's, imagine if it was like, if request not format equals html. Elif request format equals json and in each, so [02:00:30] only one of these branches is gonna run. And then here we would say, okay, render the index template here.

We'd say render the index dot js o template. This is just pseudo code. But think of the respond to as kind of statement where it's like, okay, if the request was json execute this block. If the request in this case an empty block because we're doing the default thing of render, uh, movies index, so we can just [02:01:00] leave it blank.

But that's what, that's

which we're not gonna really do a lot, but because it's such an important part of most web apps these days, because you're gonna wanna probably have an iPhone app,

you're gonna want it

with the actor. Couldn't sound that I'm,[02:01:30] 

it's so the format json, it doesn't render show. When you render show it's in for a template that corresponds to that name in the actors and also corresponds to the format of the request. If we look at the templates here for actors will notice. There's two show templates. There's a HTML show template, and then there's a JSON show template.

E r B is the processing, uh, system that we use, [02:02:00] like dynamically create html. J builder is a templating language for JS O. If we look at this, it's like an another like that have to learn, but it's a very first language is creating a JSON response using, using

creating J. So

it's automatically selected because of the format [02:02:30] of the request. What else? Anything puzzling in actors controller or I guess generated, but that's the same as just the model. Um, anything else? So there's the json, the J builder templating language, which we haven't got to yet, but you template building JSON responses.

We got partials here.[02:03:00] 

It's a lot that goes into this. Yeah. Um, this might have been covered before in the edit. Uh, uh, you. It says link to show and then it says at actor instead of at Actor Path. I can't remember if that's, so if I expand it out, it would be actor path and then I [02:03:30] see. But you just give it an active record objects kind of like the render thing I just showed you.

These methods, oftentimes given an active record object, can put together the rest as long as everything is named conventionally. So you have to have a name drop, helper that match name class, and then it can do it for you.

Um, yeah, so good here. [02:04:00] So I, I want it to kind of rush to this. When I learned rails, you guys, my teacher showed me the scaffold generator as the first thing and then like never built up to it like us. So when me and my cohort, like it was amazing, right? It's like, oh my gosh, you just run this one command and you already have old working app, basically.

But then as we tried to like build our own stuff, our unique value for our app, we had no idea how [02:04:30] the fact that the fact that there's an action that's being inferred automatically by the class of the object and the method poster versus method get, like we never learned any of that. All we learned was like how this method.

What argument facts and then what the output, what the effect of that was. And we'd just be like kind of trial and erroring and copy copy pasting until we got, which is a legitimate way to learn, obviously, like I was able to [02:05:00] learn. But I think hopefully having some understanding of what all software doing for you will make it easier for you to customize when you inevitably have to customize what's going on.

And ultimately, like most Rails developers, when they're learning, they generate scaffolds and then they just copy paste this up when, and they render. Like if they need a form for a actor on a some other page, they just rendered the partial and don't really worry about how it's working. And you can get really [02:05:30] far that way.

But in inevitably, you're gonna reach a wall with that strategy and you all can just write a archive from scratch. Don't use any of the helper methods. You know how to drop back down to the basics and wire it up and just make it work. So under, remember that you have that in, in your back pocket at all times.

But maybe now start with the helper methods and try to make them work [02:06:00] and try to learn how to force them to do what you want 'em to do over time, it'll become second nature for you.

All right. So like, yeah, just remember like I went through all this fast, but most of the time you're generating the scaffold and the code gets written for you, and then you just have to be able to copy paste it and make it do what you want in different contexts. So if it feels like it'd be hard for you to sit down and type this all out from scratch, that's fine.

[02:06:30] It's hard for anybody to type up and scratch so many types stuff from scratch. We generate it and then you need to be able to know how to modify it and customize it. All right, so that's all I wanted to cover today actually, no, one more thing. Sorry. Uh, the other thing that we're gonna is every app that we build is gonna need users and sign in and sign out, right?

So in the old days we wrote it by hand and then we got the draft, [02:07:00] which just wrote it for us. Now we're gonna start using called device. And this is the gem that pretty much every, like I would say, 80 plus percent of rails apps, this gem to build the signup system,

I'm gonna add check device, and then I'm gonna bundle install,[02:07:30] 

and then I have to run a command to install it. Generator device install and it adds files. This is, this is Aran a locale file in case you wanna translate to,

but now that I've installed that gem, I can use the device generator instead of draft. Cool. An [02:08:00] account, the rest of it's the same as always. It's the model name and then any column names in that table other than emails automatically because it's meant for sign in. Signout does a whole bunch of stuff for,

and in the route manage one line devised for users. That one line expands out into like 15 different routes [02:08:30] or sign in, sign out, edit profile, cancel account. It asks functionality built into it. The reason we're gonna use this gem from now on is like, what if somebody forgets their password? Well, I would, I would send that an app dev one.

Well, hopefully they have your phone number and they responsible, and then you update your password for them manually. What's something they tell you over the phone? What is the actual flow space you like? Oh, well, there's a forgot password link, which you click on it [02:09:00] and then it goes to another form where you type in your email address and then it sends you an.

With a random token that then they click on and then we verify that they have the right token. Then we give another archive type new password from the new password and then it updates the password. That's a lot of work to fill all those archives, password flow. It's a lot of work and there's a lot of ways to get it wrong and then make your app insecure and hackable.

Rather than that, we're gonna use this. [02:09:30] That means I, it's my app here. I closed it. Oh, here it's, I, uh, have to restart my server because I added a new gem. So don't forget, when you add new gems, you gotta control, restart your server to pick up the new code. The bid server command only looks at the gem file once when it starts up and great.

Now I have users slash [02:10:00] sign in and this archive and the view templates and everything in the form for logging in works. And look, there's, I forgot your password. This, and there's a thing and it will your app to a mail provider like mail gun, mail gun, that's not very robust. But once you just connect, you sign up for your API token and connect your app to a mail, this whole mobile, which is amazing.

So [02:10:30] I can sign up.

Another ation pattern character validation built in. All of that is configurable.

This is also, um, a, a password digest or that takes, so the whole thing works. Look at my code here with the draft account generator. It created some controllers. [02:11:00] It created a user authentication controller with the device gem. It doesn't even put the controller in here, the controller, it's there. Of course, we saw that the archives are working.

The controller file remains within the gem and 99.99999% of the time, you don't want necessarily the code for sign in and sign it. So put the code here for us, the controllers in the gem. Now, if you need to do something custom, you can [02:11:30] generate, you can ask it to generate the code for the controller, and then you can modify it if you want to.

But like I, I don't think I've ever done that. I've never had to modify the controller actions for sign in and sign up. They're so boilerplate. What we will do though, is we wanna modify the view templates because like,

like this, oh, I'm sign in. I gotta sign out. Okay. So we can generate view templates if we [02:12:00] want to. We can stay. It views,

spits out these views, views folder that we can then like go modify and like add bootstrap and do whatever we want. So this we, we will want to customize how that look and feel of the view templates a lot. So devise is like, sure, here you go. Knock yourself out. Controllers, we very rarely [02:12:30] modify, so generally we don't.

But there are ways can customize those into, there's a chapter here that has more details about like, okay, how do you install it? How do you generate it that? But the good thing is like we're not putting to do much coding at all of it. The only thing we are putting links in our app to the sign in signup page, sign out, [02:13:00] edit profile dev device provides these helper for, so link sign in, new user registration path.

That's it. Can you use these in your templates where relevant, but you don't have to build those arm caps at all. And then crucially, dev devices defines a helper method called Current underscore user. This helper method is gonna be available in all view templates and all controller actions. [02:13:30] We are not gonna have to touch the session hash directly, ever.

We just used this helper method, which is available everywhere, well not in models, but in controllers and actions. And they'll return n if and it'll return the actual user. That'll be site very similar draft account method, uh, think draft account, define an instance, right?

Okay. After that, [02:14:00] you gotta use conditionals. You gotta use before actions to do the actual work of authorization and conditionally hiding and joint things. That's still on you. But devise gets us really, really far with the authentication step, which is figuring out if they know who they are.

Jim Generator included the force sign in. User action devise includes one called authenticate user, exclamation point. [02:14:30] Same, same thing. So I would go into my application controller

if I want to force somebody to sign in before every action. This is fine inside the device controller. So now it's gonna make me, I, I'm already signed in. Me. Okay, fine. I'll give myself a sign out link real quick.[02:15:00] 

It's Destroy User Session Path is the name of the Route Helper Method and we need to do a method delete on it. And I also go and delete the scaffolds dot CSS because it's interacting with Bootstrap and messing up our css.

So now I'm signed out and notice [02:15:30] it doesn't let me go anywhere until I signed. That's it. So very similar to Force User, uh, that the draft account generator gave us. So, okay. Point B device gives us everything that the draft account generator gave us, but 10 times better and like so much more stuff. Like it has little Remember me checkbox so they don't have to sign in every time that they come back.

That would be a bunch of work for us to implement by hand. So we're gonna use device from now on, we're gonna leave draft [02:16:00] account behind us now draft pieces and it's gonna look a little weird, but we just not November, at the end of the day it's just RCA and HTML and peram. But let's attempt to use that from now on and only go back to draft resource.

We really, really need to do something custom. Sound good? Great. Well this is a milestone. So now [02:16:30] this is the amount of, like, these are the main methods now, but you've seen, uh, partials and the form with helper linked to re uh, in the models about how belongs to, that's kind the baseline knowledge that rails developers assume all other rails developers have.

So now you're really gonna be able to start to read Gem re and blog post Ruby Weekly. And you should be able to understand, okay, well your homework is gonna be to into practice, [02:17:00] build photogram yet again,

but you're gonna build it the way that I would build it. Starting like instead of build up incrementally learning something new along the way, and then refactoring, I build it from summer. All the tools and trade I would use when I'm starting to build like a, a client project in this video that will add more performance and security to the [02:17:30] application as well.

Okay? We're building it for real now. There's no more like, oh, I'm gonna ban you by by showing you a shortcut in a couple weeks. Not anymore. You're gonna do it the real way this time. Alright, see you next week.

