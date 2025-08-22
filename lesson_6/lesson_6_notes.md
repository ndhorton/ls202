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

## Offset Properties ##

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
