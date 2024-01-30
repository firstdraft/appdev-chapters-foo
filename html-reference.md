# HTML Reference

## The very basics

### p — a paragraph

Most text content is comprised of paragraphs, and most of the web is text; therefore, `p` elements are the workhorse of the web. But don't overuse them! Try to use them only for actual paragraphs of text. (If you're just looking for a generic block container, then try `div` instead.)

Examples:

```html
<p>
  Not much to it.
</p>
```

Produces:

<p>
  Not much to it.
</p>

### h1, h2, h3, h4, h5, h6 — a heading for any occasion

HTML offers six levels of headings — `h1` through `h6`. Choose one based on the correct semantic level of hierarchy — is it the top-level heading of the page? the secondary heading? tertiary?

Don't choose based on the default style (size, weight) that the browser assigns — we're going to override those awful default styles anyway.

Examples:

```html
<h1>Top-most heading</h1>
<h2>Second-level heading</h2>
<!-- etc -->
<h6>The last level</h6>
```

Produces:

<h1>Top-most heading</h1>
<h2>Second-level heading</h2>
<!-- etc -->
<h6>The last level</h6>

### img — images

Examples:

```html
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/86/Evolution_of_a_Tornado.jpg/1024px-Evolution_of_a_Tornado.jpg">
```

Produces:

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/86/Evolution_of_a_Tornado.jpg/1024px-Evolution_of_a_Tornado.jpg">

### a — a link

Examples:

```html
Click <a href="https://www.google.com/">here</a> to search.
```

Produces:

Click <a href="https://www.google.com/">here</a> to search.

If you want the link to open in a new tab, add the `target="_blank"` attribute:

Examples:

```html
Click <a href="https://www.google.com/" target="_blank">here</a> to search but not leave us.
```

Produces:

Click <a href="https://www.google.com/" target="_blank">here</a> to search but not leave us.

## Lists

### Unordered and ordered lists

For simple lists, you have two choices: `ul` (unordered) or `ol` (ordered) lists.

Use `ul` if the items have no particular order. Use `ol` if the items are ordered.

By default, the browser will use bullets before each item in a `ul` and will automatically number each item in an `ol` (starting with 1). We can and will overwrite these default styles; most of the time we don't want bullets at all. So choose `ul` or `ol` based on the _semantics_ of the list, not on bullets.

#### li — each item in the list

Nested within the `ul` or `ol` should come one or more `li` elements that contain the actual items in the list.

Examples:

```html
<ul>
  <li>Apple</li>
  <li>Banana</li>
  <li>Orange</li>
</ul>
```

Produces:

<ul>
  <li>Apple</li>
  <li>Banana</li>
  <li>Orange</li>
</ul>

```html
<ol>
  <li>Apple</li>
  <li>Banana</li>
  <li>Orange</li>
</ol>
```

Produces:

<ol>
  <li>Apple</li>
  <li>Banana</li>
  <li>Orange</li>
</ol>

### Definition lists

When you have a list of things along with a _label_ for each thing, a `dl` (definition list) might fit the bill. Each label goes in a `dt` (definition term), and each piece of data goes in a `dd` tag (definition description).

Examples:

```html
<dl>
  <dt>First name</dt>
  <dd>Raghu</dd>

  <dt>Last Name</dt>
  <dd>Betina</dd>

  <dt>Role</dt>
  <dd>Instructor</dd>
</dl>
```

Produces:

<dl>
  <dt>First name</dt>
  <dd>Raghu</dd>

  <dt>Last Name</dt>
  <dd>Betina</dd>

  <dt>Role</dt>
  <dd>Instructor</dd>
</dl>

## Tables

In HTML, the `<table>` element is used to represent two-dimensional, tabular data. A simple table looks like this:

```html
<table border="1">
  <tr>
    <td>First</td>
    <td>Last</td>
  </tr>
  <tr>
    <td>John</td>
    <td>Doe</td>
  </tr>
  <tr>
    <td>Jane</td>
    <td>Doe</td>
  </tr>
</table>
```

which would produce this[^border1]:

