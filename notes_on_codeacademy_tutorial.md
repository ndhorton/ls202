# Code Academy Learn HTML tutorial

## Elements and Structure

An HTML **element** consists of at least one **tag** but often consists of two tags (opening and closing tags) enclosing some optional content.

- **HTML element** -- a unit of content in an HTML document formed by HTML tags and the text or media contained by them

- **HTML tag** -- the element name, surrounded by an opening `<` and closing `>`

- **Content** -- the information (text or other elements) contained between the opening and closing tags of an HTML element

**The Body**

Only content inside the opening `<body>` and closing `</body>` tags can be displayed to the screen.

Some browsers will render content placed outside the `body` tags to accomodate mistakes in an HTML document, but not all of them. Ensure that all your displayable elements are contained within the `body` tags to ensure the page renders correctly.

**HTML Structure**

HTML is organized as a collection of family tree relationships. When an element is contained within another element, the enclosed element is said to be the **child** of the enclosing element. The child element is said to be **nested** inside of the **parent** element. The relationship between elements and their encestor and descendent elements is known as *hierarchy*.

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

- Paragraphs (`<p>`) contain and display a block of plain text that defines a paragraph

- Spans (`<span>`) contain short pieces of text or other HTML. They are used to separate small pieces of content that are on the same line as other content.

We use `<span>` *inline* within a larger section of content like a paragraph, whereas `<div>` divides content into *blocks*.

**Styling Text**

You can do some styling of text using HTML tags. The `<em>` tag emphasizes text, while the `<strong>` tag highlights important text. You can decide how you want browsers to display content within these tags. However, browsers generally have built-in style sheets that will usually style content within these tags in the following ways:

- The `<em>` tag will generally render as *italic* emphasis

- The `<strong>` tag will generally render as **bold** emphasis

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

The `<img>` tag has a required attribute called `src`. The `src` attribute must be set to the image's *source*, or the location of the image. In this case, the value of `src` must be the URL of the image, the web address or local address where the file is stored.

**Image Alts**

We can provide an accompanying 'alt' text for an image that describes its content. This is useful for assistive technologies like screen readers. Alt text is also useful if images cannot be loaded for any reason. The `alt` attribute can be added to the image tag just like the `src` attribute. The value of `alt` should be a description of the image.

Among the various uses of the `alt` attribute is SEO. Search engines cannot 'see' the images on the websites they crawl. They can, however, read alt text, so using the `alt` attribute can improve the ranking of your site.

If the image does not convey any meaningful information to a user (like, say, a block of color used purely as a design flourish) then the `alt` attribute should be should be left empty, meaining `alt=""`. For one, this signals to screen readers that the image is purely decorative and can be ignored rather than announced as present.

**Videos**

Like the `<img>` element, the `<video>` element requires a `src` attribute with a link to the video source. Unlike `<img>`, the `<video>` element requires an opening and closing tag. The enclosed content is text that will only be displayed if the video fails to load.

In addition to `src`, there are `width` and `height` attributes, used to set the size of the video displayed in the browser. The `controls` attribute instructs the browser to include basic video controls such as pausing and playing.

**Learn HTML: Structure video**

HTML is declarative; it describes desired results without explicitly listing steps that can be carried out to achieve it. It is not a general purpose language.

HTTP structures a webpage.

When we begin making a site we should ask some questions. What are the important pieces of content? How shall I structure the content of the page? What is the information hierarchy of our page going to look like?

A good way to start thinking about this is to focus on the heading hierarchy. Each level of heading should be treated as branches of a tree-like structure, where there are big topics with sub-topics as children, which are siblings to each other. We should not skip levels of heading; an `<h1>` heading should not have `<h5>` headings as its immediate children, etc.

Semantic HTML uses tags which best convey the underlying meaning of the content the tag contains.

Advantages of coherent structure:

1. Readability

2. Accessibility

3. Ease of styling

Divitis -- the overuse of the semantically meaningless `<div>` instead of semantically meaninful tags like `<section>` or `<p>`.



**Document Type Declaration**

When we write an html file, `<!DOCTYPE html.>` must be the first line. It is a declaration to the browser of what type of document to expect, along with what version of HTML is being used in the document. For now, the browser will correctly assume that the `html` in `<!DOCTYPE html>` refers to HTML5, since that is the current standard.

This is actually the simplified `!doctype` declaration introduced in HTML5. It essentially just tells the browser to run in no-quirks mode. HTML is intended to be backwards-compatible from hereon out so there should be no reason for either the declaration to change for new pages when new standards are released, nor for old pages to require the `!doctype` updating to `html5` or anything like that.

