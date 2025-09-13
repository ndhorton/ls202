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


# CSS-Tricks CSS Grid Layout Guide #

Whereas Flexbox was originally developed at Mozilla, the origin of Grid was at Microsoft. Internet Explorer 10 and 11 support only the older Microsoft syntax for Grid. All modern browsers support Grid with the new standardized syntax.

To get started, we must define a container element as a grid with `display: grid`, set the column and row sizes with `grid-template-columns` and `grid-template-rows`, and then place its child elements into the grid with `grid-column` and `grid-row`. Similarly to Flexbox, the source order of the grid items doesn't matter. Your CSS can place them in any order, which makes it super easy to rearrange your grid with media queries.

## Terminology ##

* Grid Container --- the element on which `display: grid` is applied, the direct parent of all the grid items
* Grid Item --- the children (i.e. direct descendants) of the grid container
* Grid Line --- the dividing lines that make up the structure of the grid. They can be vertical ("column grid lines") or horizontal ("row grid lines") and reside on either side of a row or column, including the outside lines of the grid
* Grid Track --- the space between two adjacent grid lines, the columns or rows of the grid
* Grid Cell --- the space between two adjacent row and two adjacent column grid lines, a single "unit" of the grid
* Grid Area --- the total space surrounded by four grid lines, consisting of any number of grid cells


## CSS Grid Properties for the Parent (Grid Container) ##

`display` --- when given the value `grid` or `inline-grid`, defines the element as a grid container and establishes a new grid formatting context for its contents. `grid` generates a block-level grid while `inline-grid` generates an inline-level grid.

---

`grid-template-columns`, `grid-template-rows` --- defines the columns or rows of the grid with a space-separated list of values. The values represent the track size, and the spaces between them represent the internal grid lines.

The possible values for these two properties are:
* `<track-size>` --- can be a length, a percentage, or a fraction of the free space in the grid using the `fr` unit
* `<line-name>` --- an arbitrary name

Grid lines are automatically assigned positive numbers based on the setting of these properties (with an alternate set of negative numbers used to specify the same lines starting with the last at `-1`).

You can also choose to explicitly name the lines. The syntax involves specifying the name in square brackets followed by a space before each length value, e.g.:

```css

.container {
	display: grid;
	grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];
	grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line];
}

```

Note that a line can have more than one name, e.g.

```css

.container {
	display: grid;
	grid-template-rows: [row1-start] 25% [row1-end row2-start] 25% [row2-end];
}

```

If your definition contains repeating parts, you can use the `repeat()` notation to streamline things.

If multiple lines share the same name, they can be referenced by their line name and count:

```css

.item {
	grid-column-start: col-start 2;
}

```

The `fr` unit allows you to set the size of a track as a fraction of the free space of the grid container. The free space is calculated after any non-flexible items.

---

`grid-template-areas` --- defines a grid template by referencing the names of the grid areas which can be specified with the `grid-area` property on grid items. Repeating the name of a grid area causes the content to span those cells. A period signifies an empty grid cell. The syntax itself provides a visualization of the structure of the grid.

The possible values for `grid-template-areas` are:
* `<grid-area-name>` --- the name of a grid area specified with `grid-area`
* `.` --- a period signifies an empty grid cell
* `none` --- no grid areas are defined

Each row in your declaration needs to have the same number of cells.

You can use any number of adjacent periods to declare a single empty cell. As long as the periods have no spaces between them they represent a single cell.

When you use this syntax, the lines on either end of the areas are getting named automatically. If the name of your grid area is `foo`, the name of the area's starting row line *and* starting column line is `foo-start`, and the name of its last row line and last column line is `foo-end`. This means that some lines might have multiple names.

---

`grid-template` --- a shorthand for setting `grid-template-rows`, `grid-template-columns`, and `grid-template-areas` in a single declaration.

Possible values:
* `none` --- sets all three properties to their initial values
* `<grid-template-rows> / <grid-template-columns>` --- sets these properties to the specified values and sets `grid-template-areas` to `none`
* syntax for specifying all three, very complex, will need to refer back to CSS-Tricks and the documentation

