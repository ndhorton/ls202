# The Box Model

## 2:1 Introduction

* The Box Model
  
  * box properties
    
    * width and height
    
    * padding and margins
    
    * borders
  
  * visual display model (`display` CSS property)
    
    * `block`
    
    * `inline`
    
    * `inline-block`
  
  * box sizing model (`box-sizing` CSS property)
    
    * `content-box`
    
    * `border-box`

* dimensions
  
  * absolute units
  
  * relative units

* container &mdash; almost always a block-level element that acts as a container to nested elements

* physical pixels

* CSS reference pixels

* length units &mdash; `px`, `em`, `rem`, `%`, `auto`

* Important CSS properties &mdash; `display`, `box-sizing`, `width`, `height`, `padding`, `border`, `margin`

## 2:2 Everything is a Box

**Box Properties**

Every element has the following properties (though the browser may ignore some of them):

* The  **width** and **height** define how much horizontal and vertical space it needs for the *content area* of the box, which may or may not include the padding and borders. In most cases, the browser can determine trhe width and height automatically.

* The **padding** is an area that surrounds the content area of the box and separates the content from its border. It is typically opaque and hides anything that it overlays.

* The **border** is a boundary that surrounds the padding.

* The **margin** is a transparent area that lies outside the border and supplies separation between elements.

* The **display** property determines how the browser lays out an element relative to its neighbors.

## The Visual Formatting Model

The `display` property has *more than two dozen* possilble values, but most CSS uses just `block`, `inline`, and `inline-block`. We call this property the *visual formatting model*.

**Block Elements**

Block elements appear on almost all webg pages: headings, paragraphs, sections, tables forms lists, and more are `block` elements.

Most `block` elements group one or more elements — some of which may themseleves be `block`s — into areas of the page. For instance, `header` elements group together elements into a page header. We often call such `block` elements **containers**. The master container (the outermost) is the `body`; every other element belongs to a container.

By default, a `block` element occupies all horizontal space avilable within its container, with nothing to the left or righ of the `block`.

Most elements are `block` elements by default. Here are some of the most common:

- `section`, `article`, `aside`, `header`, `footer`

- `p`

- `h1` through `h6`

- `blockquote`

- `ul`, `ol`, `dl`

- `figure` and `figcaption`

- `form` and `fieldset`

You can convert any element to a `block` element with the `display: block` CSS property. It's common to render links (`<a>`) and images as block elements.

**Inline Elements**

Inline elements provide a small bit of semantic meaning to content; browsers use this to alter the way they display small sections of text, which, in turn, helps the reader spot specific items with ease.

The following elements are `inline` by default:

- `span`

- `b`, `i`, `u`, `strong`, `em`

- `a`

- `sub` and `sup`

- `img`

`inline` elements handle the dimension properties (`width`, `height`, `padding`, `border`, and `margin`) differently from the way `block` elements treat them. Browsers handle *left* and *right* margins and padding for `inline` elements in the same way as for block elements, but they process other box model properties differently.

For `inline` elements, browsers:

- *ignore* the `width` and `height` properties (except with the `img` and `input` elements), but instead use values computed from the element content.

- *ignore* top and bottom margins

- *don't ignore* borders, but the results may look odd

- *don't ignore* top and bottom padding, but you won't notice this unless you have a border or background

You can convert any element to an `inline` element with the `display: inline` CSS property. The most common reason to do so is to override a previous declaration.

The left and right margins, borders and padding of inline elements affect the flow, but top and bottom do not.

## Inline-Block Elements

The `inline-block` visual display model is a *legacy* model, though in practice it is not going away any time soon. The equivalent display mode in the newer CSS Display Model Level 3 multi-keyword syntax (where you have an outer and inner value) is `inline flow-root`. It will probably be several years before `inline flow-root` and the other new display models gain traction.

