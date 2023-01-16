# Very Best Debug

- Notes:

  - [Day 7 video](https://uchicago.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=6da49302-4503-454a-9659-aedf005f678f){target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/very-best-debug-video.md){target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/very-best-debug](https://github.com/appdev-projects/very-best-debug){target="_blank"}

  - Target: [https://very-best-debug.matchthetarget.com/](https://very-best-debug.matchthetarget.com/){target="_blank"}


**BENP: Right now there is a starting from scratch tutorial including draft generators in Day 7 recording from 00:30:00 to 00:50:20. I am not transcribing this yet but can come back for it! See my note in [Video Segment: Homepage Debugging][Video Segment: Homepage Debugging] in this lesson. This probably needs a dedicated video and to be zipped with the starting from scratch and draft:generator chapters.**


## Video Segment: Homepage Debugging

-Notes:

  - time stamp 00:02:03 to 00:04:03
  - RTEM to slowly debug **/**
  - `better_errors` page console aside (da="Explain")

When we open our app in a GitPod browser with `bin/server`, right away on the **/** homepage, we are greeted with an error:

```
The action 'home' could not be found for UsersController
```

This project is bringing together everything you learned so far in the service of debugging: HTML, Ruby, RCAV, `params`, instance variables, view templates, `.each` in the view templates, `ActiveRecord` for databases, etc.

So for the first error I will start by looking at the route in `config/routes.rb` and see if I can trace the source of the problem:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "home" })
  get("/users", { :controller => "users", :action => "all_users" })
  get("/users/:username", { :controller => "user", :action => "show" })
  get("/insert_user_record", { :controller => "venues", :action => "create" })
  get("/update_users/:user_id", { :controller => "users", :action => "update" })
  
  ...
 
end
```
{: mark_lines="5"}

We see the route `"/"` that we are interested in fixing, and the error message was telling us that the `"home"` action could not be found in our `"users"` controller. Let's look at this controller:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController

  def index
    ...
  end
  
  def show
    ...
  end
  
  def create
    ...
  end
  
  def update
    ...
  end

end
```

And we see there is no `home` action defined in our controller. Hence the error message. 

Let's look at the [target](https://very-best-debug.matchthetarget.com/){target="_blank"} homepage at the URL path **/**. What is the behavior? It looks like this is just a list of users. And what's the conventional name for an action that just lists things in a Rails app? `index`! Back to our controller:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController

  def index
    matching_users = User.all
    @users = matching_users.order(:created_at)

    render({ :template => "users_templates/all_users.html.erb"})
  end
  ...

end
```
{: mark_lines="5-10"}

The first action is the one we want. It returns of an array-like object of all users from the database. Easy fix here is to just go back to our routes and change the name of the action to match our controller:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })
  get("/users", { :controller => "users", :action => "all_users" })
  get("/users/:username", { :controller => "user", :action => "show" })
  get("/insert_user_record", { :controller => "venues", :action => "create" })
  get("/update_users/:user_id", { :controller => "users", :action => "update" })
  
  ...
 
end
```
{: mark_lines="5"}

Now back in your app browser, refresh **/**. The missing action error goes away, but we get a new one:

```
Missing template users_templates/all_users.html.erb
```

**BENP: `better_errors` Page and Starting a New Project, 00:04:03 to 00:06:55. This error page could be introduced elsewhere, earlier in the class**

I want to point out the error page in our Rails app. We see the error message, but we also see that the specific line of code in our codebase that is causing the error is also shown. 

I want to emphasize, in this `better_errors` page, which is a third-party gem that does not come by default with Rails, there is a super useful REPL (Rails console) below the highlighted code error. If you ever need to, you can look at any instance variables or `params` right from this terminal. 

The REPL is frozen in time right where that error occurred. So it's a very useful playground for you find a solution and debug right on this page before you go and change things in the codebase.

We have added a lot of third-party gems like this to our Rails app to improve the development experience. When you want to start projects in the future... 

**BENP: this part of the video is just a live walk through of `starting-a-rails-project-from-scratch.md` (https://chapters.firstdraft.com/chapters/851). It was prompted by a student question. Could just copy-paste from there.. or put this whole section elsewhere. NOTE, right now there is a starting from scratch tutorial including draft generators in Day 7 recording from 00:30:00 to 00:50:20. I am not transcribing this yet but can come back for it!**

Back to the current error message on **/**:

```
Missing template users_templates/all_users.html.erb
```

