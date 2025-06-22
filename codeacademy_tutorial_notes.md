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

Selectors can be chained

Pseudo-class

e.g. `:focus`, `:visited`, `:disabled`, `:active`, `:hover`

Can be attached to any selector

Specificity is the order by which the browser decides which CSS styles will be displayed. A best practice in CSS is to style elements while using the lowest degree of specificity so that if an element needs a new style, it is easy to override.

Specificity from highest to lowest:

* ID

* class

* type

**Descendant Combinator**

CSS supports selecting elements that are nested within other elements, or descendant elements.

e.g.

```html
<ul class="main-list">
    <li> ... </li>
    <li> ... </li>
</ul
```

```css
.main-list li {
    ...
}
```

When writing our CSS, we use the class selector but then put a space followed by the descendent elements we wish to include in the rule

**Multiple Selectors**

Comma-separate a list of selectors to apply a rule to all of them

## The Box Model

Every element in a web page is interpreted by the browser as 'living' inside a box. For example, when we change the background color of an element, we change the background color of its entire box.

Properties of an element's box, from inside out:

* `width` and `height` of the *content area*

* `padding` -- the amount of space between the content area and the border

* `border` -- the thickness and style of the border surrounding the content area and padding

* `margin` -- the amount of space between the border and the outside edge of the element

**Height and Width**

You can use pixels `px` to set the `height` and `weight` properties in a ruleset. When the width and height are set in pixels, it will be the same number of pixels on all evices, so an element that fills a laptop screen will overflow a mobile screen.

**Borders**

A border is a line that surrounds an element's content area and padding, like a frame around a painting.

Borders can be set with a specific width, style, and color. E.g. `border: 3px solid coral;`

The *width* can be set using pixels (`px`) or the following keywords: `thin`, `medium`, `thick`.

The *style* is the design of the border. Web browsers support 10 different styles natively, including `none`, `dotted`, and `solid`.

The *color* can be specified in several formats, including 140 built-in color words.

The default border is `medium none color`, where color is the current color of the element. Any unset property will revert to the default.

**Border Radius**

By default, the border is rectangular like the box itself. We can modify the corners of an element's border with the `border-radius` property. If we set `border-radius: 5px;`, all four corners of the border will be set to a curvature the same as that of a circle with a 5-pixel radius.

We can also set the `border-radius` as a percentage of the width of the box; if we set `border-radius: 50%;`, and the `width` and `height` of the element are equal to each other, the resulting border will be a perfect circle.

**Padding**

The space between the content of a box and the border is known as *padding*. Padding is like the space between a painting and the frame surrounding it.

You can set the overall `padding` at once with a single value, or set each side individually with `padding-top`, `padding-right`, `padding-bottom`, and `padding-left`

You can also set these specific sides using `padding` with multiple values. When there are four values, each value sets a side in clockwise rotation from the top.

When there are three values for `padding`, the first sets the top, the second sets the left and the right to the same value, and the third sets the bottom.

With two values, the first sets top and bottom to the same value, the second sets left and right to the same value.

**Margin**

The margin is the space around the outside of the border of the box. It can be set similarly to the padding, with `margin` set to one, 2, 3, or 4 values, as well as `margin-top`, `margin-right`, `margin-bottom`, `margin-left`.

**Auto**

The `margin` property also lets you center content, albeit with a few syntax requirements. We must first set a width, since otherwise the box of an element takes up the entire horizontal of the page and thus cannot be centered. We then set the `margin` property to `0 auto`.

**Margin Collapse**

Padding is space inside an element's border and margin is space outside it. One additional difference is that top and bottom (vertical) margins *collapse*, while veritcal padding does not.

Horizontal margins of two adjacent elements are added together so that the distance between their borders will always be the sum of their neighbouring horizontal margins. 

However, vertical margins do not sum. Instead, the larger of the two neighbouring margins is used for the total vertical distance between their borders. We call this *margin collapse*.

**Minimum and Maximum Height and Width**

CSS offers two properties that can limit how narrow or how wide an element's box can be size to:

* `min-width` &mdash; this property ensures a minimum width of an element's box

* `max-width` &mdash; this property ensures a maximum width of an element's box

Similarly, there are equivalent properties for the height, `min-height` and `max-height`.

**Overflow**

Sometimes the various dimensions that compose the size of the element's box result in a box that is bigger than the parent's containing area.

To deal with this, we have the `overflow` property. The `overflow` property determines what happens to content that spills, or overflows, outside. The most commonly used values for `overflow` are:

* `hidden` &mdash; when set to this value, any content that overflows will be hidden from view

* `scroll` &mdash; a scrollbar will be added to the element's box so that the rest of the content can be viewed by scrolling