`inline-block` elements are like `block` elements except for one significant detail: `inline-block` elements do not take up an entire row when the `width` property is less than the available width. Instead, they flow in the same way that text and `inline` elements flow from one line to the next, which lets you place `inline-block` elements side by side with other `inline` or `inline-block` elements.

`inline-block` elements also differ from `inline` elements in that `inline-block` elements observe the `width` and `height` properties. The padding, borders, and margins all work like they do with `block` elements.

Browsers perfom vertical alignment for adjacent `inline-block` elements as well as ordinary `inline` elements.

It is worth noting that `<img>` elements are **not** `inline-block` elements but actually fully `inline` by default.

Any element can be converted to `inline-block` by the CSS property `display: inline-block`

## Nesting Elements and the Visual Display Model

HTML lets you nest elements inside other elements; it's built-in to the syntax of the language. However, such nesting is not uncontrolled. For instance, you can't nest `block` and `inline-block` elements within an `inline` element. Thus, you can put `em` (inline) inside a `blockquote` (block), but you can't put a `blockquote` inside an `em`.

There is one exception to this rule &mdash; you can nest `block` and `inline-block` elements inside an `a` tag provided the block does not include interactive elements like `input`, `button`, `select`, `textarea`, or another `a` tag. In practice, you will probably not use this feature.

## Other Visual Display Models

There are around two dozen visual display models. Some show up in routine development. For instance, list items default to a `list-item` display model, while table cells have a `table-cell` display model.

Two newer `display` properties have seen widespread growth in recent years: `flex` and `grid`. These properties solve a lot of design problems that plague front-end developers. `flex` is available for over 99% of browsers, while `grid` lags a bit at 96%.

Worth noting again that a new two-word syntax has been introduced for visual display models with an `inner` and `outer` conceptual model.

# 2:4 Box Sizing

* The usabvle `box-sizing` property values are `content-box` and `border-box`. The CSS standard deprecates the `padding-box` setting; **don't use it**.

* The `content-box` setting is the default setting for the `box-sizing` property for all elements in all modern browsers. In this model, the `width` and `height` properties specify the size of the actual content area. You need to add padding and borders to get the size of the visible box.

* The `border-box` setting causes the browser to interpret the `width` and `height` properties as the total width and height of the visible box excluding the margins. That is, the `width` and `height` include the content area as well as the padding and borders.

* The `border-box` setting is "best" since it simplifies the math a front-end developer must do. For example, if we have a box with a `width` of `50%` and a padding of `12px`, `border-box` ensures that it's precisely 50% of the container width, not 50% plus 24 pixels.

* If you want to use `border-box` pretty much everywhere you can add the following to your CSS:

```css
html {
    box-sizing: border-box;
}


*, *::before, *::after {
    box-sizing: inherit;
}
```



# 2:6 Padding and Margins

Padding lies inside the border, while margins lie outside it. Margins are typically transparent, while the padding is usually opaque.

Padding is part of the visible and *clickable* bounds of an element, while a margin is spacing between adjacent elements. The border, padding, and content area are all clickable, but not the margin.

The browser doesn't use the top and bottom margins and padding for `inline` elements for spacing. No matter how big the top and bottom margins are on an `inline` element, they do not affect the placement of the element's content nor the content surrounding it. However, the size of the top and bottom padding and border still affect the clickable and visible area of the element, though they will not displace the surrounding content.

## Margin Collapse

An even bigger differenced between margins and padding is that top and bottom margins "collapse" between `block` elements. If you position two adjacent `block`s one above the other, the margin betweeen them isn't the sum of the bottom margin of the first and the top margin of the second. Instead, the margin collapses to the larger of the two margins in question.

Margin collapse only affects top and bottom margins; left and right margins do not collapse. Padding does not collapse.



A useful strategy is to use margins for spacing between elements, and padding to affect the visible or clickable area of one.

Within a container, developers typically use the container element's padding to separate the contained elements from the container's border *horizontally*, and then the contained elements' margins to separate the contained elements *vertically* from both the edges of the container and each other.

