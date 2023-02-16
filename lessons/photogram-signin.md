# Photogram Signin (Intro to Authentication)

- Notes:

  - [Cookies Intro video](https://canvas.uchicago.edu/courses/41147/pages/video-photogram-signin-intro-to-authentication){:target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/photogram-signin.md){:target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/photogram-signin](https://github.com/appdev-projects/photogram-signin){:target="_blank"}

  - Target: [https://photogram-signin.matchthetarget.com/](https://photogram-signin.matchthetarget.com/){:target="_blank"}

  - Useful chapters:
    - [More ways of using cookies][More ways of using cookies]

**BENP: signin vs. sign in vs. sign-in (same for signup, signout, signon, etc.), decide and check doc for consistency**

**BENP: there are no /git commits done in the original video until around 50min when there is all of a sudden an intro to git including branching. This should have come earlier in the class, and git committing should be integrated throughout this doc as it is elsewhere**

## Video Segment: Intro and Exploring Our Starting Point

- Notes:

  - time stamp 00:00:00 to 00:02:00

For this project, we're just going to use what we learned about cookies and build an industrial-grade signin system supported by some of Rails' features. This is just being added on top of the Photogram GUI project that we already finished, so, as usual, the starting point of our app is the finishing point of that project.

Be sure to run `rails sample_data` in case your **/users** homepage is empty when you open the app browser. We're pretty familiar with the app by now, with it's list of users, list of photos, and details pages, including photo comments.

Right now, when we add a comment, we need to include a valid author ID in the form to get it to work. We're finally going to evolve this to what it should be. When a user signs up, there there will be an ID number assigned, but they won't see it, and when a user uploads a photo that photo will be associated with them by the ID numbers.

Let's start to evolve this step-by-step.

### Text Companion: Intro and Exploring Our Starting Point

## Video Segment: Storing Passwords

- Notes:

  - time stamp 00:02:00 to 00:08:39
  - migration file: `rails g migration AddPasswordDigestToUsers`
  - add `password_digest` Column to `User`
  - explore `db/migrate` and `rails db:migrate`
  - add `has_secure_password` to `app/models/user.rb` to get `.password` and `.password_confirmation`
  - `bcrypt` gem

First of all, we want to make it so that there is an actual signup page, rather than just the current "Add user" form at the top of the list of users.

What we want is for a route like **/user_sign_up** to exist. Try entering that in your app's browser, get the familiar error message, and begin debugging. But first, what do we want here?

We want this new route to display a form and for that form to have fields for username and password. Now we need a new column that will contain something related to a password. 

In our domain modeling in class, when we created this column for our `users` table, we chose to name it "password". That's a good first instinct, but it's not a good idea to store our user's passwords in plain text in our database. If our database is compromised (e.g., hacked), then anyone can see them.

What we do instead is scramble up a user's password in a deterministic way, so that we can always scramble them in the same way, but it's hard to go in the opposite direction. This is known as a *oneway hashing algorithm*. Basically, whatever the user says their password is, we don't store it, but we are able to authenticate it.

"Password digest" is the name that we choose for this scrambled-password column. So we just need to add this column to our `users` table, which already exists in our project. 

**BENP: at this point in video we use active record chapter as reference to steps**

We can add a column using our [reference](https://chapters.firstdraft.com/chapters/770#adding-or-removing-columns-from-your-table){:target="_blank"}.

First we need a migration file, just the file because we already have the model. Then we can write a method in there to add or remove a column.

At the terminal in our GitPod app, we can first do:

```
rails g migration AddPasswordDigestToUsers
```

Running that just creates a file in the `db/migrate/` GitPod workspace folder for me, and gives the file the correct name, like: `db/migrate/[TIME OF GENERATION]_add_password_digest_to_users.rb`.

The timestamp in the filename is important, because this orders the filenames correctly in the `db/migrate/` folder. Once we push this code to our production server and run `rails db:migrate`, it needs to run the migrations in order. For instance, we want the user table to be generated before we try to add a column to it!

Now we have this migration file, but we need to add our instructions on how we want to evolve the database. Let's do that:

```ruby
# db/migrate/[TIME OF GENERATION]_add_password_digest_to_users.rb

class AddPasswordDigestToUsers < ActiveRecord::Migration[6.0]
  def change
    add_column :users, :password_digest, :string
  end
end
```
{: mark_lines="5"}

The `add_column` method is saying, create a new column in the `users` table with the name `password_digest` and make this column of type `string`. We could add additional changes of adding or dropping lines on this table or others all within the `def change` method, but it's often better to keep the changes in their own respective files, with appropriate filenames.

Back at the terminal prompt, we can push our changes to the database by running:

```
rails db:migrate
```

And this command will look in the `db/migrate/` folder and see which have files have been run, and which have not been, and it will only run the latter. 

With that command, we now have added the `password_digest` column to our `app/models/user.rb` model (check the `# == Schema Information` to see the added column). Now we're ready to store a password in a secure manner.

With these steps, we have automatically added two attributes on `User`: `.password` and `.password_confirmation`. So we can call those two methods as if they were columns (even though they are not!), and Rails will make sure they match then scramble the password securely, and store them as a string in the `password_digest` column. We just need to make one addition to the model:

```ruby
# app/models/user.rb

...
class User < ApplicationRecord
  validates(:username,
            {
    :presence => true,
    :uniqueness => { :case_sensitive => false },
  })

  has_secure_password

  def comments
    ...
  end
...
end
```
{: mark_lines="11"}

This declaration in our active record model, is actually coming from the `Gemfile` in our GitPod root folder. 

We haven't discussed the `Gemfile` much **BENP: see notes in previous videos, it has been brought up a bit, might need early dedicated information**, but it's very important. It contains a list of all the libraries that our application is relying on, including Rails itself:

```ruby
# Gemfile

source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '2.7.3'

# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '~> 6.0.3', '>= 6.0.3.2'
# Use sqlite3 as the database for Active Record

# Use Puma as the app server
gem 'puma', '~> 4.1'

# Use Active Model has_secure_password
gem 'bcrypt'
...
```
{: mark_lines="9 16"}

*gem* is Ruby's name for libraries that we are borrowing from other people, `'rails'` being the motherload.

One of these gems is also called `'bcrypt'`, and that's where we're getting the `has_secure_password` method from, which automatically defines the `.password` and `.password_confirmation` methods, and scrambles the input password, *if* you have a column named `password_digest`.



### Text Companion: Storing Passwords

## Video Segment: Signup Form

- Notes:

  - time stamp 00:08:39 to 00:24:51
  - add navigation links in `app/views/layouts/application.html.erb`
  - RCAV **/user_sign_up**
  - copy and modify add user form found in `app/views/users/index.html.erb`
    - use `type="password"` inputs
  - fix `create` action to use `.password` and `.password_confirmation` before `.save`
  - control flow with `:notice` or `:alert`

Now we are ready to get **/user_sign_up** working. This is just a regular CRUD task. 

**BENP: 00:08:40 to 00:09:40 was kind of a flub, deleted this bit of transcription.**

Let's follow the usual RCAV, by first defining the route:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })

  get("/user_sign_up", { :controller => "users", :action => "new_registration_form" })
  ...
end
```
{: mark_lines=7"}

Then defining the action:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  def new_registration_form
    render({ :template => "users/signup_form.html.erb" })
  end
...
end
```
{: mark_lines="4-6"}

And get that view template doing something:

```html
<!--- app/views/users/signup_form.html.erb --->

<h1>hi</h1>
```

Once we have the page working, we're ready to add a form. Since this is the Photogram project, we actually have form that we can pull from on the `index` users action view template (`app/views/users/index.html.erb`), where we had the "Add user" form at the top of the page. 

So let's just cut (because we don't want this form here anymore!) and paste from `app/views/users/index.html.erb` into our new view template for modification:

```html
<!--- app/views/users/signup_form.html.erb --->

<h1>Sign Up</h1>

<form action="/insert_user_record">
  <label for="browser_username">Username</label>
  <input id="browser_username" type="text" name="input_username" placeholder="Enter a username...">

  <button>Sign up!</button>
</form>
```
{: mark_lines="3-10"}

This form also has an action associated with it, that is going to do exactly what we want! That's because we already designed the CRUD steps in our Photogram project. Here we want to create a user in our database, and we can see in our routes and controller file, that these steps are ready for us:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })

  get("/user_sign_up", { :controller => "users", :action => "new_registration_form" })
  
  # User routes

  # CREATE
  get("/insert_user_record", {:controller => "users", :action => "create" })
  ...
end
```
{: mark_lines="12"}

**BENP: navbar aside**

Before we go any farther, let's add a link to our view template that will get us to the signup form without needing to enter the URL. We can do this by just adding a link in our navbar in the `app/views/layouts/application.html.erb` wrapper file:

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    <nav>
      <ul>
        <li><a href="/user_sign_up">Sign Up</a></li>
        <li><a href="/users">Users</a></li>
        <li><a href="/photos">Photos</a></li>
      </ul>
    </nav>

    <%= yield %>
  </body>
</html>
```
{: mark_lines="10-16"}

**BENP: beware, the navbar comes empty in the current github project: https://github.com/appdev-projects/photogram-signin/blob/master/app/views/layouts/application.html.erb (but was already filled with some links in this video). Layout page comes up a lot below, so check all of these for consistency.**

Okay, now in our signup form we still need to modify the form to include password fields:

```html
<!--- app/views/users/signup_form.html.erb --->

<h1>Sign Up</h1>

<form action="/insert_user_record">
  <label for="browser_username">Username</label>
  <input id="browser_username" type="text" name="input_username" placeholder="Enter a username...">

  <label for="browser_password">Password</label>
  <input id="browser_password" type="password" name="input_password" placeholder="Enter a password...">

  <label for="browser_password_confirmation">Password</label>
  <input id="browser_password_confirmation" type="password" name="input_password_confirmation" placeholder="Confirm your password...">

  <button>Sign up!</button>
</form>
```
{: mark_lines="9-10 12-13"}

Note that we changed the `type=""` attribute from `"text"` to `"password"` so the user's input is hidden on screen when they fill out the form. And becasue we want the user to be sure of the hidden password, we have them confirm it in the last field.

So the **/user_sign_up** is looking like the target now, with the correct form. If we fill out the form with a new user and password, and click "Sign up!", then it should call the action `create` in the controller `users_controller.rb`, as defined by the `action="/insert_user_record"` route.

This action looks like:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  ...
  def create
    user = User.new

    user.username = params.fetch("input_username")

    user.save

    redirect_to("/users/#{user.username}")
  end
...
end
```

We instantiate a new record, fill in the username, then save the record. We are missing a password here! But does the form work as it is and add a username to the database anyway?

Clear the server log in the terminal running `bin/server`, try to create a new user and password, and click "Sign up!".  

We get an error! We do end up on the details pages at least **/users/[NEW USER]**, but I get the error:

```
undefined method `username' for nil:NilClass
```

And this error was occurring when, in the user details view template, we got to: `<h1><%= @user.username %></h1>`. So `@user` is `nil`, which means that in the `show` action when we looked up a username like: `User.where({ :username => the_username }).at(0)`, I got nothing back, because there is no user in my database with the username in in the second segment of our path!

In other words, the new user is *not* being added to the database with our sign up form. The validation failed, and if we look in the `app/controllers/users_controller.rb` file, then we see the only validation is for a `username` being `present` and unique. But we also put in the `has_secure_password` declaration. And this is the line that is preventing the user from being added without a password! Let's fix our `create` action.

The `.save` method returns `true` (if it worked) or `false` (if it didn't), so we can store that in a variable and use it to decide the next step in a conditional. To give the user more information about what is going on, we can also use the `notice` and `alert` feature, as a second argument to `redirect_to`. Remember, when the save doesn't work there is the collection called `user.errors.full_messages`, which is an array containing everything that went wrong. **BENP: when was notice and alert introduced? Could link to [Flash messages][Flash messages]**

But, most importantly, we need to assign a password field to our new user with our new `User` methods `.password` and `.password_confirmation`:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  ...
  def create
    user = User.new

    user.username = params.fetch("input_username")
    user.password = params.fetch("input_password")
    user.password_confirmation = params.fetch("input_password_confirmation")

    save_status = user.save

    if save_status == true
      redirect_to("/users/#{user.username}", { :notice => "Welcome, #{user.username}!"})
    else
      redirect_to("/user_sign_up", { :alert => user.errors.full_messages.to_sentence })
    end
  end
...
end
```
{: mark_lines="9-10 12 14-18"}

Remember `.password` and `.password_confirmation` are *not* columns in our table (we only added `password_digest`). Again, this is because of `has_secure_password` is doing all of the work of adding these attributes but keeping them hidden and safe (thanks to the `bcrypt` gem).

Now, if the save doesn't work the user will be redirected back to the form, and if it does work the user will be shown a confirmation message. Before testing, we need to add the `notice` and `alert` messages to our show and signup pages (where they are sent):

```html
<!--- app/views/users/show.html.erb --->

<div>
  <%= notice %>
</div>

<h1><%= @user.username %></h1>
...
```
{: mark_lines="3-5"}

```html
<!--- app/views/users/signup_form.html.erb --->

<div>
  <%= alert %>
</div>

<h1>Sign Up</h1>
...
```
{: mark_lines="3-5"}

With all of this done, we can visit **/user_sign_up** (you can also use the link in our navbar to get there), and test add some new users. 

Try to add the user with a valid password (takes you to the user details page with the welcome message), and without a valid password (you stay on the form and get an error message detailing what you did wrong). 

It looks like everything is working!



### Text Companion: Signup Form

## Video Segment: Notices and Alerts

- Notes:

  - time stamp 00:24:51 to 00:30:21
  - add `notice` and `alert` to `app/views/layouts/application.html.erb`
  - use `if ... present?` control flow and style green and red

Generally speaking, on every page in the application we are going to want to have the option of showing notices and alerts, so let's just remove those from the show and signup view templates and put them in my application layout view template:

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    <nav>
      ...
    </nav>

    <div>
      <%= notice %>
    </div>

    <div>
      <%= alert %>
    </div>

    <%= yield %>
  </body>
</html>
```
{: mark_lines="14-20"}

Now these `alert` and `notice` messages will appear on any page. Maybe we want to style them a bit though, to make them somewhat more prominent with red and green boxes and text:

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    <nav>
      ...
    </nav>

    <div style="border: thin green solid; color: green;">
      <%= notice %>
    </div>

    <div style="border: thin red solid; color: red;">
      <%= alert %>
    </div>

    <%= yield %>
  </body>
</html>
```
{: mark_lines="14 18"}

But if we try to use our pages now, we will see the empty box appearing even when ther is not message. So we need to further modify the code to only show the box *if* a notice or alert is `present`: 

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    <nav>
      ...
    </nav>

    <% if notice.present? %>
      <div style="border: thin green solid; color: green;">
        <%= notice %>
      </div>
    <% end %>

    <% if alert.present? %>
      <div style="border: thin red solid; color: red;">
        <%= alert %>
      </div>
    <% end %>

    <%= yield %>
  </body>
</html>
```
{: mark_lines="14 18 20 24"}

This type of conditional is something you write a lot of in your view templates, so get used to it! Once you have a user, you need conditionals to show or not show them content based on who they are and what their privilege levels are.

We are using `.present?`, which is similar to other ways of doing this, like writing `!= nil`. But `.present` is smarter, because it will look for other versions of missing information besides just `nil`.

**BENP: there is a bootstrap aside here at 00:28:39, but I think this should be left out at this point. Bootstrap is the end of the course!**



### Text Companion: Notices and Alerts

## Video Segment: Signout with `reset_session`

- Notes:

  - time stamp 00:30:21 to 00:34:03
  - add `session.store(:user_id, user.id)` to `create` action
  - RCAV **/user_sign_out** with `reset_session` in `toast_cookies` action

Now that we have our user signed up, we should also allow them to signin. That means we should set the cookie. Back in my action, if the user did successfuly sign up, then let's add a cookie:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  ...
  def create
    user = User.new

    user.username = params.fetch("input_username")
    user.password = params.fetch("input_password")
    user.password_confirmation = params.fetch("input_password_confirmation")

    save_status = user.save

    if save_status == true
      session.store(:user_id, user.id)
      redirect_to("/users/#{user.username}", { :notice => "Welcome, #{user.username}!"})
    else
      redirect_to("/user_sign_up", { :alert => user.errors.full_messages.to_sentence })
    end
  end
...
end
```
{: mark_lines="15"}

Note that we are using `session`, rather than `cookies`. These are simliar but `session` is more secure, and you can read about it [here](https://chapters.firstdraft.com/chapters/850){:target="_blank"}. 

We use the conventional name for the cookie key, which is `user_id`, and we assign this key our value of the current `user.id`. This ID number was assigned as soon as we saved the user to the database with `.save` above.

We can print this new ID number in our layout view template with some embedded Ruby like `<%= session.fetch(:user_id) %>`, and if we navigate around the site after we signup a new user, we should see the current user ID follow us around on every page. So that works! 

We also want to give the user a way to signin later. But first, let's make a "Sign out" link. Let's add this to our navbar:

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    <nav>
      <ul>
        <li><a href="/user_sign_up">Sign Up</a></li>
        <li><a href="/user_sign_out">Sign Out</a></li>
        <li><a href="/users">Users</a></li>
        <li><a href="/photos">Photos</a></li>
      </ul>
    </nav>
    ...

    <%= yield %>
  </body>
</html>
```
{: mark_lines="13"}

This route `"/user_sign_out"` just needs an RCAV that will remove all the cookies.

We can add this route:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })

  get("/user_sign_up", { :controller => "users", :action => "new_registration_form" })
  get("/user_sign_out", { :controller => "users", :action => "toast_cookies" })
  
  # User routes

  # CREATE
  get("/insert_user_record", {:controller => "users", :action => "create" })
  ...
end
```
{: mark_lines="8"}

Then add this action:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  def toast_cookies
    reset_session
    redirect_to("/", { :notice => "See ya later!" })
  end
...
end
```
{: mark_lines="4-7"}

We get the method `reset_session` from Rails, and it just deletes all the cookies in the current session. And we are just having our action redirect the user to the homepage when they signout, and giving them a success notice there.

Try to refresh your app browser and click the "Sign out" link, it should work!



### Text Companion: Signout with `reset_session`

## Video Segment: Signin with `post` and `authenticate`

- Notes:

  - time stamp 00:34:03 to 00:48:28
  - RCAV **/user_sign_in** with `new_session_form` action
  - signin form with `action="/verify_credentials"` and `method="post"`
  - `authenticate` action using `user.authenticate` and control flow

Now we want to work on our URL path **/user_sign_in**. If we navigate there, we see that we need to RCAV it:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })

  get("/user_sign_up", { :controller => "users", :action => "new_registration_form" })
  get("/user_sign_out", { :controller => "users", :action => "toast_cookies" })
  get("/user_sign_in", { :controller => "users", :action => "new_session_form" })
  
  # User routes

  # CREATE
  get("/insert_user_record", {:controller => "users", :action => "create" })
  ...