* `visible` &mdash; when set to this value, the overflow content will be displayed outside of the containing element

The overflow property is set on a parent element to instruct the browser on how to render child elements. For example, if a `<div>`'s overflow property is set to `scroll`, all children of this `<div>`  will display overflowing content with a scroll bar. You can set this more granularly with `overflow-x` and `overflow-y`.

**Resetting Defaults**

All major web browsers have a default stylesheet they use in absence of an external stylesheet. These default stylesheets are called *user agent stylesheets*. In this context, user agent is a technical term for the browser.

User agent stylesheets will often have defaults CSS rules for padding and margin. This can make it difficult to have control over the design of a webpage. Many devs choose to reset these default values so that they can truly work with a clean slate

```css
* {
    margin: 0;
    padding: 0;
}
```

This is often the first rule in an external stylesheet. Note that both properties are set to `0`. When these properties are set to `0`, we do not need a unit of measurement.

**Visibility**

Elements can be hidden from view with the `visibility` property, which can be set to:

* `hidden` &mdash; hides an element

* `visible` &mdash; displays an element

* `collapse` &mdash; collapses an element

When `visibility` is set to `hidden`, the browser will display an empty space where it would have been. If you set the `display` property to `none`, the element is removed entirely, with no space to denote an element.

# Changing the Box Model

**Content-Box**

The default `box-sizing` property applied to a web page by browsers is `content-box`. In this model, the `width` and `height` determine the width and height of the element's content box. This means that the thickness of the paddings and borders are added to the size of the content box to give the actual rendered size of the box.

This can make it difficult to layout pages, since we are having to mentally adjust the `width` and `height` to compensate for the thickness of the padding and borders.

**Border-Box**

It is common to change the `box-sizing` for every element:

```css
* {
    box-sizing: border-box;
}
```

In the `border-box` model, `width` and `height` specify the dimensions of the box at the outside of the border. This means that the actual rendered size of the box is fixed, and the size of the content box is adjusted to compensate for the thickness of the border and padding.

The Box Model properties can be found in DevTools under `Elements`. You can select an element and then select the `Computed` tab and it will show you a picture of the box model being used, below which the properties including `box-sizing` will be listed. In Firefox tools, we choose `Inspector`, select the element, and then `Layout` to see the `Box Model Properties` and a picture of the box model.

## Display and Positioning

**Flow of HTML**

A browser renders the elements of an HTML document that has no CSS from left to right, top to bottom, in the same order that the elements exist in the document. This is called the **flow** of elements in HTML.

In addition to properties that style HTML elements, CSS provides properties to change how a browser positions elements. These properties specify where an element is located on a page, if the element can share lines with other elements, and other related attributes.

The properties for adjusting the positiion of elements in the browser include:

* `position`

* `display`

* `z-index`

* `float`

* `clear`

**Position**

Block-level elements (e.g. `<div>`, `<h1>`, `<p>`) create a block the full width of their parent elements, and they prevent other elements from appearing in the same horizontal space.

Block level elements take up their own 'line' of space and don't overlap. The default position is the left hand side of the view.

This position can be changed, however, by setting its `position` property, which can take on one of five values:

* `static` &mdash; the default value

* `relative`

* `fixed`

* `sticky`

**Position: Relative**

The `relative` value for `position` allows us to position an element relative to its default `static` position on the page. We then use properties `top`, `bottom`, `right`, and `left`, along with values expressing the distance, to displace the element relative to the default. So `top: 10px` moves the element downward 10 pixels from the top. Values can be expressed in pixels, ems, and percentages, among other units.

Offsetting the `relative` element will not affect the positions of other elements.

**Position: Absolute**

When an element's `position` is set to `absolute`, all other elements on the page will ignore the element and act like it is not present on the page.  The element will be positioned relative to its closest ancestor element that has *its* position property set to anything other than `static`, or failing that to the initial containing block (either `<body>` or the viewport). We use the same `top`, `bottom`, `left`, `right` properties to offset its absolute position. The element is essentially taken out of the regular HTML flow entirely.

**Position: Fixed**

We can fix an element to a specific postion on the page even when the user scrolls by setting its `postion` to `fixed`. We can position the element using the familiar offset properties. The element is removed from normal document flow, and its position is offset relative to the initial containing block, the viewport in the case of visual media.

This technique is often used for navigation bars on web pages.

**Position: Sticky**

The `sticky` value is a `position` value that keeps an element in the document flow as the user scrolls, but sticks it to a specified position as the page scrolls past a certain point. This is done by using `position: sticky` in conjunction with the familiar offset properties plus a new one.



**Z-Index**

When boxes on a web page have a combination of different postions, the boxes and their content can overlap, making the content difficult to read or consume.

