# Application Development Lessons

This repository was originally pulled from the [appdev-textbook](https://github.com/firstdraft/appdev-textbook) repository, which was being written in bookdown. That repository in turn was largely based on the [appdev-chapters](https://github.com/firstdraft/appdev-chapters) repo. 

This repository is a place to rewrite any bookdown chapters from the "textbook" into the format required for "lessons".

## Instructions to Prepare a Lesson

Here are a few things that need to be changed for the files in this repository:

 1. Rename the previous chapter by appending `-lesson.md`. We will make find-n-replace substitutions in this file, which indicates that the syntax (and some copy) was optimized for learn.

 1. Double check that any `{target...` is `{:target...` (with the `:`).

 1. Any `^` caret style footnotes need to take the form of `<aside markdown="1"></aside>` with **no indentation**. Check each footnote and see if more context needs to be added since there won't be a caret anymore. Caret's can still be used, but only really for citations since they go to the bottom of the page.

 1. Any internal cross-references need to be removed by searching for `][`. These can maybe be put back when we figure out anchor links.

 1. Any `**https:` should be replaced with `**https\:` when the intention is just to indicate a path (don't add the backslash on links out)

 1. Begin putting the lesson into sub-lessons by creating new files and appending `-part-01.md` after `-lesson`. So: 
    - `rps-rcav.md` is the original bookdown format, 
    - `rps-rcav-lesson.md` is the syntax changes for learn, and 
    - `rps-rcav-lesson-part-XX.md` is each part of the lesson which becomes a separate lesson on learn.


 1. References to Gitpod workspace and/or REPLs need to get a `<div class="proj / experiment" markdown="1"></div>` tag. Instructions to open a Gitpod should be consistent. As of now, it will direct the students to Canvas.

 1. The README for the Gitpod project should be reduced. All instructions should be contained in the lesson.

 1. Once the lesson is copied onto learn, you need to do a Ctrl+F to look for any `![` or `assets`, which indicate images. These images need to be dragged and dropped into those locations. Possibly add `{: .bleed-full }` to make it wide. Once the images are added, go back to this repository and comment out the old image path and add in the new drag-n-dropped URL.

## List of Prepared Lessons

All contained in the `lessons/` folder:

  - Intro to Ruby
    - intro-to-ruby.md
    - nouns-verbs-and-grammar.md
    - program-notes.md
    - string.md
    - integer.md
    - float.md
    - date.md
    - array.md
    - conditionals.md
    - loops.md
    - each.md
    - hash.md
    - our-own-classes.md
    - ruby-conclusions.md
    - some-more-ruby-methods.md
  - RPS-RCAV
    - rps-rcav-lesson-part-01.md
    - rps-rcav-lesson-part-02.md
    - rps-rcav-lesson-part-03.md
    - rps-rcav-lesson-part-04.md
    - rps-rcav-lesson-part-05.md
    - rps-rcav-lesson-part-06.md