end
```
{: mark_lines="9"}

We make an action to just display the signin form:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  def toast_cookies
    ...
  end

  def new_registration_form
    render({ :template => "users/signup_form.html.erb" })
  end

  def new_session_form
    render({ :template => "users/signin_form.html.erb" })
  end
...
end
```
{: mark_lines="12-14"}

And make the template:

```html
<!--- app/views/users/signin_form.html.erb --->

<h1>hi</h1>
```

Once we have the page working, we're ready to add a form. We can mostly copy-paste from the signup form, but we will need to modify it:

```html
<!--- app/views/users/signin_form.html.erb --->

<h1>Sign In</h1>

<form action="/verify_credentials">
  <label for="browser_username">Username</label>
  <input id="browser_username" type="text" name="input_username" placeholder="Enter your username...">

  <label for="browser_password">Password</label>
  <input id="browser_password" type="password" name="input_password" placeholder="Enter your password...">

  <button>Sign in!</button>
</form>
```
{: mark_lines="3-13"}

We have a new action called `"/verify_credentials"`, which is what will happen when they try to sign in. We can test the new form on our app. Enter a username and password for one of the accounts you previously added to the database, and click "Sign in!".

We are now taken to a URL that looks like: **/verify_credentials?input_username=[USERNAME]&input_password=[PASSWORD]**. That's no good! We are showing the user's secure password in the query string! 

