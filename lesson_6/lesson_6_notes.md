# 6:1 Advanced Layout Introduction #

At the simplest level, most web pages have a typical layout: a header, footer, navigation bar, and the content. Your HTML file should reflect this struture with each area defined in sequence. You can build hundreds of pages following this pattern, and control them all with a single CSS file.

CSS allows you to re-position parts of the page. This is useful in the given situation where a single CSS file is used for many pages across the website. If a site-wide change in the basic structure of the pages need to be made, like moving an ad banner from above the header to below the header, we can do this for all the web pages by making changes to the single CSS file, rather than changing the many HTML files.

This same need to fundamentally change the layout of an HTML file via CSS arises when we need the website to look different on cell phones, tablets, or desktop and laptop computers. Again, you can use CSS to reposition content elsewhere on the page when the display size reaches a certain point.

Layout-related features of CSS include floats, positioning, flex, grid, CSS frameworks, and responsive design. We will focus on:

* floated elements, including how to clear floats
* positioning with `position: absolute`
* basic media queries
* liquid and fluid layouts

# 6:2 Floats #

We can place elements side by side with the `inline` and `inline-block` display types. However, there are some cases where this isn't the best solution. For example, we might need to collapse the whitespace between two side-by-side `inline-block` elements; when we are using `inline-block`, this necessitates some ugly hacks to the HTML to avoid unwanted whitespace between elements.

In this situation, it might be better to use **floats**. A **floated** element tells the browser to move it as far to the left or right as possible, but to leave the remaining space available for additional content.

Elements float within their immediate container, which puts a limit on how far the browser can move the floated element. If you float two elements in a row in the same direction, their vertical edges (counting their margins) will touch, providing they fit in the same row. Any whitespace (other than margins and padding) that would otherwise appear between the elements will collapse.

Most developers try to keep their use-case simple when dealing with floats: make sure all floats in a group have the same height and direction (left or right), and they will wrap in a way that is easy to reason about. You can also mix left and right floats with predictable results if you're careful, again provideed the heights are consistent. Attempts at more complicated layouts using floats can quickly become impractical to predict and understand fully, even if their rendering is essentially deterministic.

# 6:3 Containing Floats #

When we use floats for layout, we often run into the "containing floats" problem. Since floats are removed from the normal document flow, in some situations their container will not actually contain them. Unlike with normal flow elements, the browser cannot automatically determine the container's height based on the size of the floated elements, and this can lead to unexpected results where the container doesn't render as we wish.

Floated elements (and absolute or fixed position elements) typically don't afffect the dimensions of their parents. Since the browser removes the content from the flow, the rendering enggine no longer cares about them. The floated or positioned elements can overwrite other content.

To fix this problem, we must add an `overflow` setting to the floated element's container's CSS, or wrap it in a **clearfix**.

## The `overflow` Property ##

Setting the `overflow` property to `hidden` or `auto` is the simplest way to ensure that the boundary of the container 'clears' the boundaries of the floated elements within it. We can apply the property to the container and it will generally expand to wrap our floated elements.

There are two edge cases we need to be aware of:

* `overflow: hidden` can cut off (clip) content that exceeds the allocated space for the text if the container has a set height or width
* `overflow: auto` can add unwanted scrollbars, which is a browser-specific behavior

If you experience either issue, you can use the clearfix approach.

According to W3C standards documentation, `overflow` creates a **block formatting** context which contains everything inside the element to which it applies, and that includes floats. To learn more, search for "block formatting context" and "floats".

## Add a 'Clearfix' ##

Instead of `overflow`, we can add a **clearfix** to the container. A clearfix is a standard pattern that developers use to ensure a container doesn't lose its floated children. It employs an invisible block element as the last child element of the container, as well as using the `clear` property.

As with `overflow`, the clearfix ensures that the parent container wraps the two floated columns. Here is an example used on container element with the `id` of `columns`:

```css
#columns::after { /* This rule is the clearfix */
  clear: both;
  content: "";
  display: block;
}
```

