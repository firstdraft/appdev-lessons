# CSS for JS by Josh Comeau

## Module 0: Fundamentals

### Anatomy

- start with anatomy of CSS style rules 
    - **selector > rule > declaration > property > value > unit**

### Media Query

- good place to mention **accessibility**

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

### Color

- **multi-format picker: https://fffuel.co/cccolor/**

- simple
    ```css
    p {
      color: red;
    }
    ```

- hex red: `#FF0000`
- hsl red: `hsl(0deg, 100%, 50%)`
- alpha values 0 (transparent) - 1 (opaque)
    - if IE need legacy method `hsla(0deg, 100%, 50%, 0.2)`
    - all other browsers support modern `hsl(0deg 100% 50% / 0.2)` OR `hsl(0deg, 100%, 50%, 0.2)` (with commas)

- `color` property for text, `background-color` for element

- can pass images and gradients as **values** to these **properties**

### Unit

- `px` for pixels is most popular
- `em` is relative unit equal to font-size of *current* element
    - `rem` is a better choice and it means "root element", so the default HTML tag of 16px font
    - only change HTML default font size with percentages, so it respects users defautl font size:
    ```css
    html {
      font-size: 150%
    }
    ```
- `%` often used with `width` and `height` to consume available space

- generally you will need a mix of *both* `px` and `rems` to make it most **accessible**

### Typography

- `font-family` property (e.g., `Arial`, `Roboto`)
- nice location to view and see e.g., bold vs italic within a family: https://fonts.google.com/
- **serif** (edge stroke adornment; print media) vs **sans-serif** (without adornment; web)

- usually we use a link tag to add external stylesheets to make different fonts available:

    ```html
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">

    <style>
      p {
        font-family: 'Roboto', Arial, sans-serif;
      }
    </style>
    ```

    - we usually surround a **web font** in quotation marks
    - when we have many separated by commas, it is a **font stack** and the device will use the first available in the list

#### bold, italic, underline

- `font-weight: bold;` or `font-weight: 700;`
    - to actually change HTML element, need `<strong>`
- `font-style: italic;`
    - to actually change HTML element, need `<em>`
- underlined = links on the web; can remove with `text-decoration: none;`
- `<b>` and `<i>` are confusing, best to avoid

#### alignment
    
- `text-align` property to shift characters horizontally (e.g., `right` or `center`)
    - don't use for images, only text

#### Spacing

- `letter-spacing` or `line-height` properties, but `line-height` takes *unitless* number (relative to fontsize)
- **minimum line height should be 1.5**, chrome default is only 1.15!

### Browser Debugging

- need to use "Inspect element" to see what is what!
- **Elements** tab to select different boxes
    - use arrow tool tip to select elements on the page and highlight in the dev tools
    - sub-tab **Styles** shows all CSS for the element!
        - crossed out things are overwritten or invalid or **commented out in the code**
        - can toggle styles on and off and add your own styles directly here! but be careful, because page refresh = all work gone
        - **force element state** buttons to show state styles (e.g., hover)
        - shift+click on color to cycle through different representations
        - generally want color contrast > 4.5

- firefox has some nice features that show *why* a style isn't working. stick with chrome but useful to have firefox for tricky debugging

## Module 1: Rendering Logic I