We need to hide that by changing the form attribute `method="post"`:

```html
<!--- app/views/users/signin_form.html.erb --->

<h1>Sign In</h1>

<form action="/verify_credentials" method="post">
  ...
</form>
```
{: mark_lines="5"}

With this more advanced method, the information that we enter in the form will no longer go into a query string, and we will need to use a different route method than `get()`, as we've done. We will instead use `post()` to build the route in the form action:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  get("/", { :controller => "users", :action => "index" })

  get("/user_sign_up", { :controller => "users", :action => "new_registration_form" })
  get("/user_sign_out", { :controller => "users", :action => "toast_cookies" })
  get("/user_sign_in", { :controller => "users", :action => "new_session_form" })
  post("/verify_credentials", { :controller => "users", :action => "authenticate" })
  
  # User routes

  # CREATE
  get("/insert_user_record", {:controller => "users", :action => "create" })
  ...
end
```
{: mark_lines="10"}

The form method and the route method *must* match, or Rails won't find it. `get()` is the default form method, so we don't need to write it as the attribute. 

Now we define `"authenticate"`:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  def authenticate
    render({ :plain => "hi" })
  end
...
end
```
{: mark_lines="4-6"}

Now if we refresh **/user_sign_in**, re-enter some login information, and click the button, then we will be taken to "hi" and there will be none of the form inputs in a query string at that URL.

