# 4:1 Lists and Tables Introduction #

* Learn to constuct simple lists and nested lists.
* Learn to create horizontal lists.
* Using pseudo-classes `:hover` and `:focus`.
* Construct simple tables with headers, body, and footers.

## List Types ##

* Understand the difference between ordered, unordered, and description lists.
* Explain when to use which list type.

## Table Structures ##

* Understand the differences between columns, rows, and cells.
* Use table headers, body, and footers.
* Know the differences between table headers, row headings, and column headings.


# 4:2 Lists Overview #

HTML provides a mere six tags to implement the three list types: **unordered**, **ordered**, and **description**.

Tags for three types of list:
* `ul` --- unordered list
* `ol` --- ordered list
* `dl` --- description list

Tags for children of lists:
* `li` --- list item
* `dd` --- description definition
* `dt` --- description term

## Unordered Lists ##

Unordered lists contain a sequence of unordered items. By unordered, we mean that there is no visual numbering or naming system for the items in the list. The content itself may have an implicit ordering, perhaps alphabetical, but the browser displays a **bullet** --- a glyph that looks like a small dot, disc, circle, or square --- instead of a number or letter before each item. By default, browsers render unordered lists vertically, each item preceded by a bullet. However, you can choose a horizontal display and hide the bullets. You can even use custom bullets.

HTML uses the `<ul>` and `<li>` tags to construct unordered lists.

## Ordered Lists ##

Ordered lists have ordered content; that is, they have a sequence that is a visual component of the list. By default, most browsers render a vertical list of numbered items, but you can change this to roman numerals as well as alphabetic letters, including foreign alphabets. Examples of ordered lists include a numbered list of the top 10 programming languages, or a numbered list of the steps required to make a pot of coffee.

HTML uses the `<ol>` and `<li>` tags to construct ordered lists.

## Description Lists ##

Description lists (called definition lists before HTML5) contain a list of terms and definitions. Examples of definition lists include dictionaries, bibliographies, and, that relic of the past, the phone book.

HTML uses the `<dl>`, `<dt>`, and `<dd>` tags to consturct description lists.

Here is a simple example:
```html
    <dl>
      <dt>Unordered</dt>
      <dd>A simple list with bullets.</dd>
      <dd>A plain list with no bullets or sequence numbers.</dd>

      <dt>Ordered</dt>
      <dd>A simple list with sequence numbers or letters.</dd>

      <dt>Description</dt>
      <dt>Definition</dt>
      <dd>A list with terms and definitions.</dd>
    </dl>
```

Each grouping may have more than one term (`dt`) and more than one definition (`dd`). The first item above has one term and two definitions, while the final includes two terms and one definition.

## Nested Lists ##

You can nest any list within another list, regardless of types. You can even mix and match them --- put an unordered list inside a description list, for instance.

Unordered list bullets change at each level of nesting. Most browsers will cycle through several different bullets as you nest unordered lists more deeply. Neither ordered lists, nor description lists, do anything similar.

&#9608; is a 'full block' character, rarely used now.

## Navigation Menus ##

Developers frequently use unordered lists to construct navigation menus, both vertical and horizontal. Commonly, you start out with HTML and CSS that looks something like this:

```html
    <nav>
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Projects</a></li>
        <li><a href="#">Team</a></li>
        <li><a href="#">Help</a></li>
      </ul>
    </nav>
```

```css
      nav ul {
        background-color: powderblue;
        list-style-type: none;
        padding-left: 0;
        width: 200px;
      }

      nav li {
        font-size: 1.25rem;
      }

      nav a {
        box-sizing: border-box;
        color: blue;
        display: inline-block;
        line-height: 2.5;
        padding: 0 10px;
        text-decoration: none;
        width: 100%;
      }

      nav a:hover,
      nav a:focus {
        background-color: blue;
        color: white;
      }
```

Our CSS removes the list bullets with the `list-style-type` property, and uses the `:hover` and `:focus` **pseudo-classes** to draw a highlight bar on the menu at appropriate times.

> CSS provides more than 30 pseudo-classes that you can use as selectors. Here, we use `:hover` to determine whether the user's mouse cursor is above one of our links, while we use `:focus` to determine if the link has the current keyboard focus (i.e. with the `tab` key).
> Some pseudo-classes, like `:last-child`, let you select elements based on their reelationship to other elements. Others, like `:hover`, let you detect and react to user activity on the page. Still others, like `:full-screen`, can detect the user's browser state.

If you want a horizontal list, you need a few changes:

* Reset the width of the menu (`ul`).
* Set the font size for the list (`ul`) to `0`, then restore it for the list items (`li`).
* Set the list items to `inline-block`.
* Set the width of the list items to a value that will distribute the values the way you want them distributed (typically, you want a percentage width).
* Center the list items horizontally.

```html
nav ul {
	font-size: 0;
	width: 100%;
}

nav li {
	display: inline-block;
	font-size: 1.25rem;
	text-align: center:
	width: 25%;
}
```

When creating a nav bar, `<ul>` is more semantically meaningful than simply having a series of `<div>` elements, since a nav bar is essentially a list of navigation options. However, using `<ul>` also helps with consistent styling and behavior because browsers have built-in default styles for list elements, such as spacing, than can we can then customize easily. This means we have a predictable base appearance as a starting point for adjustments and tweaks. By contrast, `div` elements have no inherent list semantics or default styles, and you would need to add more CSS to duplicate list behavior and layout.

N.B. the `line-height` property generally works best with a unitless value that acts as a multiplier of the element's current line-height.


# 4:4 Tables Overview #

Back in the earliest days of the web, long before CSS took off, most developers employed tables to implement layouts. For instance, sites often used a format that had a banner at the top of the page, a footer at the bottom of the page, and two or three columns of content, navigation items, and ads between the two. Today, we use CSS to do that; back then, the solution required tables, so most developers learned how to use them for layout.

However, from the beginning, such code was a hack, and most people knew it. The HTML designers intended tables for use with tabular data --- data in which the horizontal and vertical positions of each item were significant.

Using tables to lay out non-tabular data was a frowned-upon workaround and led to the development of CSS and, later, the introduction of flex and grid in CSS.

Today, you should use tables for strictly tabular data, not layout.

## Table Tags ##

HTML provides a variety of tags to construct tables. The ones you'll see most often are:
* `<table>`	--- defines a table.
* `<tr>`		--- defines a single row in a table.
* `<td>`		--- defines a single data cell of content in a table. Each row contains zero or more cells.
* `<th>`		--- defines a single heading. The first cell in a row or column is typically a heading, but this is not required.
* `<thead>`	--- defines a set of one or more rows that comprise the header of the table.
* `<tbody>`	--- defines a set of one or more rows that comprise the body of the table.
* `<tfoot>`	--- defines a set of one or more rows that comprise the body of the table.

## Semantic Table HTML and Heading Scope ##

You can use the `thead`, `tfoot`, and `tbody` elements to provide semantic identification of the header, footer, and body rows.

You can also add the `scope` attribute to identify `<th>` elements as row (`scope="row"`) or column (`scope="col"`) headings.

## `rowspan` ##

You can use the `rowspan` attribute on certain table elements. Notably, if we use the `rowspan` attribute with `<th>`, we can make a heading that applies to more than one row. E.g., `rowspan="3"` will make a heading take up three rows of space in the same column, with the text content centred vertically.
