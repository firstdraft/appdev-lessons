# Refactoring MSM Queries

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