Let's look in our folder on GitPod for this file. We see right away when we take a look for it that the folder is called `user_templates/`, whereas we have in our action `users_templates/`, with an extra `s` after `user`. 

We could change the foldername, or we could change the path for the rendered template in our action. So far our convention has been to use the singular name of the record, so we will change the `index` action to `render({ :template => "user_templates/all_users.html.erb"})`. 

Now when we refresh **/** in our app's browser, the page loads without an error. If for some reason you still have an error on the page, you may need to close down the server terminal, and restart it. This is just a bug in GitPod **BENP: is this still a bug?**.

And remember, the database in our new app is empty, so that's why you may not see any records in your "List of users". We need to run `rails sample_data` in a terminal on GitPod to get some toy data.

**BENP: 00:08:30 to 00:10:55 had to deal with project bug, showing that `faker` is missing from the gem file. Maybe too advanced to show to class? At this point you go into all this stuff about the GEM file and `bundle install`.**

The rest of the debugging is up to you, here are some things to keep in mind **BENP: just copy pasted these from README. Probably can be integrated in text**:

  1. [**READ THE ERROR MESSAGE**](https://chapters.firstdraft.com/chapters/754#read-the-error-message-rtem)
  1. When you understand the error message, work to figure out a solution to fix the error so the Route/Controller/Action/View functions like the target.
  1. Remember that the error will guide you to the bug and our skills as developers are determined by how many bugs we understand how to fix
  1. Refer to the [routing chapter](https://chapters.firstdraft.com/chapters/772) if you are stuck on the RCAV
  1. Once you have `/users` working correctly, check the routes file and get each working the same as the target


**BENP: from here on there is the Very Best Debugging solutions, done interactively with class input**

  
### Text Companion: Homepage Debugging

## Video Segment: Typos and `NilClass` Bug

-Notes:

  - time stamp 00:11:35 to 00:17:47
  - RTEM to slowly debug **/venues/[ID of venue]**
  - tricky bug: `undefined method 'address' for nil:NilClass` 
  - `ActiveRecord::Relation` single instance `.at(0)`

In our app, let's try to manually navigate to **/venues/1**. We are trying to get to a venue details page, like in our target. We get a "no route matches" error. 

Based on the developer conventions from the Rails community, we were expecting the list of things we are interested in (the `index` action) to be on a URL with the plural name of the thing of interest, in this case **/venues**. Also, for the individual venue, it is typical to put the details page at **/venues/[ID of venue]**. In this case, we tried to get to the details page of the venue from our `venues` table with the `id` column value of "1".

We could have named these routes anything we want, like **/venue_details**. But we don't because it is usually good to follow conventions.

Back to the error, let's check our route:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })
  get("/users", { :controller => "users", :action => "all_users" })
  get("/users/:username", { :controller => "user", :action => "show" })
  get("/insert_user_record", { :controller => "venues", :action => "create" })
  get("/update_users/:user_id", { :controller => "users", :action => "update" })

  get("/venues", { :controller => "venues", :action => "index" })
  get("/insert_venue_record", { :controller => "venues", :action => "create" })
  get("/venue/:an_id", { :controller => "venue", :action => "show" })
  post("/update_venue/:the_id", { :controller => "application", :action => "update" })
  get("/delete_venue/:id_to_delete", { :controller => "venue", :action => "destroy" })
  
  get("/insert_comment_record", { :controller => "comments", :action => "create" })
 
end
```
{: mark_lines="13"}

Right away, we can spot that the path *and* controller `"venue"` should say `"venues"` to match the controller file `app/controllers/venues_controller.rb`, which is, again by convention, the plural `snake_case` name of the table. Change these both to `"venues"`, and refresh **/venues/1**. A new error:

```
param is missing or the value is empty: venue_id
```

In the error page, we see the highlighted code is in the `app/controllers/venue_controllers.rb` file in the `show` action in the first line:

```ruby
# app/controllers/venue_controllers.rb

class VenuesController < ApplicationController
  ...
  def show
    venue_id = params.fetch("venue_id")
    matching_venues = Venue.where({ :id => venue_id })
    the_venue = matching_venues

    render({ :template => "venue_templates/details.html.erb" })
  end
  ...
end
```
{: mark_lines="6"}

On the error page you can also note that I have the "Request Info" section of the page, where it actually shows me my "Request parameters" hash. We see that in our action we are trying to look up the `venue_id` from `params`, but in our `params` hash (which we can also have a look at in the error page REPL), we have this key as `an_id`. This is the name we gave it up in our `config/routes.rb` file, so we can change the name there *or* in the action:

```ruby
# app/controllers/venue_controllers.rb