The `::after` pseudo-element creates a child element at the end of the selected element(s); here, we put it at the end of our container. We define this child as a block element, which means it must be on a line by itself. The `content: ""` property sets the content of the child element: an empty string. Thus, the clearfix child is invisible. Lastly, we use `clear: both` to "clear" the floats inside the continer, which forces the invisible child directly below the floated content. The container can see the clearfix, so all it needs to do is stretch itself to enclose the clearfix, and, by doing so, the floated content as well. The final result is similar to that of using `overflow`.

`clear` takes values of `right`, `left`, or `both`. `right` and `left` refer to the type of floated element it will clear, while `both` clears any floated element that it finds. You can use any of these values with `clear`, but you should use `clear: both` unless you find that you need `left` or `right` for some specific reason.

Use double colons with pseduo-elements. The standard lets you get away with a single colon, but this flexibility may not endure.

CSS presently supports around a dozen pseudo-elements, and nearly half of those are experimental. `::after` and `::before` are the most useful.

# 6:4 Practice Problems Floats (1) #

Adding `overflow: hidden` to the last floated element in a row and removing the `float` and `width` properties cause it to take up the remaining space within the row.

This technique is useful when your last element should take up the leftover space in a variable-width layout.

If we have a left hand column element floated left with a variable width of 70%, and a non-floated element with `overflow: hidden` set following it, the non-floated element will effectively take up 30% (as long as `box-sizing: border-box` is set) regardless of how the window is resized.



# 6:6 Positioning #

When you need to fine-tune the placement of elements within their containers or need to overlay them atop others, CSS positioning comes into play.

## Offset Properties ##

Before we talk about the `position` property, we need to be aware of the **offset properties**: `top`, `right`, `bottom`, and `left`. They work in conjunction with `position` to determine what direction you want to move an element and how far.

Each offset measures the *inward* distance from the side of the container named by the offset property. For instance, `bottom: 50px` indicates a position 50px inward from (above) the bottom edge of the container. If you memorize one fact from this page, remember that *the offset is always inward* when workng with positive offset values.

Negative offsets shift elements in the opposite direction. That is, they cause the browser to push the edges outward from the container.

## The `position` Property ##

The `position` property tells the browser how to position the selected elements.

### `postion: static` ###

Static positioning is the default. While floated, grid, flex, as well as elements with absolute and fixed positioning get removed from the page flow, statically positioned items are part of the page flow. They appear in the same order that they appear in the markup. The offset properties do not affect static elements.

### `position: relative` ###

Relative positioning moves an element to a new position relative to where the browser would otherwise put it.

For instance, if you include `left: 50px` and `bottom: 100px` with `position relative`, the browser will shift the element 50px inward from the left edge and 100px upward from the bottom edge from where the browser would place it otherwise.

When using relative positioning, you should typically provide at most one vertical offset (`top` xor `bottom`) and at most one horizontal offset (`left` xor `right`).

The CSS standard does permit using both vertical or both horizontal properties at the same time:

* `left` overrides `right` for left-to-right languages.
* `right` overrides `left` for right-to-left languages.
* `top` overrides `bottom` at all times

Relative positioning *does not* remove an item from the document flow (unlike absolute or fixed positioning). The browser positions the next element as though the previous one still occupied its pre-offset location. Each box respects the area that the previous one would occupy in the absence of positioning offsets.

### `position: absolute` ###

Absolute positioning causes the browser to move the element to a new position within a container element. By default, the container is the *nearest ancestor element that has a fixed, relative, absolute, or sticky position. If no such ancestor is present, the browser uses the initial containing block; that is, the browser positions the element at an absolute position on the page.

N.B. the course doesn't cover `position: sticky`, so look that up later.

The W3C CSS2.2 standards document has this to say about the initial containing block:

