# `HTML styleguide`

Some rules to follow when writing HTML markup for AMARO projects.

## Table of contents

- `TODO`

## General principles

- Strive for a semantic HTML code.
- Paragraphs of text should always be placed in a `<p>` tag.
- Never use multiple `<br>` tags to space content. Use CSS to space them if needed.
- Items in list form should always be in `<ul>`, `<ol>` or `<dl>`. **Never** use a set of `<div>` or `<p>`.
- Every form input that has text attached should utilize a `<label>` tag.
- Radio and checkboxes elements should always be wrapped inside it's `<label>` to make it user-friendly.

## Syntax

- Onle one style should exist across the entire code-base.
- Always use double quotes on attributes, never single quotes.
- Don't include a trailing slash in self-closing tags, unless it's required (React, JSX).
- Use soft tabs with two spaces - they're the only way to guarantee code renders the same in any environment.
- Nested elements should be indented once (two spaces).

## Line length

- Keep maximum line length at 80 characters.

## Doctype

- Always use the HTML 5 doctype declaration.

      <!doctype html>

## Quotes

- Always use double quotes `""` to wrap attributes values.

      <button class="btn btn--default">Default button</button>

## Meta tags

> Meta data is data (information) about data.

- The `<meta>` tag provides meta data about the HTML document.
- Meta data will not be displayed on the page, but will be parsable by the machine.

### Character encoding

- All markup should be delivered as `UTF-8`, as it's the most friendly for internationalization.
- It should be designated in both the HTTP header and the head of the document.

      <meta charset="utf-8">

### Keywords

- Define keywords for search engines.

      <meta name="keywords" content="AMARO, fashion, clothes, women, ecommerce">

### Description

- Define a description of the web page.

<meta name="description" content="Marca de fast fashion online. As últimas tendências de moda, inspiradas no streetstyle e nas passarelas internacionais. Troca e frete grátis para todo Brasil. Entrega rápida para todo o Brasil.">

### Viewport

- Define some informations about the page viewport, such as size, scale, maximum scale, if it's resizable and others.

<meta name="viewport" content="width=device-width, initial-scale=1 maximum-scale=1, user-scalable=no">

### `lang`

- From the HTML 5 spec:

> Authors are encouraged to specify a lang attribute on the root html element, giving the document's language. This aids speech synthesis tools to determine what pronunciation to use, translation tools to determine rules to use, and so forth.

- So, always define the document `lang`.

      <html lang="pt-br">

### IE compatibility mode

- Internet Explorer supports the use of a document compatibility `<meta>` tag to specify what version of IE the page should be rendered as. Unless circumstances require otherwise, it's most useful to instruct IR to use the latest supported mode with **edge mode**.

      <meta http-equiv="X-UA-Compatible" content="IE-Edge">

## CSS and JS includes

- Per the HTML spec, typically there is no need to specify a `type` when including CSS and JavaScript files as `text/css` and `text/javascript` are their respective defaults.

      <link rel="stylesheet" href="css/main.css">
      <script src="js/app.js"></script>

## Naming

- Always use lowercase tag and attribute names.

      <div class="container"> ... </div>

## Attributes order

- Classes make for great reusable components, so they come before every other attributes except for attributes that indicates source path.
- ID's are more specific and should be used sparingly (e.g. for in-page bookmarks), so they come after.
- HTML attributes should come in this particular order for easier reading:
    - First thing: `src`, `href`, `for`, `type`
    - Then, always: `class`
    - Then: `id`, `name`, `title`, `alt`
    - If needed: `aria-*`, `data-*`, `role`

        <a href="#first-title" class="link" data-modal="toggle">Size Guide</a>
        <input type="text" class="input--underlined">
        <img src="path/to/image.jpg" title="AMARO" alt="AMARO logo">

## HTML5 elements

- Use the HTML 5 elements such as `<header>`, `<footer>`, and `<section>` where appropriate.
- Also use HTML 5 form input types.

      <input type="search">
      <input type="email">
      <input type="tel">

## Boolean attributes

- A boolean attribute is one that needs no declared value.
- XHTML required you to declare a value, but HTML 5 has no such requirement.

      <button class="btn btn--buy" disabled>Comprar</button>
      <input type="checkbox" value="1" checked>

## Lean markup

- Whenever possible, avoid superfluous parent elements when writing HTML.
- Many times this requires iteration and refactoring, but produces less HTML.

      <!-- Avoid -->
      <div class="avatar">
        <img src="path/to/image.jpg">
      </div> <!-- /.avatar -->

      <!-- Prefer -->
      <img src="path/to/image.jpg" class="avatar">

## New lines

- Write every block on a new line.
- Don't add 2 different tags in the same line.

      <ul>
        <li>
          <a href="#">Link 1</a>
        </li>
        <li>
          <a href="#">Link 2</a>
        </li>
        <li>
          <a href="#">Link 3</a>
          </li>
      </ul>

## Self closing tags

- There is no need to add a final slash `/` in self closing tags.


      <!-- Prefer -->
      <br>
      <hr>
      <img src="path/to/image.jpg">

**NOTE:** This is **required** in JSX.

## Optional closing tags

- Always close optional closing tags

      <ul>
        <li>Item 1</li> <!-- <li> is a optional closing tag -->
        <li>Item 2</li>
        <li>Item 3</li>
      </ul>

## Multiple attributes

- It's cool to break multiple attributes in several lines to enforce readability whenever needed.

## Whitespace

- Always add an empty line at the end of your file.
