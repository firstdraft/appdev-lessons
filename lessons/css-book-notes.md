# CSS for JS by Josh Comeau

## Fundamentals

### Anatomy

- start with anatomy of CSS style rules 
    - **selector > rule > declaration > property > value > unit**

### Media Query

- @media queries because different screen sizes are very important
    - provides a nice intro to conditionals!

        ```css
        @media (condition) {
        /* Some CSS that'll run if the condition is met. */
        }

        @media (max-width: 300px) {
            .small-only {
              color: red;
              font-size: 50%;
            }
        }
        ```

    - we typically use either `max-width` to add styles on small screens, or `min-width` to add styles on larger ones.

### Selectors

- different types of selectors: **elements** vs. **class**

    ```css
    /* Turn all links red! */
    a {
      color: red;
    }

    /*
    Remove the underline from all elements that
    have been given a class of `navigation-link`
    */
    .navigation-link {
      text-decoration: none;
    }
    ```

    - different **combinators** (e.g., `nav a` descendent selector vs `nav > a` child selector)
        - **children** (one level) vs **descendents** (n-levels)

### Pseudo Classes and Elements

- "pseudo-classes" can probably be skipped: apply CSS based on element's state (`:hover` could be a nice one to show though):

    ```html
    <style>
        button:hover {
            color: blue;
        }
    </style>

    <button>Hover over me!</button>
    ```

    - could be shown with `<button>` elements
    - "pseudo-elements" generally use `::` indicator, these can be attributes within an html tag (e.g. `placeholder` in `<input type="text" placeholder="A1A 1A1" />`)

- using `::before` or `::after` pseudo-elements are ok if the `content` is just decorative 

## Color

- simple
    ```
    p {
      color: red;
    }
    ```