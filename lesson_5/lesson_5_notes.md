# 5:1 Forms Introduction #

Forms are the principal way that users interact with Web applications. HTML5 offers more than a dozen different form-related tags and more than two dozen different input types.

MDN has a [series of articles](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms) on forms, providing more detailed coverage.

## What to Focus On ##

* Use the `form` tag.
* Know the differences between checkboxes, radio buttons, and selection lists.
* Use `input` and `textarea` text tags.
* Understand the `type` attribute on `input` tags.
	* `checkbox`, `radio`
	* `text`, `email`, `tel`, `password`
	* `submit`, `reset`
	* `hidden`
* Construct `select` lists.
* Use labels in a form with both container and `for` formats.
* Use description lists to help format forms.

# 5:2 Forms Overview #

HTML forms let you gather information from users. The vast range of data types requires that you have a large number of form controls at your disposal, each of which has different attributes to describe the characteristics of each item.

Forms are the point where front-end and back-end concerns come together. It's crucial to understand how forms and their controls work. A form displays information to the user, solicits updates, performs some optional rudimentary validation, and then sends the form data to the server.

However, that is all that forms do. They don't, for instance, update information on the server. For that, the application needs back-end software, such as a Ruby program, that accepts the data from the browser and does something with it. Most web applicatoins also use JavaScript to pre-validate forms before sending the results to the server.

## The `form` Tag ##

The `form` tag is the parent for all form-related tags. The `form` tag tells the browser where and how to send the data. The most important attributes are `action` and `method`.

A form should contain at least one `input`, `textarea`, or `select` tag; without one, the form is useless. The terms **control**, **widget**, and **input** are all commonly used to refer to any of these elements, though there is no single term that is commonly-accepted as the correct generic term.

### The `method` Attribute ###

The `method` attribute tells the browser whether it should use the HTTP GET or HTTP POST mehtod when sending the data to the server. You should use `method="get"` when requesting information from the server, and use `method="post"` when updating data on the server.

HTTP supports several other methods, but HTML limits you to GET and POST. You must use JavaScript or a backend application (**HTTP method overriding**) to use the other methods.

### The `action` and `formaction` Attributes ###

`action` provides the URL to which the browser sends requests. Individual action items (`button` and `input type="submit"` elements) in a form can override the form's `action` value by using the `formaction` attribute (so `formaction` is a tag for nested elements, not `form` itself).

## The `fieldset` Tag ##

`fieldset` is an optional tag that groups together form content as a set of related data; most browsers draw a border around the content by default. While it's common to remove that border with CSS, `fieldset` still provides useful semantic data to the browser, and developers can reference it in their CSS for layout and styling purposes.

Forms can have multiple `fieldset` tags.

## The `input` Tag ##

The `input` tag describes a control or widget; that is, a mechism that lets the user supply information or a request to the application on the server.

Each `input` requires a `type` attribute. The `type` has many valid values, most of which are new in HTML5. Each value indicates the type of widget required. For instace, `type="text"` provides space for the user to enter some text, while `type="submit"` provides a button that submits the form to the server.

Most `input` controls require a `name` attribute to specify the name of each item. The browser uses these names to identify each data item in the form, while the back-end application looks for that name to find the appropriate value.

`input` is a self-closing tag.

## The `label` Tag ##

The `label` tag provides a way to associate some identifying text with an input field. For instance,

```html
<label for="phone">Phone</label>
<input type="text" id="phone" name="phone_number">
```

The browser uses the `for` attribute in the `label` tag and the `id` attribute in the `input` tag to associate the two items. one advantage of this association is that the user can click on the label to make the cursor jump to the desired filed.

You can also use `label` tags as containers.

```html
<label>
  Phone
  <input type="text" name="phone">
 </label>
```

The "container" syntax eliminates the need for the `for` and `id` attributes, so it's easier to use. However, styling can be more difficult with the container syntax, and there are times when you must use a `for` attribute, so learn both variants.


# 5:3 Input Types #

The most versatile and widely used form widget is the `input` element. Most controls are `input` elements.

