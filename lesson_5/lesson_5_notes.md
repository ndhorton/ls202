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

## The `method` Attribute ##

The `method` attribute tells the browser whether it should use the HTTP GET or HTTP POST mehtod when sending the data to the server. You should use `method="get"` when requesting information from the server, and use `method="post"` when updating data on the server.

HTTP supports several other methods, but HTML limits you to GET and POST. You must use JavaScript or a backend application (**HTTP method overriding**) to use the other methods.

## The `action` and `formaction` Attributes ##

`action` provides the URL to which the browser sends requests. Individual action items (`button` and `input type="submit"` elements) in a form can override the form's `action` value by using the `formaction` attribute.

## 