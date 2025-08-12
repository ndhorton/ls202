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