Some types of `input` look identical in most browsers, such as the `text`, `email`, and `tel` types, but some look radically different: a `text` input looks nothing like a `submit` button or a `checkbox`.

## Type ##

The `type` attribute is required. HTML5 has introduced a great number of new types. Not all are in widespread use, but they all serve a purpose.

The most common types are:
* `text`
* `password`
* `email`
* `tel`
* `checkbox`
* `radio`
* `submit`
* `reset`

### `text` ###

The `text` type creates a simple text entry field. The user can enter any text desired in this control, though the developer should almost always validate the data. Use the `maxlength` attribute to specify the input's maximum length.

### `password` ###

The `password` type creates a single-line text field with an obscured value, often used for passwords and other sensitive information. Use the `maxlength` attribute to specify the input's maximum length.

### `email` ###

The `email` type allows entry of an email addresss in the form `username@domain`. Browsers that implement this type try to prevent incorrectly formatted email addresses. However, the developer should almost always validate the data too.

### `tel` ###

The `tel` type allows entry of a telephone number. Browsers that implement this type don't validate the input since phone numbers vary so much worldwide.

### `checkbox` ###

The `checkbox` type lets the user choose one or more items from a series of yes/no-type options. Use the `value` attribute to give the value the form sends to the server when the user selects that checkbox. Use the `checked` attribute to pre-select checkboxes. Use the `name` attribute to name a set of related checkboxes. The user can select zero or more items in each set of checkboxes.

You can select checked elements in CSS with the `:checked` pseudo-class, which lets you change the appearance of checked radio buttons and checkboxes. Note that this pseudo-class doesn't look for the actual checked attribute; instead, it selects based on the current state of the checkbox.

One workflow is to ensure that a set of checkboxes have the same `name` and that each has its own unique `value`. The browser sends a `name=value` pair for each selected checbox and no value for the unselected ones.

Another workflow is to give each checkbox in the set its own unique `name` and no `value`. In this case, the browser will send, for each checked checkbox, the `name` with the value of `on` (e.g. `pepperoni=on`).

Use the format that your server-side code expects. In most cases, it's easiest to use the second method that uses seperate `name` values.

N.B. it is still considered best practice to use `value` with checkboxes.


### `radio` ###

The `radio` type lets the user choose either one item or none from a list of options.

The `checked` attribute and the `:checked` CSS pseudo-class work as they do for checkboxes.

Use the `value` attribute to define the value submitted by checking the radio button. Use the `checked` attribute to mark the default radio button. If there is no default button, use the `required` attribute on all of the buttons in a group to enforce selecting a button. Use the `name` attribute to name a set of related buttons. The user can select precisely one radio button from each group.

The user does not have to select a radio button if you don't pre-select one with the `checked` attribute and none of the buttons have a `required` attribute. If you pre-select any, you must pre-select precisely one.

N.B. if the desired behavior is that the user is able to select no options, then it is perhaps best to have a separate radio button labeled `None` or something similar. The problem is that if a user clicks on a radio button, there is no way to return to the state where none of the radio buttons are selected. So it seems generally best not to make use of the fact that radio buttons allow you to let the user select zero items from a radio button set.

Typically, radio buttons work best with short lists. At a certain point, often around 5-8 items, they become unwieldy, both for the developer and the user. You may want to consider using the `select` list control. You may in this case want to use the `select` list control instead.


### `submit` ###

The `submit` type creates a button that the user can click to submit the contents of a form to the server. The `action` attribute on the `form` tag typically provides the URL of the server, but you can override that by using the `formaction` attribute with the `submit` tag.

The `value` attribute is used by the browser as the label on the button.

### `reset` ###

