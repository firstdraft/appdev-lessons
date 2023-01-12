# Refactoring Fortune Teller with Dynamic Routes

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