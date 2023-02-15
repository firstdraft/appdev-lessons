# Photogram GUI

- Notes:

  - [Video](https://canvas.uchicago.edu/courses/41147/pages/video-photogram-gui){:target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/photogram-gui.md){:target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/photogram-gui](https://github.com/appdev-projects/photogram-gui){:target="_blank"}

  - Target: [https://photogram-gui.matchthetarget.com/](https://photogram-gui.matchthetarget.com/){:target="_blank"}

  - Useful chapters:

    - [Time to CRUD][Time to CRUD]

## Video Segment: CRUD with Forms

- Notes:

  - time stamp 00:00:00 to 00:05:11
  - CRUD in relation to MSM app
  - forms for getting data into query string and then into database

**BENP: up to 00:10:00 is just a walk through with lots of talking in the target. I wrote down what was said but no screenshots. Video is pretty good as is up to this point.**

In this project, Photogram *GUI*, we're finally going to be building a *Graphical User Interface*, for our users to *CRUD*, **C**reate, **R**ead, **U**pdate and **D**elete data into our database tables. 

We've already done a lot of work with the **R** part. Given some data, we have displayed that data in our webpages a whole bunch of different ways. We've done really complicated queries to display that data. We've shown the rows in a table, we've shown an individual record details based on the ID number in the URL, and we're using `params`. 

We also showed the records associated to an individual record in a *one-to-many* association. For example, the movies in the filmography for a director. We put those movies right on the details page in the director. So that was pretty great. We also showed, in a *many-to-many* relationship, the rows associated to a record. For example, on the actor details page, we showed all of the movies in a filmography. 

So we've done actually, believe it or not, quite advanced queries, if you ask a database person. And all without really thinking too hard about it. All we were doing was using `.where`, our bread-and-butter query method, and using what we have been thinking about since week one: *foreign keys* and *join tables* to connect our entities together in 1-N and N-N relationships, and doing lookups. And that's all CRUD applications boil down to. 

Okay, but we're missing one huge thing, which is, how do we get the data into the database in the first place? So far, we've been relying on `rails console` (manual entry), **/rails/db** (visual interface), and `rails sample_data` (rake task for sample data).

We need to give our users a way to enter data. The whole point of our applications was keeping track of important information on behalf of our users: **record keeping**. And so we spent the first couple of weeks figuring out how to think of what that information is, and design database tables to keep track of that information. 

Let's give them some forms (`<form></form>`) to fill out so that they can tell us their information (`<label></label>` and `<input>`). And then when they click submit (`<button></button>`) on those forms, we know that that information is going to go to some other URL, specified by the action attribute of the opening form tag (`<form action="/URL/here/">`). The information they provide in the form is going to be put into the *query string* on that next URL (**/URL/here?input_one=foo&input_two=bar**), and then Rails is going to stick all that into the `params` hash. And then we can take all that stuff out of the `params` hash in that second action. Phew!

In the past, we just computed some stuff and then kind of showed them some output and then forgot about all that stuff. Or maybe we put it into a *cookie* that we store in their browser, which is useful for a whole bunch of stuff, especially sign-in and sign-up in the next week. **BENP: we didn't talk about cookies up to this point, maybe leave out**

Now, we're going to take all that information from the user and **save it into a record in our database**, rather than us, the developers, using `rails console`, **/rails/db**, and/or `rails sample_data`. And so it's all going to finally come together. Everything we learned about routing, RCAV, `params`, forms, all that stuff. And everything we've been learning about `ActiveRecord` and databases, that's finally going to come together, and we're going to build our [target Photogram app](https://photogram-gui.matchthetarget.com/){:target="_blank"}.



### Text Companion: CRUD with Forms

## Video Segment: Explore the Target

- Notes:

  - time stamp 00:05:11 to 00:10:05
  - CRUD in relation to Photogram GUI

**BENP: here's where screenshots or GIFs could be inserted**

It's very simple. Right now it's just a list of users and photos. Next week, we're going to add the final piece of this, which is *cookies* for sign-in and sign-up. But right now, anybody can just add users and it just adds the record to the table. So there are no accounts yet. It's just like adding an actor or adding a director. We are just adding records to the table right now.

There's a form to add [**/users**](https://photogram-gui.matchthetarget.com/users){:target="_blank"}. There's a form to add [**/photos**](https://photogram-gui.matchthetarget.com/photos){:target="_blank"}. And that's what we have to wire up. 

In addition to that, if we go into the details page of a user, like [**/users/desmond**](https://photogram-gui.matchthetarget.com/users/desmond){:target="_blank"}, there's also a form with the username pre-populated. Notice this URL **/users/desmond** isn't an ID number, but it's a username, and follows the same principle as putting the ID number. We know how to build a route where this can vary, and then take that information and use it to populate a page. We did that! We're going to do that again, but now we're going put a form in here and let them update some information. If we change the username with the form to "desmond2" and click "Update user", I come back to the same URL, but now changed to **/users/desmond2**. 

Now, similarly, you've got **/photos**, and you can go to the details page of one, say [**/photos/861**](https://photogram-gui.matchthetarget.com/photos/861){:target="_blank"}. There's a another edit form here, and again if I change something and click "Update photo", I'll end up back on the details page and that change has been persisted. And I can delete the photo. 

If I scroll down farther on the photo details page, there's a section for "Comments", and I can add a new comment. Now, when I'm adding a new comment, I have to type in an "Author ID", which is kind of annoying. You have to provide a valid ID number, or it's not going to work. So there's a new concept of *validation*. 

**BENP: `validates` is used in this project and there are notes and examples below, but this is covered in much more detail in [Data integrity with Validations][Data integrity with Validations]**

Okay, so there's some work to be done to get here to this target. Believe it or not, little of this is new. We've done forms, we've done `params`, we've done dynamic routes, we've done `ActiveRecord`, and we've done CRUD at the `rails console` (e.g., with `.new`, then add attribute values, then `.save`). 

It might help to actually keep that [CRUD chapter section](https://chapters.firstdraft.com/chapters/770#time-to-crud){:target="_blank"} handy for reference. In fact, another useful chapter to keep open for reference is the compendium [one reference chapter](https://chapters.firstdraft.com/chapters/774){:target="_blank"}, which is a concise class and method reference. **BENP: editorialized that last sentence, which you bring up a few minutes later in video**

Let's get started.



### Text Companion: Explore the Target

## Video Segment: Explore the ERD

- Notes:

  - time stamp 00:10:10 to 00:18:15
  - examine **/rails/db**, run `rails sample_data` 
  - examine ERD (https://github.com/appdev-projects/photogram-gui/blob/master/erd.png)
  - discuss 1-N and N-N relationships in the domain

As usual, I'm going to start with `config/routes.rb`, because that's the entry point to any Rails application: the list of URLs a user can visit. You can also use the tool **/rails/info** in the browser of your workspace, which will answer the same question: what requests does this Rails app respond to right now?

Open that file now:

```ruby
# config/routes.rb

Rails.application.routes.draw do


end
```

It's empty! Looks like we need to build it all from scratch... not quite true. If I visit **/rails/db** in my browser, I at least have database tables created for `comments`, `follow_requests`, `likes`, `photos`, and `users`. We've been planning this architecture for a long time for our social network. 

The database is, however, empty, and we don't have any routes defined. We can hope that someone wrote a rake task to populate our database with sample data... and if you run `rails sample_data` at the terminal in GitPod you will find that this is the case!

If we click on the `users` table in **/rails/db** (taking us to **/rails/db/tables/users/data**), we see we have lots of columns, and it might help to actually view our domain model:

![](https://github.com/appdev-projects/photogram-gui/blob/master/erd.png)

This is our *Entity Relationship Diagram* or *ERD*. I like to include such diagrams with my project README. In fact there's a gem that generates such ERDs for you.

Remember we have users and photos in a 1-N association. I called the foreign key `owner_id` in `photos`, to keep track of which user owns which photo. Conventionally we would call the foreign key whatever the other table is called with an `_id`, `user_id` in this case. But, sometimes we want something more descriptive, and in the end it is up to me, the developer to choose these names. 

Photos also have `caption`, `comments_count`, and `likes_count`. I didn't necessarily even need the `_count` columns, since these could be looked up with the photo foreign key columns. But it's nice to keep the value here so I can use `.order` by the number of likes for sorting the records.

We also have a join table for an N-N relationship called `likes` with the two foreign keys `fan_id` (from `users` table) and `photo_id` (from `photos` table). Again, we see a more descriptive name chosen in this case than the conventional `user_id` for this table.

Now we have our `comments` table, which is very similar to `likes`, with foreign key columns for the `users` (`author_id` here) and `photos` (`photo_id` again), and the addition of the comment text in the `body` column.

Within the `users` table we also have an internal N-N relationship, since one user can have many followers and leaders, and this is captured in the `follow_requests` table. We note that here the model classname will be `FollowRequest` (`snake_case` to `CamelCase` and made singular). Follow requests has two foreign key columns, both from the `users` table: `recipient_id` and `sender_id`. There is also the `status` column for keeping track of whether the "pending" request was "accepted" or "rejected".

We won't tackle all of this now. Today, we are just building an interface for users to enter records into these tables, update them, and delete them.

This means we're going to have to do a lot of RCAV to set everything up. 



### Text Companion: Explore the ERD

## Video Segment: Explore Model Classes

- Notes:

  - time stamp 00:18:15 to 00:20:58
  - examine `app/models/user.rb`
  - association accessor instance methods there and in other models
  - `validates` (first mention, only detailed later in https://github.com/appdev-projects/msm-validations and [Data integrity with Validations][Data integrity with Validations])

But we actually have even more in our starting point that will help us. The model files are already in the project, for instance, you can find:

```ruby
# app/models/user.rb

# == Schema Information
#
# Table name: users
#
#  id             :integer          not null, primary key
#  comments_count :integer
#  likes_count    :integer
#  private        :boolean
#  username       :string
#  created_at     :datetime         not null
#  updated_at     :datetime         not null
#

class User < ApplicationRecord
  validates(:username, {
    :presence => true,
    :uniqueness => { :case_sensitive => false },
  })

  def comments
    my_id = self.id

    matching_comments = Comment.where({ :author_id => my_id })

    return matching_comments
  end
...
end
```

And these are full of *association accessor instance methods*  **BENP: I have not been using or have been loose with instance vs class method, probably need to comb through everything and check consistency**, like `comments` above, which you can use out-of-the-box to query across your tables. This is what we spent all the time building when we refactored MSM queries, and you get it here for free. Note that there are also some `validates` functions, which we haven't discussed yet, to do the validations of data entered into our tables.

**BENP: here is the first mention of `validates`, which we use here, but is covered much more in chapter/project that follows Photogram GUI: https://github.com/appdev-projects/msm-validations**

The `comments` method will return a list of comments made by a given user, and would be used like `a_user.comments`. This is an `ActiveRecord::Relation` returned, and one could `.each` over the rows to display data on a page! No need for writing out these queries over and over again on your view templates. Ever!

Take a look at the model files for each table in `app/models`. **Spend time reading them**. There are a lot of methods and having them are going to make our job a lot easier. Familiarlize yourself with what you have so that you are armed to build out the app. 



### Text Companion: Explore Model Classes

## Video Segment: Users `index`

- Notes:

  - time stamp 00:20:58 to 00:27:25
  - RCAV to get table of users at **/users**
  - query in `index` action to get `ActiveRecord::Relation` object `@list_of_users`

Let's start building out the pages. The homepage **/** in our target is the list of users (also at the path **/users**). So let's RCAV.

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })
  get("/users", { :controller => "users", :action => "index" })

end
```
{: mark_lines="5-6"}

We are using the standard, conventional names in use in the Rails community from here on out. That means we name the controller for the page after the table plural. For the action that just lists our records, we call it `index`. Now we create that controller and action:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  def index
    
    render({ :template => "user_templates/index.html.erb" })
  end
end
```

Now we create the view template `user_templates/index.html.erb`, place some copy there (why not.. "hi"?), and view it in our browser at **/** or **/users**:

```html
<!--- app/views/user_templates/index.html.erb --->

<h1>hi</h1>
```

We can view the [target](https://photogram-gui.matchthetarget.com/){:target="_blank"}, and see that we want a table with a list of users here. So let's put some mockup in our view template based on what we see there:

```html
<!--- app/views/user_templates/index.html.erb --->

<h1>List of users</h1>

<table border="1">
  <tr>
    <th>
      ID
    </th>

    <th>
      Username
    </th>

    <td>
    </td>
  </tr>
</table>
```
{: mark_lines="3-18"}

If we now refresh the **/users** URL, this is going to make a blank table with three columns that we want to fill in with the ID, username, and a "Show details" link. So now we need all of the user records from our `users` table. What we want is something like:

```html
<!--- app/views/user_templates/index.html.erb --->

<h1>List of users</h1>

<table border="1">
  <tr>
    <th>
      ID
    </th>

    <th>
      Username
    </th>

    <td>
    </td>
  </tr>
  
  <% @list_of_users.each do |a_user| %>
    <tr>
      <td>
        <%= a_user.id %>
      </td>

      <td>
        <%= a_user.username %>
      </td>

      <td>
        Show details
      </td>
    </tr>
  <% end %>

</table>
```
{: mark_lines="19-33"}

We want an instance variable to loop over in our *front-end*. Specifically we want a list of rows from our `users` table and then we can get things like the `.id` and `.username` from each row. We'll make the "Show details" link work later. 

Let's go back to our action in the *back-end* and prepare this instance variable `@list_of_users`:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  def index
    @list_of_users = User.all.order({ :username => :asc })
    render({ :template => "user_templates/index.html.erb" })
  end
end
```
{: mark_lines="5"}

And now, since we defined the variable, if we refresh **/users** in our browser, then we will see the populated table with our list of records with no error messages. And we even ordered is alphabetically by username using `.order({ :username => :asc })` in the action.

Now would be a good time for a `rails grade` and a **/git** commit if everything is working like the target.



### Text Companion: Users `index`

## Video Segment: User Details `show`

- Notes:

  - time stamp 00:27:25 to 00:47:40
  - more on `validates` (probably should be moved from here)
  - RCAV a details page with flexible / dynamic routes, using **/users/:path_username**
  - `redirect_to` if `nil` user, otherwise `render({ :template => "user_templates/show.html.erb" })`
  - "Own photos" table with association accessor methods `@the_user.own_photos` and `a_photo.poster.username`
  - Faker gem

We still need to make the "Show details" link work. This user details page has the username as the second dynamic segment. In the past we have just used the ID number to do this. But every user has to have a *valid* username, which we saw in our model, but didn't discuss:

```ruby
# app/models/user.rb

...
class User < ApplicationRecord
  validates(:username, {
    :presence => true,
    :uniqueness => { :case_sensitive => false },
  })
...
end
```

What is this saying? Well we are using the inherited function `validates()` and the first argument is the column of our `users` table, `username`. The second argument is a hash containing some requirements for the `username` value. It must be present, so it must exist, with `:presence => true`, and it must be unique among users and case-sensitive, with `:uniqueness => { :case_sensitive => false }`. So a user must include a username, it must not exist in the table, and if a user like "raghu" exists, then "Raghu" won't work. **BENP: this aside about validates could be removed. Actually probably not because comes back below (see my note there)**

Before we get "Show details" to work on our index page, we need to build the show action, which is the user details page. Just like how we had movie or director details.

If in our app we go to **/users/austin** (or any other username in our table), then we get the "no route matches" error and we can start debugging the RCAV:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })
  get("/users", { :controller => "users", :action => "index" })
  get("/users/:path_username", { :controller => "users", :action => "show" })

end
```
{: mark_lines="7"}

We are using a dynamic route with the second segment `:path_username`, which we know will end up in our `params`, and we use the conventional action name for showing the details of a record, `show`. Now we create that action and show something in our view template:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
...
  def show
    render({ :template => "user_templates/show.html.erb" })
  end
end
```
{: mark_lines="5-7"}

Right away we put in some mockup to match the target here:

```html
<!--- app/views/user_templates/show.html.erb --->

<h1>username</h1>

<dl>
  <dt>ID</dt>
  <dd>user_id</dd>

  <dt>Edit user</dt>
  <dd>Form goes here</dd>
</dl>

<h2>Own photos (photo count count goes here)</h2>

<table border="1">

</table>
```

Of course, we will now need to fill in the static HTML here with dynamic embedded Ruby to get the page to work for each user.

In my server log on GitPod (the terminal running `bin/server`), we can see that anything I put in the second segment of **/users/austin**, will end up in the `params`, like `{"path_username"=>"austin"}`. That is available in our show action. So let's make it work now:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
...
  def show
    url_username = params.fetch("path_username")
    @the_user = User.where({ :username => url_username }).first
    render({ :template => "user_templates/show.html.erb" })
  end
end
```
{: mark_lines="6-7"}

We got the username from the URL path, then we used that username to find the matching record in our `users` table by searching the `username` column (which we have access to through the `User` model). We are expecting one record, so we use `.first` to get back a single object, our instance variable `@the_user`, which we'll use in our view template.

But wait! This `@the_user` could be empty or `nil`, if there is no valid username that was entered in the URL found in our table. What do we do then? Well we can check on this and redirect if necessary:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
...
  def show
    url_username = params.fetch("path_username")
    @the_user = User.where({ :username => url_username }).first

    if @the_user == nil
      redirect_to("/")
    else
      render({ :template => "user_templates/show.html.erb" })
  end
end
```
{: mark_lines="9-12"}

So now if you get back a `nil` user, then you are redirected to the homepage, otherwise you are taken to the details page. Now, if we really wanted to write our code *defensively* like this, we would need to put similar `if-else` statements in many other places. But we won't worry about this for now, we just want to be aware of the possibility of returning `nil` and one solution. **BENP: this `nil` redirect aside is also removable, you comment out the code in the video...**

Back to the view template with our new `@the_user` object:

```html
<!--- app/views/user_templates/show.html.erb --->

<h1><%= @the_user.username %></h1>

<dl>
  <dt>ID</dt>
  <dd><%= @the_user.id %></dd>

  <dt>Edit user</dt>
  <dd>Form goes here</dd>
</dl>
...
```
{: mark_lines="3 7"}

We have some progress. Now, what about the "Own photos" section farther down the page? Association accessor methods to the rescue! We have pre-defined a method `own_photos` in the `app/models/user.rb` model (go see for yourself). This method returns a list of a given users photos, which we can put in the table (or even call a `.count` on to get the number of records):

```html
<!--- app/views/user_templates/show.html.erb --->

...
<h2>Own photos (<%= @the_user.own_photos.count %>)</h2>

<table border="1">
  <tr>
    <th>Image</th>
    <th>Owner</th>
    <th>Caption</th>
    <th>Posted</th>
    <th></th>
  </tr>
  <% @the_user.own_photos.each do |a_photo| %>
    <tr>
      <td><img src="<%= a_photo.image %>"></td>
      <td><%= a_photo.poster.username %></td>
      <td><%= a_photo.caption %></td>
      <td><%= a_photo.created_at %></td>
      <td>Show details</td>
    </tr>
  <% end %>
</table>
```
{: mark_lines="4-23"}

These are all the familiar patterns of `.each` looping over table records and accessing attributes to print in a table (or assign to an HTML tag attribute as in `<img src="">`). 

Note that we could have easily just used the `@the_user.username` to fill the "Owner" column, because we are on that user's page. But we showed off another association accessor method, by going from the photo `a_photo` through the method in the `Photo` model `poster` (have a look in `app/models/photo.rb` and see for yourself), to give us back the user that posted that image, and call `username` there.

As an aside, we generated all this random data with a gem called [Faker](https://github.com/faker-ruby/faker){:target="_blank"}. Very useful for testing purposes.



### Text Companion: User Details `show`

## Video Segment: Adding Navigation Links

- Notes:

  - time stamp 00:47:40 to 00:50:45
  - add navbar links to the `app/views/layouts/application.html.erb`

Before we go any further, I want a way to navigate my site by clicking rather than manually entering URLs. Let's add the navigation links in the page headers like we see on the target for "Users" and "Photos".

To do that we go into our layout view and add it in the `<body>` tag around where we want the pages to `<%= yield %>`:

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    <title>Photogram GUI</title>
    <%= csrf_meta_tags %>

    <!-- Expand the number of characters we can use in the document beyond basic ASCII 🎉 -->
    <meta charset="utf-8">

    <!-- Make it responsive to small screens -->
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <%= csp_meta_tag %>
    <%= stylesheet_link_tag    'application', media: 'all' %>
  </head>

  <body>
    <nav>
      <ul>
        <li><a href="/users">Users</a></li>
        <li><a href="/photos">Photos</a></li>
      </ul>
    </nav>
    
    <%= yield %>
  </body>
</html>
```
{: mark_lines="20-25"}

Remember, Rails made this file for you and included all of the HTML header information we discussed early on, so we don't need to worry about putting this on all of our view templates. Rails gives you a huge head start with this and so many other files that we see in the GitPod workspace.

By adding this code to our application layout file, we will see that anywhere we go in our app, the nav bar will follow.



### Text Companion: Adding Navigation Links

## Video Segment: Users Show Details Link

- Notes:

  - time stamp 00:50:45 to 00:52:44
  - add show details link on **/users** table with `href="/users/<%= a_user.username %>"`

Let's go back and make the user "Show details" link on the **/users** page actually work, so we don't need to manually enter usernames in our URL path to get to their page.

```html
<!--- app/views/user_templates/index.html.erb --->

...  
  <% @list_of_users.each do |a_user| %>
    <tr>
      <td>
        <%= a_user.id %>
      </td>

      <td>
        <%= a_user.username %>
      </td>

      <td>
        <a href="/users/<%= a_user.username %>">Show details</a>
      </td>
    </tr>
  <% end %>

</table>
```
{: mark_lines="15"}

And this link will work right away for each user in the table because we defined our dynamic routes, like **/users/anisa**, **/users/austin**, etc. So this `href=""` attribute will lead to a defined route when we click the "Show details" link in our table on **/users**.

The index and show pages for users is looking good, so let's `rails grade` and **/git** commit.



### Text Companion: Users Show Details Link

## Video Segment: Photos `index`

- Notes:

  - time stamp 00:52:44 to 01:00:00
  - RCAV **/photos** and get list of photos in `index` action for table in view template
  - include show details link with `href="/photos/<%= a_photo.id %>"`

Let's work on the photos page now so we can move on to our new stuff, which is the "Delete" links and the forms. The usual steps now:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })
  get("/users", { :controller => "users", :action => "index" })
  get("/users/:path_username", { :controller => "users", :action => "show" })
  get("/photos", { :controller => "photos", :action => "index" })

end
```
{: mark_lines="8"}

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  def index
    render({ :template => "photo_templates/index.html.erb" })
  end
end
```

```html
<!--- app/views/photo_templates/index.html.erb --->

<h1>hi</h1>
```

And once that's working and we have no errors when we go to **/photos** in our browser, we add mockup HTML from the target and what we *want* to loop in our table:

```html
<!--- app/views/photo_templates/index.html.erb --->

<h1>List of photos</h1>

<table border="1">
  <tr>
    <th>Image</th>
    <th>Caption</th>
    <th>Owner</th>
    <th>Posted</th>
    <td></td>
  </tr>

  <% @list_of_photos.each do |a_photo| %>
    <tr>
      <td>Some image</td>
      <td>Some caption</td>
      <td>Some username</td>
      <td>Some time</td>
      <td>Show details</td>
    </tr>
  <% end %>
</table>
```

And now we need to get our required instance variable in the action on the back-end:

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  def index
    @list_of_photos = Photo.all.order({ :created_at => :desc })
    render({ :template => "photo_templates/index.html.erb" })
  end
end
```
{: mark_lines="5"}

In our new controller action we ordered by newest photo first (`created_at` column ordered into descending time). And now we can fill in our static HTML in the loop with our new dynamic Ruby:

```html
<!--- app/views/photo_templates/index.html.erb --->

<h1>List of photos</h1>

<table border="1">
  <tr>
    <th>Image</th>
    <th>Caption</th>
    <th>Owner</th>
    <th>Posted</th>
    <td></td>
  </tr>

  <% @list_of_photos.each do |a_photo| %>
    <tr>
      <td><img src="<%= a_photo.image %>"></td>
      <td><%= a_photo.caption %></td>
      <td><%= a_photo.poster.username %></td>
      <td><%= a_photo.created_at %></td>
      <td><a href="/photos/<%= a_photo.id %>">Show details</a></td>
    </tr>
  <% end %>
</table>
```
{: mark_lines="16-20"}

And if we refresh **/photos**, we will see our nice table of records. Let's **/git** commit it.



### Text Companion: Photos `index`

## Video Segment: Photo Details `show`

- Notes:

  - time stamp 01:00:00 to 01:06:43
  - RCAV **/photos/:path_id** flexible route
  - use photo ID from URL in `params` in `show` action to get photo details and display

Now if I click on one of the "Show details" links on **/photos**, I get a "no route matches" error. So we can RCAV that now.

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })
  get("/users", { :controller => "users", :action => "index" })
  get("/users/:path_username", { :controller => "users", :action => "show" })
  get("/photos", { :controller => "photos", :action => "index" })
  get("/photos/:path_id", { :controller => "photos", :action => "show" })

end
```
{: mark_lines="9"}

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  ...
  def show
    render({ :template => "photo_templates/show.html.erb" })
  end
end
```
{: mark_lines="5-7"}

```html
<!--- app/views/photo_templates/show.html.erb --->

<h1>hi</h1>
```

And once that's working and we have no errors when we go to **/photos/777** in our browser (or any photo ID in that second segment), we add mockup HTML from the target and what we *want* to display:

```html
<!--- app/views/photo_templates/show.html.erb --->

<h1>Photo Details</h1>

<dl>
  <dt>Image</dt>
  <dd>Some image</dd>

  <dt>Caption</dt>
  <dd>Some caption</dd>

  <dt>Owner</dt>
  <dd>Some owner</dd>

  <dt>Posted</dt>
  <dd>Some time</dd>

  <dt>Edit photo</dt>
  <dd>Form goes here</dd>

  <dt>Delete photo</dt>
  <dd>Delete this photo</dd>
</dl>
```

And now we need to get our instance variable in the action on the back-end. Well we have the ID number of the photo is our URL path, and we have defined this path dynamically in `config/routes.rb`, so we know this photo ID number is in `params` (you can check in the `bin/server` terminal log when you visit a photo details page). Well then, back in the action we can:

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  ...
  def show
    url_id = params.fetch("path_id")
    @the_photo = Photo.where({ :id => url_id }).first
    render({ :template => "photo_templates/show.html.erb" })
  end
end
```
{: mark_lines="6-7"}

And use this photo record back in the template to replace the static portions:

```html
<!--- app/views/photo_templates/show.html.erb --->

<h1>Photo Details</h1>

<dl>
  <dt>Image</dt>
  <dd><img src="<%= @the_photo.image %>"></dd>

  <dt>Caption</dt>
  <dd><%= @the_photo.caption %></dd>

  <dt>Owner</dt>
  <dd><%= @the_photo.poster.username %></dd>

  <dt>Posted</dt>
  <dd><%= @the_photo.created_at %></dd>
  ...
</dl>
```
{: mark_lines="7 10 13 16"}

And if we refresh **/photos/777** (or any other photo), we will see our details (minus the form and delete link). 



### Text Companion: Photo Details Page

## Video Segment: Photo Comments with Association Accessors

- Notes:

  - time stamp 01:06:43 to 01:10:54
  - get "Comments" section on photo details page using `@the_photo.comments.each` and `a_comment.commenter` association accessor methods

Just like in the target, we still need to add the photo comments below the photo details on the show page. We can "View Source" on the target and get some static HTML to begin working with:

```html
<!--- app/views/photo_templates/show.html.erb --->

<h1>Photo Details</h1>

...

<h2>Comments</h2>

<table>
  <tr>
    <th>Commenter</th>
    <th>Comment</th>
    <th>Posted</th>
  </tr>

  <% @list_of_comments do |a_comment| %>
    <tr>
      <td>Some commenter name</td>
      <td>The comment</td>
      <td>Created at</td>
    </tr>
  <% end %>
</table>
```
{: mark_lines="8-24"}

Now we could go back into our action and define something in the `show` action to get this `@list_of_comments` variable that we want for each photo. But, wait! Association accessor methods! Have another look in `app/models/photo.rb`... If you look then you will find the method `.comments`. Great, so let's use that on the `@the_photo` record that we already have on this page, and fill in the comment attributes (column values) in the loop as well:

```html
<!--- app/views/photo_templates/show.html.erb --->

...

  <% @the_photo.comments.each do |a_comment| %>
    <tr>
      <td><%= a_comment.commenter.username %></td>
      <td><%= a_comment.body %></td>
      <td><%= a_comment.created_at %></td>
    </tr>
  <% end %>
</table>
```
{: mark_lines="5 7-9"}

Note that we are using yet another association accessor method `.commenter` (you can find that in `app/models/comment.rb`) on our `a_comment` variable to get the username (because this method returns a user). 

Let's **/git** commit all of this before we move on to updating and deleting records with forms.



### Text Companion: Photo Comments with Association Accessors

## Video Segment: Delete Photo Link

- Notes:

  - time stamp 01:10:54 to 01:20:07
  - moving to the D in CRUD
  - get "Delete this photo" link on photo details page by RCAVing `"/delete_photo/<%= @the_photo.id %>"` 
  - `.destroy` in the action to delete photo

On the photo details page (maybe **/photos/777**), let's think about that delete link. This is just static right now:

```html
<!--- app/views/photo_templates/show.html.erb --->

<h1>Photo Details</h1>

<dl>
  ...

  <dt>Delete photo</dt>
  <dd><a href="">Delete this photo</a></dd>
</dl>
```
{: mark_lines="9"}

When I click on the "Delete this photo" link, it needs to take me to a URL (empty `href=""` right now) that knows the photo ID I'm interested in deleting, and then the action for that URL will look up the photo with that ID and call `.destroy`. After that, we need to send the user somewhere, and it can't be back to the photo details page because that photo will be gone.

If we look at the target and "View Source", we will find the structure of this delete link is: `href="/delete_photo/photo_ID_number"`, where `photo_ID_number` is the photo ID of the photo page we are currently on. This segment of the path will need to be dynamic, like:

```html
<!--- app/views/photo_templates/show.html.erb --->

<h1>Photo Details</h1>

<dl>
  ...

  <dt>Delete photo</dt>
  <dd><a href="/delete_photo/<%= @the_photo.id %>">Delete this photo</a></dd>
</dl>
```
{: mark_lines="9"}

Now this link will not work yet when we click it in our app. "No route matches", because we haven't defined the route! Let's do that:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })
  get("/users", { :controller => "users", :action => "index" })
  get("/users/:path_username", { :controller => "users", :action => "show" })
  get("/photos", { :controller => "photos", :action => "index" })
  get("/photos/:path_id", { :controller => "photos", :action => "show" })
  get("/delete_photo/:path_id", { :controller => "photos", :action => "delete" }))

end
```
{: mark_lines="10"}

And let's also define this action that will destroy the record and redirect the user to the **/photos** page (as the target does when a photo is deleted):

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  ...
  def delete
    url_id = params.fetch("path_id")
    the_photo = Photo.where({ :id => url_id }).first
    the_photo.destroy
    redirect_to("/photos")
  end
end
```
{: mark_lines="5-10"}

**BENP: in the above code, in the video you use `baii` as the action name and you also originally render a `baii.html.erb` template. Could this just be skipped as I have it? We have already seen redirect_to, it's nothing new. We also do the render then redirect_to dance in the Photo Create Form section below, and here I left this in because it is done more concisely.**

And this is it! `.destroy` issues the SQL to the database and deletes the record from the table. Try going to a photo details page and clicking on the "Delete this photo" link now.

We have just set the action to redirect to the **/photos** page, but we could have also had this action render another page with some information, like a page that informs the user that the action was successful.

Let's make a **/git** commit!



### Text Companion: Delete Photo Link

## Video Segment: Create Photo Form

- Notes:

  - time stamp 01:20:07 to 01:36:27
  - moving to the C in CRUD
  - build up form in `app/views/photo_templates/index.html.erb`
  - RCAV `action="/insert_photo"` with action `create`
  - fetch `params` from form, `.save` to database

We're done with reading and deleting, so now let's do the trickier ones. Create and update. 

For create, in the [target](https://photogram-gui.matchthetarget.com/photos){:target="_blank"} at **/photos**, there is a form above the table with all the photos.

As an example we can choose a URL, maybe one of the images on the Chicago Booth [homepage](https://www.chicagobooth.edu/){:target="_blank"}, like [this one](https://www.chicagobooth.edu/-/media/project/chicago-booth/why-booth/a-global-footprint/building-connections-across-asia/chicago-booth-hong-kong-location.jpg){:target="_blank"}. You can right click on any image of your choosing on the page and click on "Copy image address" to get the URL. **BENP: might want to change the image in case this URL changes**

Now we can take our URL back to the target, paste it into the first input on the form, and put some caption in the second input (maybe "UChicago Campus"). For the last input on the form, "Owner ID", if you put in a user ID that doesn't exist, like "1", then it's not going to add the photo to the table. Why? Because we have a validation on this `Photo` model:

```ruby
# app/models/photo.rb

...
class Photo < ApplicationRecord
  validates(:poster, { :presence => true })
  
  def poster
    my_owner_id = self.owner_id

    matching_users = User.where({ :id => my_owner_id })

    the_user = matching_users.at(0)

    return the_user
  end
...
end
```

The association accessor method `poster` returns a user based on an ID. Above this method, there is a validation associated with it. This is saying that the return of `poster` (`the_user`) must be present (`{ :presence => true }`), it cannot be `nil`. **BENP: another validation aside, I see it is important now to keep the previous aside**

So if we try and use a valid "Owner ID" in our add photo form (you can check for a valid user ID in the **/users** table), then the photo will be added to the top of our **/photos** index page. Actually, the form takes us directly to the show page for that photo we just added.

We need to make this form in our app now. This is standard stuff that we've done before for form generation, but the trick now will just be getting the input to save to our database. Try to build the form out for yourself! I'll wait... **BENP: could lnk to active record and forms chapters**

Let's work on this together. We need to add a form to our **/photos** index view template:

```html
<!--- app/views/photo_templates/index.html.erb --->

<h1>List of photos</h1>

<hr>

<form>
  <input>
  <textarea></textarea>
  <input>
  <button>Add photo</button>
</form>

<hr>
...
```
{: mark_lines="5-14"}

To give ourselves a little visual space, we added `<hr>` tags, which stands for "horizontal rule", and just adds some horizontal lines to bracket the form. The rest is just the skeleton of the `<form>` we want with two `<input>`s (no closing tag required), one `<textarea>`, and a `<button>`.

Let's add some labels (and some code spacing for readability) to the inputs:

```html
<!--- app/views/photo_templates/index.html.erb --->

...
<form>
  <label>Image</label>
  <input>

  <label>Caption</label>
  <textarea></textarea>

  <label>Owner ID</label>
  <input>

  <button>Add photo</button>
</form>
...
```
{: mark_lines="5 8 11"}

We also need to make sure that we tie each label to an input to make the form valid usign `for=` and `id=`:

```html
<!--- app/views/photo_templates/index.html.erb --->

...
<form>
  <label for="image_box">Image</label>
  <input id="image_box">

  <label for="caption_box">Caption</label>
  <textarea id="caption_box"></textarea>

  <label for="owner_id_box">Owner ID</label>
  <input id="owner_id_box">

  <button>Add photo</button>
</form>
...
```
{: mark_lines="5-6 8-9 11-12"}

If we refresh **/photos**, we will see that cosmetically the from is already looking good. But it won't do anything yet. When I click on "Add photo", I want the form to have an action that points to a new URL, and that URL should call an action that actually takes the input to the form and adds a record to the database. 

So we need to add an `action=""` with a URL, and we also need to add a `name` for each form input, which will go into our query string:

```html
<!--- app/views/photo_templates/index.html.erb --->

...
<form action="/insert_photo">
  <label for="image_box">Image</label>
  <input id="image_box" name="query_image">

  <label for="caption_box">Caption</label>
  <textarea id="caption_box" name="query_caption" ></textarea>

  <label for="owner_id_box">Owner ID</label>
  <input id="owner_id_box" name="query_owner_id">

  <button>Add photo</button>
</form>
...
```
{: mark_lines="4 6 9 12"}

Now if you put some input into the form and click "Add button", then you will be routed to a new URL that begins with **/insert_photo?**, and has all of your named inputs (`query_`) and values following the **?**. 

So everything we typed is saved in the query string, and that means it was sent to the `params` hash, which we can access in our back-end action.

We could also add additional attributes to the `<input>` and `<textarea>`, like `placeholder=""` or `type=""`, but that's up to you. For now the form is functional.

Our new URL is getting the "no route matches" error, because we still need to define the route and make the action:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })
  get("/users", { :controller => "users", :action => "index" })
  get("/users/:path_username", { :controller => "users", :action => "show" })
  get("/photos", { :controller => "photos", :action => "index" })
  get("/photos/:path_id", { :controller => "photos", :action => "show" })
  get("/delete_photo/:path_id", { :controller => "photos", :action => "delete" }))
  get("/insert_photo", { :controller => "photos", :action => "create" }))

end
```
{: mark_lines="11"}

And let's also define this action that will create the record and redirect the user to the new show page of that photo. At first I'm just going to make a view template to get the action working and rendering some new HTML:

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  ...
  def create

    render({ :template => "photo_templates/create.html.erb" })
  end
end
```
{: mark_lines="5-8"}

Once we get that page to say "hi" after we click on the "Add photo" button on our new, filled-out form, then we can return to the action and get it to do what we actually want. First we need to go into `params` and pull out the input from our query string:

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  ...
  def create
    input_image = params.fetch("query_image")
    input_caption = params.fetch("query_caption")
    input_owner_id = params.fetch("query_owner_id")

    render({ :template => "photo_templates/create.html.erb" })
  end
end
```
{: mark_lines="6-8"}

So how can we save this information into our database? We just need to create a new `Photo` instance, fill in the attributes, and `.save` it to issue the SQL and add the record to our table:

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  ...
  def create
    input_image = params.fetch("query_image")
    input_caption = params.fetch("query_caption")
    input_owner_id = params.fetch("query_owner_id")
    
    new_photo = Photo.new
    new_photo.image = input_image
    new_photo.caption = input_caption
    new_photo.owner_id = input_owner_id
    new_photo.save

    render({ :template => "photo_templates/create.html.erb" })
  end
end
```
{: mark_lines="10-14"}

We can already try and re-submit the form on **/photos**, and we should be brought again to the `create.html.erb` template that is just saying "hi". It's hard to tell that anything was added to our database, but if we go to our GitPod terminal where `bin/server` is running and look in the log, then we will see the SQL telling us that our photo was saved. 

And the new photo was even assigned a unique photo ID that we can use to go directly to (`redirect_to`) the show page of our new photo:

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  ...
  def create
    input_image = params.fetch("query_image")
    input_caption = params.fetch("query_caption")
    input_owner_id = params.fetch("query_owner_id")
    
    new_photo = Photo.new
    new_photo.image = input_image
    new_photo.caption = input_caption
    new_photo.owner_id = input_owner_id
    new_photo.save

    # render({ :template => "photo_templates/create.html.erb" })
    redirect_to("/photos/" + new_photo.id.to_s)
  end
end
```
{: mark_lines="16-17"}

Try and add some new URLs to the form on your own and watch it work!

Time to **/git** commit.



### Text Companion: Create Photo Form

## Video Segment: Update Photo Form

- Notes:

  - time stamp 01:36:27 to 01:50:56
  - moving to the U in CRUD
  - build up form in `app/views/photo_templates/show.html.erb`
  - RCAV `action="/update_photo/<%= @the_photo.id %>"` with action `update`
  - fetch `params` from path, `.save` to database

One last thing to do! We did read, we did delete, and we now did create. So it's time to add an update form to our photo page. Right now we should have:

```html
<!--- app/views/photo_templates/show.html.erb --->

<h1>Photo Details</h1>

<dl>
  <dt>Image</dt>
  <dd><img src="<%= @the_photo.image %>"></dd>

  <dt>Caption</dt>
  <dd><%= @the_photo.caption %></dd>

  <dt>Owner</dt>
  <dd><%= @the_photo.poster.username %></dd>

  <dt>Posted</dt>
  <dd><%= @the_photo.created_at %></dd>
  
  <dt>Edit photo</dt>
  <dd>Form goes here</dd>

  <dt>Delete photo</dt>
  <dd><a href="/delete_photo/<%= @the_photo.id %>">Delete this photo</a></dd>
</dl>
...
```

So everything is working, but we need to zoom in on the `<dd>Form goes here</dd>` tag and place a form for updating the photo right there.

We can go to a photo details page in our [target](https://photogram-gui.matchthetarget.com/photos/777){:target="_blank"} and save some time by just viewing the page source (right click, "View source"), then copy-pasting the relevant form into our own view template:

```html
<!--- app/views/photo_templates/show.html.erb --->

...
  <dt>Edit photo</dt>
  <dd>
    <form action="/update_photo/777">
      <label for="browser_image">Image</label>
      <input id="browser_image" type="text" name="input_image" placeholder="Enter a URL for the image..." value="https://robohash.org/dolorehicincidunt.png?size=300x300&amp;set=set1">

      <label for="browser_caption">Caption</label>
      <textarea id="browser_caption" name="input_caption" placeholder="Enter a caption for the photo...">Once you’ve accepted your flaws, no one can use them against you.</textarea>

      <button>Update photo</button>
    </form>
  </dd>
...
```
{: mark_lines="5-15"}

Now, back in our app, if we visit a photo details page and try to click the "Update photo" link, then we will get a "no route matches" error, because we haven't defined the `action="/update_photo/777"`, or made it dynamic to change the photo ID in the second segment. 

Also, we see that there is pre-populated input to the form "Image" and "Caption" fields. These are data taken from our database for whatever image matches the current photo ID (`777` in our example). 

The "Image" field is pre-populated with the `value=""` attribute to `<input>`, whereas "Caption" is just pre-populated by placing data between the `<textarea></textarea>` tags. (A weird, archaic HTML inconsistency, since `<textarea>` doesn't have a `value=""` attribute available.) This pre-population also needs to be made dynamic, with information taken from the current photo page that we are on.

Let's do all of that using the embedded Ruby tags and instance variables that we have access to on this page! While we're at it, we will also rename the copy-pasted `name` attributes after our previous convention using a leading `query_` rather than `input_`:

```html
<!--- app/views/photo_templates/show.html.erb --->

...
  <dt>Edit photo</dt>
  <dd>
    <form action="/update_photo/<%= @the_photo.id %>">
      <label for="browser_image">Image</label>
      <input id="browser_image" type="text" name="query_image" placeholder="Enter a URL for the image..." value="<%= @the_photo.image %>">

      <label for="browser_caption">Caption</label>
      <textarea id="browser_caption" name="query_caption" placeholder="Enter a caption for the photo..."><%= @the_photo.caption %></textarea>

      <button>Update photo</button>
    </form>
  </dd>
...
```
{: mark_lines="6 8 11"}

Refresh a photo details page in your app, and try to visit other photos as well. You will see the form content dynamically updating on each page.

Okay, now we can try to fill out a form, maybe by just changing any given caption to "Caption Updated" in the "Caption" field of the form on one of the photo details pages. And when you click "Update photo", you still get "no route matches", but at least you get inputs in the **?** query string in the new URL. 

Let's RCAV it:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })
  get("/users", { :controller => "users", :action => "index" })
  get("/users/:path_username", { :controller => "users", :action => "show" })
  get("/photos", { :controller => "photos", :action => "index" })
  get("/photos/:path_id", { :controller => "photos", :action => "show" })
  get("/delete_photo/:path_id", { :controller => "photos", :action => "delete" }))
  get("/insert_photo", { :controller => "photos", :action => "create" }))
  get("/update_photo/:path_id", { :controller => "photos", :action => "update" }))

end
```
{: mark_lines="12"}

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  ...
  def update

    render({ :template => "photo_templates/update.html.erb" })
  end
end
```
{: mark_lines="5-8"}

And once we get the form to say "hi" (put that in `app/views/photo_templates/update.html.erb`), we can get the action to do what we want.

First we get the parameters of interest out of the hash, then we find the matching photo with the given ID (part of our dynamic path!), then we update the photo in our database using the form input that we pull from the query string. Additionally, rather than rendering, we will redirect the form back to the current photo page so we can see the update:

**BENP: at 01:46:00, there is a kinda confusing aside about check boxes and false argument to fetch.. leaving this out**

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
  ...
  def update
    the_id = params.fetch("path_id")
    the_photo = Photo.where({ :id => the_id }).first

    image = params.fetch("query_image")
    caption = params.fetch("query_caption")
    the_photo.caption = caption
    the_photo.image = image
    the_photo.save
    
    # render({ :template => "photo_templates/update.html.erb" })
    redirect_to("/photos/" + the_photo.id.to_s)
  end
end
```
{: mark_lines="6-16"}

Try and update some captions on your photos. If you see everything working as you expect, then you can do a `rails grade` to check your work, and a **/git** commit.

You can now CRUD!

The remaining tasks you see on the `rails grade` results page are up to you to complete.

### Text Companion: Update Photo Form

## Finish and Submit Photogram GUI

- Notes:

  - Copied from README at [https://github.com/appdev-projects/photogram-gui#readme](https://github.com/appdev-projects/photogram-gui#readme){:target="_blank"}

### Tasks

The required tasks are:

 - `/users` should
    - display all the users
    - a link to get to details for each user
    - a form to add a new user
 - `/users/[USERNAME]` should
    - display the username of the user
    - the photos posted by the user
 - `/photos` should have a form to add a new photo
 - `/photos/[ID]` should
    - display the details of a photo
    - displays the comments that have been made on the photo
    - have a form to add a comment to the photo

### Workflow

 1. As often as you like, reset your database with sample data: `rails sample_data`
 2. Start the web server: `bin/server`
 3. *Always Be Committing (ABC)* at **/git**
 4. Check out your database visually at `/rails/db`
 5. Run `rails grade` as often as you like to see how you are doing, but **test whatever you're working on manually first to make sure it matches the target's behavior**. Don't debug using `rails grade`; that is a terribly slow feedback loop.

### Things to keep in mind

  - I added some _validations_, rules to try and help prevent bogus data from entering your tables, to your models. If your record is mysteriously not saving, then a validation is failing (or you just forgot to call `.save`, which I do all the time).
 - Don't be alarmed by the number of automated tests. Most of them are there as hints to help you structure your forms correctly.
 - It's okay to View Source on the target to get hints on what HTML we used.
 - When you make forms, don't forget to add a `<label>` for every form control (`<input>`, `<textarea>`, etc). The `<label>` should have a `for=""` attribute that matches the `id=""` attribute of the input. For example,

    ```html
    <label for="zebra">Fan</label>
    <input id="zebra" type="text" name="qs_fan_id">
    ```