The `reset` type creates a button that the user can click to reset the contents of a form to its default values. Clicking a `reset button does not send a request to the server.

The `value` attribute is used by the browser as the label on the button.

MDN says that `reset` is not recommended.

# 5:4 Input Attributes #

The `input` tag supports a variety of attributes --- some work with most input types, and some with just one. We describe the features worth memorizing in this assignment.

## The `value` Attribute ##

Most input controls can use the `value` attribute, but the meaning varies with the `type`.

* For text-based types such as `text`, `email`, and `number`, the `value` assigns a default value for the control. If you don't supply a default value, the browser uses an empty string.

You should use `value` for text-based `input` element types when you already have a value that the user might wish to edit, either loaded from a database or provided by the user during the session.

* `checkbox` and `radio` `input` types use the `value` attribute to set the value that the form submits for the indicated checkbox or radio group element.

Technically, `radio` input types don't require the `value` attribute. If you omit the `value` attribute, the browser will send the parameter name given by the `name` attribute with a value of `on`.

Launch School recommends always using the `value` attribute for radio buttons, and using `name` to group related radio buttons together. If several radio buttons belong together, they should all have the same `name` value.

If we want to leave all of the radio buttons unselected, but still require a selection, we can add a required attribute to each button.

* Button types such as `submit`, `rest`, and the `button` type use the `value` attribute for the label that appears on the button.

Note that `type="button"` is out of favor; consider using the `<button>` element instead.

## The `size` and `maxlength` Attributes ##

These attributes apply to most text-based input types.

The `size` attribute lets you control the size of an `input` element in characters. You can also specify the width with the CSS `width` property, but it does not support character measurements.

`size` is an approximation for the width of the input box. The HTML5 standard requires that "the user agent should ensure that at least that many characters are visible"; in practice, you may see both more and fewer characters displayed. The CSS width overrides the `size` attribute in CSS-enabled browsers.

The `maxlength` attribute limits the maximum length of input values; this value can be more or less than the `size` value.

HTML5 also supports a `minlength` attribute, but support for this attribute is inadequate at the time of this writing.


## The `placeholder` Attribute ##

The `placeholder` attribute lets you display some text when a field is empty to help describe the expected input; it applies to most of the text-based `input` types.

Most browsers display a `placeholder` text using a grayed-out format, and they erase the placeholder text as soon as you start typing.

You may see sites that use placeholders as a substitute for labels. Don't do this yourself, though, since it breaks screen readers. Labels and placeholders have different purposes, so use them appropriately. If you're forced to use placeholders, include the labels too, but hide them using CSS. This hack works well since most screen readers can read the hidden text.

## The `disabled` Attribute ##

The `disabled` attribute lets you disable `input` elements; the browser renders disabled elements but won't let the user interact with them. The rendering looks different from enabled elements, often by using a gray or lighter color. `disabled` also turns on the `:disabled` CSS pseudo-class. (Non-disabled elements set the `:enabled` pseudo-class).

Most web applications handle the `disabled` attribute programmatically, either at the time the application generates the HTML or dynamically with JavaScript. You still need to know that `disabled` exists, though; you may have to write some HTML for a program that expects disabled inputs on the original form.

This last paragraph expresses that in many web apps, whether a form input is disabled or enabled often depends on the application logic. An input element may be disabled if the user lacks certain permissions, or is not logged in, or it conflicts with other options chosen elsewhere, etc. The app might add or remove the `disabled` attribute when generating HTML dynamically server-side, or use JavaScript in the browser to add or remove it from the element in the DOM.


## The `required` Attribute ##

The `required` attribute marks an `input` as required; the browser won't let you submit the form until the user completes all required fields. `required` also turns on the CSS pseudo-class `:required`.


## The `autocomplete` Attribute ##

You can use `autocomplete` on most `input` text-box elements. This attribute prevents the browser from storing data for later reuse by the browser's autocomplete features (or, if set to `on`, permits autocomplete to work).

Autocomplete is common on smartphones and tablets but can be a nuisance. You can use the values `on` and `off` to explicitly turn `autocomplete` on or ff on any given field.

The `autocomplete` option does not affect the `password` input type.

## The `autocapitalize` Attribute ##

Some browsers recognize an `autocapitalize` attribute to turn autocapitalization on and off for the first letter of words or sentences. Browsers that recognize this attribute default to the value `autocapitalize="sentences"`. Use `autocapitalize="none"` when expecting input that you don't want to capitalize. You can also specify `autocapitalize="words"` or `autocapitalize="characters"`.

`autocapitalize` is not part of the HTML standard, but an attribute provided by some *mobile* browsers, such as iOS Safari and Google Chrome. It does not affect desktop and laptop systems. The W3C HTML validator presently complains about `autocapitalize` since it is non-standard. If you want to use this attribute, you'll have to suffer that complaint.

## The `autocorrect` Attribute ##

Some browsers support an `autocorrect` attribute that turns automatic spelling correction on and off. You can disable this feature with `autocorrect="off"`; you should usually disable it with names, addresses, and other information where autocorrection would be a bother.

`autocorrect` is non-standard HTML, but an attribute presently provided by iOS Mobile Safari. Since it is non-standard, the W3C HTML validator will complain about the `autocorrect` attribute. If you want to use this attribute, you'll need to get used to this complaint.


# 5:5 Select and Textarea #

## The `textarea` Element ##

`textarea` lets the user input multiple lines of text. Unlike `text`-type inputs, which ignore carriage returns, newlines, and other whitespace charcters, `textarea` elements retain them and use them to format the text into lines and paragraphs. Unlike other controls, though, the value of the `textarea` doesn't use the `value` attribute to provide a value for the element. Instead, an initial value can be provided within the opening `<textarea>` tag and the closing `</textarea>` tag.

Since `textarea` preserves whitespace, it's common practice to code the opening and closing tags on the same line unles the initial text content contains newlines.



### Rows and Cols ###

`textarea use the `rows` and `cols` attributes to control the height and width of the text box; `rows` is the height in lines, while `cols` is the width in characters. As with the `size` attribute on `input` tags, neither measurement is precise --- the browser may choose to display more or fewer lines or columns than requested. The CSS `height` and `width` properties will also override these attributes. Furthermore, the `rows` value is not a maximum for the number of lines of input allowed; instead, it's the number of visible lines. The text box enables vertical scrolling when the content exceeds the `rows` count.

