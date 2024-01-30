# HTML Cheatsheet

## Basic Syntax

An HTML page is made up of **elements**.

An **element** is constructed from an opening tag, content, and a closing tag. The general structure looks like:

```html
<tagname>Content goes here...</tagname>
```

<small>`tagname` is a not a real HTML tag, but a placeholder for any HTML tag.</small>

### Attributes

An attribute specifies additional information about the element. One or more attributes can be added inside the opening tag after the tag name. Attributes are usually structured as name/value pairs in the format `name="value"`.

For example:

```html
<a href="https://www.wikipedia.org">
  Go to Wikipedia
</a>
```

Most attributes only make sense on specific elements.

For example:
- `href=""` is for `<a>` elements, to specify where to take the user when they click the link.
- `src=""` is for `<img>` elements, to specify the url of the image to load.
- `for=""` is for `<label>` elements, to specify which input element it is paired with.

Some attributes can be put on almost any element, like `class=""` or `id=""`. ​Any single `id` should only be used **once** per document. A class can and should be used repeatedly.

### Exceptions

There are a few elements that don't require content and therefore don't have a closing tag.

The most common ones are:
- `<img>`
- `<input>`
- `<br>`
- `<hr>`
- `<meta>`
- `<link>`

### Nesting Elements

Elements can contain other elements. When that happens, the one inside is known as a **child element** and the one outside is the **parent element**.

If there are multiple levels of nesting, then all the elements inside an outer element are its _descendants_. Similarly, an element that contains other elements is referred to as an _ancestor_.

## Required Elements

There are required elements that every HTML page must have to be considered **valid**, according to [W3](https://www.w3.org/Consortium/) HTML specifications. You can paste any HTML into the [W3C Validator](https://validator.w3.org/#validate_by_input) to verify that your document is valid.

### Doctype Declaration

```html
<!DOCTYPE html>
```

This must be **the very first line** in the file. It instructs the web browser about what version of HTML the page is written in.

### `<html>` element

```html
<!DOCTYPE html>
<html>
</html>
```

The `<html>` element is the ancestor of every other HTML element on the page (except for the `<!DOCTYPE>` declaration). It contains **exactly** two other elements: `<head>` and `<body>`.

### `<head>` element

```html
<!DOCTYPE html>
<html>
  <head>
  </head>
</html>
```

This element contains information and instructions for the browser on how to process the document; things like what title or icon to put in the browser tab, what style sheets to load, what language to use, etc. 

### `<title>` element

```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Cheatsheet</title>
  </head>
</html>
```

This element is used to assign a title to an HTML document. These titles are not displayed in the browser window, but they are used as the page name by search engines and displayed by browsers in the title bar, on the page tab, and as the page name of bookmarked webpages.

### `<body>` element

```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Cheatsheet</title>
  </head>
  <body></body>
</html>
```

This element contains all other elements and content that a user can see or interact with. It must be the second element inside of the parent `<html>` element, following only the `<head>` element.

## Types of Elements

### Block-level

A block-level element always starts on a new line and takes up the full width of its parent element.

Common block-level elements include:
- `<div></div>`
- `<h1><h1>` through `<h6></h6>`
- `<p></p>`

### Inline

An inline elment does not start on a new line and only takes up as much width as necessary.

Common inline elements include:
- `<img>`
- `<a></a>`
- `<span></span>`

<hr>
