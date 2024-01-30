# Forms, Query Strings, and Params

We use forms to collect information from users. Only by submitting this information to our application, and processing it, does our application start to become interesting.

## A bare bones HTML form

```html
<form>
</form>
```

### Required elements and attributes

A form must have an `action` attribute. The value of this attribute is the route/URL that the user should visit when the form is submitted.

```html
<form action="/process_form">
</form>
```

Forms generally capture user input using `<input>`[^Input] elements. Each `<input>` must be a child element of the form.

```html
<form action="/process_form">
  <input>
</form>
```

[^Input]: `<input>` elements are one of [the few HTML elements](https://chapters.firstdraft.com/chapters/879#exceptions) that don't require a closing tag.

A `<button>` element is required to submit the form.

```html
<form action="/process_form">
  <input>
  <button>Submit</button>
</form>
```


### `<input>` attributes

At a minimum, each `<input>` needs a `name` attribute and a `value` attribute.

The value for the `name` attribute can be anything, but it should be unique within the form.

```html
<!-- GOOD -->
<form action="/process_form">
  <input name="email">
  <input name="password">
  <button>Submit</button>
</form>
```

```html
<!-- BAD -->
<form action="/process_form">
  <input name="email">
  <input name="email">
  <button>Submit</button>
</form>
```

By default the `value` attribute is empty, but it will automatically receive the text that the user typed into the field as the value.

You can also set an initial value for the `value` attribute. This is especially useful for "edit" forms.

```html
<form action="/process_form">
  <input name="email" value="test@example.com">
  <button>Submit</button>
</form>
```

which renders in the browser like this:

<div class="full-bleed">
  <input name="email" value="test@example.com">
</div>

## Submitting a form

Forms are used to collect information from our users and that information is sent to our app for processing. But how does our app _know_ what the user typed in the form?

### Query string

The query string is an optional part of a URL that begins with a `?`. Since it's optional, you can add a query string to the end of any URL:

<span style="font-size: 1.2rem;font-family: monospace;">http://www.example.com/<span style="color: red; text-decoration: underline;">?fruit=apple&color=green</span></span>

A query string functions similar to a Ruby Hash— it's a list of key-value pairs. In the example, `fruit` and `color` are keys, while `apple` and `green` are the values. 

Forms are useful because they _automatically_ create a query string when they are submitted. The keys in the resulting query string come from the `name` attribute of the `<input>` while the `value` comes from whatever the user typed into that field. The URL segment before the query string comes from the `action` attribute of the `<form>`.

```html
<form action="http://www.example.com/">
  <input name="fruit" value="apple">
  <input name="color" value="green">
  <button>Submit</button>
</form>
```
  
<span style="font-size: 1.2rem;font-family: monospace;">http://www.example.com/<span style="color: red; text-decoration: underline;">?fruit=apple&color=green</span></span>


So when a form is submitted, the user is sent to the URL that was specified in the `action` attribute of the form. The name-value pairs from each input field inside the `<form>` element are added as a query string onto the URL from the `action`. Try it out!

## Demo

<div class="iframe-container" style="overflow: hidden;padding-top: 56.25%;position: relative;"><iframe loading="lazy" style="border: 0;height: 100%;left: 0;position: absolute;top: 0;width: 100%;" src="https://jelani.dev/form-demo/"></iframe></div>

## params

In Rails, `params` is a special Hash that is defined every time someone visits a URL. Rails will first check to see if a query string is present and if it finds one, it adds any name/value pairs into a Ruby Hash. With the user input in a Hash we can more easily access and manipulate it in our application.

Assuming our application has a route defined for `/add_fruit` and a user submitted a form that resulted in visit to this URL:

<span style="font-size: 1.2rem;font-family: monospace;">/add_fruit<span style="color: red;">?fruit=apple&color=green</span></span>

Rails reads the query string and adds each name/value pair into the `params` Hash:

<span style="font-size: 1.2rem;font-family: monospace;">{<span style="color: red; ">&quot;fruit&quot; <span style="color:black;">=></span> &quot;apple&quot;<span style="color:black;">,</span> &quot;color&quot; <span style="color:black;">=></span> &quot;green&quot;</span>}</span>

Try it out!

### params Demo

<div class="iframe-container" style="overflow: hidden;padding-top: 56.25%;position: relative;"><iframe loading="lazy" style="border: 0;height: 100%;left: 0;position: absolute;top: 0;width: 100%;" src="https://jelani.dev/form-demo/params"></iframe></div>

## Valid forms

While the previous forms were all _functional_ in that they created a query string with all of the information that a user filled out, they were technically invalid.

In order for a form to be considered valid by HTML standards, it must have a `<label>` element that is connected to each `<input>` element that the user interacts with.

First, add the `<label>` elements for each `<input>`:

```html
<form action="/process_url">
  <label>Fruit</label>
  <input name="fruit">
  <label>Color</label>
  <input name="color">
  <button>Submit</button>
</form>
```

Then, in order to connect one `<label>` to one `<input>`, both the `<label>` and `<input>` need an attribute with the **same** unique value.

The `<label>` element needs a `for=""` attribute while the `<input>` element needs an `id=""` attribute.

The value of these attributes can be anything, but remember it must be unique.

A complete valid form looks like this:

```html
<form action="/process_url">
  <label for="zebra">Fruit</label>
  <input id="zebra" name="fruit">
  <label for="giraffe">Color</label>
  <input id="giraffe" name="color">
  <button>Submit</button>
</form>
```

### Why use valid forms?

There are several reasons we need to write valid forms in our HTML:
- The tests for `rails grade` will fail, since they won't know how to fill out your forms.
- For users visiting our app from a phone, it's hard to tap on checkboxes. In valids forms, if you click on a label, it checks/unchecks the connected checkbox.
- Screen readers need the `for=""` and `id=""` attributes in order to understand how to fill out the form.
- Search engines penalize you if the forms on your site are invalid.

<br>