class VenuesController < ApplicationController
  ...
  def show
    venue_id = params.fetch("an_id")
    matching_venues = Venue.where({ :id => venue_id })
    the_venue = matching_venues

    render({ :template => "venue_templates/details.html.erb" })
  end
  ...
end
```
{: mark_lines="6"}

And once we have the correct parameter, we can refresh **/venues/1**, and get another error:

```
undefined method `address' for nil:NilClass
```

It is common to stop after you get to undefined method and go searching for this missing method. But you need to **Read The *whole* Error Message**. We can see that the highlighted code where the error occurred is in `views/venue_templates/details.html.erb` where we try and do `@the_venue.address`. The problem is that we are calling `.address` *on* a `nil` object. What is the `nil` object? `@the_venue`!

In our error page REPL, if we type `>> @the_venue`, indeed we will see the return `=> nil`. We expected an instance of `Venue` from our `venues` table here.

Let's start by looking at our show action above. We are taking an ID from the path (here "1"): `venue_id = params.fetch("an_id")`. Then we are looking up the matching venues from the table: `matching_venues = Venue.where({ :id => venue_id })`. 

We can see how this looks by going back to our error page REPL and entering `>> Venue.where({ :id => 1 })`. And we will see that this returns an `ActiveRecord::Relation` with one venue in it.

Now we want to get just the first venue, because we only want one result and we don't want the full array-like `ActiveRecord::Relation`. Right away we see the two errors: we need to call `.at(0)` or `.first`, and we also need to make the action variable an instance variable so we can access it in our view template:

```ruby
# app/controllers/venue_controllers.rb

class VenuesController < ApplicationController
  ...
  def show
    venue_id = params.fetch("an_id")
    matching_venues = Venue.where({ :id => venue_id })
    @the_venue = matching_venues.at(0)

    render({ :template => "venue_templates/details.html.erb" })
  end
  ...
end
```
{: mark_lines="8"}

This was tricky, because with instance variables in Ruby, there is no error if the instance variable doesn't exist. It just returns a `nil` object. Then when we try and call our defined methods on that object, we begin to get error messages. But the error is not with the methods, but rather with the object they are being called on.

If we refresh **/venues/1** and get another error message:

```
undefined method `address' for #<Venue:ActiveRecord_Relation:...>
```

again, don't stop reading after `undefined method 'address'`. We can now see that the venue object is being returned, so that's good. But the `.address` is undefined. But that's because we are not returning a single instance of `Venue`, we are getting an `ActiveRecord::Relation` **BENP: okay, I have been writing :: everywhere, but in the error message it is _, which is correct?**. That means we are trying to call `.address` on an array-like object, and we forgot the `.at(0)` in our `show` action above.


  
### Text Companion: Typos and `NilClass` Bug

## Video Segment: Association Accessor `self.id` Bug

-Notes:

  - time stamp 00:17:47 to 00:28:35
  - RTEM to continue debugging **/venues/[ID of venue]**
  - tricky bug: `self.id` in `Comment#commenter`, rather than `self.author_id`

Now, assuming the `show` bugs have been dealt with, if we refresh **/venues/1**, then we get the error:

```
undefined method `username' for nil:NilClass
```

And we see the highlighted code in the view template is coming where we try to call `comment.commenter.username`. 

From our experience, we know that the `comment.commenter` is somehow `nil`. Above this, we see that we are calling `.comments` on our `@the_venue` object in order to get a list of comments for looping over and displaying: `@the_venue.comments.each do |comment|`.

Because the `.each` call didn't throw an error, we can assume that the `.comments` method is returning an array-like object `ActiveRecord::Relation` of the comments associated with that venue ID. But inside of this loop, the `comment`, or the `.commenter` method called on it, is `nil`.

Let's check in our error page REPL. We can start with just `>> @the_venue`, which should return our instance of `Venue`. Then we can try `>> @the_venue.comments`, which should return an array-like object full of comments that match the venue. Good. 

But where is this `.comments` method from? It is in the model! Any method that we call on a class from our database is defined in the class file. Let's go look at that First, in order to get from a `Venue` to a `Comment`, we can look at the `Comment` model to remind us of the names of the columns:

```ruby
# app/models/comment.rb

