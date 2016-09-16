# `CSS styleguide`

Some rules to follow when writing CSS for AMARO projects.

## Quotes

> Rulesets should only ever inherit and add to previous ones, never undo. - _Harry Roberts_

> We're not designing pages, we're designing systems of components. - _Stephen Hay_

## Notes

- Do not use ID selectors.
- Do not use `js-*` prefixed classes for styling.
- There's no need to manually add vendor prefixes to the code as it's done during our build process.

## Formatting

- Use soft tabs made by 2 paces for indentation.
- Use dashes over camelCase for block component names.
- When using multiple selectors in a rule declaration, give each selector its own line.
- In properties, put a space after, but not before, the `:` character.
- Add a blank line between each rule declaration.
- Don't prefix property values or color parameters with a leading zero, e.g. `opacity: .5`.
- Avoid specifying units for zero values, e.g. `margin: 0;`

## Colors

- Always use HEX color values.
- Always use lowercase letters in color declarations.
- Use the shorthand notation when possible.
- If you need to add opacity to a color it's prefered to use Sass `lighten` and `darken` functions.
- Do not use other scales like color names, HSL and others.

      $amaro-black: #333;
      $amaro-gray: lighten($amaro-black, 42%);
      $amaro-red: #ab2929;

## `!important`

- Avoid using `!important` at all.

> If you can explain why an `!important` is important, it's probably not important at all.

## Immutables (a.k.a. constants)

- Variables that act as constants should be named in `SNAKE_CASE_ALL_CAPS` followed by `!default`.

      $FONT_SIZE: 16px !default;

## `js-*` prefixed classes

- We use `js-*` prefixed classes to handle behavioral changes in JavaScript.
- This reduce the risk that changing the structure or theme of components will inadvertently affect the functionality.
- It's not necessary to use them in every case, just think of them as a tool in your utility belt.
- `js-*` classes should not, under any circumstances, be styled.

      <a href="/login" class="btn btn--primary js-btn-login">Login</a>

## Scales

- Some stuff can get out of hand super easily.
- Stuff like `font-size`, `line-height`, `padding`, and `z-index` can have thousands of different values in the application.
- That's why we use a standard scale for these items.
- All values for these properties must come from the definitions in the `_scales.sass` partial inside the `/_helpers` folder.

      // z-index scale example
      $z-index-1: 100;
      $z-index-2: 200;
      $z-index-3: 300;
      $z-index-4: 400;
      $z-index-5: 500;
      $z-index-6: 600;
      $z-index-7: 700;
      $z-index-8: 800;
      $z-index-9: 900;

## Specificity

- Although in the name (cascading style sheets) cascading can introduce unnecessary performance overhead for applying styles.
- The BEM methodology solves this brilliantly by allowing an easy way to create unique classes names.
- Try to abstract the selectors from elements. Elements can be easily changed, class names stays the same.

      // Avoid
      ul.user-list li span a:hover {
        color: red;
      }

      // Prefer
      .user-list__item .link:hover
        color: $amaro-red

## Quotes

- Quotes are optional in CSS and it's pre-processors. We chose to use quotes as it's visually clearer that the string is not a selector or a property.

      background-image: url("/path/to/image.jpg")
      font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;

## Ordering

1. Property declarations
    - List all standard declarations. Anything that isn't an `@include`, pseudo element or a nested selector.
    - Properties should be ordered alphabetically.
2. `@include` declarations
    - Grouping `@include` declarations at the end makes it easier to read the entire selector.
3.  Pseudo Elements
    - Pseudo elements should de declared after the `@include` rules but before any nested element to keep component consistency.
4. Nested selectors
    - **If necessary**, nested selectors go last.
    - `@include` and pseudo element rules applies to nested selectors.
    - Add a whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors.

## Variables

Prefer dash-cased variable names (e.g. `$my-variable`) over camelCased or snake_cased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. `$_my-variable`).

## Nesting

> Just because you can, doesn't mean you should do it.

- Avoid unnecessary nesting. Consider nesting only if you must scope styles to a parent and if there are multiple elements to be nested.
- A maximum of 2 levels of nesting is accepted.