[^border1]: The `border="1"` attribute is rarely used. It throws a quick and dirty border around all cells; I include it here to make it easy to see what's going on in these examples. In reality, we would use CSS if we want borders.

<table border="1">
  <tr>
    <td>First</td>
    <td>Last</td>
  </tr>
  <tr>
    <td>John</td>
    <td>Doe</td>
  </tr>
  <tr>
    <td>Jane</td>
    <td>Doe</td>
  </tr>
</table>

The things to keep in mind about tables are:

 - Every piece of data must reside within a cell, a `<td>` (table data) element.
 - Every `<td>` element must reside within a row, a `<tr>` element.
 - Every `<tr>` must have the same number of cells, or things get out of whack.

Despite this last rule, you can, however, "merge" cells using the `colspan` attribute:

```html
<table border="1">
  <tr>
    <td colspan="2">People</td>
  </tr>
  <tr>
    <td>John</td>
    <td>Doe</td>
  </tr>
  <tr>
    <td>Jane</td>
    <td>Doe</td>
  </tr>
</table>
```

produces:

<table border="1">
  <tr>
    <td colspan="2">People</td>
  </tr>
  <tr>
    <td>John</td>
    <td>Doe</td>
  </tr>
  <tr>
    <td>Jane</td>
    <td>Doe</td>
  </tr>
</table>

You can see that we've merged two cells in the first row together; the `colspan="2"` on the first cell ensures that we don't violate the "every `<tr>` must have the same number of cells" rule.

There's also a similar `rowspan` attribute to merge vertically, although we use it much more rarely.

## Generic elements

### div — a generic block level container

The `div` tag defines a division or a section in an HTML document. Similar to a `p` tag, but it should be used to contain or group together other tags, not just text.

```html
Regular text
<div>
  Block level <a href="https://google.com">element</a>
</div>
```

Regular text
<div>
  Block level <a href="https://google.com">element</a>
</div>

### span — a generic in-line container

The `span` tag is used to group inline-elements in a document. It provides no visual change by itself. It's most commonly used to style or select a specific part of text.

```html
My mother has <span>brown</span> eyes
```

My mother has <span>brown</span> eyes
## Housekeeping

### html

The `html` tag tells the browser that this is an HTML document. It is used as a container for all of the HTML of an entire document or page (except for the `<!DOCTYPE>` declaration).

```html
<!DOCTYPE html>
<html>
  
</html>
```
### head

The `head` tag  contains information about an HTML document that is used by browsers and web crawlers but is not displayed to website visitors. The head is where you put information like the page title, the character selection, or link to your site's [favicon](https://www.w3schools.com/html/html_favicon.asp){:target="_blank"}.

```html
<!DOCTYPE html>
<html>
  <head>
    
  </head>
</html>
```
### body

The `body` tag contains the entire content of a webpage. It must be the second element inside of the parent html element, following only the head element. Any text, links images, list, or tables go inside the body.

```html
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    This is a whole HTML page.
  </body>
</html>
```

#### title

The `title` tag is required and used to assign a title to an HTML document. These titles are not displayed in the browser window, but they are used as the page name by search engines and displayed by browsers in the title bar, on the page tab, and as the page name of bookmarked webpages.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Reference</title>
  </head>
  <body>
    This is a whole HTML page.
  </body>
</html>
```

![](/assets/browser-title.jpg)

With the addition of `<title>`, we now have a complete, valid HTML document.

#### meta

The `meta` tag is  used to add machine-readable information to an HTML page. These tags always go in the `head` tag and are typically used to specify information about the content of the page. For example, page description, keywords, author of the document, or type of characters used.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Reference</title>
    <meta charset="utf-8">
    <meta name="author" content="John Doe">
  </head>
  <body>
    This is a whole HTML page.
  </body>
</html>
```

#### link

The `link` tag defines a link between a document and an external resource. This element is most commonly used to define the relationship between a document and one or more external CSS stylesheets.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Reference</title>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="theme.css">
  </head>
  <body>
    This is a whole HTML page.
  </body>
</html>
```
