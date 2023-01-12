# MSM Signin

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