Most browsers today let the user resize the `textarea` box by dragging and dropping a small triangle that appears in the lower-right corner of the text box. You can disable this feature with the CSS `resize` property.


## The `select` Element ##

`select` creates a drop-down list of options from which the user can select zero or more options. It has two possible child elements: `option` and `optgroup`. `select` uses the `name` attribute like other form elements, but it uses the `option` elements within it to describe the values shown to the user and sent to the server.

### The `option` Element ###

An `option` defines one of the choices a user can make in a `select` tag. A `select` element is useless without its `option` elements. Each `option` represents a possible value for the `select`, and they use the `value` attribute as the value sent to the server with the `select` element's name. If an `option` does not have a `value` attribute, the browser uses the text contained by the `option` element instead.

`select` elements often have a placeholder `option` that says something like `Choose one` and has a `value` of an empty string, as well as `disabled` and `selected` attributes set. This option works something like the `placeholder` attribute on text boxes: the user can see some helpful text, but she cannot select that text.

By default, `sselect` lets the user choose precisely one option or leave the option unselected if it contains a `disabled selected` option. If you add the `multiple` attribute, the user can select more than one option. On most browsers, a `select` with `multiple` set appears as a (possibly scrolling) rectangle that displays several options. The user then Ctrl-clicks (Windows) or Cmd-clicks (Mac) to select the options she wants. You can also supply the `size` attribute to control the height of the selection box.


# 5:6 Form Layouts #

## Difficulties Styling `select` (and others) ##

Select (and several input types) are difficult to style with traditional CSS and HTML. This is because they were added before CSS was developed, and their internal components initially relied on the OS to supply e.g. a drop-down menu, or a file-picker. Inertia and the desire for backwards-compatability kept this situation from being improved. 