# == Schema Information
#
# Table name: comments
#
#  id         :integer          not null, primary key
#  body       :string
#  created_at :datetime         not null
#  updated_at :datetime         not null
#  author_id  :integer
#  venue_id   :integer
#
...
```
{: mark_lines="12"}

In the `# == Schema Information` we see there is a foreign key column called `venue_id`. So we want to find all of the comments where ID in this column matches my current venue of interest. In the `Venue` model, we find:

```ruby
# app/models/venue.rb

# == Schema Information
#
# Table name: venues
#
#  id           :integer          not null, primary key
#  address      :string
#  name         :string
#  neighborhood :string
#  created_at   :datetime         not null
#  updated_at   :datetime         not null
#

class Venue < ApplicationRecord

  def comments
    my_id = self.id
    matching_comments = Comment.where({ :venue_id => my_id })
    return matching_comments
  end
end
```
{: mark_lines="17-21"}

This `comments` method in an association accessor method. It first says, get the current venue ID (our `@the_venue` instance variable) using the `self.id` call. It then searches the `venue_id` column of the `Comment` model (which accesses the `comments` table) for my current ID, and then it returns all of these matching rows.

So it looks like in our view template the `comments` method should be doing the right thing. And we saw this was the case in our error page REPL when we typed `>> @the_venue.comments`. It returned an array-like object full of comments that match the venue.

That brings us to the block variable `comment` in our `.each` loop. At the error page REPL, type `>> comment`. Indeed a single `Comment` object is return, which is a row from the table `comments` in our database.

Now at the REPL try: `>> comment.commenter`. It gives us `=> nil`! 

How could we replace our code and manually traverse from the comment to the username associated with that comment? If we look at our `Comment` instance, we can see there is a foreign key column called `author_id` with a value of "96". This is the key that we can use in `User` to look up which user authored a given comment. 

To write this out: `User.where({ :id => 96 })`. Then we can `.at(0)` and `.username` on that to get the name we want. At the REPL: `>> User.where({ :id => 96 }).at(0).username` should return `=> "jolie"` **BENP: are the returns consistent with faker? will it always be "jolie"**. 

So this does work. We can traverse manually to get the username, and `comment.commenter` is not failing and returning `nil` because there is no username. **This is something you need to start to consider. There may be entries that *do* have `nil` values in a given column. Some bugs can be caused by invalid data and not problems in our code.**

However, here we saw the bug was not caused by invalid data. That means we need to go look in the `Comment` model at the `.commenter` method:

```ruby
# app/models/comment.rb

# == Schema Information
#
# Table name: comments
#
#  id         :integer          not null, primary key
#  body       :string
#  created_at :datetime         not null
#  updated_at :datetime         not null
#  author_id  :integer
#  venue_id   :integer
#

class Comment < ApplicationRecord
  def commenter
    my_id = self.id
    matching_users = User.where({ :id => my_id })
    the_user = matching_users.at(0)
    return the_user
  end
end
```
{: mark_lines="16-21"}

**BENP: on https://github.com/appdev-projects/very-best-debug/blob/master/app/models/comment.rb the line already is corrected and says `my_id = self.author_id`. I changed it above to match the video**

We are taking the `self.id`! But what we want is the `author_id` foreign key column *not* the primary key of the given comment. So change the line to `my_id = self.author_id`, and refresh **/venues/1** once more in our browser. It works!
  
### Text Companion: Association Accessor `self.id` Bug

## Finish and Submit Very Best Debug

-Notes:

  - below copied from README: https://github.com/appdev-projects/very-best-debug#readme

### Standard Workflow

  1. The goal of this assignment is to make the code work by correcting all of the bugs that are contained within
  1. Checkout the target to see how your code should function
  1. Run `rails sample_data` to populate your database
  1. Start with visiting the route `/users`
  1. You will see an error message, [**READ THE ERROR MESSAGE**](https://chapters.firstdraft.com/chapters/754#read-the-error-message-rtem)
  1. When you understand the error message, work to figure out a solution to fix the error so the Route/Controller/Action/View functions like the target.
  1. Remember that the error will guide you to the bug and our skills as developers are determined by how many bugs we understand how to fix
  1. Refer to the [routing chapter](https://chapters.firstdraft.com/chapters/772) if you are stuck on the RCAV
  1. Once you have `/users` working correctly, check the routes file and get each working the same as the target
  1. Run `rails grade` once all the routes are working to see what else still does not match the target
 1. As you work, remember to navigate to `/git` and **commit often as you work.**
 1. **Be sure you test the behavior of your app manually to make sure it matches the target's behavior**. Don't use `rails grade` to debug.