We need to actually make the `authenticate` action actually work now, by signing in the user (set the cookie with their ID number), *if* they put in the correct password. In pseudo-code:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  def authenticate
    # get the username from params
    # get the password from params
    
    # lookup the record from the db matching username
    # if there's no record, redirect to signin form

    # if there is a record, check to see if password matches
    # if so, set the cookie and redirect to homepage
    # if not, redirect back to sign in form

    render({ :plain => "hi" })
  end
...
end
```
{: mark_lines="5-13"}

Let's do all of that now:

```ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  def authenticate
    un = params.fetch("input_username")
    pw = params.fetch("input_password")
    
    # lookup the record from the db matching username
    user = User.where({ :username => un }).at(0)

    # if there's no record, redirect to signin form
    if user == nil
      redirect_to("/user_sign_in", { :alert => "No one by that name 'round these parts" })
    else
      # if there is a record, check to see if password matches
      if user.authenticate(pw)
        # if so, set the cookie and redirect to homepage
        session.store(:user_id, user.id)
        redirect_to("/", { :notice => "Welcome back #{user.username}!" })
      else
        # if not, redirect back to sign in form
        redirect_to("/user_sign_in", { :alert => "Nice try" })
      end
    end
  end
...
end
```
{: mark_lines="5-25"}

Because we used `has_secure_password` in out `app/models/user.rb` model, we get the awesome method `.authenticate`, which we used on our instance of `User` above to do the oneway encryption on the input password to see if it matches that user's encrypted password in the database. If the authentication passes, then `user.authenticate(pw)` returns the record, which, for the purposes of a conditional, counts as `true` ("truthy", actually), and we can use it to decide the next step.

With all this new code, try to play with the signin form now at **/user_sign_in**. Try with the right username, but wrong password, vice versa, and with no password. Finally try with everything correct. 

It should all work now!

We now have a robust signin-signout system built with Rails.

### Text Companion: Signin with `post` and `authenticate`

## Video Segment: `git` 

- Notes:

  - time stamp 00:48:28 to 00:52:09

**BENP: I am not transcribing this part of the video yet. Isn't there /git stuff way earlier in the class? Needs to be zipped with that and have its own dedicated content**

### Text Companion: `git`

## Video Segment: Remove User-Facing IDs

- Notes:

  - time stamp 00:52:09 to 00:59:53
  - put `photo.owner_id = session.fetch(:user_id)` and `comment.author_id = session.fetch(:user_id)` in backend `create` actions of add photo and add comment forms

Another thing we don't want in our app is the requirement of users to enter valid ID numbers when they want to post photos or comments, like in the "Owner ID" field in the form at the top of the **/photos** index page.

We can go into the photo index page, find that form, and modify it:

**BENP: why is this called `all_photos.html.erb` and not `index.html.erb`?**

```html
<!--- app/views/photos/all_photos.html.erb --->