Since `grid-template` doesn't reset the *implicit grid properties* `grid-auto-columns`, `grid-auto-rows`, and `grid-auto-flow`, which is probably what you want to do in most cases, it's recommended to use the `grid` property instead of `grid-template`.

---

`column-gap`, `row-gap`(, `grid-column-gap`, `grid-row-gap`) --- specify the size of the grid lines. You can think of it like setting the width of the gutters between the columns/rows. The gutters are only created between the columns/rows, not on the outer edges.

Possible values:
* `<line-size>` --- a length value

`column-gap` and `row-gap` are the new standard syntax. You should use these as first choice over `grid-column-gap` and `grid-row-gap`. The new syntax is supported in all modern browsers but not Internet Explorer.

---

`gap`(, `grid-gap`) --- a shorthand for `row-gap` and `column-gap`.

The possible values for `gap` (new standard syntax) are one or two lengths. If there is one length given, it represents both `row-gap` and `column-gap`. Otherwise, the first length is `row-gap` and the second `column-gap`.

The `grid-` prefix is deprecated, but might possibly never be removed.

---

`justify-items` --- aligns grid items along the inline (row) axis, as opposed to `align-items` which aligns along the block (column) axis). This value applies to all grid items inside the container.

Possible values for `justify-items`:
* `start` --- aligns items to be flush with the start edge of their cell
* `end` --- aligns items to be flush with the end edge of their cell
* `center` --- aligns items in the center of their cell
* `stretch` --- fills the whole width of the cell (this is the default)

This behavior can also be set on individual grid items via the `justify-self` property.

---

`align-items` --- aligns grid items along the block (column) axis (as opposed to `justify-items` which aligns them along the inline (row) axis). This value applies to all grid items inside the container.

Possible values for `align-items`:
* `stretch` --- fills the whole height of the cell (default)
* `start`
* `end`
* `center`
* `baseline` --- align itemss along text baseline. There are modifiers to `baseline`: `first baseline` and `last baseline`, which will use the baseline from the first or last line respectively in the case of multi-line text.

This behavior can also be set on individual grid items via the `align-self` property.

There are also modifier keywords `safe` and `unsafe`. Usage is like e.g. `align-items: safe end`. The `safe` keyword means "try to align like this, but not if it means aligning an item such that it moves into an inaccessible overflow area", while `unsafe` will permit content being moved there.

---

`place-items` --- sets both the `align-items` and `justify-items` properties in a single declaration.

Values:
* `<align-items>` `<justify-items>`

A single value can be used to set both.

---

`justify-content` --- sometimes the total size of your grid might be less than the size of its grid container. This could happen if all your gird items are sized with non-flexible units like `px`. In this case, you can set the alignment of the grid within the grid container. This property aligns the grid along the inline (row) axis (as opposed to `align-content` which aligns the grid along the block (column) axis).

Values:
* `start`
* `end`
* `center`
* `stretch`
* `space-around` --- places an even amount of space between each grid item, with half-sized spaces on the far ends
* `space-between` --- places an even amount of space between each grid item, with no space at the far ends
* `space-evenly` --- places an even amount of space between each grid item, including the far ends

---

`align-content` --- as above but aligns content along the block (column) axis as opposed to the row. The values are the same as `justify-content`.

---

`place-content` --- sets both the `align-content` and `justify-content` properties in a single declaration.

Values:
* `<align-content> <justify-content>`

If the first value is omitted, a single value sets both properties.

---

`grid-auto-columns`, `grid-auto-rows` --- specifies the size of any auto-generated grid tracks (aka *implicit grid tracks*). Implicit tracks get created when there are more grid items than cells in the grid or when a grid item is placed outside of the explicit grid.

When we manually define a fixed number of lines and tracks that form a grid by using the properties `grid-template-rows`, `grid-template-columns`, and `grid-template-areas`, we are defining the *explicit grid*.

