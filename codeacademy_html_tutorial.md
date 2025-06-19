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

**Inputs**

If we want to create an input field in our form, we can use the `<input>` element. `<input>` has a `type` attribute, which determines how it renders on the web page and what kind of data it can accept.

If `type` has the value `text`, the browser renders a text field that users can type text into. `text` is the default value of `type`.

It is important that we include a `name` attribute for the `<input>`; without this, information in the `<input>` won't be sent when the form is submitted.

After users type into the `<input>` field, the value of the `value` attribute becomes what is typed into the field. The value of `value` is paired as the value of a parameter with the value of `name` as the key of the parameter and sent as text when the form is submitted. If we set the `value` attribute explicitly, the effect is to have this initial text value of `value` as the text in the input box before the user edits and types their own.

**Labels**

We can provide instruction to the user on what the input element is for using the `<label>` element.

The `<label>` element has opening and closing tags and displays the content between them. To associate a `<label>` and an `<input>`, the `<input>` needs an `id` attribute. We then assign the `for` attribute of the `<label>` to the value of the `<input>`'s `id`. If we click on the `<label>` element in the rendered page, the browser highlights the associated `<input>` element.

**Passwords**

The `type` attribute of the `<input>` element can be set to `password` to replace visible input text with another character like `*`. When the form is sent, however, the user input as it was actually typed will be sent.

**Numbers**

We can set the `<input>` field's `type` element to `number` in order to restrict the input to numbers. The `step` attribute can be used to specify how much the arrows next to the input box increase or decrease the current number by. The default behaviour is still to let users type whatever number they like, even with the arrows next to the box useable as an alternative.

**Ranges**

We can also limit the numbers that can be entered in a numerical input. If we set `type` to `range`, we can create a slider. To set the minimum and maximum values, we use the `min` and `max` attributes of the `<input>`. We can also use the `step` attribute to determine how the slider adjusts the number.

**Checkboxes**

We can use the `"checkbox"` value for the input `type` to create a checkbox. We must set a value for the `value` attribute, since users are not entering text themselves. If we use the same `name` for multiple checkboxes, their data will be submitted grouped together under a single parameter name. The default behavior is that checkboxes are for multiple options where users can select more than one option if they wish.

**Radio Buttons**

Radio buttons are generally for when we want users to select only one option out of a group of options. We create a radio button by setting the `<input>` `type` attribute to `radio`.

**Dropdown list**

We can create a dropdown list or menu of choices using the `<select>` and `<option>` elements. `<select>` is to `<option>` similarly as `<ul>` is to `<li>`. The `<select>` element should have an `id` to match a `<label>`, and a `name` attribute, while the `<option>` elements should have a `value` attribute, which, if that option is selected, will be submitted as the value to the `name` name of the `<select>` element. The default is that only one option can be selected.

**Datalist**

We can use a `<datalist>` in conjunction with a `text` `<input>` to create a user interface to be able to search a large dropdown list of options using the text input as filter. We add a `list` attribute to our `<input>` whose value is the `id` of the `<datalist>` element containing our choices in order to associate the text input to the datalist. The choices are `<option>` children of the `<datalist>`, and are the same as the options in a regular dropdown list, with `value` attributes and descriptive text content.

The default filter query behavior is that user input is treated case-insensitively.

The default behavior is that users can type text into the input and this will narrow the options in the drop down list, but if the user wishes they can type some text that is not contained in the options and submit this custom user text.

Important to note that `<datalist>` is an HTML5 addition that is still only partially supported by the various browsers and might not be recommended by professionals.

**Textarea element**

An `<input>` element with `type="text"` creates a single row input field for users to enter text. If we use the`<textarea>` element instead, users will be given an input box with the number of `rows` and `cols` (columns) given by these attributes. This is useful when users need to submit larger quantities of text.

The default behavior is that the user can change the size of the resulting text box by clicking on the the bottom-right corner and dragging to resize, changing the way the page renders as they do so.

We can add pre-filled text by placing the default text between the opening and closing tags.

**Submit Form**

To create a submit buttion in a `<form>`, we can use an `<input>` element with the `type` set to `submit`. The button will bear text on it, and the browser will provide a default such as "Submit" or "Submit Query". If we wish to provide a different legend, we can set the `value` attribute of the `<input>`.

## Form Validation

Validation is the concept of checking user provided data against the required data.

Server-side validation is when data is sent to the server for validation, as when we enter our details in a login page. The form on the login pagge accepts username and password input, then sends the data to a server that checks the pair matches the data in the data store.

Client-side validation is when we want to check the data stored by the browser. This validation occurs before data is sent to the server. Different browsers implement client-side validation differently, but this is the general idea.

All modern browsers share HTML5's built-in client-side validation. It saves us time from having to send information to the server and wait for the server to send back a response. This can also help protect the server from malicious code from a malicious user. It also allows us to quickly give feedback to users for specific fields rather than having them fill in a form again if the data they input into the form was rejected.

**Requiring an Input**

Sometimes we have fields in our `<form>` that must be filled in before the `<form>` can be submitted. To enforce this, we can add the `required` attribute to an `<input>` element. The `required` attribute does not need a value because it is a Boolean attribute. If you want, you can set a Boolean attribute to its own name, e.g. `required="required"`, but this is unnecessary.

For number `<input>`s (e.g `type="number"`, `type="range"`), we have the `min` and `max` attributes which can be set to minimum and maximum values. If we try to input a number outside these parameters, a warning will appear. These can be used in conjunction with `required`.

