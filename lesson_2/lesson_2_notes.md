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
