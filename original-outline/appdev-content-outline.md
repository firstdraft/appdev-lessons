# AppDev Outline

This document is a chronological outline of the AppDev course content, based on the Canvas material for "BUSN 36110 81 (Summer 2022) Application Development". 

## Diátaxis

In an effort towards [Diátaxis](https://diataxis.fr/), the content is identified by small chunks of material and tags are used in the section headers. **We should strive to keep these all separated**.

  1. (da="Tutorial")
      - *pratical-study quadrant*
      - practical guided tutorials that produce meaningful results
      - avoid abstraction, generalization, explanation, choices

  1. (da="HowTo")
      - *pratical-work quadrant*
      - similar to tutorial, but more concise with no digression or teaching

  1. (da="Explain")
      - *theoretical-study quadrant*
      - understanding-oriented discussions referring to big-picture topics
      - include concepts, connections, abstraction, generalzation, alternatives, optional readings
  
  1. (da="TechRef")
      - *theoretical-work quadrant*
      - indexes, glossaries, dictionaries
      - pure information, concise, no ambiguity, provide examples

  1. (da="Exercise")
      - *our own*
      - this is not part of the cannon, but we add it

One could argue that "Exercises" are an offshoot of "Tutorials". But I keep them separated for now.

Note, the difference between "Tutorials" and "HowTo" [here](https://diataxis.fr/tutorials-how-to/#whats-the-difference-between-a-tutorial-and-how-to-guide). Both describe a sequence of actions and are done hands-on. They are distinguished by the user needs: *study* ("Tutorial") vs. *work* ("HowTo"). Tutorials provide a learning experience, how-to-guides help the user accomplish a task. 

For us, the line is blurry, but a breakdown could be that any **gitpod and other videos are "Tutorials"** and the **written accompaniment is a "HowTo"**. How-to-guides should never be videos, because a user should be able to quickly refer to what they need, without buffering or scrubbing.


## The structure

The outline is ordered with heading levels like so:

  - \# Week
    - \## Topic
      - \### Video Segment (tutorial or explanation)
        - \#### Text Companion (how-to if tutorial, otherwise written explanation, always *concise*)

Exercises are also peppered into the structure. See next section for technical references.

## Technical References: Code vs. Terminology

There are two types of technical references. One is for terms, the **terminology reference**, which can be related to specific programming languages, however, any examples of HTML tags, Ruby methods, etc. should go into the **code reference**. There is one code reference for each subject area: *HTML*, *CSS*, *Ruby*, etc.

Both of these glossaries could be built up through the class, meaning the students would only see the most recent terms and those introduced previously. By the end, this is a long glossary sectioned by course units.

These code references already exist:
  
  - Ruby:
    - [Ruby Foundations Slides](https://firstdraft.slides.com/raghubetina/05-ruby-foundations?token=SFyjvCyP)
    - `the-one-reference.md`
    - `optional-syntaxes-in-ruby.rb`

  - HTML + CSS:  
    - [HTML + CSS Recap Slides](https://firstdraft.slides.com/raghubetina/html-and-css-recap?token=8gU8ghvw)
    - `html-reference.md`
    - `html-cheatsheet.md`
    - `classbook.md`


## What's missing?

Running list of things TODO:

  - The location(s) of the technical references ("TechRef"), and how they are built up

  - Command-line basics
    - could just be a short "Tutorial" video along with a "TechRef" of all the commands shown in the course
    - place to explain directory structure and filepaths

  - Dedicated video + text content of technical setup. Gitpod and github accounts, opening gitpod workspace, tab organization, /git commiting, rails grade, etc. Can be done with "RPS HTML" or "String" as example. **See "Gitpod Technical Setup" topic in "Week 1" below.**

  - Dedicated video + text content of gems and Gemfile (and maybe `bundle`). This is found throughout content right now.

  - CSS reference, there is some here: `classbook.md`

  - Text doc with "keyboard magic" commands (e.g., TAB completion, opening/clearing terminal). 

  - Dedicated video + text for ideas.firstdraft.com with domain model for OfferUp. **See Week 6" topic "Domain Modeling"**

  - Video tutorial for https://association-accessors.firstdraft.com/. This is in the last 10 minutes of Day 7 recording right now. Maybe a dedicated chapter for `belongs_to`, `has_many`, `scope`, `through`, and use of `.joins()` for queries.

  - Dedicated video + text content for starting from scratch, generator resources, and migration. This is spread across videos (e.g., Day 7 video, Day 8 short video, Photogram and MSM signin), chapters (e.g., `active-record.md`, `draft-generators.md`, `draft-account.md`), classroom examples (Day 8 recordings). **See "Week 8" topic "Starting from Scratch with Generators" below.**

  - API videos for Mailgun, Twilio, etc. 

  - Print stylesheet applied to any lesson to make hard copies (pdf)

  - Heroku alternative video / writeup


---

# Week 1 

  - *None of Week 1 is transcribed*

---

## Course Overview (da="Explain")

  - Bird's Eye View Slides (https://slides.com/raghubetina/01-birds-eye-view?token=u4vg--N6)
    - 01-09: Course intro
    - 10-15: What does it mean to know how to code?
    - 16-21: SaaS
    - 22-26: URLs
    - 27-33: Raghu's journey
    - 34-40: How learning SaaS has evolved
    - 41-46: Ruby on Rails, Play the whole game
    - 47-49: Teaching team
    - 50-79: Record keeping (history, tables, databases, domain modeling, CRUD)
    - 80-88: Must See Movies example relational database tables

---

## Gitpod Technical Setup

  - Most of this is in the RPS HTML video, but it could have dedicated content
  - Some of this is also in "Assignment Week 3 (pre-class) Part 3: String" video
  
  - Chapters:
    - `day-2-notes.md`
    - `rails-grade.md`
    - `fixing-your-organization-permissions.md`
    - `gitpod-snapshot.md`
    - `hard-reload.md`

### Video Segment: Setting Up Accounts (da="Tutorial")

  - Setting up github and gitpod
  - Fixing permissions (`fixing-your-organization-permissions.md`)

#### Text Companion: Setting Up Accounts (da="HowTo")

### Video Segment: Starting a New Gitpod Project (da="Tutorial")

  - can use RPS HTML as example
  - forking, workspace layout, bin/server, tab management
  - could be chance to talk about file structures and terminal

#### Text Companion: Starting a New Gitpod Project (da="HowTo")

### Video Segment: Rails Grade and Git Committing (da="Tutorial")

  - kind of awkward placement, this video and text could go early in RPS HTML video
  - manually checking work, rails grade, /git commiting
  - `rails-grade.md`
  - `gitpod-snapshot.md`

#### Text Companion: Rails Grade and Git Committing (da="HowTo")

---

# Week 2

  - *None of Week 2 is transcribed*

---

## Rock, Paper, Scissors HTML

  - *This content has not been transcribed and may change*
  - Technical setup is contained in this video for now

  - Chapters:
    - `day-2-notes.md`
    - `rails-grade.md`
    - `fixing-your-organization-permissions.md`
    - `gitpod-snapshot.md`
    - `html-reference.md`
    - `html-cheatsheet.md`
    - `classbook.md`

  - Project: https://github.com/appdev-projects/rps-html

### Video Segment: Nth bite-size chunk of RPS HTML (da="Tutorial")

  - *The pattern repeats*

#### Text Companion: Nth bite-size chunk of RPS HTML (da="HowTo")

### Finish and Submit RPS HTML (da="Exercise")

  - Demo `gitpod-snapshot.md`

---

## Deploying to Heroku

- *This content has not been transcribed and may change*

- Chapters:
    - `deploying-to-heroku.md`

### Video Segment: Deploying to Heroku, Optional (da="Tutorial")

  - dedicated video with signing up and how it works

#### Text Companion: Deploying to Heroku, Optional (da="HowTo")

---

## Rock, Paper, Scissors CSS

  - *This content has not been transcribed and may change*

  - Chapters:
    - `classbook.md`

  - Project: https://github.com/appdev-projects/rps-css

### Video Segment: Nth bite-size chunk of RPS CSS (da="Tutorial")

  - *The pattern repeats*

#### Text Companion: Nth bite-size chunk of RPS CSS (da="HowTo")

### Finish and Submit RPS CSS (da="Exercise")

---

## Relationships (da="Explain")

  - Records and Relationships Slides (https://firstdraft.slides.com/raghubetina/records-and-relationships?token=hKsM-8iq)
    - 01: Get to know each other
    - 02: Types of associations

### Practice Identifying Relationships (da="Exercise")

  - Records and Relationships Slides (https://firstdraft.slides.com/raghubetina/records-and-relationships?token=hKsM-8iq)
    - 03-25: Practice identifying relationship
    - 26: ERD & Ideas Slides (*but this doesn't actually come next*)

---

## HTML Recap (da="Explain")

  - *this could all just be in the technical reference for HTML, with Replit exercises following the review*

  - Chapters:
    - `html-reference.md`
    - `html-cheatsheet.md`

  - HTML and CSS Recap Slides (https://firstdraft.slides.com/raghubetina/html-and-css-recap?token=8gU8ghvw)  
    - 01-05: HTML basics

### HTML Replits (da="Exercise")

  - HTML and CSS Recap Slides (https://firstdraft.slides.com/raghubetina/html-and-css-recap?token=8gU8ghvw)  
    - 05-07: HTML Replits

---

## CSS Recap (da="Explain")

  - *this could all just be in the technical reference for CSS, with Replit exercises following the review*

  - Chapters:
    - `classbook.md`

  - HTML and CSS Recap Slides (https://firstdraft.slides.com/raghubetina/html-and-css-recap?token=8gU8ghvw)  
    - 09-13: CSS Fundamentals
    - 15: External style sheets

### CSS Replits (da="Exercise")

  - HTML and CSS Recap Slides (https://firstdraft.slides.com/raghubetina/html-and-css-recap?token=8gU8ghvw)  
    - 14: CSS Fundamentals Replit
    - 16: External style sheets Replit

---

## Style Sheets Recap (da="Explain")

  - HTML and CSS Recap Slides (https://firstdraft.slides.com/raghubetina/html-and-css-recap?token=8gU8ghvw)  
    - 20-23, 25-26: Borrowing style sheets
    - 28: Bootstrap

### Style Sheets Replits (da="Exercise")

  - HTML and CSS Recap Slides (https://firstdraft.slides.com/raghubetina/html-and-css-recap?token=8gU8ghvw)  
    - 24: Google Fonts Replit
    - 27: Font Awesome Replit

---

## Design (da="Explain")

  - HTML and CSS Recap Slides (https://firstdraft.slides.com/raghubetina/html-and-css-recap?token=8gU8ghvw)  
    - 29: Readings
    - 31-34: Basic rules (mixed in with some Replits)

  - Chapters:
    - `design-resources.md`

  - Optional readings:
    - Typography: http://practicaltypography.com/typography-in-ten-minutes.html
    - Seven Rules 
      - Part 1: https://learnui.design/blog/7-rules-for-creating-gorgeous-ui-part-1.html
      - Part 2: https://learnui.design/blog/7-rules-for-creating-gorgeous-ui-part-2.html

---

## Linkinbio (da="Tutorial", da="HowTo", da="Exercise")

   - Chapters:
    - `linkinbio.md`

   - Project: https://github.com/appdev-projects/linkinbio

### Finish and Submit Linkinbio (da="Exercise")

---

# Week 3

  - *None of Week 3 is transcribed*

---

## Intro to Ruby

  - These are all the pre-class Ruby homework assignments

  - Chapters:
    - `the-one-reference.md`

### Nouns, Verbs, and Grammar (da="Explain", da="Exercise")

  - `noun-verbs-and-grammar.md`
  - "Exercises" in Replits

### Program Notes (da="Explain")

  - `program-notes.md`

### String (da="Explain", da="Exercise")

  - `string.md`
  - "Exercises" in Replits

### Video Segment: Setting up String Gitpod (da="Tutorial")

  - *not yet transcribed*
  - This video + text overlaps with "Week 1 Technical Setup" material
  - Chance to review technical setup (from forking on gitpod to rails grade)

#### Text Companion: Setting up String Gitpod (da="HowTo")

### String Gitpod Exercise (da="Exercise")

  - Project: https://github.com/appdev-projects/string-chapter

### Integer (da="Explain", da="Exercise")

  - `integer.md`
  - "Exercises" in Replits

### Integer Gitpod Exercise (da="Exercise")

  - Project: https://github.com/appdev-projects/integer-chapter

### Float (da="Explain", da="Exercise")

  - `float.md`
  - "Exercises" in Replits
  - `more-on-floats.md` (not used here, but related)

### Float Gitpod Exercise (da="Exercise")

  - Project: https://github.com/appdev-projects/float-chapter

### Other Ruby (da="Explain", da="Exercise")

  - Previous pattern repeats

  - Chapters (Projects):
    - `date.md` (https://github.com/appdev-projects/date-chapter)
    - `array.md` (https://github.com/appdev-projects/array-chapter)
    - `conditionals.md` (https://github.com/appdev-projects/if-statements-chapter)
    - `loops.md` (https://github.com/appdev-projects/loops-chapter)
    - `each.md` (https://github.com/appdev-projects/each-chapter)
    - `hash.md` (https://github.com/appdev-projects/hash-chapter)
    - `our-own-classes.md` (https://github.com/appdev-projects/our-own-classes-chapter)

---

## More Ruby (da="Explain")

  - Ruby Foundations Slides (https://firstdraft.slides.com/raghubetina/05-ruby-foundations?token=SFyjvCyP)
    - 01-06: Basic recap
    - 07-08: Inventors, google-fu

  Chapters:
    - `the-one-reference.md`

### Ruby Gym (da="Exercise")

  - https://checkins.firstdraft.com/exercises/113/student

### Optional Ruby Practice (da="Exercise")

  - See Canvas, links to Treehouse (https://teamtreehouse.com/library/ruby-basics-2) and CodeCademy (https://www.codecademy.com/learn/learn-ruby)

---

# Week 4

---

## Rock, Paper, Scissors RCAV

  - Transcription `adding-routes-RPS-RCAV.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - `adding-routes.md`
    - `rcav-flowchart.md`
    - Routing - RCAV Slides: https://firstdraft.slides.com/raghubetina/06-routing-rcav?token=43w7FD8Q

  - Project: https://github.com/appdev-projects/rps-rcav

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Dynamic Web Applications and URLs (da="Explain")

  - request lifecycle of Route, Controller, Action, View
  - web interface and URLs
  - actions
  - render and redirect

#### Text Companion: Dynamic Web Applications and URLs (da="Explain")

### Video Segment: Route (da="Explain")

  - all about routing and `config/routes.rb`
  - `get()`

#### Text Companion: Route (da="Explain")

### Video Segment: Controller, Action, View (da="Explain")

  - all about `app/controllers/`
  - `ApplicationController` inheritance

#### Text Companion: Controller, Action, View (da="Explain")

### Video Segment: Dropping `self.` (da="Explain")

  - why we drop `self.`

#### Text Companion: Dropping .self (da="Explain")

### Video Segment: Our First RCAV (da="Tutorial")

  - debugging an RCAV for **/rock** 
  - RTEM
  - ends with `redirect_to`

#### Text Companion: Our First RCAV (da="HowTo")

### Video Segment: Render HTML (da="Tutorial")

  - from `render({ :plain => "Hello, world!" })` to `render({ :template => "game_templates/user_rock.html.erb" })`
  - `.html` vs. `.html.erb`
  - `app/views/` view templates rather than `public/`

#### Text Companion: Render HTML (da="HowTo")

### Video Segment: Embedded Ruby Tags (da="Tutorial")

  - all about `<% %>` and `<%= %>` in a view template

#### Text Companion: Embedded Ruby Tags (da="HowTo")

### Video Segment: Control Flow with Embedded Ruby (da="Tutorial")

  - conditionals
  - all about `<% if ... %>`

#### Text Companion: Control Flow with Embedded Ruby (da="HowTo")

### Video Segment: Homepage (da="Tutorial")

  - RCAV with `render` for **/**

#### Text Companion: Homepage (da="HowTo")

### Video Segment: Reinforce RCAV with /paper (da="Tutorial")

  - RCAV with `render` for **/paper**

#### Text Companion: Reinforce RCAV with /paper (da="HowTo")

### Video Segment: Embedded Ruby in the Controller with Instance Variables (da="Tutorial")

  - moving conditional control flow `<% if ... %>` from **/rock** into the `ApplicationController` action `play_rock`
  - local variables vs. instance variables with `@`-notation

#### Text Companion: Embedded Ruby in the Controller with Instance Variables (da="HowTo")

### Video Segment: Linking Pages with Layouts (da="Tutorial")

  - all about `app/views/layouts/wrapper.html.erb` to get some headers, footers, and navigation links
  - `layout("wrapper.html.erb")` in `ApplicationController`
  - `:layout` argument for `render()`

#### Text Companion: Linking Pages with Layouts (da="HowTo")

### Finish and Submit RPS RCAV (da="Exercise")

### RCAV Addendums

  - Stuff that I did not zip in from the chapter `adding-routes.md`:
    - Addendum: Rendering JSON
    - Addendum: Custom Controller Files

---

## Omnicalc 1 (Forms and Query Strings)

 - Transcription `forms-query-strings-and-params-Omnicalc-Part1.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - `forms-query-strings-and-params.md`

  - Project: https://github.com/appdev-projects/omnicalc-1

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Exploring the Target (da="Explain")

  - we want forms to get information
  - what is a query string

#### Text Companion: Exploring the Target (da="Explain")

### Video Segment: /square/new RCAV (da="Tutorial")

  - RCAV with RTEM for **/square/new**
  - debugging

#### Text Companion: /square/new RCAV (da="HowTo")

### Video Segment: /square/new Form (da="Tutorial")

  - building a form in the **/square/new** view template
  - `<form></form>`, `<label></label>`, `<input>`, `<button></button>`
  - valid forms with `for=""` and `id=""`

#### Text Companion: /square/new Form (da="HowTo")

### Video Segment: Query String and Parameters Hash (da="Tutorial")

  - everything after **?** from **/square/new** form and the Parameters `Hash`

#### Text Companion: Query String and Parameters (da="HowTo")

### Video Segment: /square/results RCAV (da="Tutorial")

  - building the **/square/results** RCAV and form
  - more on query strings

#### Text Companion: /square/results RCAV (da="HowTo")

### Video Segment: Form Action and `params` (da="Tutorial")

  - adding `action="/square/results"` to the **/square/new** form 
  - using `params` Hash in the **/square/results** action to fetch from query string, calculate, and display

#### Text Companion: Form Action and params (da="HowTo")

### Video Segment: Independence of Routes (da="Tutorial")

  - use **/random/results** RCAV developed *before* **/random/new** to highlight independence of routes

#### Text Companion: Independence of Routes (da="HowTo")

### Finish and Submit Omnicalc 1 (da="Exercise")

  - see `forms-query-strings-and-params-Omnicalc-Part1.md` "Notes from the README" section for additional stuff that could go here

---

## Fortune Teller

  - Transcription `fortune-teller.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - README text at bottom of `fortune-teller.md`
    - `adding-routes.md`
    - `rcav-flowchart.md`
    - Routing -- RCAV Slides: https://firstdraft.slides.com/raghubetina/06-routing-rcav?token=43w7FD8Q
  
  - Project: https://github.com/appdev-projects/fortune-teller

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Routes and Controllers in Fortune Teller (da="Tutorial")

  - practice routing
  - stepping away from `app/controllers/application_controller.rb`, and using `app/controllers/numbers_controller.rb`
  - inheritance: `NumbersController < ApplicationController < ActionController::Base`

#### Text Companion: Routes and Controllers in Fortune Teller (da="HowTo")

### Video Segment: `.each` Loop on `@` Instance Variable (da="Tutorial")

  - from `@zebra` instance variable array to `.each` loop in the view template for **/lottery/lucky**
  - embedded Ruby tags `<%= %>` vs. `<% %>`

#### Text Companion: `winners` Action (da="HowTo")

### Video Segment: RCAV /lottery/unlucky (da="Tutorial")

  - RCAV practice. re-do the **/lottery/lucky** but with different copy. try to type everything, avoid copy-paste

#### Text Companion: RCAV /lottery/unlucky (da="HowTo")

### Video Segment: Navbar and Zodiac Debugging (da="Tutorial")

  - aside to `app/views/layouts/application.html.erb` to show <nav>
  - debug **/zodiacs/aries** together
  - RTEM

#### Text Companion: Navbar and Zodiac Debugging (da="HowTo")

### Finish and Submit Fortune Teller (da="Exercise")

  - see README text at bottom of `fortune-teller.md` for additional stuff "Debugging checklist" that could go here

---

## Omnicalc 2 (Forms, Params, APIs)

  - Transcription `Omicalc-Part2.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - `forms-query-strings-and-params.md`
    - `omnicalc-api.md`
    - `meteorologist-intro-to-apis.md` 
    - `storing-credentials-securely.md` 
    - `google-translate.md` 
    - `sending-emails-and-texts.md`
    - **Right now a bunch of this found much later in the Day 5 material on Canvas. See my notes below, APIs might need devoted video (maybe one for each API).**

  - Project: https://github.com/appdev-projects/omnicalc-2

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Exploring the Target (da="Explain")

  - doing math, intro to APIs
  - Street to Coordinates
  - Translate with SMS

#### Text Companion: Exploring the Target (da="Explain")

### Video Segment: Reviewing Query Strings (da="Tutorial")

  - examine target **/wizard_add** and implement using query string and `params`

#### Text Companion: Reviewing Query Strings (da="HowTo")

### Video Segment: Reviewing Forms (da="Tutorial")

  - examine target **/add** and implement using forms

#### Text Companion: Reviewing Forms (da="HowTo")

### Video Segment: Intro to APIs with Street to Coordinates (da="Tutorial")

  - there is a bunch of explanation here about APIs
  - implementing **/experiment** for "Street to Coordinates"
  - API keys
  - JSON
  - Google Maps API
  - JSON to Hash with `JSON.parse(open(@url).read)`

#### Text Companion: Intro to APIs with Street to Coordinates (da="HowTo")

### Finish and Submit Omnicalc 2 (da="Exercise")

  - see README text at bottom of `Omicalc-Part2.md` for additional stuff that could go here
  - API stretch goal should maybe go in a separate place?

---

# Week 5

---

## Refactoring Fortune Teller with Dynamic Routes

  - There is no video yet, everything is in the chapter `refactoring-fortune-teller-with-dynamic-routes.md`

  - Chapters (and slides):
    - `refactoring-fortune-teller-with-dynamic-routes.md`
    - README text at bottom of `fortune-teller.md`
    - `rcav-flowchart.md`

  - Project: https://github.com/appdev-projects/refactoring-fortune-teller

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Part 1: Dice (da="Tutorial")

  - dynamic route segments
  - see `refactoring-fortune-teller-with-dynamic-routes.md` chapter section
  - `get("/roll/:number_of_dice/:how_many_sides", { :controller => "dice", :action => "infinity_and_beyond" })`
  - `params.fetch("number_of_dice")` and `params.fetch("how_many_sides")`

#### Text Companion: Part 1: Dice (da="HowTo")

### Video Segment: Part 2: Horoscopes (da="Tutorial")

  - dynamic route segments, our own classes
  - see `refactoring-fortune-teller-with-dynamic-routes.md` chapter section
  - `Zodiac` class in `app/models/`
  - `get("/zodiacs/:the_sign", { :controller => "fortunes", :action => "horoscopes" })`
  - `String#to_sym`
  - regressions and refactoring, importance of automated tests

#### Text Companion: Part 2: Horoscopes (da="HowTo")

### Finish and Submit Refactoring Fortune Teller (da="Exercise")

  - optional extra challenge, refactor RPS RCAV with dynamic routes

---

## Dashboards (Dynamic Route Segments)

  - Transcription `dashboards.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - covid tracking text at bottom of `dashboards.md` (from README)
    - `refactoring-fortune-teller-with-dynamic-routes.md`
  
  - Project: https://github.com/appdev-projects/dashboards

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: URLs and Dynamic Routes (da="Explain")

  - dynamic route segments in `params`. sometimes we call these flexible routes.
  - using **/chapters/841** as example
  - wildcards

#### Text Companion: URLs and Dynamic Routes (da="Explain")

### Video Segment: Exchange Rate API Intro (da="Explain")

  - explore https://api.exchangerate.host/symbols
  - discuss JSON format
  - using **/symbols** and **/convert**

#### Text Companion: Exchange Rate API Intro (da="Explain")

### Video Segment: Building /forex (da="Tutorial")

  - RCAV **/forex** URL that lists all available currency symbols from JSON keys at https://api.exchangerate.host/symbols

#### Text Companion: Building /forex (da="HowTo")

### Video Segment: Building /forex/SYMBOL/SYMBOL (da="Tutorial")

  - RCAV **/forex/SYMBOL/SYMBOL** URL with dynamic route segments that lists all available currency exchange rates from JSON at https://api.exchangerate.host/convert with query strings like **?from=USD&to=EUR**

#### Text Companion: Building /forex/SYMBOL/SYMBOL (da="HowTo")

### Finish and Submit Dashboards (da="Exercise")

---

## Classroom Domain Modeling (da="Explain")

  - this was largely a classroom exercise and is partially written up in `day-5-domain-modeling.md`
  
  - ERD and Ideas Slides (https://firstdraft.slides.com/raghubetina/erd-and-ideas?token=B9Lja2V8)
    - 01-09: review MSM tables
    - 10-11: Yap model
    - 12-15: Photogram model
    - 16-17: Very Best model
    - 18: entity relationship diagrams (https://www.lucidchart.com/pages/er-diagrams#section_0)
    - 19-23: model Booth Ride Share, MyFitness, Chew, Mock Interviewer

---

## Rubber Duck Debugging (da="Explain")

  - just a reading: https://www.thoughtfulcode.com/rubber-duck-debugging-psychology/

---

## Omnicalc Debug, Optional Practice (da="Exercise")

  - Un-graded assignment, but there are tests built in

  - Chapters (and slides):
    - `refactoring-fortune-teller-with-dynamic-routes.md`
    - README text at https://github.com/appdev-projects/omnicalc-debug#readme

  - Project: https://github.com/appdev-projects/omnicalc-debug

---

## APIs Demo: Google Translate and SMS with Twilio, Optional (da="Tutorial", da="Explain")

  - No video

  - Chapters (and slides):
    - `google-translate.md` 
    - `sending-emails-and-texts.md`
    - `storing-credentials-securely.md`
  
  - Project:
    - Start: https://github.com/appdev-targets/omnicalc-2-api-starting-point
    - Solution: https://github.com/appdev-targets/omnicalc-2-api-starting-point/tree/translate-solution

---

## MSM Queries (Intro to Databases)

  - Transcription `MSM-queries.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - `active-record.md`
    - `our-own-classes.md`
    - "additional query tasks" from the README at the bottom of `MSM-queries.md`

  - Project: https://github.com/appdev-projects/msm-queries 

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Recordkeeping Review, Exploring the Target (da="Explain")

  - showing Bird's Eye View Slides 72-73
  - database backed web appplication
  - explore **/directors/youngest** and **/directors/eldest**
  - explore index (tables) and show (details) pages

#### Text Companion: Recordkeeping Review, Exploring the Target (da="Explain")

### Video Segment: Exploring /rails/db (da="Explain")

  - clicking around in **/rails/db**
  - looking at tables
  - development database SQLite
  - 

#### Text Companion: Exploring /rails/db (da="Explain")

### Video Segment: SQL and `ActiveRecord` Intro (da="Explain", da="Tutorial")

  - adding a record with SQL command in `directors` table at **/rails/db/sql** in the SQL Editor
  - Ruby to performant SQL with `ActiveRecord` object relational mapper
  - database transactions

#### Text Companion: SQL and `ActiveRecord` Intro (da="Explain", da="HowTo")

### Video Segment: Creating `app/models/` Classes (da="Explain")

  - just showing off `app/models/` files for the four tables that we would like to have
  - not actually creating these yet
  - review `our-own-classes.md`
  - inheritance from `ApplicationRecord`

#### Text Companion: Creating `app/models/` Classes (da="Explain")

### Video Segment: RCAV /directors and `Director` Class (da="Tutorial")

  - wire up **/directors** with RCAV
  - database naming conventions: `get("/directors", { :controller => "directors", :action => "index" })`, `app/models/director.rb`, `Director` class, `directors` table
  - inheritence in model: `Director < ApplicationRecord < ActiveRecord::Base`
  - `.each` to list database info from the one record we added manually via SQL on inherited `.all` method to `Director`
  - create `app/models/`: `movies.rb`, `actors.rb`, and `characters.rb`

#### Text Companion: RCAV /directors and `Director` Class (da="HowTo")

### Video Segment: Rails Console (da="Tutorial")

  - explore `Director` in `rails console`
  - state of terminal (`pry(main)>` vs `$`)
  - `rails console` quirks: pagination, quiting view, exiting

#### Text Companion: Rails Console (da="HowTo")

### Video Segment: Reading and Creating Records (da="Tutorial")

  - explore `Director` in `rails console`
  - R and C in CRUD
  - reading records with `Director.all.at(0)`
  - creating records with `.new` and `.save`

#### Text Companion: Reading and Creating Records (da="HowTo")

### Video Segment: `sample_data` (da="Tutorial")

  - test data without `.save`
  - `rails sample_data`
  - rake task in `tasks/dev.rake`
  - view **/rails/db**

#### Text Companion: `sample_data` (da="HowTo")

### Video Segment: Finishing /directors `index` (da="Tutorial")

  - moving `Director.all` from view template to controller
  - `.each` to loop over `@list_of_directors` object, `ActiveRecord::Relation`
  - formatting results into a table
  - images with robohash (still necessary? works now...)
  - linking to details page with flexible route and primary key, `href="/director/<%= a_director.id %>"`

#### Text Companion: Finishing /directors Index (da="HowTo")

### Video Segment: Database Query with `.where` (da="Tutorial")

  - RCAV **/directors/eldest**
  - query DB in `rails console`, building up to `Director.where.not({ :dob => nil }).order({ :dob => :asc }).first`
  - put query into `wisest` action, and put `@oldest` director into view template `app/views/director_templates/eldest.html.erb`
  - http://strftime.net/ to get `.dob` formatted

#### Text Companion: Database Query with `.where` (da="HowTo")

### Video Segment: Flexible Routes for Director Details (da="Tutorial")

  - should title be "flexible" or "dynamic"?
  - return to unfinished "Show details" links on `index` page
  - importance of placement of static **/director/eldest** vs. flexible **/director/:an_id** in `config/routes.rb`
  - fetch director ID from `params` and query DB first in `rails console`
  - aside: using `tp Movie.where({ :year => 1994 }), "title", "year", "id"` in `rails console` to explore table 
  - place finished query in the action `director_details` and the director info in the view template
  - `time_ago_in_words()`

#### Text Companion: Flexible Routes for Director Details (da="HowTo")

### Video Segment: Filmography (da="Tutorial")

  - foreign keys for `director_id` in `Movie`
  - `rails console` to show `tp Movie.where({ :director_id => 1 }), "title", "year", "id"`
  - add query to `director_details`
  - format filmography table in view template `app/views/director_templates/show.html.erb`, including the query: `<%= Director.where({ :id => a_film.director_id }).at(0).name %>`

#### Text Companion: Filmography (da="HowTo")

### Finish and Submit MSM Queries (da="Exercise")

---

# Week 6

---

## Classroom Queries Debug (da="Exercise")

  - Chapters (and slides):
    - README at https://github.com/appdev-projects/classroom-queries-debug#readme
  
  - Project: https://github.com/appdev-projects/classroom-queries-debug

---

## Different Ruby Styles (da="Explain")

  - just read `optional-syntaxes-in-ruby.md`

---

## History of ML, Optional Reading (da="Explain")

  - many links, could be compressed, see Canvas

---

## Refactoring MSM Queries

  - Transcription `refactoring-MSM-queries.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - `refactoring-msm-queries-with-methods.md`

  - Project: https://github.com/appdev-projects/refactoring-msm-queries-1

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Exploring the Target, What is Refactoring? (da="Explain")

  - explore target, which is a solution to MSM Queries ()
  - technical debt, refactoring
  - automated tests with `rails grade`

#### Text Companion: Exploring the Target, What is Refactoring? (da="Explain")

### Video Segment: Actor Details `show` Page (da="Explain")

  - examine view template and `show` action in `app/controllers/actors_controller.rb`
  - reiterate `ActiveRecord::Relation`

#### Text Companion: Actor Details `show` Page (da="Explain")

### Video Segment: `ActiveRecord::Relation` Review (da="Explain")

  - `rails console` to explore `ActiveRecord` objects

#### Text Companion: `ActiveRecord::Relation` Review (da="Explain")

### Video Segment: Actor Details Filmography (da="Explain")

  - `ActiveRecord::Relation` objects in `app/views/actor_templates/show.html.erb` to query from `Actor` to `Character`, `Character` to `Movie`, and `Movie` to `Director` on 

#### Text Companion: Actor Details Filmography (da="Explain")

### Video Segment: Defining Instance Methods in the Model (da="Tutorial")

  - define `title_with_year` in `app/models/movie.rb`
  - see `refactoring-msm-queries-with-methods.md` section "Instance method review"
  - use of `self.` in model method
  - apply new method to `app/views/movie_templates/show.html.erb`

#### Text Companion: Defining Instance Methods in the Model (da="HowTo")

### Video Segment: `Movie#director` (da="Tutorial")

  - define `director` in `app/models/movie.rb` to get rid of query in view templates and replace with `@the_movie.director`
  - apply new method to `app/views/movie_templates/show.html.erb`
  - 1-N association

#### Text Companion: `Movie#director` (da="HowTo")

### Video Segment: `Director#filmography` (da="Tutorial")

  - other side of 1-N association
  - define `filmography` in `app/models/director.rb` to get rid of query in view templates and replace with `@the_director.filmography`
  - apply new method to `app/views/director_templates/show.html.erb`

#### Text Companion: `Director#filmography` (da="HowTo")

### Additional Association Accessor Methods (da="Exercise")

  - work independently to define additional 1-N associations:

  ```ruby
  # Director#filmography (we did this!)
  # Movie#director (and this!)
  # Movie#characters
  # Character#movie
  # Actor#characters
  # Character#actor
  ```

### Video Segment: Additional Association Accessor Methods Solved (da="Tutorial")

  - finish 1-N association accessor methods in the models

#### Text Companion: Additional Association Accessor Methods Solved (da="HowTo")

### Video Segment: Applying Association Accessor Methods (da="Tutorial")

  - replace all DB queries with 1-N association accessor methods in the view templates

#### Text Companion: Applying Association Accessor Methods (da="HowTo")

### Finish and Submit Refactoring MSM Queries (da="Exercise")

---

## Domain Modeling (da="Exercise", da="Explain")

  - see `day-6-recording.md` for Canvas links
  - domain model OfferUp
  - solution is here: https://canvas.uchicago.edu/courses/41147/assignments/465866

### Video Segment: Ideas Tutorial (da="Tutorial")

  - content does not exist 
  - dedicated tutorial for [ideas.firstdraft.com](https://firstdraft.com/) with domain model for OfferUp

#### Text Companion: Ideas Tutorial (da="HowTo")

  - can be pulled from https://canvas.uchicago.edu/courses/41147/pages/firstdraft-ideas-erd-tool

---

# Week 7

---

## Photogram GUI

  - Transcription `photogram-gui.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - `active-record.md` CRUD section (https://chapters.firstdraft.com/chapters/770#time-to-crud)

  - Project: https://github.com/appdev-projects/photogram-gui

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: CRUD with Forms (da="Explain")

  - CRUD in relation to MSM app
  - forms for getting data into query string and then into database

#### Text Companion: CRUD with Forms (da="Explain")

### Video Segment: Explore the Target (da="Explain")

  - CRUD in relation to Photogram GUI

#### Text Companion: Explore the Target (da="Explain")

### Video Segment: Explore the ERD (da="Explain")

  - examine **/rails/db**, run `rails sample_data` 
  - examine ERD (https://github.com/appdev-projects/photogram-gui/blob/master/erd.png)
  - discuss 1-N and N-N relationships in the domain

#### Text Companion: Explore the ERD (da="Explain")

### Video Segment: Explore Model Classes (da="Explain")

  - examine `app/models/user.rb`
  - association accessor instance methods there and in other models
  - `validates` (first mention, only detailed later in https://github.com/appdev-projects/msm-validations and `data-integrity-with-validations.md`)

#### Text Companion: Explore Model Classes (da="Explain")

### Video Segment: Users `index` (da="Tutorial")

  - RCAV to get table of users at **/users**
  - query in `index` action to get `ActiveRecord::Relation` object `@list_of_users`

#### Text Companion: Users `index` (da="HowTo")

### Video Segment: User Details `show` (da="Tutorial")

  - more on `validates` (probably should be moved from here)
  - RCAV a details page with flexible / dynamic routes, using **/users/:path_username**
  - `redirect_to` if `nil` user, otherwise `render({ :template => "user_templates/show.html.erb" })`
  - "Own photos" table with association accessor methods `@the_user.own_photos` and `a_photo.poster.username`
  - Faker gem

#### Text Companion: User Details `show` (da="HowTo")

### Video Segment: Adding Navigation Links (da="Tutorial")

  - add navbar links to the `app/views/layouts/application.html.erb`

#### Text Companion: Adding Navigation Links (da="HowTo")

### Video Segment: Users Show Details Link (da="Tutorial")

  - add show details link on **/users** table with `href="/users/<%= a_user.username %>"`

#### Text Companion: Users Show Details Link (da="HowTo")

### Video Segment: Photos `index` (da="Tutorial")

  - RCAV **/photos** and get list of photos in `index` action for table in view template
  - include show details link with `href="/photos/<%= a_photo.id %>"`

#### Text Companion: Photos `index` (da="HowTo")

### Video Segment: Photo Details `show` (da="Tutorial")

  - RCAV **/photos/:path_id** flexible route
  - use photo ID from URL in `params` in `show` action to get photo details and display

#### Text Companion: Photo Details Page (da="HowTo")

### Video Segment: Photo Comments with Association Accessors (da="Tutorial")

  - get "Comments" section on photo details page using `@the_photo.comments.each` and `a_comment.commenter` association accessor methods

#### Text Companion: Photo Comments with Association Accessors (da="HowTo")

### Video Segment: Delete Photo Link (da="Tutorial")

  - moving to the D in CRUD
  - get "Delete this photo" link on photo details page by RCAVing `"/delete_photo/<%= @the_photo.id %>"` 
  - `.destroy` in the action to delete photo

#### Text Companion: Delete Photo Link (da="HowTo")

### Video Segment: Create Photo Form (da="Tutorial")

  - moving to the C in CRUD
  - build up form in `app/views/photo_templates/index.html.erb`
  - RCAV `action="/insert_photo"` with action `create`
  - fetch `params` from form, `.save` to database

#### Text Companion: Create Photo Form (da="HowTo")

### Video Segment: Update Photo Form (da="Tutorial")

  - moving to the U in CRUD
  - build up form in `app/views/photo_templates/show.html.erb`
  - RCAV `action="/update_photo/<%= @the_photo.id %>"` with action `update`
  - fetch `params` from path, `.save` to database

#### Text Companion: Update Photo Form (da="HowTo")

### Finish and Submit Photogram GUI (da="Exercise")

---

## MSM Validations, Optional Exercise (da="Exercise")

  - Un-graded assignment, but there are tests built in

  - Chapters (and slides):
    - `ata-integrity-with-validations.md`
    - README text at https://github.com/appdev-projects/msm-validations#readme

  - Project: https://github.com/appdev-projects/msm-validations

---

## Very Best Debug

  - Transcription `very-best-debug-video.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Homepage Debugging (da="Tutorial")

  - RTEM to slowly debug **/**
  - `better_errors` page console aside (da="Explain")
  
#### Text Companion: Homepage Debugging (da="HowTo")

### Video Segment: Typos and `NilClass` Bug (da="Tutorial")

  - RTEM to slowly debug **/venues/[ID of venue]**
  - tricky bug: `undefined method 'address' for nil:NilClass` 
  - `ActiveRecord::Relation` single instance `.at(0)`
  
#### Text Companion: Typos and `NilClass` Bug (da="HowTo")

### Video Segment: Association Accessor `self.id` Bug (da="Tutorial")

  - RTEM to continue debugging **/venues/[ID of venue]**
  - tricky bug: `self.id` in `Comment#commenter`, rather than `self.author_id` 
  
#### Text Companion: Association Accessor `self.id` Bug (da="HowTo")

### Finish and Submit Very Best Debug (da="Exercise")

  - see list from README: https://github.com/appdev-projects/very-best-debug#readme

---

## draft:resource generator (da="Explain")

  - just a reading in `draft-generators.md`

---

## Refactoring MSM -- Again!

  - Transcription `refactoring-MSM-queries-again.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - helper app: https://association-accessors.firstdraft.com/

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: `belongs_to` (da="Tutorial", da="Explain)

  - refactor 1-N `Character#movie`, going from the "many" to the "one"
  - why `belongs_to` is better than previous method definitions
  - aside into `.joins` at the `rails console`

#### Text Companion: `belongs_to` (da="HowTo")

### Video Segment: `has_many` (da="Tutorial")

  - refactor 1-N `Movie#characters`, going from the "one" to the "many"
  - aside into method syntax for `Director#filmography`

#### Text Companion: `has_many` (da="HowTo")

### Finish and Submit Refactoring MSM -- Again! (da="Exercise")

  - using https://association-accessors.firstdraft.com/ (needs a video tutorial)

---

## Photogram Associations, Optional Exercise (da="Exercise")

  - Un-graded assignment, no tests, no `rails grade`

  - `has_many`, `belongs_to`, `scope`, `through`

  - Chapters (and slides):
    - using https://association-accessors.firstdraft.com/ (needs a video tutorial)
    - two readings:
      - https://guides.rubyonrails.org/association_basics.html
      - stretch goal: https://remimercier.com/scoped-active-record-associations/

  - Project: https://github.com/appdev-projects/photogram-associations

---

# Week 8

---

## Cookies Intro

  - Transcription `cookies-with-video.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - `cookies.md`

  - Project: https://github.com/appdev-projects/cookies-intro

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Exploring Browser Cookies (da="Explain")

  - in Chrome, visit [target](https://cookies-intro.matchthetarget.com/), "Inspect" > "Application" > "Cookies", Name/Value pairs

#### Text Companion: Exploring Browser Cookies (da="Explain")

### Video Segment: `cookies` Object (da="Tutorial")

  - explore `<%= cookies %>` on `app/views/calculation_templates/addition_form.html.erb`
  - `cookies.store()` in `add` action and show in view template

#### Text Companion: `cookies` Object (da="HowTo")

### Finish and Submit Cookies Intro (da="Exercise")

  - see `cookies.md` for requirements

---

## Photogram Signin (Intro to Authentication)

  - Transcription `photogram-signin.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - `cookies-vs-session.md`

  - Project: https://github.com/appdev-projects/photogram-signin

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Storing Passwords (da="Tutorial")

  - migration file: `rails g migration AddPasswordDigestToUsers`
  - add `password_digest` Column to `User`
  - explore `db/migrate` and `rails db:migrate`
  - add `has_secure_password` to `app/models/user.rb` to get `.password` and `.password_confirmation`
  - `bcrypt` gem

#### Text Companion: Storing Passwords (da="HowTo")

### Video Segment: Signup Form (da="Tutorial")

  - add navigation links in `app/views/layouts/application.html.erb`
  - RCAV **/user_sign_up**
  - copy and modify add user form found in `app/views/users/index.html.erb`
    - use `type="password"` inputs
  - fix `create` action to use `.password` and `.password_confirmation` before `.save`
  - control flow with `:notice` or `:alert`

#### Text Companion: Signup Form (da="HowTo")

### Video Segment: Notices and Alerts (da="Tutorial")

  - add `notice` and `alert` to `app/views/layouts/application.html.erb`
  - use `if ... present?` control flow and style green and red

#### Text Companion: Notices and Alerts (da="HowTo")

### Video Segment: Signout with `reset_session` (da="Tutorial")

  - add `session.store(:user_id, user.id)` to `create` action
  - RCAV **/user_sign_out** with `reset_session` in `toast_cookies` action

#### Text Companion: Signout with `reset_session` (da="HowTo")

### Video Segment: Signin with `post` and `authenticate` (da="Tutorial")

  - RCAV **/user_sign_in** with `new_session_form` action
  - signin form with `action="/verify_credentials"` and `method="post"`
  - `authenticate` action using `user.authenticate` and control flow

#### Text Companion: Signin with `post` and `authenticate` (da="HowTo")

### Video Segment: Remove User-Facing IDs (da="Tutorial")

  - put `photo.owner_id = session.fetch(:user_id)` and `comment.author_id = session.fetch(:user_id)` in backend `create` actions of add photo and add comment forms

#### Text Companion: Remove User-Facing IDs (da="HowTo")

### Finish and Submit Photogram Signin (da="Exercise")

---

## Starting from Scratch with Generators

  - Day 8 Short Video Recording, which is *not* transcribed, additional materials (see "Todo": https://github.com/orgs/firstdraft/projects/11/views/1)

  - Chapters (and slides):
    - `starting-a-rails-project-from-scratch.md`
    - `active-record.md`
    - `draft-generators.md`
    - `draft-account.md`
    - ideas.firstdraft.com generators with co-pilot

  - Some of these steps are also done in the MSM signin video at the beginning. *This can be a review*.

### Video Segment: Starting from Scratch with Generators (da="Tutorial")

#### Text Companion: Starting from Scratch with Generators (da="HowTo")

---

## MSM Signin

  - Transcription `MSM-signin.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):
    - `draft-generators.md`
    - `draft-account.md`

  - Project: https://github.com/appdev-projects/msm-signin

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Exploring the Target (da="Explain")

  - show off signin, out, up, and **/bookmarks** in the [target](https://msm-signin.matchthetarget.com)

#### Text Companion: Exploring the Target (da="Explain")

### Video Segment: Creating `movies` with `generate model` (da="Tutorial")

  - run `rails generate model movie` in our blank app
  - explore file in `db/migrate/`
  - run `rails db:migrate`
  - visit **/rails/db**

#### Text Companion: Creating `movies` with `generate model` (da="HowTo")

### Video Segment: Creating `movies` with `generate draft:resource` (da="Tutorial")

  - run `rails db:rollback` then `rails generate draft:resource movie`
  - explore `config/routes.rb` to view CRUD routes
  - explore `app/controllers/movies_controller.rb` to view CRUD actions
  - explore generated view templates
  - run `rails db:migrate`
  - aside into `schema.rb` and migration versioning

#### Text Companion: Creating `movies` with `generate draft:resource` (da="HowTo")

### Video Segment: `generate draft:resource` for Entire Database (da="Tutorial")

  - run `rails db:rollback` then `rails generate draft:resource` and `rails db:migrate` for all tables in database

#### Text Companion: `generate draft:resource` for Entire Database (da="HowTo")

### Video Segment: Association Accessor Methods (da="Tutorial")

  - use `belongs_to` and `has_many` on the table models
  - can use https://association-accessors.firstdraft.com

#### Text Companion: Association Accessor Methods (da="HowTo")

### Video Segment: Nav Links and `sample_data` (da="Tutorial")

  - add links to `app/views/layouts/application.html.erb`
  - run `sample_data`
  - point out [loading data from a CSV](https://chapters.firstdraft.com/chapters/791) and [adding a `sample_data` rake task](https://chapters.firstdraft.com/chapters/852)

#### Text Companion: Nav Links and `sample_data` (da="HowTo")

### Video Segment: `validates` and Summarize Startup (da="Tutorial")

  - add `validates :title, :presence => true` to `app/models/movie.rb`
  - summarize starting from scratch steps

#### Text Companion: `validates` and Summarize Startup (da="HowTo")

### Video Segment: `generate draft:account` (da="Tutorial")

  - getting `users` table with `draft:account`
  - explore new CRUD routes, models, and actions

#### Text Companion: `generate draft:account` (da="HowTo")

### Video Segment: Conditional Links, Alerts, and Notices (da="Tutorial")

  - control flow showing of links in `app/views/layouts/application.html.erb` using `if session.fetch(:user_id) == nil`
  - explore `:alert` and `:notice` in `app/controllers/movies_controller.rb`
  - add alerts and notices to application layout

#### Text Companion: Conditional Links, Alerts, and Notices (da="HowTo")

### Video Segment: Bookmark (da="Tutorial")

  - run `rails generate draft:resource bookmark`
  - tailoring user experience by allowing them to add records to a join table
  - create `action="/insert_bookmark"` form in `app/views/movies/show.html.erb`
  - use the provided CRUD action, changing parameter names to matchup

#### Text Companion: Bookmark (da="HowTo")

### Video Segment: Un-Bookmark (da="Tutorial")

  - add conditional flow to bookmark action with `Bookmark.where({ :movie_id => @the_movie.id, :user_id => session.fetch(:user_id) })`
  - add `href="/delete_bookmark/<%= the_bookmark.id %>"` link

#### Text Companion: Un-Bookmark (da="HowTo")

### Video Segment: Bookmark Index for Current User (da="Tutorial")

  - conditional flow to application layout for showing bookmarks
  - modify `index` action in `app/controllers/bookmarks_controller.rb`
  - three primary uses of `session.fetch(:user_id)` cookie
  - define association accessor methods in user, bookmark, and movie models

#### Text Companion: Bookmark Index for Current User (da="HowTo")

### Video Segment: `@current_user` (da="Tutorial")

  - add `load_current_user` action to `app/controllers/bookmarks_controller.rb` to get `@current_user`
  - use `before_action(:load_current_user)` in `app/controllers/application_controller.rb` to get `@current_user` everywhere
  - apply `@current_user.bookmarks` in bookmarks `index` action

#### Text Companion: `@current_user` (da="HowTo")

### Video Segment: Bookmark Drop-Down Form (da="Tutorial")

  - create a drop-down form on `app/views/bookmarks/index.html.erb`
  - using `<select name="query_movie_id">` with `<option value="<%= a_movie.id %>">`
  - hiding ID keys from user

#### Text Companion: Bookmark Drop-Down Form (da="HowTo")

### Finish and Submit MSM Signin (da="Exercise")

---

# Week 9

## Bootstrap Intro -- Task List (da="Exercise")

  - This video is *not yet transcribed* because it was a lot of visual show-and-tell.

  - Here are some time-stamp notes for things that could be transcribed:

    - **00:19:00 to 00:30:49**: useful `validates`, `has_many`, `reset_session`, new stuff and review

    - **00:31:40 to 00:42:45**: `sample_data` task (already chapter `sample-data.md`, but chapter uses Photogram and here done with Task List)

    - **00:51:06 to 00:53:28**: `force_user_sign_in` and `skip_before_action` is covered for the first time.   

---

# Final Project and Extra Topics (da="Exercise")

---

## Photogram Final

  - `photogram-final.md`
  - https://github.com/appdev-projects/photogram-final

---

## Building Your Own Idea

  - long text with links to github and starting from scratch: https://canvas.uchicago.edu/courses/41147/assignments/465848

---

## Extra Topics

  - extra topics, none of this is touched or transcribed: https://canvas.uchicago.edu/courses/41147/pages/extra-topics-written-guides-and-videos

  - chapters:
    - `ransack.md`
    - `image-uploads.md`
    - `loading-data-from-a-csv-file-into-your-database.md`
    - `google-map.md`
    - `exporting-data-into-a-csv.md`
    - `web-scraping-quickstart.md`