<h1>List of photos</h1>

<form action="/insert_photo_record">
  <label for="browser_input">Image</label>
  <input id="browser_input" type="text" name="input_image" placeholder="Enter a URL for the image...">

  <label for="browser_caption">Caption</label>
  <textarea id="browser_caption" name="input_caption" placeholder="Enter a caption for the photo..."></textarea>

  <label for="browser_user_id">Owner ID</label>
  <input id="browser_user_id" type="text" name="input_owner_id" placeholder="Enter an ID of a User">

  <button>Add photo</button>
</form>
...
```

We could change the `type="text"` attribute to `type="hidden"` on the "Owner ID" and pre-populate the value with the current user ID. But instead, we are just going to get rid of that field entirely:

```html
<!--- app/views/photos/all_photos.html.erb --->

<h1>List of photos</h1>

<form action="/insert_photo_record">
  <label for="browser_input">Image</label>
  <input id="browser_input" type="text" name="input_image" placeholder="Enter a URL for the image...">

  <label for="browser_caption">Caption</label>
  <textarea id="browser_caption" name="input_caption" placeholder="Enter a caption for the photo..."></textarea>

  <button>Add photo</button>
</form>
...
```
{: mark_lines="11"}

And now in the backend, when the photo is submitted an the route `"/insert_photo_record"` is called, it goes to the `create` action in `app/controllers/photos_controller.rb`. We can change the user ID, which we used to fetch from the `params` hash as input to the form, to come from the cookies in the `session` hash:

```ruby
# app/controllers/photos_controller.rb