Another technique is to use margins everywhere except where you definitely need padding. You probably need to use padding when:

* You want to change the height or width of a border.

* You want to adjust how much background is visible around an element.

* You want to alter the amount of clickable area.

* You want to avoid margin collapse.

* You want some horizontal spacing to the left or right of an `inline` element.

* As before, use the container's padding to separate the left and right sides of a container's border from its content. Use margins for the veritcal gap(s) between elements and between elements and the border of the container.



# 2:7 Dimensions #

Some CSS properties require lengths as property values to provide the size of some detail on the page, e.g. `width` `height`, `margin`, `padding`, `border`, or `font-size`.

These properties can take values such as `12px`, `3rem`, or `50%`; we call these values **measurements** or **dimensions**. We also call `px`, `rem`, `%`, etc. **measurement units** or **units**.



## Absolute Units ##

CSS has one absolute unit of significance: the **pixel**. However, the meaning of this term in CSS is more complex a physical pixel on a given display.

Since pixels vary in size from high-resolution to low-resolution displays, and this isn't much of a basis for an absolute unit, CSS distinguishes between a **physical pixel** (also called a **device pixel** or a **display pixel**) and what is known as a **CSS reference pixel** (also called a **CSS pixel** or **reference pixel**).

The size of a CSS reference pixel is the size of a pixel on a display that has 96 pixels per inch. However, if you are working on a high-resolution display, you might have, say, 192 pixels per inch.

To account for this, CSS would use a total of four physical pixels on that high-resolution display for each CSS pixel. Remember that pixels are 2-dimensional, so we need four high-resolution pixels to equal one low-resolution pixel. Without this trick, images that look okay on a low-resolution screen appear much smaller when viewed on a high-resolution display of the same physical size. Browsers use CSS pixels so the image seems to be about the same size on both low- and high- resolution screens.

Even so, this isn't a complete solution to the problem of absolute pixel units. If you place a 27-inch desktop display and a 5-inch phone side by side and view the same 200-pixel by 200-pixel images on both devices, the images will not appear to be the same size.

To account for this, CSS defines the reference pixel based on the **angular diameter** of the CSS pixel **as viewed from the typical viewing distance (TVD) for the display**. The TVD for a phone (around 14 inches) is less than the TVD for a 27-inch desktop display (about 33 inches), so if we place both screens at the appropriate TVD, that 200x200 pixel image appears to be the same size (or close to it, anyway).

In the end, this means that CSS pixels are as close to an absolute unit as you can get with CSS, provided you take the TVD into account.

