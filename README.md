# Application Development Textbook

This repository will hold the outline for a textbook written with [bookdown](https://bookdown.org/). Some notes about using bookdown can be found [here](https://www.bendirt.com/bookdown/). But there are more and better details in the section below.

The site is deployed at [https://firstdraft.github.io/appdev-textbook/](https://firstdraft.github.io/appdev-textbook/) from the `docs/` folder, which was generated locally with the R command `bookdown::render_book()`.

## Practical guide to get to work

Here is a practical guide for how to edit and compile the book. A lot more details can be found in the [official documentation](https://bookdown.org/yihui/bookdown/), and there are some important details in the next section.

1. Our file structure:

    ```
    .
    ├── assets                         # images, one subdir for each lesson file
    │    └── lesson-name  
    │        └── <...>.png
    ├── docs                           # compiled by bookdown::render_book()
    │   └── <...>.html
    ├── glossaries                     # tech ref glossaries
    │   └── <...>-reference.md  
    ├── lessons                        # markdown file for each lesson / chapter
    │   └── <lesson-name>.md
    ├── original-outline               # original outline for reference
    │   └── appdev-content-outline.md
    ├── _bookdown.yml                  # config file with chapter order and compilation location docs/
    ├── _output.yml                    # config file with styling of output
    ├── .nojekyll                      # tell github pages not to render with jekyll
    ├── index.md                       # required by bookdown, frontmatter for book
    ├── outline-notes.md               # first chapter, meta-notes
    └── README.md
    ```                   

1. Add a lesson (chapter) by creating a `.md` file in `lessons/` or `glossaries/`. The file needs to start with `# My File!`, which will be the chapter heading. By convention, I name the file `my-file.md` (lower case, hyphens, remove punctuation). This makes cross-referencing the chapter easier. The file should only contain *one* `<h1>` heading (I think it can contain more, but we may just want to follow this convention to keep things separated):

      ```
      # My File!

      ## A sub-section

      ### Another sub

      ## And so on
      ```

1. When you add a lesson, you need to go into the `_bookdown.yml` configuration file and add it to the `rmd_files` list *in the location you want it to appear*:

      ```
      rmd_files: 
        [
          # frontmatter
          "index.md", 
          "outline-notes.md",

          # lessons
          "lessons/course-overview.md", 
          =====> "lessons/my-file.md", <=====
          "lessons/technical-setup.md",
          ...
      ```

1. When you add a lesson (new `.md`  file), also make an `assets/` sub-directory (even if it's empty). Like `lessons/my-file.md`, `assets/my-file/`. **And if you change the `.md` file-name, change the sub-directory name**. Never put chapter numbers in any filenames. We don't want to imply any order.

1. Here are instructions for getting R to work with VS Code so we can render the book: [https://www.bendirt.com/bookdown/#installing-r-with-vs-code](https://www.bendirt.com/bookdown/#installing-r-with-vs-code)

1. You should have installed these packages in the R terminal: 
      - `install.packages("languageserver")`
      - `install.packages("rmarkdown")`
      - `install.packages("bookdown")`
  
1. You can now access these commands from you interactive R terminal opened in the book directory:

      - **`bookdown::render_book()`** will render with default settings and will find the `_output.yml` and `_bookdown.yml` configuration files to instruct it. 
          - Once the book is rendered, you can install the VSCode extension [Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server) and you should be able to view the HTML documnet at `http://127.0.0.1:3000/docs/`. 

          - If you get 404'd at that address, try to open one of the `.html` files in the `docs/` folder and click the "Open Preview" in the VSCode editor, which should open the local port for viewing.

      - **`bookdown::preview_chapter("lesson/my-file.md")`** will just re-render the chapter you specify and is faster when the book is getting long. But other chapters are not re-rendered so cross-references may not work correctly.

      - **`bookdown::clean_book(TRUE)`**, if something is going wrong and you just want to re-render the whole book from scratch. Run `bookdown::render_book()` after this command.

### Notes and Quirks of Bookdown

- Additional book configuration is contained in the required `index.md` file in the frontmatter:

  ```
  ---
  title: "AD1"
  author: "Ben + Raghu"
  date: "`r Sys.Date()`"
  description: "This book covers the AD1 course at UChicago"
  url: # 'https\://bookdown.org/john/awesome/'
  github-repo: "bpurinton/appdev-textbook"
  site: bookdown::bookdown_site 
  documentclass: book
  favicon: "assets/favicon.ico"
  ---
  ```

  **So there are three places configuration needs to be changed:** 
    1. `index.md` frontmatter (title, author, date, url, github-repo, etc.)
    2.  `_bookdown.yml` (view and edit github links, and file order)
    3. `_output.yml` (type of output format and styling options for that format)

  **There are some github links spread around that need to be changed if the repo is moved, find and replace with `<location>/<repo-name>`. Currently they are `firstdraft/appdev-textbook`**

---

- There are many options for [the render function](https://bookdown.org/yihui/bookdown/build-the-book.html#build-the-book) and the [`_bookdown.yml` file](https://bookdown.org/yihui/bookdown/configuration.html#configuration) and[`_output.yml` file](https://bookdown.org/yihui/bookdown/output-formats.html#output-formats) configuration files.

---

- If you don't want a section to be numbered then identify it like so `# My un-numbered section {-}`

---

- The glossaries are kept in a separate directory and the *first* glossary in the `_bookdown.yml` `rmd_files` starts with: 

  ```
  # (APPENDIX) Glossaries {-}

  # Terminology Technical Reference
  ```

  This separates the glossaries from the main content in the rendered book

---

- Bookdown can use `.Rmd` (R-markdown) files that can include executable blocks for R code for generating figures, etc. It's also happy to just use `.md` files. 

---

- It is built on pandoc so the kramdown tags like `{:}` need to be written like `{}` (no colon)

---

- Cross-referencing ([documentation](https://bookdown.org/yihui/bookdown/cross-references.html)) can be a little tricky, but it works like this:

  - `[some text][My File!]`, and "some text" will then link to the named section in the book, *include the full section name with puncutation*. 
  
  - This also works for sub-sections. Like if we had our file:

      ```
      # My File!

      ## A sub-section

      ### Another sub

      ## And so on
      ```
    
    Then in another file we could write:

      ```
      # My other lesson

      A [backlink][A sub-section] to first lesson's subsection
      ```
    
    If you want a *unique* section identifier we need to do it differently. You can name it like (*always include the `#`*):

      ```
      ## A sub-section {#myID}
      ```
    
    And then I would link it in other files by writing:

      ```
      # My other lesson

      A [backlink](#myID) to first lesson's subsection
      ```
    
    **Broken internal links are probably going to happen. If you change a section name, you need to find and replace all such names in *all* files, using clever `[name]` or `{#name}` or `(#name)` in the search.**

---

- I'm still working on text cross-referencing for the glossaries and may add notes for that here.

---

- I am rendering the document online using github pages by setting the "Pages" branch to `/docs`. That means re-rendering any changes locally and then pushing the static `/docs` folder to github and waiting for the deploy action to run. There may be a better automated way. The documentation suggests using travis with github pages: [https://bookdown.org/yihui/bookdown/github.html#github](https://bookdown.org/yihui/bookdown/github.html#github).

---

- We can add widgets.. something to consider: [https://bookdown.org/yihui/bookdown/html-widgets.html](https://bookdown.org/yihui/bookdown/html-widgets.html)