The document type declaration is not a tag or element. It adds no content or structure to the page, it is simply a browser directive.



**File extension**

HTML code is always saved with an `.html` extension.

**The `<html>` tag**

To create HTML structure and content, we must add opening and closing `<html>` tags after declaring the `doctype`. Anything within the `<html> ... </html>` tags will be interpreted as HTML code. Without these tags, it is theoretically possible that the browser will not interpret our HTML code correctly. The `<html>` element is the root element of an HTML document.



**The Head**

The `<head>` element is a sibling to the `<body>` and both are children of `<html>`. Where the `<body>` element contains the content of the page, the `<head>` element contains metadata about the page itself.

This metadata is information about the page that isn't displayed directly in the web page.

The `<head>` is usually the first element under the `<html>` element.

**Page Titles**

A tab in a web browser displays the web page's title, given in the `<title>` element, always within the `<head>` element of the page.



**Linking to other web pages**

The **anchor** `<a>` element is used to add links to other pages. The `<a>` element must contain an `href` (hypertext reference) attribute, whose value is is the address of or path to the resource we are linking to (which could be a local filepath or a full URL).

**Opening Links in a new window or tab**

The `<a>` element has an optional `target` attribute that can be used to tell the browser to open the linked resource in a new tab or window. Whether the link is opened in a new tab or a new window depends on the browser; there is no HTML-only (i.e. without JavaScript) way to decide whether it is opened in a tab or window. Most modern browsers open the link in a new tab for better user experience. Before the advent of browser tabs, the link was opened in a new window.

The `target` attribute specifies how a link should open.

The `target` attribute is useful when we want to link to another website, but hope the user returns to ours.

For a link to open in a new tab or window, the `target` attribute requires the value `_blank`.

**Linking to relative page**

We can link web pages together using a **relative path**. In this context, a complete URL can be considered an **absolute path**.

**Linking at will**

Instead of text, the enclosed content of an `<a>` element can be nearly any element, including images.

**Linking to the same page**

In order to link to a target on the same page, we must give the target element an `id` attribute and a unique value. The `href` of the link should be given the value of a `#` followed by the `id` value of the target element.

An `id` is especially helpful for organizing content belonging to a `div`.



**Whitespace and indentation**

Programmers use two tools visualize the relationship between elements: whitespace and indentation. The browser ignores the whitespace and indentation in a page when rendering it.

The W3C is responsible for maintaining the style standards of HTML. Currently, W3C recommends two spaces of indentation when writing HTML. This standard is followed by the majority of professional web developers.



**Comments**

Comments begin with `<!--` and end with `-->`.



## Tables

The `<table>` element will contain all of the tabular data we plan on displaying.

The table row element `<tr>` contains a row of table data.

Each cell must be defined. You can add data using the table data `<td>` element.

To add titles to rows and columns, you can use the table heading element `<th>`. Like table data, a table heading must be placed within a table row.

The column headers can be sectioned off with the `<thead>` element.

The body of the table can be sectioned off with the `<tbody>` element.

The footer of the table, where we might put data such as totals and other cells involving calculations, can be sectioned off using `<tfoot>`.



## Forms

The `<form>` element is the foundation of a web form. The `action` attribute determines where the information gathered by the form is sent. The `method` attribute has a value corresponding to the HTTP request method we want to use (e.g. `POST`).

We can nest text elements within the `<form>` element like headings and paragraphs.

If we want to create an input field in our form, we can use the `<input>` element. `<input>` has a `type` attribute, which determines how it renders on the web page and what kind of data it can accept.

If `type` has the value `text`, the browser renders a text field that users can type text into. `text` is the default value of `type`.

It is important that we include a `name` attribute for the `<input>`; without this, information in the `<input>` won't be sent when the form is submitted.

After users type into the `<input>` field, the value of the `value` attribute becomes what is typed into the field. The value of `value` is paired as the value of a parameter with the value of `name` as the key of the parameter and sent as text when the form is submitted. If we set the `value` attribute explicitly, the effect is to have this initial text value of `value` as the text in the input box before the user edits and types their own.

We can provide instruction to the user on what the input element is for using the `<label>` element.

The `<label>` element has opening and closing tags and displays the content between them. To associate a `<label>` and an `<input>`, the `<input>` needs an `id` attribute. We then assign the `for` attribute of the `<label>` to the value of the `<input>`'s `id`. If we click on the `<label>` element in the rendered page, the browser highlights the associated `<input>` element.
