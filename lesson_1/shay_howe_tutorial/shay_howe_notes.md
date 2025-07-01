# Building Your First Web Page #

## Common Self-Closing Elements ##

* `<br>`

* `<embed>` (deprecated)

* `<hr>`

* `<img>`

* `<input>`

* `<link>`

* `<meta>`

* `<param>` (deprecated)

* `<source>`

* `<wbr>`

# Getting to Know HTML #

Semantic HTML

CSS Utility Classes
Utility-First CSS
Functional CSS
Separation of concerns vs direction of dependencies
Composition over inheritance / Composition over subcomponents


## `mailto` ##

To create an email link, we can use an an `<a>` element with an `href` value beginning with `mailto:`, e.g. `<a href="mailto:shay@awesome.com>`.
To add a subject line, we can use the `subject` query parameter after the email address in the URL.
Adding email body text can be done with the `body` query parameter.
Spaces can be encoded with `%20` and line breaks with `%0A`.
```html
<a href="mailto:shay@awesome.com?subject=Reaching%20Out&body=How%20are%20you">Email me</a>
```
## `target="_blank"` ##

Opening links in a new window/tab can be achieved by adding the `target="_blank"` attribute-value pair to `<a>`.

# Getting to Know CSS #

## The Cascade ##

Styles are applied from top to bottom of a stylesheet in a **cascade**. When there is a conflict, styles declared lower down take precedence over styles declared further up.

This is complicated by **specificity**, however. Specifity weight is given in the form `x-y-z`, where `x` represents the column for the ID selector, `y` the column for the class selector, and `z` the column for the type selector. For instance, in the following code, the `p` selector styles are given the specificity `0-0-1`.
```css
p {
    /* ... */
}
```

The higher the specificity weight of a selector, the higher precedence the selector is given when a styling conflict occurs. For instance, if a paragraph element is selected using a type selector in one place (`p`) and an ID selector in another place, the ID selector will take precedence even if it is appears further up in the cascade.

When we combine selectors, the rightmost selector is known as the **key selector**. Any selector to the left of the key selector serves as a **prequalifier**.

The best practice is to not prefix a class selector with a type selector (without spaces).


Note that direct styling of a selected element always takes precedence over inherited styles, no matter the precedence weight of the parent's selector or the positions of the rulesets in the cascade.

