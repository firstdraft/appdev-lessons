# Must See Movies Queries (Intro to Databases)

- Notes:

  - [Original video](https://canvas.uchicago.edu/courses/41147/pages/video-msm-queries-intro-to-databases){:target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/MSM-queries.md){:target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/msm-queries](https://github.com/appdev-projects/msm-queries){:target="_blank"}

  - Target: [https://msm-queries.matchthetarget.com/](https://msm-queries.matchthetarget.com/){:target="_blank"}

  - Useful chapters:

    - [ActiveRecord][ActiveRecord]
    - [Our own classes][Our own classes]

**BENP: MSM should be written out when possible (similar to RPS)**

## Video Segment: Recordkeeping Review, Exploring the Target

-Notes:

  - time stamp 00:00:00 to 00:04:30
  - showing Bird's Eye View Slides 72-73
  - database backed web appplication
  - explore **/directors/youngest** and **/directors/eldest**
  - explore index (tables) and show (details) pages

**BENP: Video starts with review of some Day 1 slides [01. Bird's Eye View](https://firstdraft.slides.com/raghubetina/01-birds-eye-view?token=u4vg--N6#/70). Just Slide 71 and 72.**

This is a very big day. Remember eons ago, back on Day 1, when I claimed the killer application of computing is just recordkeeping? And we spend a lot of time and effort learning how to architect database tables, and figure out what information applications have to keep track of on behalf of their users, and how to design database tables to be capable of keeping track of that information in a way that allows a database to grow in the right direction. 

Now finally after all this time, we know enough HTML, we know enough Ruby, we know about routing, we know about `params`, and we've been populating our embedded Ruby templates with information from forms (data from our users), and we've even gotten information from external APIs and populated our embedded Ruby templates with useful info from someone else's database.

Finally it's time for us to store the information that users are typing into forms in our own databases and then populate our Ruby templates with information from those database tables. Thus, we come back around on our original goal of building a *database backed web application*. 

In other words, we're going to build Software as a Service. So let's get started.

**BENP: Starting our Gitpod Workspace, 00:01:45 to 00:01:54**

[Here is the assignment](https://github.com/appdev-projects/msm-queries){:target="_blank"}. As usual:

1. Start the web server by running `bin/server`.
2. Navigate to your live application preview.
3. As you work, remember to navigate to **/git** and *Always Be Committing (ABC)*.
4. Organize your workspace tabs.
5. Run `rails grade` as often as you like to see how you are doing, but make sure you **test your app manually first** to make sure it matches the target's behavior.

**BENP: possible image(s) (better, GIFs?) of starting a workspace, opening /git, organizing tabs, noting the target favicon. But these are probably in a different chapter.**

The target for this project is [here](https://msm-queries.matchthetarget.com){:target="_blank"}. 

If we take a look at the target homepage at the path **/**, we will see the familiar movies, directors, and actors database content that we have been diagramming. We will build a simple web application that displays this data in a very straightforward manner.

There's a list of all directors and a details page for each director. About as simple as you can imagine for our first contact with a database driven web application.

We also have a page that shows just the youngest director (**/directors/youngest**) and just the eldest (**/directors/eldest**). This will give us practice on how to narrow and query our data for just specific pieces of information.

If we were to go and delete the eldest director by clicking on their name and then the "delete" link, and then come back and look at **/directors/eldest**, the page would change. So this is a live page, not just static HTML.

Also if I have **/movies**, and similarly **/actors**, what's important on a given movie page, I have the name of the director. That's not just a string in the movie table. If I were to edit that director's name, that would update on the movie page. So that is a *foreign key* being stored and we are connecting up these entities using their keys and then doing lookups to populate the pages.

Finally, if I go to the details page of a given director, at the bottom there is a "Filmography" with all the films that that person has directed. This is also being drawn dynamically. 

It doesn't look like much, but our target has all of the elements of IMDB. It isn't styled well, but we could throw some bootstrap in and make it look nice. Right now there are one-to-many and many-to-many connections, and if we throw some cookies in here for authentification sign-in and sign-out, then we would have a full application.

Moving away from the target, let's get going now in our Rails app on Gitpod. We have a lot of work to do in our application.



### Text Companion: Recordkeeping Review, Exploring the Target

## Video Segment: Exploring /rails/db

-Notes:

  - time stamp 00:04:30 to 00:08:21
  - clicking around in **/rails/db**
  - looking at tables
  - development database SQLite

How do we create a database table? How do we put data into the table? How do we get it back out? How do we get that data into controller action? How do we get it into a view template?

Here's a couple things that are going to make our job easier, the README and a chapter [ActiveRecord][ActiveRecord]. **BENP: these two items need to be zipped in to this doc**

There's also a couple of tools included in this (and every other) Gitpod Rails project:

- **http://[YOUR APP DOMAIN]/rails/info**: shows all visitable routes in the applications
- **http://[YOUR APP DOMAIN]/rails/db**: shows a visual interface for the database

These are kind of like **/git**, which we've already used. They are URL paths that are only available in development mode for our apps, but once the app is deployed to users in production mode, they won't be visible.

If we open our app browser, we can see that we do have a homepage **/** with the links for directors, movies, etc., but if we try any of the links, then we get a "no route matches" error. 

Before we do anything, navigate to **/rails/db** in the browser. You will see a really cool gem. This is not included in Rails by default, it's rather a third party gem from the community. It's a visual interface to your database:

![](assets/msm-queries/rails-db.png)

Rails includes a database out-of-the-box. This is unlike other frameworks, where you need to pick one, connect to it, etc. If you're lucky you can easily connect to it, but you still have to set it up. 

Rails includes a development database called *SQLite* (often pronounced as *Sequel Light*). **/rails/db** gives you a visual way of looking at your database. You can see on the left the four tables that I've already created for this project: `actors`, `characters`, `directors`, and `movies` **BENP: here and elsewhere below I put table names in code font**, and added the columns we are familiar with.

If you click on `actors`, you will be brought to the URL **/rails/db/tables/actors/data**, and you will see a blank table with columns *Name*, *Dob*, *Bio*, *Image*, *Created at*, and *Updated at*. These were already put together for you. In the next project you will create your own tables.

Creating your own tables is also covered in the [ActiveRecord][ActiveRecord] chapter. **BENP: probably zip this part of the chapter into the next project when it is actually relevant. At 00:07:51 in this video, there is a teaser of the commands, but this should be left out at this point.**



### Text Companion: Exploring /rails/db

## Video Segment: SQL and `ActiveRecord` Intro

-Notes:

  - time stamp 00:08:21 to 00:12:03
  - adding a record with SQL command in `directors` table at **/rails/db/sql** in the SQL Editor
  - Ruby to performant SQL with `ActiveRecord` object relational mapper
  - database transactions

Another cool thing about **/rails/db**, is that, if you happen to know *Structured Query Language (SQL)*, then you can click "SQL Editor", which will bring you to **/rails/db/sql**, where you can actually execute SQL commands.

SQL (often pronounced as *Sequel* **BENP: is that right?**), is the actual language that relational databases use.

For example, an **BENP: an or a, depends on pronounciation** SQL statement for adding a director to the `directors` table looks like:

```sql
INSERT INTO "directors" ("name", "dob", "bio", "image", "created_at", "updated_at")
VALUES ("Greta Gerwig", "1983-08-04", "Greta Celeste Gerwig /ˈɡɜːrwɪɡ/; born August 4, 1983) is an American actress and filmmaker. She first garnered attention after working on and appearing in several mumblecore films. Between 2006 and 2009, she appeared in a number of films by Joe Swanberg, some of which she co-wrote or co-directed, including Hannah Takes the Stairs 2007) and Nights and Weekends 2008).", "https://upload.wikimedia.org/wikipedia/commons/thumb/1/1c/Greta_Gerwig_Berlinale_2018.jpg/330px-Greta_Gerwig_Berlinale_2018.jpg", "2020-05-19 17:47:04.103354", "2020-05-19 17:47:04.103354")
```

SQL is a create language, though it is hard to just type out by hand. But it is very powerful. For application development, you don't really need to do it by hand anymore. I haven't actually written raw SQL for quite some time now. The Ruby library we use called `ActiveRecord` basically translates Ruby into such good SQL that it's probably better than what you would write by hand. 

If you are doing very advanced data analysis and generating reports, then you probably want to learn SQL.

If we copy, past, and "execute" (click the button) those two lines of SQL code in our "SQL Editor" on **/rails/db/sql**, then navigate to our `directors` table by clicking the link on the left side of the browser, we will see a new row (a new *record*) has been added to our previously empty table.

So the SQL statement issued a transaction with the database! 

Now this data is saved forever in my actual database on my server, which is in some sense a much more secure and safe storage space than storing cookies on my users' browser. You only get a tiny amount of storage space for cookies and the users can clear this whenever they want. Cookies are useful for uniquely identifying users (and is the only way to do that), so they are important for certain things. But for actually storing information for the long run, you need to store it yourself in a database (storage space) that you control. **BENP: this cookies aside can be dropped I think**

Fundamentally all we do to store data is issue SQL statements to the database. Now, we don't have time to learn SQL, and we really wouldn't want to anyway. We're just going to use the amazing Ruby library included with Rails called `ActiveRecord`. This allows us to just think in terms of Ruby, and classes, and instances, and just do the Ruby that we are used to (we don't need to run the below anywhere, this was already done in our SQL prompt above):

```ruby
d = Director.new
d.name = "Greta Gerwig"
d.dob = "August 4, 1983"
d.bio = "Greta Celeste Gerwig /ˈɡɜːrwɪɡ/; born August 4, 1983) is an American actress and filmmaker. She first garnered attention after working on and appearing in several mumblecore films. Between 2006 and 2009, she appeared in a number of films by Joe Swanberg, some of which she co-wrote or co-directed, including Hannah Takes the Stairs 2007) and Nights and Weekends 2008)."
d.image = "https://upload.wikimedia.org/wikipedia/commons/thumb/1/1c/Greta_Gerwig_Berlinale_2018.jpg/330px-Greta_Gerwig_Berlinale_2018.jpg"
d.save
```

Here, we use `.new` to create a new class variable instance (a new row in our `directors` table), and then we use the attribute accessors `.name`, `.dob`, `.bio`, and `.image` to assign values to that instance. Finally, we call a method `.save` to put together and issue the SQL statement that will actually add the row (record) to our database table. 

So `ActiveRecord`, called an *object relational mapper*, is a perfect, elegant mapping between the Ruby that we are comfortable with and performant SQL.



### Text Companion: SQL and `ActiveRecord` Intro

## Video Segment: Creating `app/models/` Classes

-Notes:

  - time stamp 00:12:03 to 00:14:35
  - just showing off `app/models/` files for the four tables that we would like to have
  - not actually creating these yet
  - review [Our own classes][Our own classes]
  - inheritance from `ApplicationRecord`

Okay, so let's do this. First we'll go back to our Rails application and create Ruby classes for the four tables in our database. We need to create four files, each containing a new class in the Gitpod folder `app/models/`:

```ruby
# app/models/actor.rb

class Actor < ApplicationRecord
end
```

```ruby
# app/models/character.rb

class Character < ApplicationRecord
end
```

```ruby
# app/models/director.rb

class Director < ApplicationRecord
end
```

```ruby
# app/models/movie.rb

class Movie < ApplicationRecord
end
```

Each filename is the table (singular), and it contains the same (but capitalized) classname. For instance, the table `actors` has a file `app/models/actor.rb`, containing a class `Actor`. 

It's been a long-time, and if you're rusty that's understandable. Now might be a good time to review the idea of defining classes [here](https://chapters.firstdraft.com/chapters/769){:target="_blank"}. **BENP: could include a few code blocks from this doc here**

We haven't used the `app/models/` folder yet, but that's where all of our database-related Ruby code goes. In some sense, it's the most important folder to us, as that's where all of our business logic goes **BENP: what is business logic?**. 

Importantly, in the above files, we inherit `<` from a base class called `ApplicationRecord`, and that is where we get all of our amazing power. That is a base class provided by Rails, and our classes will inherit methods that translate code to SQL and have insane amounts of power that we will have a lot of time to learn about.



### Text Companion: Creating `app/models/` Classes

## Video Segment: RCAV /directors and `Director` Class

-Notes:

  - time stamp 00:14:35 to 00:28:12
  - wire up **/directors** with RCAV
  - database naming conventions: `get("/directors", { :controller => "directors", :action => "index" })`, `app/models/director.rb`, `Director` class, `directors` table
  - inheritence in model: `Director < ApplicationRecord < ActiveRecord::Base`
  - `.each` to list database info from the one record we added manually via SQL on inherited `.all` method to `Director`
  - create `app/models/`: `movies.rb`, `actors.rb`, and `characters.rb`

Before we proceed, as you know there's no point in writing code or doing anything unless you have a way of seeing what is happening as you go. There's a bunch of ways we could do this. 

Let's pick a page to work on. How about the first page linked in the [target](https://msm-queries.matchthetarget.com){:target="_blank"}, the list of all directors: **/directors**.

So we navigate our app browser to that URL and begin debugging our RCAV. I am also going to keep open the tab **/rails/db** because it's a useful visual reference. 

As usual the first error message is "no route matches", so connect the dots and make it say hello:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  get("/", { :controller => "application", :action => "homepage" })
  
  get("/directors", { :controller => "directors", :action => "index" })
end
```
{: mark_lines="6"}

Now that we're in the world of databases, we are going to stick to some common conventions for naming things. Very quickly you will see that we want one controller per database table (`"directors"`). And then the action where we list the whole database is typically called `"index"`. You will almost always have an action that just lists all the records in the table, or at least many records, and that is usually called `"index"`. 

Now to the controller (create the file and fill it in):

```ruby
# app/controllers/directors_controller.rb

class DirectorsController < ApplicationController
  def index

    render({ :template => "director_templates/index.html.erb" })
  end
end
```

And we create the view template:

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>hi</h1>
```

If that all works when we refresh our app browser, then we can begin to add some pseudo-code from the target ("View Source" on the page of interest) to our view template:

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>List of all directors</h1>

<%= Director.all %>
```
{: mark_lines="3-5"}

We just want to embed some Ruby code, where we imagine that we have a way to list our entire `directors` table using a class called `Director` with a method called `.all`. That would be cool if we could do something like that, and get all of our directors in an array to put into a table on our HTML page.

If we refresh **/directors** in our app browser, then we get the error "uninitialized constant ... Director", because we haven't defined our class yet.

To define the `Director` class, if you haven't already, then create the file `director.rb` in `app/models/` and fill it in:

```ruby
# app/models/director.rb

class Director
end
```

Now if we refresh **/directors**, the error message changes to: "undefined method \`all' for Director:Class". So we do have a `Director` class (Rails knows to look in `app/models/` for it), but no method `.all`... Well, we can inherit this method!

```ruby
# app/models/director.rb

class Director < ApplicationRecord
end
```
{: mark_lines="3"}

We don't need to write the method in here (like `def Director.all` and all the SQL stuff that would come after that), because we are just going to use the `.all` method inherited from `ApplicationRecord`. We can actually look into `app/models/` and we would see the file `application_record.rb`, which looks like:

```ruby
# app/models/application_record.rb

class ApplicationRecord < ActiveRecord::Base
  self.abstract_class = true
end
```

We see that this class actually itself inherits from the aforementioned `ActiveRecord::Base` from inside the Rails gem.

Now try to refresh **/directors**. It works! We should see (assuming we just have the one Greta Gerwig entry that we issued from the SQL editor on **/rails/db**) something like:

"Director::ActiveRecord_Relation (array with 1 Director instance inside)"

Think about this! I didn't need to do anything. I just inherited the `.all` method. This was able to go to the database, find (out of four tables) the table I wanted to connect to based on the name of the class, and then it issued the SQL to get the records, and then it returned the records to us as this class `ActiveRecord_Relation`.

`ActiveRecord_Relation` is an important class to memorize the name of. It is not an array, but it is like an array. It has multiple things inside. **`ActiveRecord_Relation` is a term to memorize: it means, "an array full of rows from the database".**

We can go to **/rails/db** and click the link to our `directors` table, and at the top of the page use the useful "+ ADD" button on the top of the page to manually enter another director record into the database (you can just put your name and some random information for now), and if we refresh the **/directors** page again, we would see:

"Director::ActiveRecord_Relation (array with 2 Director instances inside)"

The page is dynamically updating with the `.all` command reconnecting to the database table everytime I load the page!

`ActiveRecord_Relation` is a funny looking name, but it's just an array. Which means we can call all the array methods, like:

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>List of all directors</h1>

<%= Director.all.count %>
```
{: mark_lines="5"}

`.count` to print the number of records on our page. Or, what we want, a `.each` loop to print our records into a table:

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>List of all directors</h1>

<% Director.all.each do |a_director| %>
  <li>
    <%= a_director %>
  </li>
<% end %>
```
{: mark_lines="5-9"}

If we refresh our URL now, we would see that each list item is an instance of the `Director` class that we defined in `app/models/director.rb`. And each of these instances have attribute accessors associated with the *columns* of the table. To start, if we modify the view template to:

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>List of all directors</h1>

<% Director.all.each do |a_director| %>
  <li>
    <%= a_director.name %>,
    <%= a_director.dob %>,
    <%= a_director.bio %>,
    <%= a_director.id %>,
  </li>
<% end %>
```
{: mark_lines="7-10"}

Then the name, DOB, bio, and table ID of each director will be printed in a list on our refreshed **/directors** page. Remember, we still haven't done anything special in our `app/models/director.rb` file. But we get our attribute accessors for free from Rails using our inherited functionality. 

If we tried to change one of our embedded Ruby tags in the view template to `<%= a_director.title %>`, then we would get the page error: "undefined method 'title' for #Director". That's because `title` is an attribute associated with the `movies` table, and we are pulling records from `directors` with our `Director` class. All for free, just by defining our classes.

If you haven't done so, let's define the other three classes now by creating and filling in those files in `app/models/`: `movies.rb`, `actors.rb`, and `characters.rb`. 



### Text Companion: RCAV /directors and `Director` Class

## Video Segment: Rails Console

-Notes:

  - time stamp 00:28:12 to 00:32:16
  - explore `Director` in `rails console`
  - state of terminal (`pry(main)>` vs `$`)
  - `rails console` quirks: pagination, quiting view, exiting

Alright, now that we have all four classes in our `app/models/` folder we can continue.

One thing we may have noted is that it's a bit cumbersome to play with our models in a view template, where we need to keep going to the `app/views/` folder, modifying the template's embedded Ruby tags, and then refreshing our browser URL to see the results. 

Let's look at a better place to do this, the Rails console. We've already seen this a bit. Go to Gitpod, make sure your terminal window is open (<kbd>Ctrl</kbd> + <kbd>J</kbd>:), and open a new terminal (keep the `bin/server` terminal running so the browser tab doesn't crash). You can can open a new terminal by going to the top menu "Terminal" and selecting "New Terminal". 

Now at this fresh terminal you can enter `rails console` (or just `rails c` for short will do the same thing):

```ruby
gitpod /workspace/msm-queries $ rails console
```

**BENP: not sure the code block name for terminal, leaving it as ruby blank**

And what should come up is something like:

```ruby
Running via Spring preloader in process 8739
Loading development environment (Rails 6.0.3.2)
[1] pry(main)> 
```

This is just like the REPLs that we have already seen and used. We can enter whatever Ruby code interactively one line at a time and see printed out results! Now, at the terminal running `rails console`, try to enter:

```ruby
pry(main)> Director.all
```

This should give you something like:

```ruby
  (0.2ms)  SELECT COUNT(*) FROM "directors"
=> Director::ActiveRecord_Relation (array with 2 Director instances inside)
```

Just like what we saw when experimenting with our view template and the embedded Ruby tag `<%= Director.all %>`.

**Keep in mind what state your terminal is in.** If you see something like `pry(main)>` at the terminal prompt, then you know you are not in a regular `$`-sign terminal prompt and if you try to run `rails grade`, you will get an "undefined local varialbe or method grade" error. To exit the `rails console` and get back to a regular terminal, you need to run `pry(main)> exit`.

**BENP: Rails Console Quirks, 00:30:05 to 00:32:16**

A quick aside with some important notes about `rails console`:

Try to enter:

```ruby
pry(main)> Director.all.at(0)
```

Since `Director.all` is a type of array, we can use the array method `.at(0)` to get the first time. Now, what you should see, assuming that first entry is Greta Gerwig and your terminal window is too small to fit the entire bio, is something like:

```ruby
  Director Load (0.2ms)  SELECT "directors".* FROM "directors" WHERE "directors"."name" = ? ORDER BY "directors"."id" ASC LIMIT ?  [["name", "Greta Gerwig"], ["LIMIT", 1]]
=> #<Director:0x0000558c86d7d8a0
id: 1,
name: "Greta Gerwig",
dob: Thu, 04 Aug 1983,
bio:
  "Greta Celeste Gerwig /ˈɡɜːrwɪɡ/; born August 4, 1983) is an American actress and filmmaker. She first garnered attention after working on a
:
```

Sometimes when the output of a Ruby expression is very long, `rails console` is going to paginate it for you. You will have a `:` prompt when this is true, and you can hit <kbd>return</kbd> to scroll through line by line, or <kbd>space</kbd> to scroll through page by page.

When you reach the end of the output, you'll see `(END)`.

**To get back to the regular prompt so that you can enter your next command, just hit <kbd>q</kbd> at any time.**

And one last thing: if you are in `rails console` and then make a change to a model (for example, you define a new method or fix a syntax error), then, annoyingly, **you have to `exit` and then start a new `rails console`** to pick up the new logic. The console is not live-loading with changes we make to our app. Or, you can use the `reload!` method. **BENP: "reload doesn't always work in my experience, maybe delete this last sentence**



### Text Companion: Rails Console

## Video Segment: Reading and Creating Records

-Notes:

  - time stamp 00:32:16 to 00:36:35
  - explore `Director` in `rails console`
  - R and C in CRUD
  - reading records with `Director.all.at(0)`
  - creating records with `.new` and `.save`

Let's now explore our tables from the `rails console` prompt! 

Our main goal, is that we need to learn the Ruby required to **C**reate, **R**ead, **U**pdate, and **D**elete records. Once we know all the Ruby to CRUD, we can connect that with all the other Ruby we learned, and we'll be able to create an app.

Actually, we already started on the **R**, to read from our table in the view template. For instance if we, at the `rails console`, enter:

```ruby
pry(main)> a = Director.all
  (0.2ms)  SELECT COUNT(*) FROM "directors"
=> Director::ActiveRecord_Relation (array with 2 Director instances inside)
pry(main)> a.at(0)
  Director Load (0.2ms)  SELECT "directors".* FROM "directors" WHERE "directors"."name" = ? ORDER BY "directors"."id" ASC LIMIT ?  [["name", "Greta Gerwig"], ["LIMIT", 1]]
=> #<Director:0x0000558c86d7d8a0
id: 1,
name: "Greta Gerwig",
dob: Thu, 04 Aug 1983,
bio:
  "Greta Celeste Gerwig /ˈɡɜːrwɪɡ/; born August 4, 1983) is an American actress and filmmaker. She first garnered attention after working on a
: 
```

Press <kbd>q</kbd> to get back to the prompt if our output is paginated with the `:` symbol.

But we wanted that second input (`a.at(0)`) in its own variable. Well we can just press the <kbd>Up Arrow</kbd> on our keyboard at the prompt and that will give me back the last run line, then I can jump to the beginning of the line with <kbd>Cntrl</kbd> + <kbd>a</kbd>, and put it in its own variable:

```ruby
pry(main)> x = a.at(0)
pry(main)> x.name
=> "Greta Gerwig"
```

So we `.all` to get the records, `.at()` to select one of the records, and then `.name` to get one of the column values, and you have **R**ead a value from the database! There's a lot more depth for reading that we can go into, but there's the most basic.

**BENP: Rails Console Creating Records, 00:34:35 to 00:36:35**

Now, let's move onto **C**reating records. Let's create a new `actor` in our `actors` database table. This is just like how we created a new `Person` in our [previous exercises](https://chapters.firstdraft.com/chapters/769#our-own-classes){:target="_blank"}. There's even a reference for how to do it in this case [here](https://chapters.firstdraft.com/chapters/770#new){:target="_blank"}. 

Again, in the `rails console`, enter line-by-line:

```ruby
pry(main)> a = Actor.new
...
pry(main)> a.name = "Morgan Freeman"
...
pry(main)> a.dob = "June 1, 1937"
...
```

Now, we could fill out every attribute of `a`, with the exception of `created_at`, `updated_at`, and `id`, as these are **automatically filled in by Rails and we don't want to edit them**. But if we just have a look now at the variable:

```ruby
pry(main)> a
=> #<Actor:0x0000558c85f492e8
 id: nil,
 name: "Morgan Freeman",
 dob: Tue, 01 Jun 1937,
 bio: nil,
 image: nil,
 created_at: nil,
 updated_at: nil>
```

we see `a` is just an `Actor` instance being populated by information we enter. But if we go to our tab with the **/rails/db** page running and go to our table `actors`, we don't see this data there.

The reason is, it's not sure if we're done populating the columns. So when we *are* done, we need to call the very important method `.save`:

```ruby
pry(main)> a.save
   (0.1ms)  begin transaction
  Actor Create (0.8ms)  INSERT INTO "actors" ("name", "dob", "created_at", "updated_at") VALUES (?, ?, ?, ?)  [["name", "Morgan Freeman"], ["dob", "1937-06-01"], ["created_at", "2022-12-20 21:24:14.030804"], ["updated_at", "2022-12-20 21:24:14.030804"]]
   (1.9ms)  commit transaction
=> true
```

What happened there? It begins a transaction, issues the robust SQL, and enters it in the database! Have a look again at the `actors` table in **/rails/db** to see for yourself. And we have now **C**reated records.



### Text Companion: Reading and Creating Records

## Video Segment: `sample_data`

-Notes:

  - time stamp 00:36:35 to 00:42:10
  - test data without `.save`
  - `rails sample_data`
  - rake task in `tasks/dev.rake`
  - view **/rails/db**

So far we have just manually entering data. For instance if we try:

```ruby
pry(main)> Movie.count
```

(We can leave off `.all` on the class itself! It's a class-level method because it is so commonly done, and you will often see it omitted.)

And that will return: `=> 0`.

So, the only thing really missing right now is our big database to play with. It would be a ***huge*** pain to manually enter a ton of movies, actors, characters, and directors (not to mention keeping track of the foreign keys!). Try a few yourself and see (don't forget to `.save` to update the database with each new entry). 

But wait, stop! That would take forever. In the real world, someone would initially have to add all of our data, whether it's us, or our employees, or our users (through forms in their browser, obviously, not through `rails console`).

Luckily for us we don't need to do any of this manual entering for this project! We have included a handy program that you can run.

If you open a fresh terminal on Gitpod, get back to your regular `$`-sign command prompt, and run the command `rails sample_data`:

```ruby
gitpod /workspace/msm-queries $ rails sample_data
There are 34 directors in the database
There are 52 movies in the database
There are 652 actors in the database
There are 724 characters in the database
```

It will run a *rake task* **BENP: might need to define rake task here**, that I wrote called `sample_data`, which you can find in the `tasks/dev.rake` file. 

This Ruby script will do the process of adding data to our database and making sure the foreign keys are all correct. You can see the number of records entered in each table. This program will also first delete any previous records we entered, so we can start with a fresh dataset from scratch.

If you refresh **/rails/db**, then you will see all of these data in our tables. Also, if you go back to the **/directors** page that we were working on, you will see many entries now being listed. Progress!



### Text Companion: `sample_data`

## Video Segment: Finishing /directors `index`

-Notes:

  - time stamp 00:42:10 to 00:51:10
  - moving `Director.all` from view template to controller
  - `.each` to loop over `@list_of_directors` object, `ActiveRecord::Relation`
  - formatting results into a table
  - images with robohash (still necessary? works now...)
  - linking to details page with flexible route and primary key, `href="/director/<%= a_director.id %>"`

Now that I have my data, we could return to a `rails console` and practice some more interesting queries:

```ruby
pry(main)> Movie.count
 (0.1ms)  SELECT COUNT(*) FROM "movies"
=> 52
pry(main)> Director.count
 (0.1ms)  SELECT COUNT(*) FROM "directors"
=> 34
```

We will need to read data more precisely than just listing it all out for our task.

Before we do that, though, if we look at our [target](https://msm-queries.matchthetarget.com){:target="_blank"}, and go to the list of all directors: **/directors**, then we will see that we have the necessary data to finish that page in our app.

If you go back to the **/directors** page in our app, it actually looks like the only thing different compared to the target is that we have the information listed as bullets, and the target has it in a table with links for "Show details". We will just need to work on the formatting.

So let's return to our view template and fix things:

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>List of all directors</h1>

<% Director.all.each do |a_director| %>
  <li>
    <%= a_director.name %>,
    <%= a_director.dob %>,
    <%= a_director.bio %>,
    <%= a_director.id %>,
  </li>
<% end %>
```

We are just looping over a `Director.all` right in the view template. My preference here would be that we place this call in the controller and just have an instance variable with this array we can use in the view template:

```ruby
# app/controllers/directors_controller.rb

class DirectorsController < ApplicationController
  def index
    @list_of_directors = Director.all

    render({ :template => "director_templates/index.html.erb" })
  end
end
```
{: mark_lines="5"}

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>List of all directors</h1>

<% @list_of_directors.each do |a_director| %>
  <li>
    <%= a_director.name %>,
    <%= a_director.dob %>,
    <%= a_director.bio %>,
    <%= a_director.id %>,
  </li>
<% end %>
```
{: mark_lines="5"}

And rather than a list item, let's format things into a table:

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>List of all directors</h1>

<table border="1">
<% @list_of_directors.each do |a_director| %>
  <tr>
    <td><%= a_director.name %></td>
    <td><%= a_director.dob %></td>
    <td><%= a_director.bio %></td>
    <td><%= a_director.id %></td>
  </tr>
<% end %>
</table>
```
{: mark_lines="5 7-12 14"}

All we did here was put each of our previous records into a separate row (`<tr></tr>`) and each attribute into a separate column in that row (`<td></td>`), all within a loop in our `<table>` element.

If we refresh our **/directors** page and compare it with the target, we'll see that we're getting somewhere. But we do need to add table headings, move things around, add the images, and add a link to the director's page with the bio rather than putting it all in that table. Let's re-arrange things to match the target and add the image first:

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>List of all directors</h1>

<table border="1">
<% @list_of_directors.each do |a_director| %>
  <tr>
    <td><%= a_director.id %></td>
    <td>
      <img src="<%= a_director.image %>">
    </td>
    <td><%= a_director.name %></td>
    <td><%= a_director.dob %></td>
  </tr>
<% end %>
</table>
```
{: mark_lines="8-13"}

Remember, we can embed Ruby code in the HTML tag attributes, so we've done that with the image URLs (contained in `a_director.image`) from our database records in the `src=""` attribute to `<img>`. 

Using `.each` for looping over an `ActiveRecord_Relation` (an array of database rows) like `@list_of_directors`, and pulling out attributes to put them into embedded Ruby HTML documents is a huge part of our job!

As a brief aside, if those images aren't showing up on the page (for instance because the scraped image URLs are being blocked, which sometimes occurs), there's actually another way that we can get some dummy images to fill in our table: using [https://robohash.org](https://robohash.org){:target="_blank"}. RoboHash lets developers put sample images into mockups while building stuff. Unique images are generated from any text (including our entire URL strings). All we need to do is replace `src="<%= a_director.image %>"` with `src="https://robohash.org/<%= a_director.image %>"`. **BENP: I note that the director image URLs do seem to work now so maybe this aside can be eliminated**

Okay, now let's see how we can get the bio out of our table (it's not in the target) and into the director's detail page, which should be linked with "Show details". In the target, if I click a link it will take me to a URL that looks like **/director/1**. The second path segment is the `id` column value of that director, the *primary key*!

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>List of all directors</h1>

<table border="1">
<% @list_of_directors.each do |a_director| %>
  <tr>
    <td><%= a_director.id %></td>
    <td>
      <img src="<%= a_director.image %>">
    </td>
    <td><%= a_director.name %></td>
    <td><%= a_director.dob %></td>
    <td>
      <a href="/director/1">
        Show details
      </a>
    </td>
  </tr>
<% end %>
</table>
```
{: mark_lines="14-18"}

If on our **/director** page in our app, we now click some of the "Show details" links, they all take us to **/director/1**, and they all have a "no route matches" error.

How do we fill in the `href="/director/1"` attribute to get the input link to take us to the correct page? And how do we get that page to show us the director information from the database, including the long bio?

Well, for starters, we have `a_director.id`, which will give us the *primary key* for every director and we can fill in the link path with that:

```html
<!-- app/views/director_templates/index.html.erb -->

<h1>List of all directors</h1>

<table border="1">
<% @list_of_directors.each do |a_director| %>
  <tr>
    <td><%= a_director.id %></td>
    <td>
      <img src="<%= a_director.image %>">
    </td>
    <td><%= a_director.name %></td>
    <td><%= a_director.dob %></td>
    <td>
      <a href="/director/<%= a_director.id %>">
        Show details
      </a>
    </td>
  </tr>
<% end %>
</table>
```
{: mark_lines="15"}

Now when we click the link "Show details", we are being brought to the correct path for a given director, but we still haven't defined the routes or made the pages, so we're not done yet. For this, you will need to use *flexible routes*. **BENP: link to dynamic routes (or is it called flexible routes?) content**



### Text Companion: Finishing /directors Index

## Video Segment: Database Query with `.where`

-Notes:

  - time stamp 00:51:10 to 01:09:31
  - RCAV **/directors/eldest**
  - query DB in `rails console`, building up to `Director.where.not({ :dob => nil }).order({ :dob => :asc }).first`
  - put query into `wisest` action, and put `@oldest` director into view template `app/views/director_templates/eldest.html.erb`
  - http://strftime.net/ to get `.dob` formatted

Let's work on something else first. In our target we have those pages for [youngest](https://msm-queries.matchthetarget.com/directors/youngest){:target="_blank"} and [eldest](https://msm-queries.matchthetarget.com/directors/eldest){:target="_blank"} .

We will start with the **/directors/eldest** URL path in our app. As always, the first job is to make it say hello by following our RCAV:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  get("/", { :controller => "application", :action => "homepage" })
  
  get("/directors", { :controller => "directors", :action => "index" })

  get("/directors/eldest", { :controller => "directors", :action => "wisest" })
end
```
{: mark_lines="8"}

And then:

```ruby
# app/controllers/directors_controller.rb

class DirectorsController < ApplicationController
  def index
    @list_of_directors = Director.all

    render({ :template => "director_templates/index.html.erb" })
  end

  def wisest

    render({ :template => "director_templates/eldest.html.erb" })
  end
end
```
{: mark_lines="10-13"}

And (going right away to viewing the target source for the copy in our view template):

```html
<!-- app/views/director_templates/eldest.html.erb -->

<h1>Eldest director</h1>

<p>
  The eldest director in our dataset right now is Michael Curtiz, born on December 24, 1886.
</p>
```

Now that we have something showing up on our page (refresh **/directors/eldest** to be sure), we need to get it to dynamically update by looking up the oldest director and showing their name (linked to their page) and date of birth.

To figure out how to do this, we will play around in the `rails console`. So open a new terminal (or use one you have open that is not running `bin/server`), and start the console. If we do:

```ruby
pry(main)> Director.count
  (0.1ms)  SELECT COUNT(*) FROM "directors"
=> 34
```

then we see we have 34 directors. And our columns can be shown with:

```ruby
pry(main)> Director
=> Director(id: integer, name: string, dob: date, bio: text, image: string, created_at: datetime, updated_at: datetime)
```

Now, how are we going to find the oldest director? What methods do we have at our disposal?

We have many wonderful methods avaiable from `ActiveRecord`, so let's familiarize ourselves with some of them. **BENP: some of these notes come directly from zipping in [ActiveRecord][ActiveRecord] chapter content, could just be linked here.**

We will use the ["Time to CRUD" section of this chapter](https://chapters.firstdraft.com/chapters/770#time-to-crud){:target="_blank"} as reference. We see much of the things we have already discussed in this section: how to use the console, how to create records and save them, and how to read. Please read the section, so you can see some of the methods you have available that we haven't covered.

For now, let's have a look at one in particular, [`.order`](https://chapters.firstdraft.com/chapters/770#order){:target="_blank"}. This sorts an `ActiveRecord_Relation` based on some specified column and a specified direction: `:asc` for ascending, or `:desc` for descending.

In addition to this handy method, we have the all-important [`.where`](https://chapters.firstdraft.com/chapters/770#where){:target="_blank"}. `.where` is, if I had to pick one, the *most* important of the read methods. This is how we filter the table based on some criteria. We pick a column and a criteria and we can filter the records down. And you can do this as many times as you want until you are left with just the records you need (in our case, one record).

Let's put these read methods to the test in querying our database for the oldest director! Can you take a moment in your console and try to do this yourself with the reference material linked? In particular [this is important to keep in mind](https://chapters.firstdraft.com/chapters/770#where-always-returns-a-collection-not-a-single-row){:target="_blank"}.

It's a little tricky, but I'll wait...

Okay let's do it together. If I want the oldest director, then I will use the `dob` column from my table, that seems appropriate. First, I'll order by that column (note, I don't need to write `.all`, because it is standard to query all records in a database, so this is implicit):

```ruby
pry(main)> Director.order({ :dob => :asc }).first
```

We use `:asc` as the argument because in programming dates *grow* over time (they are stored as seconds **BENP: are they stored as seconds?**), so they get bigger and bigger, so the smallest `dob` column value is the oldest director. Thus, the first row in the `ActiveRecord_Relation` returned by this ordering should be what I want, so I call it with `.first` (or `.at(0)` is equivalent). If you leave off `.first`, then you will get the entire array of all rows, now ordered.

But wait, the above console query returns:

```ruby
=> #<Director:0x00005615f9231698
 id: 17,
 name: "Kátia Lund",
 dob: nil,
 bio: nil,
 image:
  "http://ia.media-imdb.com/images/M/MV5BMTUyNTEzODc1NF5BMl5BanBnXkFtZTYwOTUyMjIz._V1._SY314_CR13,0,214,314_.jpg",
 created_at: Wed, 12 Aug 2015 17:20:05 UTC +00:00,
 updated_at: Wed, 12 Aug 2015 17:20:05 UTC +00:00
```

That's not right! Kátia Lund is definitely not the eldest director, and look, the `dob` is `nil`, or empty. The value `nil` actually counts as smaller than 0 in our ordering. We're going to need to *chain* another query method if we want to avoid any `nil` values. 

How about `.where`? Or better yet, [`.where.not`](https://chapters.firstdraft.com/chapters/770#wherenotthis){:target="_blank"}. Try to solve this yourself!

Okay, if you didn't already, try to enter something like:

```ruby
pry(main)> Director.where.not({ :dob => nil }).order({ :dob => :asc }).first
```

And that should return:

```ruby
=> #<Director:0x00005615f918d020
 id: 19,
 name: "Michael Curtiz",
 dob: Fri, 24 Dec 1886,
 bio:
  "Curtiz began acting in and then directing films in his native Hungary in 1912. After WWI, he continued his filmmaking career in Austria and Germany and into the early 1920s when he directed films in other countries in Europe. M
:
```

Great!

As an aside. Sometimes when you are typing these long query strings into the console you forget a parenthesis and you get stuck:

```ruby
[7] pry(main)> Director.where.not({ :dob => nil }).order({ :dob => :asc }.first
[7] pry(main)*   
```

Where you see the `*` symbol at the prompt on the next line, the console is still waiting for you to finish entering. The console is expecting more code! Nothing is working here. Well just remember you can always <kbd>Ctrl</kbd> + <kbd>c</kbd> to get out of that state and go back to fix the expression.

Anyway, now that I've figured out the code in the `rails console`, let's add it to our controller as an instance variable:

```ruby
# app/controllers/directors_controller.rb

class DirectorsController < ApplicationController
  def index
    @list_of_directors = Director.all

    render({ :template => "director_templates/index.html.erb" })
  end

  def wisest
    @oldest = Director.where.not({ :dob => nil }).order({ :dob => :asc }).first

    render({ :template => "director_templates/eldest.html.erb" })
  end
end
```
{: mark_lines="10-13"}

And let's put that instance variable into our view template, keeping in mind that this variable is a record from our database table with attributes (column values) that we can access:

```html
<!-- app/views/director_templates/eldest.html.erb -->

<h1>Eldest director</h1>

<p>
  The eldest director in our dataset right now is <%= @oldest.name %>, born on <%= @oldest.dob %>.
</p>
```
{: mark_lines="6"}

Now refresh **/directors/eldest**. Looking good! 

We can pretty easily get the director name to link to the director's page like we did with the "Show details" links on **/directors** (we haven't RCAV'd these links yet, but we will soon).

Now, how can we get the formatting for the date of birth to match the target? Well for that we can use [http://strftime.net/](http://strftime.net/){:target="_blank"}. 

You never need to memorize these odd string formating characters for dates. Just use a resource for `strftime`, and over time you may beging to grow familiar with them. With the help of that tool we can reformat the date like so:

```html
<!-- app/views/director_templates/eldest.html.erb -->

<h1>Eldest director</h1>

<p>
  The eldest director in our dataset right now is <a href="/directors/<%= @director.id %>"><%= @oldest.name %></a>, born on <%= @oldest.dob.strftime("%B %e, %Y") %>.
</p>
```
{: mark_lines="6"}

And our page is up and running like the target. 

By the way, have you been using `rails grade` to check your progress and **/git** committing when you get things working?!?! Do it now if you haven't.



### Text Companion: Database Query with `.where`

## Video Segment: Flexible Routes for Director Details

-Notes:

  - time stamp 01:09:31 to 01:23:36
  - should title be "flexible" or "dynamic"?
  - return to unfinished "Show details" links on `index` page
  - importance of placement of static **/director/eldest** vs. flexible **/director/:an_id** in `config/routes.rb`
  - fetch director ID from `params` and query DB first in `rails console`
  - aside: using `tp Movie.where({ :year => 1994 }), "title", "year", "id"` in `rails console` to explore table 
  - place finished query in the action `director_details` and the director info in the view template
  - `time_ago_in_words()`

Now we need to make some flexible routes like **/director/1**, that accept the `id` number of a director in the second segment of the path. Let's begin by visiting such a segment.

First, notice that if we enter the URL path **/director/eldest**, this second segment **eldest** is not bringing us to a director page. That's because the `config/routes.rb` file will search for and match routes starting top to bottom, so we just need to be careful where we put our new routes (they will need to be below the route we don't want to be flexible):

```ruby
# config/routes.rb

Rails.application.routes.draw do
  get("/", { :controller => "application", :action => "homepage" })
  
  get("/directors", { :controller => "directors", :action => "index" })

  get("/directors/eldest", { :controller => "directors", :action => "wisest" })

  get("/directors/:an_id", { :controller => "directors", :action => "director_details" })
end
```
{: mark_lines="10"}

If we put the new route *above* the **/directors/eldest** route, then we would lose our ability to reach that route! So we put it *below*.

Long story short, if you define a flexible route that matches a static route that you want to have, make sure that your ***static* routes come *above* your *flexible* routes.**

Now let's make our director's pages working. We know already about flexible routes. **BENP: link to content / assignment here?**

We can get `:an_id` above out from our `params` variable. Visit a "Show details" link on the **/directors** page, and note in the Gitpod terminal running `bin/server`:

```
...
  Parameters: {"an_id"=>"1"}
...
```

Okay, let's get this data into our controller:

```ruby
# app/controllers/directors_controller.rb

class DirectorsController < ApplicationController
  def index
    @list_of_directors = Director.all

    render({ :template => "director_templates/index.html.erb" })
  end

  def wisest
    @oldest = Director.where.not({ :dob => nil }).order({ :dob => :asc }).first

    render({ :template => "director_templates/eldest.html.erb" })
  end

  def director_details
    # params looks like {"an_id"=>"1"}

    the_id = params.fetch("an_id")

    render({ :template => "director_templates/show.html.erb" })
  end
end
```
{: mark_lines="16-22"}

Now how do I get the actual director record that matches `the_id`? With a database query! Try it in our console:

```ruby
pry(main)> Director.where({ :id => "1" }).first
  Director Load (0.3ms)  SELECT "directors".* FROM "directors" WHERE "directors"."id" = ? ORDER BY "directors"."id" ASC LIMIT ?  [["id", 1], ["LIMIT", 1]]
=> #<Director:0x00005615f90b0710
 id: 1,
 name: "Frank Darabont",
 dob: Wed, 28 Jan 1959,
 bio:
  "Three-time Oscar nominee Frank Darabont was born in a refugee camp in 1959 in Montbeliard, France, the son of Hungarian parents who had fled Budapest during the failed 1956 Hungarian revolution. Brought to America as an infant
:
```

Don't forget the `.first` or `.at(0)`, or you will just get back an array rather than a single record.

As another aside, you can view records in your console with some table printing. For instance, at the console we could view the movies. Like what if you wanted to show the movies that were made in 1994?

```ruby
pry(main)> Movie.where({ :year => 1994 })
   (0.1ms)  SELECT COUNT(*) FROM "movies" WHERE "movies"."year" = ?  [["year", 1994]]
=> Movie::ActiveRecord_Relation (array with 4 Movie instances inside)
```

We see there are four movies, but how can we quick n' dirty actually see them? We can use a nice method called "table print", or `tp`:

```ruby
pry(main)> tp Movie.where({ :year => 1994 })
  Movie Load (0.2ms)  SELECT "movies".* FROM "movies" WHERE "movies"."year" = ?  [["year", 1994]]
ID | TITLE                    | YEAR | DURATION | DESCRIPTION                    | IMAGE                          | DIRECTOR_ID | CREATED_AT              | UPDATED_AT             
---|--------------------------|------|----------|--------------------------------|--------------------------------|-------------|-------------------------|------------------------
1  | The Shawshank Redemption | 1994 | 142      | Two imprisoned men bond ove... | http://ia.media-imdb.com/im... | 1           | 2015-08-12 17:20:05     | 2015-08-12 17:20:05    
4  | Pulp Fiction             | 1994 | 154      | The lives of two mob hit me... | http://ia.media-imdb.com/im... | 3           | 2015-08-12 17:20:05     | 2015-08-12 17:20:05  
...
```

Now this is ugly, because it is printing every column, so we can also specify just a few columns like so, with comma separated values of strings:

```ruby
pry(main)> tp Movie.where({ :year => 1994 }), "title", "year", "id"
  Movie Load (0.2ms)  SELECT "movies".* FROM "movies" WHERE "movies"."year" = ?  [["year", 1994]]
TITLE                    | YEAR | ID
-------------------------|------|---
The Shawshank Redemption | 1994 | 1 
Pulp Fiction             | 1994 | 4 
Forrest Gump             | 1994 | 18
Léon: The Professional   | 1994 | 31
=> 0.00055176
```

Okay, back to the task at hand, we can put the working database query in our controller to get the director record:

```ruby
# app/controllers/directors_controller.rb

class DirectorsController < ApplicationController
  def index
    @list_of_directors = Director.all

    render({ :template => "director_templates/index.html.erb" })
  end

  def wisest
    @oldest = Director.where.not({ :dob => nil }).order({ :dob => :asc }).first

    render({ :template => "director_templates/eldest.html.erb" })
  end

  def director_details
    # params looks like {"an_id"=>"1"}

    the_id = params.fetch("an_id")
    @the_director = Director.where({ :id => the_id }).first

    render({ :template => "director_templates/show.html.erb" })
  end
end
```
{: mark_lines="20"}

And we can use this director record `@the_director` instance variable in our view template to generate dynamic content at each flexible route (copy pasting a lot from our target to save time and populating with the instance variable).

```html
<!-- app/views/director_templates/show.html.erb -->

<h1>Director #<%= @the_director.id %> details</h1>

<dl>
  <dt>Name</dt>
  <dd><%= @the_director.name %></dd>
  <dt>Dob</dt>
  <dd><%= @the_director.dob %></dd>
  <dt>Bio</dt>
  <dd><%= @the_director.bio %></dd>
  <dt>Image</dt>
  <dd><img src=<%= @the_director.image %>></dd>
  <dt>Created at</dt>
  <dd><%= @the_director.created_at %></dd>
  <dt>Updated at</dt>
  <dd><%= @the_director.updated_at %></dd>
</dl>
```

And just to note, the target has some nice formatting for the "Created at" and "Updated at" information. The way this is done is simply wrapping the instance variable attribute, which come out as `Time` classes, in the inherited Rails function `time_ago_in_words()`, like: `<%= time_ago_in_words(@the_director.created_at) %>`. 

The "Show details" pages on **/directors** now appear to be working (test is manually yourself), so we can `rails grade` and **/git** commit, then move on to the next thing.



### Text Companion: Flexible Routes for Director Details

## Video Segment: Filmography

-Notes:

  - time stamp 01:23:36 to 01:35:54
  - foreign keys for `director_id` in `Movie`
  - `rails console` to show `tp Movie.where({ :director_id => 1 }), "title", "year", "id"`
  - add query to `director_details`
  - format filmography table in view template `app/views/director_templates/show.html.erb`, including the query: `<%= Director.where({ :id => a_film.director_id }).at(0).name %>`

We now want our director's pages to list the filmography (the `movies`) that each director made. On Day One, we spent a long time thinking about how our tables relate to one another, and this largely came down to keeping track of *foreign keys* added to each table.

If you forget what columns you have in your table, you can navigate in your browser to **/rails/db**, click on a given table, and then select the "Schema" tab above the table. This will give you the real column names, datatype, and other information.

Let's begin by playing around in our `rails console`. What if we did:

```ruby
pry(main)> tp Movie.where({ :director_id => 1 }), "title", "year", "id"
  Movie Load (0.2ms)  SELECT "movies".* FROM "movies" WHERE "movies"."director_id" = ?  [["director_id", 1]]
TITLE                    | YEAR | ID
-------------------------|------|---
The Shawshank Redemption | 1994 | 1 
=> 0.00032467
```

We wanted to find all of the movies that had a given director (with `id` of 1). And we know our `movies` table keeps track of this director ID with the *foreign key* column `director_id`. So we just query our database table (the class `Movie` in Rails) for a given `director_id`, and we get back all of those records (nicely formatted above with `tp` and a few columns of interest).

Let's add this query to our action in the controller:

```ruby
# app/controllers/directors_controller.rb

class DirectorsController < ApplicationController
  def index
    @list_of_directors = Director.all

    render({ :template => "director_templates/index.html.erb" })
  end

  def wisest
    @oldest = Director.where.not({ :dob => nil }).order({ :dob => :asc }).first

    render({ :template => "director_templates/eldest.html.erb" })
  end

  def director_details
    # params looks like {"an_id"=>"1"}

    the_id = params.fetch("an_id")
    @the_director = Director.where({ :id => the_id }).first
    @filmography = Movie.where({ :director_id => @the_director.id })

    render({ :template => "director_templates/show.html.erb" })
  end
end
```
{: mark_lines="21"}

Noting above that we need to use the current director (`@the_director`) ID to query our database for just that person's filmography.

Also note, `@filmography` is an `ActiveRecord_Relation` array (we didn't call `.first` or `.at(0)` on it) containing potentially many records. So in our view template we will need to loop over it with `.each` and format the attributes for each record into a table. Just like we did for the `index` action on our `@list_of_directors`!

So now in our view template, we can:

```html
<!-- app/views/director_templates/show.html.erb -->

<h1>Director #<%= @the_director.id %> details</h1>

<dl>
  <dt>Name</dt>
  <dd><%= @the_director.name %></dd>
  <dt>Dob</dt>
  <dd><%= @the_director.dob %></dd>
  <dt>Bio</dt>
  <dd><%= @the_director.bio %></dd>
  <dt>Image</dt>
  <dd><img src=<%= @the_director.image %>></dd>
  <dt>Created at</dt>
  <dd><%= @the_director.created_at %></dd>
  <dt>Updated at</dt>
  <dd><%= @the_director.updated_at %></dd>
</dl>

<h2>Filmography</h2>

<table border="1">
<% @filmography.each do |a_film| %>
  <tr>
    <td><%= a_film.id %></td>
    <td><img src="<%= a_film.image %>"></td>
    <td><%= a_film.title %></td>
    <td><%= a_film.year %></td>
    <td><%= a_film.director_id %></td>
  </tr>
<% end %>
</table>
```
{: mark_lines="22-32"}

If we click around now on our "Show details" pages on **/directors**, then we should see the table of filmographies updating on each page.

But there's something pesky. Right now we are showing users a column with `a_film.director_id`, which is just the ID number of the director. **We don't every want to show users ID numbers, we want to show them information associated with that id.** In this case, we want the name of the director, but that's not a column we have in `a_flim`, which comes from our `movies` table. So how to get this?

We could use the `@the_director.name` from above since we are on this page, but ignore this for a moment. If we didn't have the name already available, we could use another database query and a mix of invisible and visible embedded Ruby tags:

```html
<!-- app/views/director_templates/show.html.erb -->

<h1>Director #<%= @the_director.id %> details</h1>

<dl>
  <dt>Name</dt>
  <dd><%= @the_director.name %></dd>
  <dt>Dob</dt>
  <dd><%= @the_director.dob %></dd>
  <dt>Bio</dt>
  <dd><%= @the_director.bio %></dd>
  <dt>Image</dt>
  <dd><img src=<%= @the_director.image %>></dd>
  <dt>Created at</dt>
  <dd><%= @the_director.created_at %></dd>
  <dt>Updated at</dt>
  <dd><%= @the_director.updated_at %></dd>
</dl>

<h2>Filmography</h2>

<table border="1">
<% @filmography.each do |a_film| %>
  <tr>
    <td><%= a_film.id %></td>
    <td><img src="<%= a_film.image %>"></td>
    <td><%= a_film.title %></td>
    <td><%= a_film.year %></td>
    <td>
      <% d = Director.where({ :id => a_film.director_id }).at(0) %>
      <%= d.name %>
    </td>
  </tr>
<% end %>
</table>
```
{: mark_lines="31-34"}

Okay, now that we have a filmography we've really circled back on all of the early stuff we talked about with one-to-many and many-to-many relationships. This is what makes our applications powerful!

Now, after a `rails grade` and potentially a **/git** commit if everything is work, the rest of the project to match the target is up to you.



### Text Companion: Filmography

## Finish and Submit MSM Queries

### Additional Query Tasks for Practice

- Notes:

  - Copied from [https://github.com/appdev-projects/msm-queries#tasks](https://github.com/appdev-projects/msm-queries#tasks){:target="_blank"}

#### Finding a movie by title

How many years ago was "Casablanca" released?

 - Use the [`.where` method](https://chapters.firstdraft.com/chapters/770#where). It is everything.
 - Remember that [`.where` always returns a collection, not a single row](https://chapters.firstdraft.com/chapters/770#where-always-returns-a-collection-not-a-single-row).
 - Calculate the value dynamically (using e.g. `Time.now.year`), so that the number is always up to date.

#### Other queries

 - How many movies in our table are from [before](https://chapters.firstdraft.com/chapters/770#less-than-or-greater-than) the year 2000?
    - Displays the titles and years of the films.
 - Who is the youngest director in our table?
    - Display the date of birth of the director. (Remember you can call `.strftime("")` on `Time`, `Date`, and `DateTime`s to format them. Tools like [strftime.net](http://strftime.net/) and [For a Good Strftime](https://www.foragoodstrftime.com/) exist to help compose the formatting string argument.)
 - How many directors in our table are less than 55 years old?
    - Display their names and dates of birth.
 - How many films in our table were directed by Francis Ford Coppola?
    - Display the titles and years of the films.
 - How many films did Morgan Freeman appear in?
    - Display the titles and years of the films.