**Checking Text Length**

We can also set minimum and maximum lengths for text input elements. For an `<input type="text">` element, we can use the `minlength` and/or `maxlength` attributes to which we assign numbers representing numbers of characters.

If the user enters too few characters and attempts to submit, a warning appears. If they type the maximum number of characters they will simply be prevented from typing any more.

**Matching a Pattern**

For cases where we want user provided text to follow specific guidelines, we use the `pattern` attribute and assign it a regular expression. The regex must be a valid JavaScript regex of the `RegExp` type.

If the user attempts to submit text that doesn't match the regex, they will be given a warning asking them to match the requested format.

## Semantic HTML

In HTML, we use a combination of non-semantic elements and semantic elements. In the context of HTML, 'semantic' elements provide information about the content between the opening and closing tags.

By using Semantic HTML, we select HTML elements based on their meaning, not on how they are presented by the browser. Elements such as `<div>` and `<span>` are not semantic elements since they provide no context as to what is inside of their tags.

For example, instead of using a `<div>` element to contain our page header, we could use a `<header>` element, which is always used to contain and denote a heading section of a web page. By using a `<header>` instead of a `<div>`, we provide context as to what information is inside of the opening and closing tag.

Reasons to use Semantic HTML:

* Accessibility: Semantic HTML makes webpages accessible for mobile devices and for people with disabilities as well. This is because screen readers and browsers are able to interpret the code better.

* SEO: it improves the website SEO, or Search Engine Optimization. Search engines are better able to identify the content of your website and weight the most important content appropriately

* Easy to Understand: Semantic HTML also makes the websit's source code easier to read for developers

**Header and Nav**

A `<header>` is a container usually for either navigational links or introductory content containing `<h1>` to `<h6>` headings.

A `<nav>` is used to define a block of navigation links such as menus and tables of contents. Note that `<nav>` can be used inside of the `<header>` element but can also be used on its own.

**Main and Footer**

Two more structural elements are `<main>` and `<footer>`.

Structural elements like `<header>`, `<nav>`, `<main>` and `<footer>` help describe where an element is located based on conventional web development standards.

The element `<main>` is used to encapsulate the dominant dontent within a webpage. By using `<main>` instead of  `<div>`, screen readers and web browsers are better able to identify that whatever is inside of the tag is the bulk of the content.

The `<footer>` element contains information such as:

* Contact information

* Copyright information

* Terms of use

* Site Map

* Reference to top of page links

The `<footer>` tag is separate from the `<main>` element and typically resides at the bottom of the content.

**Article and Section**

`<section>` defines elements in a document, such as chapters, headings, or any other area of the document with the same theme.

The `<article>` element holds content that makes sense on its own. `<article>` can hold content such as articles, blogs, comments, magazines, etc.

**The Aside Element**

The `<aside>` element is used to mark additional information that can enhance another element but isn't required in order to understand the main content. This element can be used alongside other elements such as `<article>` or `<section>`.

Some common uses of the `<aside>` element are:

* Bibliographies

* Endnotes

* Comments

* Pull quotes

* Editorial sidebars

* Additional information

**Figure and Figcaption**

Similarly to `<aside>`, which is used for additional textual information, we can add a related image or illustration using the `<figure>` and `<figcaption>` elements.

`<figure>` is an element used to encapsulate media such as an image, illustration, diagram, code snippet, etc, which is referenced in the main flow of the document.

We can add a caption to the image by using a `<figcaption>` element. `<figcaption>` is an element used to describe the media in the `<figure>` element. Ususally, `<figcaption>` is nested inside `<figure>`.

**Audio**

We add audio to our page using a the `<audio>` element. We can either use a `src` attribute within the `<audio>` tag, or use one or more `<source>` elements nested inside. `<source>` has a `src` attribute, which references the location of the audio source. Another useful attribute is the `type`, which can be set to values like `audio/mp3`; this acts as a hint to the browser. The `<audio>` tag itself has attributes such as `controls`, a Boolean whose presence adds standard audio controls, and another Boolean `autoplay`, whose presence starts the audio playing as soon as possible.

The reason that `<source>` is often used is that multiple sources of different filetypes can be given within a single `<audio>` element using a series of `<source>` tags. This will support more clients by offering a variety of formats; if a particular browser lacks the ability to decode one, it can pick another. The `type` attribute gives the MIME type explicitly, so the browser need only actually download its prefered option.

Using `<source>` with `<audio>` is considered best practice.

**Video and Embed**

We can use a `<video>` element to add videos to a website in a similar fashion to `<audio>`. Again, we can use the `src` attribute or a `<source>` element to specify the location of the video. `controls` and `autoplay` are supported attributes, along with `loop`. Text given between `<video>` tags will only be displayed if the video fails to load.

Another tag that can be used to incorporate multimedia content into a page is the `<embed>` tag, which can embed any media content including videos, audio, files, and gifs from a local or external source. This means that websites that have an embed button have some form of media content that can be added to other websites. The `<embed>` tag is a self-closing tag, unlike the `<video>` element.

Note that `<embed>` is a deprecated tag and other alternatives should be used in its place.



# Learn CSS tutorial

Inline style, internal stylesheet, external/linked stylesheet

Ruleset or rule, selector, declaration block, declaration, `property: value;`

Type selector `h1`

Class selector `.class_name`

Universal selector `*`

Attribute selector `[]`

ID selector `#id_name`