If there are more grid items than cells in the grid, or when a grid item is placed outside of the explicit grid, the grid container automatically generates grid tracks by adding grid lines to the grid. The explicit grid together with these additional implicit tracks and lines forms the so called  *implicit grid*.

The widths and heights of the implicit tracks are set automatically. They are only big enough to fit the placed grid items, but it's possible to change this default behavior.

The `grid-auto-columns` and `grid-auto-rows` properties give us control over the size of implicit tracks.

Possible values:
* `<track-size>` --- can be a length, a percentage, or a fraction of the free space in the grid

---

`grid-auto-flow` --- if you have grid items that you don't explicitly place on the grid, the *auto-placement algorithm* kicks in to automatically place the items. `grid-auto-flow` controls how the auto-placement algorithm works.

Possible values:
* `row` --- tells the auto-placement algorithm to fill in each row in turn, adding new rows as necessary (default)
* `column` --- tells the auto-placement algorithm to fill in each dolumn in turn, adding new columns as necessary
* `row dense` or `column dense` --- tells the auto-placement algorithm to attempt to fill in holes earlier in the grid if smaller items come up later

Note that `dense` only changes the visual order of your items and might cause them to appear out of order, which is bad for accessibility.

---

`grid` --- a shorthand for setting all of the following properties in a single declaration: `grid-template-rows`, `grid-template-columns`, `grid-template-areas`, `grid-auto-rows`, `grid-auto-columns`, and `grid-auto-flow`. Note: you can only specify the explicit or the implicit grid properties in a single `grid` declaration.

Values:
* `none` --- sets all sub-properties to their initial values
* `<grid-template>` --- works the same as the `grid-template` shorthand
* `<grid-template-rows> / [ auto-flow && dense? ] <grid-auto-columns>?` --- sets `grid-template-rows` to the specified value. If the `auto-flow` keyword is to the right of the slash, it sets `grid-auto-flow` to `column`. If the `dense` keyword is specified in addition, the auto-placement algorithm uses a "dense" packing algorithm. If `grid-auto-columns` is omitted, it is set to `auto`.
* `[ auto-flow && dense? ] <grid-auto-rows>? / <grid-template-columns>` --- sets `grid-template-columns` to the specified value. If the `auto-flow` keyword is to the left of the slash, it sets `grid-auto-flow` to `row`. If the `dense` keyword is also specified, the auto-placement algorithm uses a "dense" packing algorithm. If `grid-auto-rows` is omitted, it is set to `auto`.

`grid` also accepts a more complex but quite handy syntax for setting everything at once. You specify `grid-template-areas`, `grid-template-rows`, `grid-template-columns`, and all the other sub-properties are set to their initial values. What you're doing is specifying the line names and track sizes inline with their respective grid areas.

## CSS Grid Properties for the Children (Grid Items) ##

Note: `float`, `display: inline-block`, `display: table-cell`, `vertical-align`, and `column-*` properties have no effect on a grid item.

### The `grid-column-start`, `grid-column-end`, `grid-row-start`, and `grid-row-end` Properties ###

The properties determine a grid item's location within the grid by referring to specific grid lines. `grid-column-start`/`grid-row-start` is the line where the item begins, and `grid-column-end`/`grid-row-end` is the line where the item ends.

Values:
* `<line>` --- can be a number to refer to a numbered grid line, or a name to refer to a named grid line
* `span <number>` --- the item will span across the provided number of grid tracks
* `span <name>` --- the item will span across until it hits the next line with the provided name
* `auto` --- indicates auto-placement, an automatic span, or a default span of one

Items can overlap each other. You can use `z-index` to control their stacking order.

### The `grid-column` and `grid-row` Properties ###

Shorthand for `grid-column-start` + `grid-column-end`, and `grid-row-start` + `grid-row-end`, respectively.

Values:
* `<start-line> / <end-line>` --- each one accepts all the same values as the longhand version, including `span`.

If no end line value is declared, the item will span 1 track by default.

### The `grid-area` Property ###

