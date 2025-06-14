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



# Code Academy tutorial

An HTML <strong>element</strong> consists of at least one <strong>tag</strong> but often consists of two tags (opening and closing tags) enclosing some optional content.



* <strong>HTML element</strong> -- a unit of content in an HTML document formed by HTML tags and the text or media contained by them

* <strong>HTML tag</strong> -- the element name, surrounded by an opening `<` and closing `>`

* <strong>Content</strong> -- the information (text or other elements) contained between the opening and closing tags of an HTML element



**The Body**

Only content inside the opening `<body>` and closing `</body>` tags can be displayed to the screen.

Some browsers will render content placed outside the `body` tags to accomodate mistakes in an HTML document, but not all of them. Ensure that all your displayable elements are contained within the `body` tags to ensure the page renders correctly.



**HTML Structure**

HTML is organized as a collection of family tree relationships. When an element is contained within another element, the enclosed element is said to be the <strong>child</strong> of the enclosing element. The child element is said to be <strong>nested</strong> inside of the <strong>parent</strong> element. The relationship between elements and their encestor and descendent elements is known as <em>hierarchy</em>.

Child elements can inherit behavior and styling from their parent element.



**Divs**

`<div>` is short for 'division'. Divs function as containers that dive the page into sections; a div is useful for grouping elements together. `<div>`s don't inherently have a visual representation, but they are very useful when we want to apply custom styles to our HTML elements. `<div>`s allow us to group HTML elments to apply the same styles for all HTML elements inside. We can also style the `<div>` element as a whole.



**Attributes**

Attributes can be added to the opening tag of an element to change its behaviour or provide extra data about it. Attributes are name-value pairs, where the name and value are separated by `=`.

A common attribute is the `id`. This attribute can serve several functions in HTML, one of which is helping us identify content on a page.

Example use:

```html
<div id="intro">
  <h1>Introduction</h1>
</div>
```

**Paragraphs and Spans**

* Paragraphs (`<p>`) contain and display a block of plain text that defines a paragraph

* Spans (`<span>`) contain short pieces of text or other HTML. They are used to separate small pieces of content that are on the same line as other content.

We use `<span>` <em>inline</em> within a larger section of content like a paragraph, whereas `<div>` divides content into <em>blocks</em>.



**Styling Text**

You can do some styling of text using HTML tags. The `<em>` tag emphasizes text, while the `<strong>` tag highlights important text. You can decide how you want browsers to display content within these tags. However, browsers generally have built-in style sheets that will usually style content within these tags in the following ways:

* The `<em>` tag will generally render as <em>italic</em> emphasis

* The `<strong>` tag will generally render as <strong>bold</strong> emphasis



**Line Breaks**

The spacing between code in an HTML file doesn't affect the positioning of elements in the browser.

The line break element `<br>`, only composed of a starting tag, can be used anywhere within your HTML code and a line break will be shown in the browser.



**Unordered Lists**

In HTML, you can use an **unordered list** tag `<ul>` to create a list of items without sequential numbering (instead with bullet points or similar).

The `<ul>` element should not hold raw text and won't automatically format raw text into an unordered list of items. Individual list items must be added to the unordered list using the `<li>` tag (list item).



**Ordered Lists**

Ordered lists `<ol>` are like unordered lists except that each list item is sequentially numbered.



**Images**

The `<img>` tag allows you to add an image to a web page. Like the line break tag, the `<img>` tag is self-closing. Self-closing tags can be written with or with a `/` at the end, so `<img>` is the same as `<img/>`.

Aside: With tags that require a closing tag (like `<p>`...`</p>`), if we do not have any content to go between the opening and closing tag, we can simply combine them using the `/` syntax at the end of the opening tag (like `<p/>`) and this saves us having to write the second tag.

The `<img>` tag has a required attribute called `src`. The `src` attribute must be set to the image's <em>source</em>, or the location of the image. In this case, the value of `src` must be the URL of the image, the web address or local address where the file is stored.



**Image Alts**

We can provide an accompanying 'alt' text for an image that describes its content. This is useful for assistive technologies like screen readers. Alt text is also useful if images cannot be loaded for any reason. The `alt` attribute can be added to the image tag just like the `src` attribute. The value of `alt` should be a description of the image.

Among the various uses of the `alt` attribute is SEO. Search engines cannot 'see' the images on the websites they crawl. They can, however, read alt text, so using the `alt` attribute can improve the ranking of your site.

If the image does not convey any meaningful information to a user (like, say, a block of color used purely as a design flourish) then the `alt` attribute should be should be left empty, meaining `alt=""`. For one, this signals to screen readers that the image is purely decorative and can be ignored rather than announced as present.



**Videos**

Like the `<img>` element, the `<video>` element requires a `src` attribute with a link to the video source. Unlike `<img>`, the `<video>` element requires an opening and closing tag. The enclosed content is text that will only be displayed if the video fails to load.

In addition to `src`, there are `width` and `height` attributes, used to set the size of the video displayed in the browser. The `controls` attribute instructs the browser to include basic video controls such as pausing and playing.



**Learn HTML: Structure video**

HTML is declarative; it describes desired results without explicitly listing steps that can be carried out to achieve it.