class PhotosController < ApplicationController
...
  def create
    # user_id = params.fetch("input_owner_id")
    user_id = session.fetch(:user_id)
    image = params.fetch("input_image")
    caption = params.fetch("input_caption")
    photo = Photo.new
    photo.owner_id = user_id
    photo.image = image
    photo.caption = caption
    photo.save
    redirect_to("/photos/#{photo.id}")
  end
...
end
```
{: mark_lines="6-7"}

We set this cookie when the user signed in, so it is available in *all* of our controller actions! No more need for user input of their ID prior to adding a photo. 

Try it yourself by finding a photo URL online and adding it to the table (assuming you are signed in as a Photogram user).

**BENP: 00:54:10 to 00:57:00, we are getting a lecture about git committing now... probably not necessary at this point in the class. Also going into branching off and branch names.**

We can also go through this exact same process on the "Photo ID" and "Author ID" fields in the comment section of the photo details page. Now that we have cookies, we never want to show any ID numbers from our database to the users.

**BENP: why is this called `details.html.erb` and not `show.html.erb`?**

```html
<!--- app/views/photos/details.html.erb --->

<h1>Photo Details</h1>

...
<h3>Add a new comment</h3>

<form action="/insert_comment_record">
  <label for="browser_photo_id">Photo ID</label>
  <input id="browser_photo_id" type="text" value="<%= @photo.id %>" name="input_photo_id">

  <label for="browser_author_id">Author ID</label>
  <input id="browser_author_id" type="text" name="input_author_id">

  <label for="browser_comment">Comment</label>
  <textarea id="browser_comment" name="input_body" placeholder="Enter a comment..."></textarea>

  <button>Add comment</button>
