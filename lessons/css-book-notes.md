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

- experiment with selecting an element and changing CSS styles, e.g., on a `a` link in the rule for `cursor` property, change to `crosshair`

## Module 1: Rendering Logic I


### Default Styles

- can steal Josh's common-sense functional styles: https://courses.joshwcomeau.com/css-for-js/treasure-trove/010-global-styles

```css
/*
  Typographic tweaks!
  4. Add accessible line-height
  5. Improve text rendering
*/
body {
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
}

/*
  6. Improve media defaults
*/
img, picture, video, canvas, svg {
  display: block;
  max-width: 100%;
}

/*
  7. Remove built-in form typography styles
*/
input, button, textarea, select {
  font: inherit;
}
```

### Inheritance

- certain CSS properties **inherit** (pass down through all **descendants**)

```html
<style>
  p {
    color: deeppink;
  }
</style>

<p>
  I know <em>you</em> are, but what am I?
</p>
```

- `<em>` inherits the `color` from `<p>`
- won't work with `border` property (kinda obvious why)

- most inherited properties are **typography related**: `color`, `font-size`, `text-shadow`, etc.

- can **force inheritance**: `color: inherit` declaration

### The Cascade

- browser chooses one of conflicting property values when there is overlap (e.g., element selector and class selector both have a `color` property)
- "winner" depends on **specificity**
    - classes are more specific than element tags
    - IDs are more specific than classes

### Block and Inline Directions

- The **web was built for displaying inter-linked documents**, so CSS mechanics are inherited from print world
- words are combined into **blocks** (e.g., `<p>`)
- pages are just blocks stacked up
- so we have horizontally oriented words and vertically oriented blocks (two directions)
- CSS has a **block** and and **inline** direction

- this is the **flow layout** (see below)

### Logical Properties

- only really important for *internationalization*

### The Box Model

**Box Model is shown in dev tools by the colored rectangles**

The four aspects that make up the box model are:
  1. Content
    - what's the copy
  2. Padding
    - what's the inner space
  3. Border
    - what's surrounding the inner space
  4. Margin
    - space around the element

- use declaration `box-sizing: border-box` to include padding and border on size of a box, to make this default behavior add:

    ```css
    *,
    *::before,
    *::after {
      box-sizing: border-box;
    }
    ```

- padding can be set globally (`padding: 20px`) or assymetrically (`padding-top: 20px`; `padding: top right bottom left`)

- border style is set with `border: width style color;` 
- `border-radius: 25 px` **rounds all corners**; `border-radius: top-left top-right bottom-right bottom-left` can **round individual corners**
- `border-radius: 50%` creates a circle / oval

- `outline: width style color` goes around the border and does not affect layout (**outline = box shadowing**)

- symmetric margins with `margin: 20px`, assymetric with `margin: top right bottom left`
- margins can be negative to put element outside of parent
- margins dictate the **gap between elements**
- `margin: auto` (or `margin-left/right: auto`) try to use all available space for the margins; good for **centering** (if `width` has been set)

### Flow Layout

- default of seven layout modes (also positioned, flexbox, css grid, etc.)
- **flow layout = microsoft word** intendended for documents
- plain HTML doc w/out CSS uses flow
- **block** (`<div>`, `<header>`, etc.) and **inline** (copy, `<a>`, `<span>`) elements
- `display: block` declaration can turn **any element into a block**
- blocks take up the entire width, can be shrunk with `width: fit-content`, **but block elements cannot be placed side-by-side**

```html
<style>
h2 {
  width: fit-content;
  border: 2px dotted;
}

.red-box {
  border: 10px solid red;
}
</style>

<h2>
  Hello World
</h2>
<div class="red-box"></div>
```

- `display: inline-block` is a way of changing an inline element to have block behavior (e.g., can give it margin and alignment), but it doesn't allow line wrapping

### Width Algorithms

- `auto`, `min-content`, `max-content`, `fit-content`
- create a centered wrapper:
    ```css
    max-width-wrapper {
        max-width: 350px;
        margin-left: auto;
        margin-right: auto;
        padding-left: 16px;
        padding-right: 16px;
    }
    ```

