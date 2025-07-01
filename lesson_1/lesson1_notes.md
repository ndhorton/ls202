# 1:1

Docs and standards:

* MDN - unofficial docs

* W3C - specs

* WHATWG - for newest HTML and DOM specs

# 1:2

Come back for the section on what you need to understand for later courses to test yourself.

Vocab -- become comfortable with

* element and tag

* self-closing tag

* document type definition (DOCTYPE, DTD)

* attribute

* selector

* property

* id, class, and name

<u>Basic HTML elements</u>

Start with:

* `<p>` -- paragraph, the primary organizational construct for text on web pages

* `<a>` -- anchor, hyperlinks to other web pages

* `<h1>`...`<h6>` -- headings of various levels

Then:

* `<em>`, `<strong>`

* `<header>`, `<main>`

* `<article>`, `<section>`, `<aside>`

* `<div>`, `<span>`

<u>Using CSS with HTML</u>

Three ways to use CSS in an HTML document:

* inline

* internal

* external

Using `<style>` tag for internal CSS

<u>Basic CSS Selectors</u>

* tag name

* `id` attribute

* `class` attribute

<u>CSS Properties</u>

Don't try to memorize CSS properties at first; you need to see them in action. Retain them based on their usefulness in practice.

Important properties that you will certainly memorize include:

* `color`

* `background-color`

* `font-family`

* `font-size`



# 1:6

HTML provides three ways to identify certain elements: `class`, `id`, and `name`. Any element can use a `class` or `id` attribute, and a variety of elements can use the `name` attribute. Some elements can use all three at once:

```html
<input type="submit" name="save" id="save-button" class="default-button">
```

## Class

`class` is a global attribute. A class should group a number of elements on the page semantically. Classes are used by CSS to select a set of elements, also by JavaScript.

* Use the `class` attribute to assign a class or classes to an element.

* Any number of elements may belong to the same class.

* Any element can belong to one or more classes. List all the names separated by spaces in the `class` attribute, e.g `class="executive management full-time"`.

* Prefer semantic class names; they should provide meaning. For instance, use `teaching-assistant` rather than `yellow-background`.

* Use CSS selectors (`.classname`) to select elements by class, e.g. `.teaching-assistant`.

* Class selectors have lower CSS specificity than ID selectors (an ID selector overrides a class selector), but higher than tag name selectors (a class selector overrides a tag selector). Thus, the `.teaching-assistant` selector overrides the `tr` selector.

## ID

The `id` global attribute applies a unique identification string to a single element, such as a headline; no other `id` atrributes on the page should have the same ID.

* Ust he `id` attribute to assign an ID to an element.

* Each ID on a page must be unique.

* Eache element can have one ID or none.

* Use semantic ID names; they should provide meaning. For instance, use an ID name of `headline` rather than `big-font`.

* Use CSS ID selectors (`#idname`) to select elements by ID, e.g. `#headline`.

* ID selectors have higher CSS specificity than class selecctors (an ID selector can override a class selector).

The browser won't tell you when you use the same ID on more than one element. In fact, it may even apply your styles to several tags with the same ID. You will run into problems with JavaScript, though, if you try to take advantage of this behaviour. Use the W3C HTML validator to catch accidental ID duplication.

## Name

For now, all you must know about the `name` attribute is that it ties form elements to data on the server - it typically doesn't play a role in styling. You can use the `[name="field-name"]` attribute selector to select elements by name, but you should use a class or ID selector instead. When you submit a form, the browser sends the form data to the server using name/value pairs in which each name comes from the associated `name` attribute.

* Use the `name` attribute to assign a name to a form data element that the server can use to obtain the value (e.g. `<input type="text">`).

* Not all tags accept the `name` attribute; it applies to input controls in forms. Some other elemnts have a `name` attribute, too, but with a different meaning.

* Always use a `name` attribute on form elements that accept it.

* Each name in a form should be unique within that form except for radio buttons and checkboxes that belong to a single group.

* Use descriptive `name` values, not semantic. For instance, use `name="last-name"` instead of `name="input-field"`.

* Avoid trying to select elements in CSS by using the `name` attribute.