The `z-index` property controls how far back or how far forward an element should appear on the web page when elements overlap. This can be thought of as the depth of elements, with deeper elements appearing behind shallower elements.

The `z-index` property accepts integer values. The default value is `0`. The value has meaning relative to the values of overlapping elements; an element with a higher value will be placed further forward than an overlapping element with a lower value.



**Inline Display**

Every HTML element has a default `display` value that determines if it can share horizontal space with other elements. Some elements fill the entire browser from left to right regardless of the size of their content.

Some elements fill the entire browser from left to right regardless of the size of their content. Other elements only take up as much horizontal space as their content requires and can be directly next to other elements.

Three of the possible values for `display` are

* `inline`

* `block`

* `inline-block`

The default display for some elements, such as `<em>`, `<strong>`, and `<a>`, is called **inline**. Inline elements have a box that wraps tightly around their content, inly taking up the amount of space necessary to display their content and not requiring a new line after each element. `inline` elements cannot be altered in size with the `height` or `width` CSS properties.

The CSS `display` property provides the ability to make any element an inline element. This includes elements that are not inline by default such as paragraphs, divs, and headings.



**Block Display**

Some elements are not displayed in the same line as the content around them. These are called **block-level** elements. These elements fill the entire width of the page by default, but their `width` property can also be set. Unless otherwise specified, they are the height necessary to accomodate their content.

Elements that are block-level by default include all levels of heading elements (`<h1>` through `<h6>`), `<p>`, `<div>` and `<footer>`.



**Inline-Block Display**

Another value for the `display` property is `inline-block`. Inline-block display combines features of both inline and block elements. Inline-block elements can appear next to each other and we can specify their dimensions using the `width` and `height` properties. Images are an example of default inline-block elements.



**Float**

If you simply want to move an element as far left or as far right as possible in its container, you can use the `float` property.

The `float` property is comonly used for wrapping text around an image. Note, however, that moving elements left or right for layout purposes is better achieved through tools like CSS grid and flexbox.

The `float` property is often set using the values `left` or `right`, which move the element as far in the named direction as possible.

This works for `static` and `relative` positioned elements. Floated elements must have a `width` specified; otherwise, the element will assume the full width of its containing elmenet, and changing the float value will not yield any visible results.



**Clear**

The `float` property can be used to float multiple elements at once, and when these elements have different heights it can affect their layout on the page. Elements can 'bump into' each other and not allow other elements to properly move to the left or right.

The `clear` property specifies how elements should behave when they bump into each other on the page. It can take on one of the following values:

* `left` &mdash; the left side of the element will not touch any other element within the same containing element

* `right` &mdash; the right side of the element will not touch any other element within the same containing element

* `both` &mdash; nether side of the element will touch any other element within the same containing element

* `none` &mdash; the element can touch either side



Note that even if an element has not itself been `float`ed, you may still need the `clear` property if it gets positioned next to a floated element (an `inline-block` element, say).



## Colors

Colors in CSS can be described in three different ways:

* Named colors (or keyword colors)

* RGB &mdash; numeric values describing a mix of red, green, and blue

* HSL &mdash; numeric values that describe a mix of hue, saturation, and lightness



* `color` &mdash; foreground color

* `background-color`



**Hexadecimal**

A hex color begins with a `#` character followed by three or six characters. The characters represent values for red, blue, and green.

Six character hex colors are three pairs of characters with each pair representing red, green, or blue concentration.

Certain colors can be represented by three characters when every pair consists of two of the same hex digit. E.g. the aqua color `#00FFFF` can become `#0FF`.



**Decimal RGB colors**

There is another syntax for representing RGB values, commonly referred to as "RGB value" or just "RGB", that uses decimal numbers rather than hexadecimal, and it looks like this: `color: rgb( 23, 45, 23);`

Each of the three values is a decimal integer from 0 to 255.

You should pick either decimal or hexadecimal and stick to it consistantly throughout a stylesheet.



**Hue, Saturation, and Lightness**

The RGB color scheme is close to how computers represent colors internally.

The HSL system is equally powerful.

The syntax for HSL is similar to the RGB value scheme: `color: hsl(120, 60%, 70%)`. The first value represents the degree of the hue, and can be between 0 and 360. The second and third numbers are percentages representing saturation and lightness.

Hue refers to an angle on a color wheel. Red is 0 degrees, green is 120 degrees, blue is 240 degrees, and then back to red at 360.

Saturation refgers to the intensity or purity of the color. The color becomes richer toward 100% and grayer toward 0%.

Lightness refers to how light or dark the color is. 50% is normal lightness. 100% is closer to white, and 0% is closer to black.

HSL is convenient for adjusting the lightness or saturation all at once, rather than across three values.

HSL is also convenient for generating a palette of colors by keeping lightness and saturation at the same levels and simply varying hue from color to color.



