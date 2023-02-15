# Omnicalc Debug

- Notes:

  - Optional un-graded assignment, but there are tests built in

  - Project (ungraded): [https://github.com/appdev-projects/omnicalc-debug](https://github.com/appdev-projects/omnicalc-debug){:target="_blank"}

  - Useful chapters:
    - [Refactoring Fortune Teller with Dynamic Routes][Refactoring Fortune Teller with Dynamic Routes]

**Reading to insert around here: [Rubber Duck Debugging](https://www.thoughtfulcode.com/rubber-duck-debugging-psychology/){:target="_blank"}**

## Omnicalc Debug README

- Notes:

  - Copied from [https://github.com/appdev-projects/omnicalc-debug#readme](https://github.com/appdev-projects/omnicalc-debug#readme){:target="_blank"}

Here is your [target](https://omnicalc-debug.matchthetarget.com/) 

The starting point of this app has four different forms which take input from users, some of which run through the Google Maps API and the DarkSky API, be sure to [update your enviroment credientals](https://chapters.firstdraft.com/chapters/792).  

<strong>YOUR JOB:</strong> Debug all 4 forms.

It might be helpful to keep [the Forms chapter](https://chapters.firstdraft.com/chapters/881) open while working.

Debugging checklist:

 1. READ the error message. Extract as much useful information from it as possible.
 2. If there's no error message, find another way to give yourself feedback; **make the invisible visible**.
    - Use the server log.
    - Print things; in this new world, that means use embedded Ruby tags (`<%=  %>`) in the view templates. We can't use the `p` method anymore since we aren't writing command line programs anymore.
 3. If all else fails — the error message isn't helpful, or there isn't one and you can't spot the issue visually — delete the offending code (or comment it out), and re-type the R→C→A→V from scratch. Hopefully you've been making lots of git commits, so there's no fear in doing so.