Gives an item a name so that it can be referenced by a template created with the `grid-template-areas` property on the Grid container.

Alternatively, this property can be used as an even shorter shorthand for `grid-row-start` + `grid-column-start` + `grid-row-end` + `grid-column-end`.

Values:
* `name` --- a name of your choosing
* `<row-start> / <column-start> / <row-end> / <column-end>` --- can be numbers or named lines

### The `justify-self` Property ###

Aligns a grid item inside a cell along the inline (row) axis (as opposed to `align-self` which aligns along the block(column) axis). This value applies to a grid item inside a single cell.

Values:
* `start` --- aligns the grid item to be flush with the start edge of the cell
* `end` --- aligns the grid item to be flush with the end edge of the cell
* `center` --- aligns the grid item in the center of the cell
* `stretch` --- fills the whole width of the cell (default)

To set alignment for *all* the items in a grid, this behavior can be set on the grid container with `justify-items`.

### The `align-self` Property ###

Aligns a grid item inside a cell along the block (column) axis (as opposed to `justify-self`), which aligns along the inline (row) axis). This value applies to the content inside a single grid item.

Values:
* `start` --- aligns the grid item to be flush with the start edge of the cell
* `end` --- aligns the grid item to be flush with the end edge of the cell
* `center`
* `stretch` (default)

To align *all* the items in a grid, we can use the `align-items` property on the Grid container.

### The `place-self` Property ###

`place-self` sets both the `align-self` and `justify-self` properties in a single declaration.

Value:
* `auto` --- the default alignment for the layout mode
* `<align-self> / <justify-self>` --- the first value sets `align-self`, the second value `justify-self`. If the second value is omitted, the first value is assigned to both properties

## Special Units and Fractions ##

Fractional units are common in Grid, e.g. `1fr`. They mean "portion of the remaining space". Unlike percentages, fractions are flexible and forgiving. If you add padding to an element, it won't necessarily cause the problems associated with percentages on elements using 'content-box'. Fractional units are much more friendly in relation to absolute lengths than percentages are.

When sizing rows and columns, you can use lengths but you also have keywords:
* `min-content` --- the minimum size of the content. In a line of text, the `min-content` would be the size of the longest word
* `max-content` --- the maximum size of the content. The `max-content` of a line of text would be the length of the whole line
* `auto` --- this keyword is like `fr` units, except that `auto` "loses the fight" for remaining space against `fr` units
 
The `fit-content()` function uses the space available, but never less than `min-content` and never more than `max-content`.

The `minmax()` function sets a minimum and maximum value for what the length is able to be. This is useful in combination with relative units. 

The `min()` function takes two arguments and returns the minimum value. The `max()` function takes two arguments and returns the maximum value.

Masonry is an experimental feature of CSS grid. There are lots of approaches to masonry layout (or waterfall layout) in CSS, but most of them are trickery with major downsides, or they simply don't do what you expect. The spec now has an official way, but it is not enabled by default in any web browsers yet.

Subgrid is another new and very useful feature of grids that allows grid items to have a grid of their own that inherits grid lines from the parent grid. This feature has newly made it into browsers, and is available on all contemporary browser updates released in the last couple of years. Not available on older versions of the contemporary browsers, and definitely not in Internet Explorer.

It is also useful to be aware of `display: contents`. This is not the same as subgrid, but it can be a useful tool for similar but not identical purposes. This property solves a different class of problems involved in grid layouts.

# Aerolab Flexbox and Grid #

One way to center the content within a Grid item is to declare that item `display: flex`. Thereafter, we can use `justify-content` and `align-items` to `center` the content.

# 6:10 Guided Project: Flex #

It's a good idea to start out by getting rid of all margins and padding at the global level to decrease the cross-browser differences. We can use the `*` selector in this project; you would typically use a CSS reset for this.

```css
* {
  margin: 0;
  padding: 0;
}

html {
  background-color: white;
  color: black;
  font: normal 24px Helvetica, Arial, sans-serif;
}
```