This has started to be addressed, at least in the major browsers. What began as previously proprietary browser extensions are now standardized across most big browsers under the `appearance` property. To ensure the widest compatability, however, we can, if necessary, include the older proprietary syntax. The most compatible setting for `appearance` is `none`, which strips away most of the OS-provided styling for many of the problematic elements, allowing styling of many components with CSS. The `select` element can now be completely styled with 'customizable select elements', as MDN calls them. This feature is still not universal across all browsers, however, and for maximum compatibility you should use `appearance: none`.

For backwards compatability with older versions of browsers, we can use:
```css
select {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}
```

We can check "Can I Use" for details of such recent browser features.

Details of this can be found under the MDN pages on form layouts.

## Inline Images ##

We can embed 'inline images' in our pages using a Data URL. A data URL begins with the `data:` scheme, followed by the type of image, e.g. `svg+xml`. This is then followed up with the encoding, and finally the data itself. If the encoding is `base64`, for instance, then the image has been encoded from binary into a type of HTML-safe text character base-64, where data can be embedded directly as the remainder of the URL. This means that we do not need to issue a separate request for the image as an additional resource, as we would using a normal network URL scheme like `http:`.

## Important new properies ##

* `border-radius`
* `appearance`
* `background-image` --- in the context of using an inline image as a custom widget in a `select` element
* `background-position`
* `background-repeat`

## Styling the relation between `label` and `input` ##

There are two basic orientations for `label` in relation to its associated `input`: top-and-bottom and side-by-side.

Of the two orientations, top-and-bottom is easier to work with and typically more flexible. All we need to do is make the `label` and `input` elements `display: block`, and then maybe set the width either directly or using the width of a wrapper container element.

The side-by-side orientation is slightly harder, but not too hard. The default `display` setting of `input` and `label` is `inline`. However, like the `img` element, `input` has the exceptional ability to respond to `width` and `height` properties even in its `inline` default mode. Nevertheless, when we set `label` to `inline-block`, it is often useful to set `input` to `inline-block` as well, so that other developers are aware that both elements are actually being styled by `width` and `height` even if they are unaware that `input` behaves like `img` in this regard.

We generally want a wrapper for our `label` and `input` pairs. Semantically it is better to place pairs (whether top-and-bottom or side-by-side) in a description list, as opposed to a `div` with a class. Placing one pair per list give the greatest flexibility.


Aside: The `action="#"` attribute setting on a `form` permits your code to pass W3C validation whereas using an empty string does not.

## Types of widgets ##

*From MDN's 'Styling web forms'*

Easy to style:  
* `<form>`
* `<fieldset>` and `<legend>`
* Single-line text `<input>` elements (e.g. where type is `text`, `url`, `email`) except for `type="search"`
* Multi=line `<textarea>`
* Buttons (both `<input type="button">` and `<button>`)
* `<label>`
* `<output>`

Harder to style
* Checkboxes and radio buttons
* `<input type="search">`

With internals that can't be styled in CSS alone:
* `<input type="color">`
* Date-related controls such as `<input type="datetime-local">`
* `<input type="range">`
* `<input type="file">`
* Elements involved in creating dropdown widgets, inluding `<select>`, `<option>`, `<optgroup>` and `<datalist>` (`<select>` is now fully customizable via HTML and CSS)
* `<progress>` and `<meter>`

Most of these have workarounds (or in the case of `<select>` a solution) for most aspects of styling. `<progress>` and `<meter>` bars are the least tractable, and many developers use custom solutions involving styling `<div>`s and using JavaScript, or use a library.


# 5:8 Walkthrough Project: Contact Form #

We can use the `pattern` attribute on a `type="text"` `input` element in order to get the browser to perform a RegEx check as a preliminary input validation when the user submits the form. Support for `pattern` is widespread, but may be spotty in older browsers.

When we look at the CSS ('Styles') tab in the DevTools inspector, we can see what styles the user-agent stylesheet is applying (and which have been overridden by our CSS, since those rules will be struck out).

User-agent stylesheets tend to use logical margin and padding. The terms `before` and `after`, in a left-to-right written language like English, translate to `top` and `bottom`, while `start` and `end` translate to `left` and `right`.