</form>
```

This isn't so bad, because at least the "Photo ID" is being pre-populated with the ID of the current photo whose page we are on, but the user shouldn't have to see it. So we can change that `type` to `"hidden"`. We still need the photo ID, because when we click "Add comment" and call the action at the end of `"/insert_comment_record"`, this ID will be added to the comment record in a foreign key column that associates comments to photos. We can also get rid of the label for this hidden input. Finally, we can also once more, remove the "Author ID" field:

```html
<!--- app/views/photos/details.html.erb --->

<h1>Photo Details</h1>

...
<h3>Add a new comment</h3>

<form action="/insert_comment_record">
  <input id="browser_photo_id" type="hidden" value="<%= @photo.id %>" name="input_photo_id">

  <label for="browser_comment">Comment</label>
  <textarea id="browser_comment" name="input_body" placeholder="Enter a comment..."></textarea>

  <button>Add comment</button>
</form>
```
{: mark_lines="9-10"}

And now we need to add this ID from our cookies into the action:

**BENP: the code in the video and the code available on github at https://github.com/appdev-projects/photogram-signin/blob/master/app/controllers/comments_controller.rb for this controller look very different**

```ruby
# app/controllers/comments_controller.rb

class CommentsController < ApplicationController
  def create
    comment = Comment.new

    # comment.author_id = params.fetch("input_author_id")
    comment.author_id = session.fetch(:user_id)
    comment.photo_id = params.fetch("input_photo_id")
    comment.body = params.fetch("input_body")

    comment.save

    redirect_to("/photos/#{comment.photo_id}")
  end
end
```
{: mark_lines="7-8"}

Now if we try to add a comment as a signed in user, it works, and there is only the one field to enter the comment.

Now that we have authentication under our belts, there is nothing left to learn for building CRUD backed applications. Everything from an AirBnB to a social network, you have all the tools!

### Text Companion: Remove User-Facing IDs

## Finish and Submit Photogram Signin