Remember: when there is a gap beneath an `img`, this is because `img` is `inline` by default. There are several ways of dealing with this, but one easy one (if its appropriate) is to set the `img` to `display: block`.

Remember: the `flex` property can be used with a unitless integer on flexbox items in much the same way fractions work for grid items' size.

# 6:12 CSS Frameworks #

Popular frameworks for CSS include **Bootstrap** and **Foundation**.

LS don't mention **Tailwind**, but that appears to be the most popular c. 2024. Tailwind is "utility-first", meaning that you compose Tailwind's tiny utility CSS classes in order to produce unique styles.

By contrast, Bootstrap and Foundation feature ready-made components and standard interfaces, which you can incorporate into a page wholesale. These components include HTML elements and optional JavaScript functionality in addition to CSS.

The most beneficial aspects of Bootstrap and Foundation are their handling of media queries for tablet and mobile views as well as a grid system that's already defined for you by way of generic classes.

A framework package typically has a grid system implemented with a combination of HTML, CSS, and JavaScript at it sheart. This grid has nothing to do with CSS Grid, though it's possible that frameworks may soon incorporate CSS Grid. (Bootstrap and Tailwind now incorporate Grid to differing extents.)

# 6:13 Responsive Design #

To make websites look good and provide the same functionality regardless of the device and screen size of the user, we can use media queries.

## Media Queries ##

Media queries very often define styles that change based on the current size of the browser window, which lets us customize the look for phones, tablets, small laptops, and large desktop displays.

For instance, to set a different anchor link color when the width of the screen is 480px or less, we might write:
```css
a {
	color: #f00;
}

@media (max-width: 480px) {
	a {
		color: #06c;
	}
}
```

Any styles placed inside this media query block will apply when the screen width is 480px or less.

We can also use the words `not` and `and` in media queries, and choose different media types such as `screen`, `print`, or `speech`. Most common is a combination of `screen` media type and a `min-width` or `max-width`, such as:

```css
@media screen and (max-width: 1600px) {
	/* CSS for 1600px (or smaller) screens (and no printers!) */
}
```

---
From MDN:
* Media queries allow you to apply CSS styles depending on a device's media type (such as print vs. screen) or other features or characteristics such as screen resolution or orientation, aspect ratio, browser viewport width or height, user preferences such as preferring reduced motion, data usage, or transparency.
* Media queries are used for the following:
	* To conditionally apply styles with the CSS `@media` and `@import` at-rules
	* To target specific media for the `<style>`, `<link>`, `<source>`, and other HTML elements with the `media=` or `sizes=` attributes
	* To test and monitor media states using the `Window.matchMedia()` and `EventTarget.addEventListener()` methods
* A media query is composed of an optional **media type** and any number of **media feature expressions**, which may optionally be combined in various ways using **logical operators**. Media queries are case-insensitive.
	* Media types define the broad category of device for which the media query applies: `all`, `print`, `screen`. The default type is `all`, and the type is optional unless using the logical operator `only`.
	* Media features describe a specific characteristic of the user agent, output device, or environment. Media feature expressions test for presence or absence or value, and are entirely optional. Each media feature expression must be surrounded by parentheses.
	* Logical operators can be used to compose a complex media query: `not`, `and`, `or`, and `only`. You can also combine multiple media queries into a single rule by separating them with commas. The comma-separated list of media queries behaves like an `or` composition of the media queries, and allows us to apply the same styles in different situations. The `only` operator was used to prevent older browsers from applying styles without evaluating the media feature expressions but it has no effect in modern browsers.
* A media query computes to `true` when the media type (if specified) matches the device on which a document is being displayed and all media feature expressions compute as true. Queries involving unknown media types are always false.

---

## Mobile-First and Desktop-First ##

A common approach is to design a website mobile-first, meaning the standard CSS with no media queries active lays out the site for mobile, and then a series of media queries for progressively larger screens re-style the page with layouts appropriate to the sizes.

