# Rock, Paper, Scissors RCAV

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
