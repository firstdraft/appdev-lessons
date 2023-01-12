# Photogram GUI

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