**Opacity**

To use opacity in the HSL color scheme, use `hsla()` instead of `hsl()`, and four values instead of three. The `a` stands for Alpha, sometimes called the opacity.

Alpha is a decimal number from 0 to 1. If alpha is 0, the color will be completely transparent. If alpha is 1, the color will be completely opaque.

The RGB color scheme has a similar syntax for opacity, `rgba()`. Again, the last value is the alpha.

Hex colors can also have an alpha, by adding two more digits to a six-digit value or one more digit to a three-digit value. The hex alpha ranges from `00` (transparent) to `FF` (opaque).

The only keyword value for `color` opacity is `transparent`, which is equivalent to `rgb(0, 0, 0, 0)`.



### Typography

When a `font-family` typeface has multiple words, it is good practice to surround the name with quotes to group the words.

You can have a comma-separated list of values for `font-family`. The first value on the left will be the preferred font and if that is not available, the next font in the list will be tried, and so on. This allows us to have fallback fonts, including the Web Safe Fonts which all browsers should have. When you specify a list of fonts, you have what is known as a *font stack*. `serif` and `sans-serif` are keyword values that can be added as a final fallback font if nothing else in the font stack is available.

**Font-Weight**

The `font-weight` property can take on keyword values: `bold`, `normal` (default), `lighter` (one weight lighter than the element's parent value), `bolder` (one weight bolder than the element's parent value).

Numerical values for `font-weight` rangge from 1 (lightest) to 1000 (boldest), but it is common practice to use increments of 100. A value of 400 is equal to the keyword `normal` and a value of 700 is equal to `bold`.

Not all fonts can take a numeric `font-weight` value. It is important to look up what values can be used with a given font.

**Font Style**

The `font-style` property can italicize text with the value `italic`. The default value is `normal`.

**Text Transformation**

Text can be styled to appear in all `uppercase` or `lowercase` with the `text-transform` property.



**Text Layout**

The `letter-spacing` property sets the horizontal spacing between the characters in an element's text. This is not commonly used, but can help make certain fonts more legible. The value can be in units such as `px` or `em`.

You can set the space between words using the `word-spacing` property, which takes `px` and `em` values. `em` values are recommended because the spacing can be set based on the size of the font.

The `line-height` property controls how tall the lines of the text are. Line height values can be a unitless number or a length value in `px`, `em`, or `%`. Generally, the unitless value is preferred since it is responsive based on the current font size. If the font size changes, the height will change by the proportion given by the unitless number.

The `text-align` property aligns text to its parent element.



**Web Fonts**

Free font services such as Google Fonts and Adobe Fonts host fonts that you can link to from your HTML document with a provided `<link>` element.

You can also use fonts from paid font distributors like `fonts.com` by downloading and hosting them with the rest of your site's files. You can create a `@font-face` at-rule in your CSS stylesheet to link to the relative path of the font file.



**Web Fonts Using `<link>`**

Generate a `<link>` embedding from Google fonts and paste into your HTML file. Then you can use the font in your CSS like any other.



**Web Fonts Using `@font-face`**

We can download fonts and load them into our CSS file using a `@font-face` ruleset.

Fonts can be downloaded in a format such as:

* OTF (OpenType Font)

* TTF (TrueType Font)

* WOFF (Web Open Font Format)

* WOFF2 (Web Open Font Format 2)

The different formats are a progression of standards for how fonts will work with different browsers, with WOFF2 being the most progressive. It's a good idea to include TTF, WOFF, and WOFF2 formats with your `@font-face` rule to ensure compatibility on all browsers.

Google Fonts may only provide a TTF font, in which case you can use other tools to convert TTF to the other formats.

Then you can load the downloaded font with the `@font-face` at-rule like:

```css
@font-face {
  font-family: 'MyParagraphFont';
  src: url('fonts/Roboto.woff2') format('woff2'),
       url('fonts/Roboto.woff') format('woff'),
       url('fonts/Roboto.ttf') format('truetype');
}

```

The `@font-face` at-rule is used as the selector. It's recommended to define this ruleset at the top of your CSS stylesheet.

Inside the declaration block, the `font-family` property is used to set a custom name for the downloaded font. The name can be anything you choose, but it must be surrounded by quotation marks. In the example, the font is named `'MyParagraphFont'`.

The `src` property contains three values, each specifying the relative path to the font file and its format. In this example, the font files are stored in a folder named `fonts` within the working directory.

Note that the ordering for the different formats is important because our browser will start from the top of the list and search until it finds a font format that it supports. So they should be listed in order of most preferred to least preferred.

We can then set the `font-family` on any element using the `font-family` property with the value of the name you gave the font using `font-family` in the `@font-face` ruleset.