The outer/topmost section contains not only the layout for mobile but also any styles common to all viewport sizes (usually colors, font families, etc). Then you would add a series of media queries, each of which modifies the layout for progressively larger displays (and possibly a media query for printers).

Conversely, the desktop-first approach to site design starts with the full-scale large desktop design first, and then progressively provides media queries for the smaller displays.

The mobile-first approach frequently results in faster downloads on mobile devices, while the desktop-first approach results in slower downloads.

Most developers consider the mobile-first approach to be best-practice.

## Breakpoints ##

Each step up (or down, in desktop-first) in screen size is known as a **breakpoint**.

Each breakpoint represents a size of screen/viewport, not a specific device necessarily. Contemporary mobile devices now cover a continuum of different screen sizes, and its hard to differentiate between a large phone and a small tablet.

Instead of asking whether you're working on a cell phone or desktop, it's more natural and useful to ask what layout works best over a particular range of screen sizes, then build each of those layouts with the appropriate media query.

## Emulating Devices in Google Chrome ##

As well as screen sizes of smaller devices, Chrome lets you emulate slower connection speeds by choosing mid-tier mobile or low-tier mobile.

For emulating devices, you will also need to add the HTML `<meta name="viewport">` element described below.

## Using Your Page on Multiple Devices ##

If you design your application with responsiveness in mind, you must put the following `<meta>` element in the `<head>` part of the `<html>`. It tells mobile devices how to handle that page; without it, those devices often display a miniaturized version of the page instead of showing the desired mobile device page described by your media queries and CSS.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Don't use this tag if your app has no responsiveness traits.


## Fluid and Liquid Layouts ##

Some terminology
* fixed-width layouts
* responsive design
* fluid layouts
* liquid layouts
* elastic layouts
* hybrid layouts

These types of layouts are all fairly similar in essence. Further, people tend to use one term in place of another.

Fixed-width layout simply means a non-responsive layout that does not change with window resizing, or for smaller devices.

Responsive design is a web design approach to make web pages render well on all screen sizes and resolutions while ensuring good usability. Is a way of designing web layouts so that they are flexible and work well across different device screen sizes, resolutions, etc. Typically, we use media query breakpoints to change the layout of the content to fit screen width.

Liquid layouts often employ percentage values for widths to maintain the same width ratios for content areas as the browser width changes.

The foundation of liquid and fluid layouts is to style elements such that elements retain their proportion of the width of the window 
regardless of the window resizing.

### Liquid Layouts ###

In a liquid layout, we can set two columns to `float: left`, with their container set to `overflow: hidden`, and then set `width` percentages such that both columns are displayed side-by-side. Of course, this means that if we change one percentage, we must change the other so they sum to 100%.

Alternately, we can set the first column to `float: left` and then set the second column to `overflow: hidden`. This means we only have to set the `width` on the floated element and the column to its right will resize automatically so that both columns sit side-by-side with a proportion dictated by the floated element, regardless of how we resize the window.

### Fluid Layouts ###

Liquid layouts ordinarily take up the entire width of the browser window, no matter how big it gets. If you want to restrict the expansion or collapse, you need to use a fluid layout. Once the window reaches one of the limits, the element will cease expanding or collapsing and remain fixed in width as the window width continues to change in the same direction. Fluid layouts expand and collapse like a liquid layout to a point, then become fixed once the browser width reaches a specific size.

We can achieve this by setting a `min-width` and `max-width` on the container element for our page layout.

According to a StackOverflow user citing a textbook on web design, an **elastic** layout has its elements' widths defined in terms of ems rather than percentages. This way, they resize dependent on font size rather than viewport width. In principle, it's the behavior most browsers make available through Page Zoom.

An **adaptive** layout means having several fixed-width layouts of different sizes which we switch between dependent on the size range within which the actual size of the viewport falls. In this scheme, a responsive layout means combining adaptive and liquid layouts, so that regardless of window size the proportions of element widths in relation to each other will be the same within the size range between breakpoints, and the layout then changes significantly (like an elastic layout) when the window resizing hits a breakpoint.