> The difference between CSS reference pixels and physical pixels can pose a problem when using a design document to build a web page. If you have a high-resolution screen (like Apple's Retina displays) and view an image in Photoshop at 100% of its size, then look at it in your browser, the Photoshop version may appear smaller. If you're aware of this, you can account for the difference.

Other absolute units in CSS (unless the target is print rather than screen) are tied to the CSS reference pixel, such that one CSS inch is equivalent to 96 CSS pixels. Developers rarely use absolute units other than the pixel.

## Relative Units ##

CSS provides a handful of relative units of interest: the **em**, the **rem**, and percentages. There are others that we do not need to know yet.

### Ems and Rems ##

Ems and rems are proportional to the **calculated** and **root** font sizes, respectively. 

The calculated font size is the height of the current font in pixels. If we are using `em` to set the `font-size` property, the `em` is relative to the font-size of the parent container; if we are using `em` to set any other property, the calculated size is the actual element's `font-size`.

The root font size is the height of the base font for the document: the font size designated for the `html` element.

The value in front of `em` or `rem` acts as a coefficient of the font size. So, if the calculated font size is 20 pixels and the root font size is 16 pixels, then `1.5em` is `30px` (1.5 * 20), while `1.5rem` is `24px` (1.5 * 16).

> In most cases you should use pixels to specify the root font size. Some developers use ems or rems to give the user some control over the font, but this can result in odd behavior as your precisely positioned items start to overflow, overlap each other, or rearrange themselves on the page.
> Bugs in some older browsers make it a good idea to set the root font size in both the `html` and `body` elements. Always use pixels when you do so.

You may find it easier to work with rems instead of ems since rems are consistent. Once you've set the root font size for a document, `1.5rem` means the same thing everywhere in that document. This relationship isn't true for ems; they compound.

This compounding makes ems hard to use and maintain. Some older browsers, though, don't recognize rems; if you must support such browsers, use a **fallback** unit:

```css
p {
	font-size: 20px; font-size: 1.25rem;
}
```
This CSS tells the browser to use `1.25rem` as the font size. If the browser doesn't recognize rems, it falls back to `20px`. Placing both values on the same line makes the presence of a fallback easier to see, but it is not required.

> If you must use fallbacks, assuming a `16px` default font-size is your best bet, and then you need to calculate scaling from that default.

### Percentages ###

Technically, CSS doesn't consider percentages as length values, but this distinction doesn't matter much at this stage.

You can use percentages to define dimensions as a fraction of the container's width or height. If you place a `block` or `inline-block` element in a container and set it to `width: 50%`, the element's width is 50% of the width of the container. Likewise, if you need a height of one-quarter of the container's height, use `height: 25%`.

Remember: `width` and `height` have no effect on `inline` elements.

### Auto ###

The `auto` specifier also isn't a length value, but you can use it when you want to let the browser determine a width or height for you.

The specific role of `auto` depends on where you use it, but its most common uses are:
* As a `width` or `height`, it tells the browser to fit the entire element (including its margins) in its container.
* As a left or right `margin` value on a block element, it tells the browser to push the element all the way right or left (note the reversal!) inside its container. You can center a block element by setting both left and right margins to `auto`.
* As a top or bottom `margin` value, `auto` is equivalent to `0`.

Often, using `auto` with `width` or `height` is not necessary. By default, simply not specifying a `width` or `height` is the equivalent of setting them to `auto`. However, there are some situations where the `auto` value is needed. For instance, if there's another selector that sets the `width` or `height` to some other value, there's a chance that the CSS cascade will cause that value to be used unexpectedly. For this reason, specifying `auto` for `width` or `height` is a good idea (but check your team's coding standards first).

Standard CSS style omits the units when providing a length of 0 units.

## Mixing Units ##

You can freely mix units anywhere you want on a page; you can use pixels for some elements, rems for others, percentages, and `auto`, even within a single property's values.

E.g.
```css
	padding: 0.5em 10vw 0.5in 18pt;
```

However, mixing and matching units can leead to problems when you need to determine the "right" length to make something come out correct. It can make it impossible to set a value that works perfectly across all device sizes and browsers because fixed units don't scale while relative units do. This mismatch can cause layout elements to overflow, or not align as expected to do.

Trying to decide which dimensional units you should use is sometimes difficult. Here are some general guidelines -- none of these are absolute, and you will almost certainly find developers that disagree:

* Use absolute units sparingly, and stick with pixels. Pixels work well for:
	* the root font size
	* image widths and heights
	* top and bottom margins and padding, sometimes useful with left and right margins and padding
	* width or height of fixed-width/fixed-height containers such as navigation sidebars
	* border widths
	
* Use relative units liberally:
	* Use rems for fonts, possibly with a fallback to ems or pixels. The root font should use pixels.
	* If you must use ems instead of rems, try to avoid compounding font sizes.
	* Use rems, ems, or pixels for left and right margins and padding.
	* Use % for measurements that are proportional to the container element's width or height. Percentages work best for container dimensions and come in handy when you want certain areas of the page to grow and shrink as the width of the browser window changes.
	* Use `auto` with `width` and `height` to let the browser calculate an appropriate value.
	* Use `auto` with left and right margins to left-, center-, or right-justify a block elementg within its container.
	
You can ignore or break any of these rules when appropriate. We violate them often in this course.
