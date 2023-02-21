# Application Development Lessons

This repository was originally pulled from the [appdev-textbook](https://github.com/firstdraft/appdev-textbook) repository, which was being written in bookdown. That repository in turn was largely based on the [appdev-chapters](https://github.com/firstdraft/appdev-chapters) repo. 

This repository is a place to rewrite any bookdown chapters from the "textbook" into the format required for "lessons".

## Instructions to Prepare a Lesson

Here are a few things that need to be changed for the files in this repository:

 1. Rename the previous chapter by appending `-lesson.md`. We will make find-n-replace substitutions in this file, which indicates that the syntax (and some copy) was optimized for learn.

 1. Double check that any `{target...` is `{:target...` (with the `:`).

 1. Any `^` caret style footnotes need to take the form of `<aside markdown="1"></aside>` with **no indentation**. Check each footnote and see if more context needs to be added since there won't be a caret anymore. Caret's can still be used, but only really for citations since they go to the bottom of the page.

 1. Any internal cross-references need to be removed by searching for `][`. These can maybe be put back when we figure out anchor links.

 1. Remove links to old chapters, possibly replace with internal cross-references or references to other lessons.

 1. Any `**https:` should be replaced with `**https\:` when the intention is just to indicate a path (don't add the backslash on links out)

 1. Begin putting the lesson into sub-lessons by creating new files and appending `-part-01.md` after `-lesson`. So: 
    - `rps-rcav.md` is the original bookdown format, 
    - `rps-rcav-lesson.md` is the syntax changes for learn, and 
    - `rps-rcav-lesson-part-XX.md` is each part of the lesson which becomes a separate lesson on learn.

 1. References to Gitpod workspace and/or REPLs need to get a `<div class="proj / experiment" markdown="1"></div>` tag. Instructions to open a Gitpod should be consistent. As of now, it will direct the students to Canvas.

 1. The README for the Gitpod project should be reduced. All instructions should be contained in the lesson.

 1. Once the lesson is copied onto learn, you need to do a Ctrl+F to look for any `![` or `assets`, which indicate images. These images need to be dragged and dropped into those locations. Possibly add `{: .bleed-full }` to make it wide. Once the images are added, go back to this repository and comment out the old image path in the lesson and add in the new drag-n-dropped URL.

 1. Add lesson to the list below, including URL.

## List of Prepared Lessons

All contained in the `lessons/` (or sometimes `glossaries/`) folder:

  - Technical Setup
    - 
  - Intro to Ruby
    - intro-to-ruby.md, https://learn.firstdraft.com/lessons/5
    - nouns-verbs-and-grammar.md, https://learn.firstdraft.com/lessons/7
    - program-notes.md, https://learn.firstdraft.com/lessons/8
    - string.md, https://learn.firstdraft.com/lessons/9
    - integer.md, https://learn.firstdraft.com/lessons/10
    - float.md, https://learn.firstdraft.com/lessons/11
    - date.md, https://learn.firstdraft.com/lessons/12
    - array.md, https://learn.firstdraft.com/lessons/14
    - conditionals.md, https://learn.firstdraft.com/lessons/15
    - loops.md, https://learn.firstdraft.com/lessons/16
    - each.md, https://learn.firstdraft.com/lessons/17
    - hash.md, https://learn.firstdraft.com/lessons/18
    - our-own-classes.md, https://learn.firstdraft.com/lessons/19
    - ruby-conclusions.md, https://learn.firstdraft.com/lessons/20
    - some-more-ruby-methods.md, https://learn.firstdraft.com/lessons/21
  - RPS-RCAV
    - rps-rcav-lesson-part-01.md, https://learn.firstdraft.com/lessons/22
    - rps-rcav-lesson-part-02.md, https://learn.firstdraft.com/lessons/23
    - rps-rcav-lesson-part-03.md, https://learn.firstdraft.com/lessons/24
    - rps-rcav-lesson-part-04.md, https://learn.firstdraft.com/lessons/25
    - rps-rcav-lesson-part-05.md, https://learn.firstdraft.com/lessons/26
    - rps-rcav-lesson-part-06.md, https://learn.firstdraft.com/lessons/27