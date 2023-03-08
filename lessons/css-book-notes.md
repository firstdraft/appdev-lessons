# CSS for JS by Josh Comeau

## Fundamentals

- start with anatomy of CSS style rules 
    - selector > rule > declaration > property > value > unit

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

- different types of selectors: elements vs. class

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



