# MSM Queries 

(Intro to Databases)

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
