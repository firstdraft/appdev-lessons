# RPS RCAV Part 3

Let's see what fancy powers we've unlocked on our HTML page via the RCAV approach.

## Embedded Ruby Tags

Add the following to our embedded Ruby (`.html.erb`) file:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<h2>
  They played <%= %>!
</h2>
```
{: mark_lines="5-7"}

We created a new tag that *looks* like HTML, but contains a *doorway to Ruby*: 

  - `<%= %>`

We can write any Ruby we want in that ***embedded Ruby tag***. *This is what makes the whole effort of RCAV worthwhile!* 

For instance, we can write:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<h2>
  They played <%= 6 * 7 %>!
</h2>
```
{: mark_lines="6"}

And we will see the result of this computation when we refresh **/rock**. (Did you *save* the changes in the file before refreshing the browser?) But, if we right-click and "View page source" in the browser, we won't see the Ruby code. We only see the result `42`. 

The browser *only* understands HTML and has no idea of the code that allows us to make the web application dynamic. Rails is processing all of the embedded Ruby tags and injecting them in the document before it sends the plain HTML file to the browser. 

We could also do something like:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= 6 * 7 %>!
</h2>
```
{: mark_lines="5"}

Here, we used a slightly different embedded Ruby tag: 

  - `<% %>`
 
We left off the `=` sign, which means the output of this Ruby code will be hidden in the rendered HTML. But, the variable `comp_move` (the result of randomly sampling an array of three possible `String` values) is still available and we can render that by changing the file again:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= comp_move %>!
</h2>
```
{: mark_lines="8"}

Our calculated variable `comp_move` is now rendered in the final HTML output, because it is in a `<%= %>` tag, with the `=` sign. And we will see the result of this computation when we refresh **/rock**. 

Again, "View page source" here and you won't see any sign of the `comp_move` variable computation from the `<% %>` tag.

Alright, we are now finally building dynamic web applications. We are able to render a template, we are able to write some HTML, and we are able to use *embedded Ruby tags*: 

  - `<% %>` for *hidden* content, and 
  - `<%= %>` for *rendered* content.

----

#### Quiz Question

- Using the RCAV approach, we can:
- Create actions (methods) in controllers (classes) that trigger rendering or redirecting for our users visiting URLs
    - Yes, that's the basic idea behind RCAVing.
- Do exactly the same thing as placing HTML files in the `public/` folder
    - No, we can do so much more!
- Create actions on-the-fly when a user visits any URL.
    - No, we (the developers) still need to define the available URLs that a user can visit.
- Use embedded Ruby HTML files (`.html.erb`) to put Ruby code on our pages
    - Yes! And that opens a world of possibilities
{: .choose_all #why_rcav points="10" answer="[1,4]" }

----

### Completed Code

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= comp_move %>!
</h2>
```

----

## Control Flow with Embedded Ruby

With the power of Ruby, we can actually compute who won or lost our Rock, Paper, Scissors match on the page before rendering the HTML to the user. Add the following `if-else` embedded Ruby code to our view template:

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= comp_move %>!
</h2>

<% if comp_move == "rock" %>
  <h2>We tied!</h2>
<% elsif comp_move == "paper" %>
  <h2>We lost!</h2>
<% elsif comp_move == "paper" %>
  <h2>We won!</h2>
<% end %>
```
{: mark_lines="11-17"}

Do you understand this added code? *Read* it carefully and try to understand the logic before you keep reading.

---

<p style="height: 150px"></p>

--- 

We used hidden `<% %>` embedded Ruby tags in our **control flow** on each line we wanted to hide from the user. Only the result of this control flow `<h2>We tied!</h2>`, `<h2>We lost!</h2>`, or `<h2>We won!</h2>` will be rendered, *depending on the randomly sampled `comp_move` variable*. Refresh **/rock** a few times to see. 

----

#### Quiz Question

- What is the `.html.erb` syntax for hidden versus shown Ruby output?
- We can't hide the output Ruby in these files
    - Actually, we can, there's two different tags.
- `<% %>` for hidden content, `<%= %>` for shown content
    - Yes!
- `<%= %>` for hidden content, `<% %>` for shown content
    - Nope, have another look at the previous code we added to the view file.
{: .choose_best #ruby_tags points="10" answer="2" }

----

### Completed Code

```html
<!-- app/views/game_templates/user_rock.html.erb -->

<h2>We played rock!</h2>

<% comp_move = ["rock", "paper", "scissors"].sample %>

<h2>
  They played <%= comp_move %>!
</h2>

<% if comp_move == "rock" %>
  <h2>We tied!</h2>
<% elsif comp_move == "paper" %>
  <h2>We lost!</h2>
<% elsif comp_move == "paper" %>
  <h2>We won!</h2>
<% end %>
```

----

## Conclusions


If you haven't, now would be a good time to run `rails grade` at the Gitpod terminal to check your progress. For a refresher on those steps [see here](https://learn.firstdraft.com/lessons/29#getting-automated-feedback-with-rails-grade){:target="_blank"}. And remember to *Always Be Committing (ABC)*, by making a **/git** commit. For a refresher on those steps [see here](https://learn.firstdraft.com/lessons/30#using-git-in-your-projects){:target="_blank"}. 

We have a lot done, but we still have a lot to do. 

<span style="font-size: x-large">[Proceed to the next part of the lesson](https://learn.firstdraft.com/lessons/25){:target="_blank"}</span>

----