# Photogram Signin

(Intro to Authentication)

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
