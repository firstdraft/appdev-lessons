# Outline Notes

Although originally based on the chronological assignments on Canvas in ["BUSN 36110 81 (Summer 2022) Application Development"](https://canvas.uchicago.edu/courses/41147){target="_blank"}, this book may have some re-ordering. Also the original chapters at [chapters.firstdraft](https://chapters.firstdraft.com/){target="_blank"} were zipped in here.

## Diátaxis

**Update: in the original outline, sections were tagged with the type. We don't need to be so strict, but we should adhere to some rules of thumb**

  1. Terminology and code syntax should be collected in technical reference glossaries

  2. Video tutorials should not digress too much into explanations and generalizations

  3. How-to written guides and accompaniments to videos should be concise, with code that can be copy-pasted
  
  4. Explanations are room to expand on ideas and digress 

### Original Outline Diátaxis

In an effort towards [Diátaxis](https://diataxis.fr/){target="_blank"}, the content is identified by small chunks of material with tags:

  1. **da="Tutorial"**
      - *pratical-study quadrant*
      - practical guided tutorials that produce meaningful results
      - avoid abstraction, generalization, explanation, choices

  2. **da="HowTo"**
      - *pratical-work quadrant*
      - similar to tutorial, but more concise with no digression or teaching

  3. **da="Explain"**
      - *theoretical-study quadrant*
      - understanding-oriented discussions referring to big-picture topics
      - include concepts, connections, abstraction, generalzation, alternatives, optional readings
  
  4. **da="TechRef"**
      - *theoretical-work quadrant*
      - indexes, glossaries, dictionaries
      - pure information, concise, no ambiguity, provide examples

  5. **da="Exercise"**
      - *our own*
      - this is not part of the cannon, but we add it

The "TechRef" (glossaries) and "Exercise" (quizzes + projects) tags are obvious, so content in these categories is not explicitly labelled in the outline.

Note, the difference between "Tutorials" and "HowTo" [here](https://diataxis.fr/tutorials-how-to/#whats-the-difference-between-a-tutorial-and-how-to-guide){target="_blank"}. They are distinguished by the user needs: *study* ("Tutorial") vs. *work* ("HowTo"). Tutorials provide a learning experience, how-to-guides help the user accomplish a task. Any **video walkthroughs are "Tutorials"** and their **written accompaniments are "HowTos"**. How-to-guides should never be videos, because a user should be able to quickly refer to what they need, without buffering or scrubbing.

## Technical References: Code vs. Terminology

There are two types of technical references. One is for terms, the [**terminology reference**][Terminology Technical Reference], which can be related to specific programming languages, however, any examples of HTML tags, Ruby methods, etc. should go into the **code reference**. There is one code reference for each subject area: HTML+CSS, Ruby, etc.

Both of these glossaries could be built up through the class, meaning the students would only see the most recent terms and those introduced previously. By the end, this is a long glossary sectioned by course units.

These code references already exist:
  
  - Ruby:
    - [Ruby Foundations Slides](https://firstdraft.slides.com/raghubetina/05-ruby-foundations?token=SFyjvCyP){target="_blank"}
    - [The One Ruby Reference][The One Ruby Reference]
    - [Different Ruby Styles][Different Ruby Styles]

  - HTML + CSS:  
    - [HTML + CSS Recap Slides](https://firstdraft.slides.com/raghubetina/html-and-css-recap?token=8gU8ghvw){target="_blank"}
    - [HTML Reference][HTML Reference]
    - [HTML Cheatsheet][HTML Cheatsheet]
    - [Classbook][Classbook]

## What's missing?

Running list of things TODO:

  - The location(s) of the technical references ("TechRef"), and how they are built up, currently found in glossaries.

  - Command-line basics
    - could just be a short "Tutorial" video along with a "TechRef" of all the commands shown in the course
    - place to explain directory structure and filepaths

  - Dedicated video + text content of technical setup. Gitpod and github accounts, opening gitpod workspace, tab organization, /git commiting, rails grade, etc. Can be done with "RPS HTML" or "String" as example. **See [Technical Setup][Technical Setup].**

  - Dedicated video + text content of gems and Gemfile (and maybe `bundle`). This is found throughout content right now.

  - CSS reference, there is some here: [Classbook][Classbook]

  - Text doc with "keyboard magic" commands (e.g., TAB completion, opening/clearing terminal). 

  - Dedicated video + text for ideas.firstdraft.com with domain model for OfferUp. **See [Domain Modeling][Domain Modeling]**

  - Video tutorial for [https://association-accessors.firstdraft.com/](https://association-accessors.firstdraft.com/){target="_blank"}. This is in the last 10 minutes of Day 7 recording right now. Maybe a dedicated chapter for `belongs_to`, `has_many`, `scope`, `through`, and use of `.joins()` for queries. Covered in [Refactoring MSM Again][Refactoring MSM Again] and [Photogram Associations][Photogram Associations].

  - Dedicated video + text content for starting from scratch, generator resources, and migration. This is spread across videos (e.g., Day 7 video, Day 8 short video, Photogram and MSM signin), chapters (e.g., [ActiveRecord][ActiveRecord], [draft:resource generator][draft:resource generator], [draft:account generator][draft:account generator]), classroom examples (Day 8 recordings). **See [Starting from Scratch with Generators][Starting from Scratch with Generators]**

  - API videos for Mailgun, Twilio, etc. 

  - Print stylesheet applied to any lesson to make hard copies (pdf)

  - Heroku alternative video / writeup