> ## 10.1 Definition of "containing block"
>
> The position and size of an element's box(es) are sometimes calculated relative to a certain rectangle, called the containing block of the element. The containing block of an element is defined as follows:
>
> 1. The containing block in which the [root element](https://www.w3.org/TR/CSS22/conform.html#root) lives is a rectangle called the initial containing block. For continuous media, it has the dimensions of the [viewport](https://www.w3.org/TR/CSS22/visuren.html#viewport) and is anchored at the canvas origin; it is the [page area](https://www.w3.org/TR/CSS22/page.html#page-area) for paged media. The 'direction' property of the initial containing block is the same as for the root element.

We can center an absolute positioned element within its nearest relative, absolute, or sticky ancestor by setting *all four* offset properties to the same value. Note that this won't work if the absolute positioned element has an explicit height or width (though there is a way to handle that situation).

Absolute positioning removes elements from the normal document flow. No matter where you position the element, the browser won't treat that space as occupied space.

### `position: fixed` ###

Fixed positioning sets an element to a fixed position within the window. The element **does not move** if the user scrolls the page.

N.B. It is important to note that `fixed` position elements will general display over (closer to the viewer) than `static` elements. However, whether a `fixed` position element displays over or under a `relative` or `absolute` element depends on their order in the source HTML. Obviously you can control this directly using the `z-index` property.

It can be useful to use classes on wrapper elements in order to apply uniform styles to common elements within different parts of the document.

# 6:9 Flex and Grid #

The approach of using floats and position to control CSS layouts works well and has endured for years. However, floats and positioning can be hard to use for some formats. Furthermore, with both floats and positioning, you must deal with the effects of removing items from the flow.

## Flex ##

Over the past few years, the `flex` property has undergone widespread growth. Flex (or Flexbox) solves a lot of design problems that plague front-end developers. Support is now strong across contemporary browsers, with nearly universal availability to users.

Flex is a one-dimensional layout tool; you can lay out a single row or column with a single flexbox. You can also create two-dimensional formats by using multiple flexboxes, but Grid works better for two-dimensional work.

## Grid ##

Another `display` property, `grid`, has exploded on the Web and become a useful companion for Flex. Widespread use is now here with over 96% of browsers now supporting Grid. The specification is complete.

Grid is a two-dimensional layout tool; you can place elements in a grid (rows and columns) format at the same time. It's also possible to do a single row or a single column, but that's merely a degenerate form of a grid; Flex is often better for such cases.

# Video: Why Use Flexbox? --- Jay Shenk #

Flexbox is short for CSS Flexible Box Layout Module. It is an attempt to make responsive design easier and more intuitive, and to solve many long-standing CSS problems.

CSS Pain Points:  

* Floats weren't designed for layout (just content wrapping around an image)
* Floats have to be cleared
* Responsive design often requires many media queries
* When using `inline-block` and `inline` elements, whitespace in the HTML can become a problem
* Vertical alignment is problematic

Flexbox makes some of these things much easier.

Generally, Flexbox is for components and Grid is for page layouts, according to Shenk. This might loosely correspond to the one- vs two-dimensional criteria. In practice, I think it is common to nest `display: flex` elements to achieve local component and sub-component layouts that *suggest* 2d organization (e.g. two columns where one column is divided into two rows), but you would probably use Grid to organize a whole 2d page layout since page layouts are almost always 2d in complex ways. In fact, in the Grid video, Morten Rand-Hendriksen describes using nested Flexboxes as a hack.

# Video: CSS Grid Changes Everything (About Web Layouts) --- Morten Rand-Hendriksen #

[Slides for this talk are available at the speaker's website](https://mor10.com/wceu2017)

Grid is short for CSS Grid Layout Module.

Problem: current tools for web layout are *content-out* and one-dimensional. 'Content-out' means we often need to nest semantic content within meaningless container `div`s and other non-semantic elements in order to float, clear floats, position in relation to a container, etc.

Solution: two-dimensional *layout-in* tool to separate content from presentation. We simply have the semantic content in the most logical order and do all of the layout in CSS.

CSS Grid Terminology:

* Grid *container* --- any container in your document inside which you create a grid by setting `display: grid`.
* Grid *item* --- element that is a direct descendant (child) of the grid container (just like Flexbox).
* Grid *line* --- any of the horizontal (row) or vertical (column) lines separating the grid into sections. Grid lines are referenced by number, starting and ending with the outer borders of the grid.
* Grid *cell* --- the intersection between a grid row and a grid column. Effectively the same as a table cell.
* Grid *track* --- the space between two or more adjacent grid lines. Row tracks are horizontal, column tracks are vertical.
* Grid *area* --- rectangular area between four specified grid lines. Grid areas can cover one or more cells.
* Grid *gap* --- empty space between grid tracks. Commonly called gutters.

Workflow:
1. Define a grid.
2. Place items within the grid.

In the container, we set `display: grid` and use the `grid-template-columns` property to establish vertical grid lines. This property takes a list of length values (em, px, %, fr, etc) denoting the distance between each line. We can use the grid unit `fr`, which means 'fraction' of the available space. `grid-template-rows` works the same way but with horizontal grid lines.

N.B. although the video talks about the lines, it's more accurate to say that the `grid-template-*` properties define tracks (which implies defining lines). But the list of values describe the tracks (rows or columns) not the number of lines.

The `grid-column` and `grid-row` properties can be placed in the child elements if we wish to specify how many and which cells of the grid the element will occupy. So, for instance, `grid-column: 2/4` tells us that the child element will take up the space from vertical line 2 to vertical line 4.

Keeping track of the line numbers can be difficult, even though you can give the lines names. It is easier to use the `grid-template-areas` property, which applies to the grid container. This property uses a text-based grid map to apply grid area names to individual cells.

The `grid-template-areas` value is almost like ASCII art:
```css
.site {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    grid-template-rows: auto 1fr 3fr;
    grid-template-areas:
    	"title title tile"
    	"main header header"
    	"main sidebar footer";
}
```

We can then place individual items by selecting them in CSS and using the `grid-area` property in conjunction with the area names we defined in `grid-template area`:
```css
.main-content {
	grid-area: main;
}
```

Nested grids: grids are not inherited by child elements. Instead, we can create nested grids.

For old Microsoft browsers (IE and older versions of Edge), it can be necessary to use a feature query to check for Grid properties that were not supported by Windows and Edge until c. 2017.

Grid was actually developed by Microsoft engineers for Internet Explorer and its features made available through vendor-prefixed properties. However, when Grid was standardized with input from other browser vendors, the spec was changed and so many of the standard grid properties diverged from the Microsoft version. There was a gap in time where Windows needed to be altered in order to change the spec for Microsoft Edge (which had superceded IE by then) so that Edge could support the standardized spec. This is why it is necessary to make a query for the specific features that older Microsoft browsers lacked, rather than just testing for `display: grid`. The older browsers supported `display: grid` but with different Grid properties and behaviors to those implemented in modern browsers.

Another option is to serve up the mobile-targeted CSS on browsers that do not support Grid.

CSS Grid: A Practical Approach

1. Build accessible mobile-first layout without Grid.
2. Use mobile-first layout as a fallback.
3. Use `@supports` to detect grid support.
4. At the appropriate breakpoint, create layout with Grid and `grid-area`.
5. Explore new layouts as view widens.

[Rachel Andrew's "Grid by Example" website](https://gridbyexample.com/)

MDN, CSS-Tricks, etc have articles about Grid.

# CSS-Tricks: CSS Flexbox Layout Guide #

The Flexbox Layout (Flexible Box) module aims at providing a more efficient way to lay out, align and distribute space among items in a container, even when their size is unknown and/or dynamic (thus the word "flex").

The main idea behind the flex layout is to give the container the ability to alter its items' width/height (and order) to best fill the available space (mostly to accomodate to all kind of display devices and screen sizes). A flex container expands items to fill available free space or shrinks them to prevent overflow.

Most importantly, the flexbox layout is direction agnostic as opposed to the regular layouts (block which is vertically-based and inline which is horizontally based). While those work well for pages, they lack flexibility to support large or complex applications (especially when it comes to orientation changing, resizing, stretching, shrinking, etc.).

Note: Flexbox layout is most appropriate to the components of an application, and small-scale layouts, while the Grid layout is intended for larger scale layouts.

## Basics and Terminology ##

Since flexbox is a whole module and not a single property, it involves a lot of things including its whole set of properties. Some of them are meant to be set on the container (parent element, known as "flex container") whereas the others are meant to be set on the children ("flex items").

If "regular" layout is based on both block and inline flow directions, the flex layout is based on "flex-flow directions".

Items will be laid out following either the main axis (from main-start to main-end) or the cross axis (from cross-start to cross-end). The main axis can be horizontal or vertical, and then the cross axis is the other direction.

* **main axis** --- The main axis of a flex container is the primary axis along which flex items are laid out. Beware, it is not necessarily horizontal; it depends on the `flex-direction` property.
* **main-start** | **main-end** --- The flex items are placed within the container starting from main-start and going to main-end.
* **main size** --- A flex item's width or height, whichever is in the main dimension, is the item's main size. The flex item's main size property is either the `width` or `height` property, whichever is in the main dimension.
* **cross axis** --- The axis perpendicular to the main axis is called the cross axis. Its direction depends on the main axis direction.
* **cross-start** | **cross-end** --- Flex lines are filled with items and placed into the container starting on the cross-start side of the flex container and going toward the cross-end side.
* **cross size** --- The width or height of a flex item, whichever is in the cross dimension, is the item's cross size. The cross size property is whichever of `width` or `height` that is in the cross dimension.


## Flexbox Properties ##

### Properties for the Parent (flex container) ###

* `display` --- the values `flex` and `inline-flex` define a flex container; the value `flex` defines a block-level element, `flex-inline` an inline-level element. These values enable a flex context for all the element's direct children. Note that CSS columns have no effect on a flex container.
* `flex-direction` --- the four possible values are
	* `row` (default) --- left to right (assuming left-to-right text direction)
	* `row-reverse` --- the reverse horizontal direction of `row`
	* `column` --- top to bottom (assuming block axis is top to bottom)
	* `column-reverse` --- the opposite vertical direction to `column`
* `flex-wrap` --- by default, flex items will all try to fit onto one line. You can change that and allow the the items to wrap as needed with this property. The possible values are:
	* `nowrap` (default) --- all flex items will be on one line
	* `wrap` --- flex items will wrap onto multiple lines, from top to bottom
	* `wrap-reverse` --- flex items will wrap onto multiple ines from bottom to top
* `flex-flow` --- this is shorthand for the `flex-direction` and `flex-wrap` properties. The default value is `row nowrap`.
* `justify-content` --- defines the alignment along the main axis. It helps distribute extra free space leftover when either all the flex items on a line are inflexible, or are flexible but have reached their maximum size. It also exerts some control over the alignment of items when they overflow the line. Some of the possible values are:
	* `flex-start` (default) --- items are pack toward the start of the flex-direction
	* `flex-end` --- items are packed toward the end of the flex-direction
	* `flex-center` --- items are centered
	* `space-between` --- items are evenly distributed
	* `space-around` --- items are evely distributed in the line with equal space around them. Not that visually the spaces aren't equal, since all the items have equal space on both sides. The first item will have one unit of space against the container edge, but two units of space between the next item and itself because that next item has its own spacing that applies
	* `space-evenly` --- items are distributed such that the spacing between any two items (and the space to the edges) is equal
	* `start` --- items are packed toward the start of the `writing-mode` direction
	* `end` --- items are packed toward the end of the `writing-mode` direction
	* `left` --- items are packed toward the left edge of the container, unless that doesn't make sense with the `flex-direction`, and then it behaves like `start`
	* `right` --- items are packed toward right edge of the container, unless that doesn't make sense with the `flex-direction`, and then it behaves like `end`
* `align-items` --- this defines the default behavior for how flex items are laid out along the cross axis on the current line. Think of it as the `justify-content` for the cross-axis (perpendicular to the main axis). The values for this property are (`safe` and `unsafe` modifiers can be used in conjunction with all the rest of these keywords and deal with helping you prevent aligning elements such that the content becomes inaccessible):
	* `stretch` (default) --- stretch to fill the container (still respect `min-width`/`max-width`)
	* `flex-start` / `start` / `self-start` --- items are placed at the start of the cross axis. The difference between these is subtle, and is about respecting the `flex-direction` rules or the `writing-direction` rules
	* `center` --- items are centered in the cross-axis
	* `baseline` --- items are aligned such that their baselines align
* `align-content` --- for a multi-line flexbox (i.e. one with `flex-wrap` set to `wrap` or `wrap-reverse`), `align-content` aligns the flex container's lines when there is extra space in the cross-axis, similar to how `justify-content` aligns items within the main axis. Note that this property has no effect on single-line flexboxes. The possible values are (`safe` and `unsafe` can be used with all):
	* `normal` (default) --- items are packed in their default position as if no value was set
	* `flex-start` / `start` --- items packed to the start of the container. The (more supported) `flex-start` honors the `flex-direction` while `start` honors the `writing-mode` direction
	* `flex-end` / `end` --- items packed to the end of the container. The distinction between the two is the same as for the `start` values.
	* `center` --- items centred in the container
	* `space-between` --- items evenly distributed; the first line is at the start of the container while the last one is at the end
	* `space-around` --- items evenly distributed with equal space around each line
	* `space-evely` --- items are evely distributed with equal space around them
	* `stretch` --- lines stretch to take up the remaining space
* `gap` / `row-gap` / `column-gap` --- The gap property explicitly controls the space between flex items. It applies that spacing only between items, not on the outer edges. The behavior could be thought of as a minimum gutter, because, if the gutter is bigger somehow (because of something like `justify-content: space-between`), then the gap will only take effect if that space would end up smaller than the gap properties dictate. The gap properties can also be used with Grid and multi-column layout as well

### Properties for the Children (flex items) ###

* `order` --- By default, flex items are laid out in the HTML source order. However, the `order` property controls the order in which they appear in the flex container. The order value is a number, and lower numbers come first. Items with the same order number appear in source order. The default is `0`.
* `flex-grow` --- this defines the ability for a flex item to grow if necessary. It accepts a unitless number value that serves as a proportion. It dictates what amount of the available space inside the flex container the item should take up. If all items have `flex-grow` set to `1`, the remaining space in the continer will be distributed equally to all children. If one of the children has a value of `2`, that child would take up twice as much of the sapce as either one of the others (or it will try, at least). Unlike for `order`, negative numbers are invalid.
* `flex-basis` --- this defines the default size of an element before the remaining space is distributed. It can be a length (including percentages) or a keyword. The `auto` keyword means "look at my width or height property" (which was temporarily done by the `main-size` keyword until deprecated). The `content` keyword means "size it based on the item's content", but browsers lagged behind on implementing this keyword, so check availability. Other options include `content`, `min-content`, `max-content`, and `fit-content`. If set to `0`, the extra space around content isn't factored in. If set to `auto`, the extra space is distributed based on its `flex-grow` value.
* `flex` --- this is shorthand for the `flex-grow`, `flex-shrink`, and `flex-basis` combined. The second and third parameters (`flex-shrink` and `flex-basis`) are optional. The default is `0 1 auto`, but if you set it with a single number value, that changes the `flex-basis` to 0%. It is recommended that you use this shorthand property with a keyword value rather than setting the three individual properties it governs separately. The shorthand sets the other values intelligently
* `align-self` --- this allows the default alignment (or the one specified by `align-items`) to be overridden for individual flex items. The values are the same as those for `align-items` on the parent container


The Flexbox spec has changed over time, creating "old", "tweener", and "new" versions. The best way to handle this is to write in the new (and final) syntax and run your CSS through [Autoprefixer](https://css-tricks.com/autoprefixer/), which handles the fallbacks very well.

# Basic Concepts of Flexbox - MDN #

When working with flexbox you need to think in terms of two axes --- the *main axis* and the *cross axis*. The main axis is defined by the `flex-direction` property, and the cross axis runs perpendicular to it.

## The main axis ##

The main axis is defined by `flex-direction`, which has four possible values:
* `row`
* `row-reverse`
* `column`
* `column-reverse`

`row` and `row-reverse` cause the main axis to run along the row in the **inline direction**.

`column` and `column-reverse` cause your main axis to run along the column in the **block direction**, from top to bottom.

## The cross axis ##

The cross axis runs perpendicular to the main axis. Therefore, if your `flex-direction` (main axis) is set to `row` or `row-reverse`, the cross axis runs down the columns. And if your main axis is `column` or `column-reverse`, then the cross axis runs along the rows.

## Start and End Lines ##

Flexbox makes no assumption about the writing mode of the document.

Assume `flex-direction` is `row` and we are working in English: the start edge of the main axis will be on the left, and the end edge on the right.

Assume `flex-direction` is `row` and we are working in Arabic: the start edge of the main axis will be on the right, and the end edge on the left.

In both of the above cases, the start edge of the cross-axis is at the top of the flex container and the end edge at the bottom, as both languages have a horizontal writing mode.


## The flex container ##

You can explicitly control whether the flex container is displayed inline or in block formatting by using the `inline flex` or `inline-flex` values of `display` for inline flex containers, or `block flex` or `flex` for block level flex containers.

The defaults for a flex container:
* `flex-direction: row`
* Items start from the start edge of the main axis
* The items do not stretch on the main dimension but can shrink (a flex-item's `flex-grow` property's default value is `0` and its `flex-shrink` property's value is `1`).
* The items will stretch to fill the size of the cross-axis (the `align-items` property's value is `stretch`)
* The flex-item's `flex-basis` property defaults to `auto`. This means that, in each case, it will be equal to the flex item `width` in horizontal writing mode, and the flex item `height` in vertical writing mode. If the corresponding `width`/`height` is also set to `auto`, the `flex-basis` `content` value is used instead.
* All the items will be in a single row (the `flex-wrap` property's default value is `nowrap`), overflowing their container if their combined `width`/`height` exceeds the containing element `width`/`height`

The result of this is that your items will all line up in a row, using the size of the content as their size in the main axis. If there are more items than can fit in the container, they will not wrap but will instead overflow. If some items are taller than others, all items will stretch along the full length of the cross-axis.

### Multi-line flex containers with flex-wrap ###

While flexbox is a one dimensional model, it is possible to mmake flex items wrap across multiple lines. If you do this, you should consider each line as a new flex container. Any space distribution will happen across each line, without reference to the previous or subsequent lines.

## The flex items ##

To control the inline-size of each flex item, we target them directly via three properties:
* `flex-grow`
* `flex-shrink`
* `flex-basis`

In order to make sense of these properties, we need to consider the concept of **available space**. What we are doing when we change the value of these flex properties is to change the way that **available space** is distributed amongst our items. This concept of available space is also important when we come to look at aligning items.

If we have three 100 pixel-wide items in a container which is 500 pixels wide, then the space we need to lay out our items is 300 pixels. This leaves 200 pixels of available space. If we don't change the initial values then flexbox will put that space after the last item.

If instead, we would like the items to grow and fill the space, then we need to have a method of distributing the leftover space between the items. The `flex` properties that we apply to the items themselves enable dictating how that available space should be distributed among the sibling flex items.

### The `flex-basis` property ###

The `flex-basis` is what defines the size of the item on which it is set in terms of the space it leaves as available space. The initial value of this property is `auto` --- in this case the browser looks to see if the item has a size. In the example above, all of the items have a width of 100 pixels. This would then be used as the `flex-basis`.

If the items don't have a size then the content's size is used as the flex-basis. This is why when we just declare `display: flex` on the parent to create flex items, the items all move into a row and take only as much space as they need to display their contents.

### The `flex-grow` property ###

With the `flex-grow` property set to a positive integer, if there is available space, the flex item can grow along the main axis from its `flex-basis`. Whether the item stretches to take up all the available space on that axis or just a portion of the available space depends on whether the other items are allowed to grow too and the value of their `flex-grow` properties.

Each item with a positive value consumes a portion of any available space based on their `flex-grow` value. If we gave all of our items in the example above a `flex-grow` value of 1, then the available space in the flex container would be equally shared between our items and they would stretch to fill the container on the main axis. If we give our first item a `flex-grow` value of 2, and the other items a value of 1 each, there are a total of 4 parts; 2 parts of the avilable space will be given to the first item and 1 part each the other two.

### The `flex-shrink` property ###
Where the `flex-grow` property deals with adding space in the main axis, the `flex-shrink` property controls how it is taken away. If we do not have enough space in the container to lay out our items, and `flex-shrink` is set to a positive integer, then the item can become smaller than the `flex-basis`. As with `flex-grow`, different values can be assigned in order to cause one item to shrink faster than others --- an item with a higher value set for `flex-shrink` will shrink to take up proportionally less space than its siblings that have lower values.

An item can shrink down to its `min-content` size. This minimum size is taken into account while working out the actual amount of shrinkage that will happen, which means that `flex-shrink` has the potential to appear less consistent than `flex-grow` in behavior.

> Note: These values for `flex-grow` and `flex-shrink` are proportions. Typically, if we had all of our items set to `flex: 1 1 200px` and then wanted one item to grow at twice the rate, we would set that item to `flex: 2 1 200px`. However, you could also use `flex: 10 1 200px` and `flex: 20 1 200px` if you wanted.


### Shorthand values for the flex properties ###

You will very rarely see the `flex-grow`, `flex-shrink`, and `flex-basis` properties used individually; instead they are combined into the `flex` shorthand. The `flex` shorthand allows you to set the three values in this order --- `flex-grow`, `flex-shrink`, `flex-basis`.

There are also some predefined shortand values for `flex` which cover most common use cases. You will often see these used in tutorials, and in many cases these are all you will need to use. The predefined values are as follows:
* `flex: initial`
* `flex: auto`
* `flex: none`
* `flex: <positive-number>`

The `initial` value is a CSS-wide keyword that represents the initial value for a property. Setting `flex:initial` resets the item to the initial values of the three longhand properties, which is equivalent to `flex: 0 1 auto`.

Using `flex: auto` is the same as using `flex: 1 1 auto`; this is similar to `flex: initial` except items can grow and fill the container as well as shrink if needed.

Using `flex: none` will create fully inflexible flex items. It is as if you wrote `flex: 0 0 auto`. The items cannot grow or shrink and will be laid out using flexbox with a `flex-basis` of `auto`.

The shorthand you often see in tutorials is `flex: 1` or `flex: 2` and so on. This is the same as writing `flex: 1 1 0` or `flex: 2 1 0`, and so on. The items get minimum size due to `flex-basis: 0` and then proportionally grow to fill the available space. In this case, the `flex-shrink` value of `1` is redundant because the items start with minimum size --- they're not given any size that could cause them to overflow the flex container.


The `justify-items` property is ignored in flexbox layouts.

The `place-items` property is a shorthand property for `align-items` and `justify-items`. If set on a flex container, it will set the alignment but not the justification, as `justify-items` is ignored in flexbox.

There is another shorthand property, `place-content`, that defines the `align-content` and `justify-content` poroperties. The `align-content` property` only effects flex containers that wrap.

