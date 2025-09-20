# 7:1 Introduction to Design Files #

The most important part of this lesson is how to use a PSD or PNG design file as the basis for converting a design to an actual web page. PSD files require Adobe Photoshop or a strongly compatible altenative program; they give you a lot of power and flexibility in copying a design. However, you can also use PNG files with a blink **comparison**.

# 7:3 Working With Desgin Files #

## Photoshop and Design Files ##

A **design file** is a mockup of a finished web page. In practice, the design file is almost always a Photoshop document, a PSD file, which is a multi-layered image than contains layers for each part of the design: images, shapes, text, etc. You're expected to use the design file to create your image and background assets as well as obtain information regarding padding, margins, font-size, and color. Knowing your way around Photoshop well enough to extract this information will help you get work as a front-end developer.

If you plan to use Photoshop, you need to know how to:
* Use the layers palette to view the different layers in an image. You can turn layers on and off using the eyeball icon.
* Use the toolbar (the thin vertical or horizontal paletter) that provides access to most of Photoshop's tools.
* Extract assets from their layers.
* Use the Move tool to move layers around.
* Use the Marquee tool to extract and measure images and shapes.
* Export images.
* Use the Text tool to determine font characteristics.
* Use the Eyedropper tool to measure colors.

Adobe has a massive library of resources for learning to use all the different features of Photoshop. Search their site when you need information.

There are alternatives to Photoshop that can read and process PSD files, but any given program doesn't necessarily have all functionality needed to examine design files usefully. Most are not free. Some programs provide the ability to read layered PSD files, but they may lack the functionality you need to extract information from those layers.

* Photopea --- a free online alternative to Photoshop that some students recommend. The support for Launch School project files appears to be excellent. No reports of problems working on the projects in the course.
* Affinity Photo --- Serif claims that Affinity can access PSD file layers, but with some limitations. The chief lack appears to be support for "smart objects", which you may need with some design files. A 10 day trial period may be available.
* Photoshop Elements --- Adobe claims that Photoshop Elements can access PSD files, but with some limitations. It doesn't go into detail, though. A 30 day trial period may be available.
* GIMP --- As with Affinity Photo, GIMP can read PSD files with some limits, but it is also free. Note that we know that GIMP doesn't work with the Company Site project later in this lesson, but it seems to work well with the other projects provided that you use "Open as Layers" to open the files.
* Adobe Creative Assets --- This free online tool supplied by Adobe lets you look at PSD file layers, measure distances and colors, and extract resources such as images. It works somewhat differently from Photoshop and other tools, but it can be a useful alternative to purchasing Photoshop or using one of the above tools.


## PNG Design Files ##

There are several problems with using PNG files for design:
* There is no way to examine and measure fonts.
* It is hard to measure colors when the color patch is less than 5-10 pixels thick, such as line drawings and text.
* Extracting images is tedious. If it has curved, jagged, or fuzzy edges, obtaining a clean result may be almost impossible.

To use PNG design files, we need tools that:
* Open and view PNG files at the intended screen size
* Measure sizes, padding, and margins
* Measure colors

The macOS program, **Preview**, displays PNG files. Use View -> Actual Size to view the image at its actual size. Drag out rectangular marquees to measure a component. However, there is no way to measure colors.

On a Mac, Digital Color Meter (found under Applications -> Utilities) can help measure colors. Select View -> Display Values as Hexidecimal to display color values in hex, and use Display in sRGB on the drop-down list. You can use Shift-Cmd-C to copy the color under the cursor to the cut-and-paste buffer as a hex value suitable for use in your CSS.

Depending on your browser and display, you may find that text in PNG files looks blurry in your browser. This is an unfortunate side effect of the difference between physical and CSS pixels.


### Blink Comparisons ###

The lack of font measurements and the difficulty of measuring small items makes PNG files an inadequate substitute for a PSD file. Using Preview and Digital Color Meter will get you most of the way, but, sooner or later, you must perform a blink comparison.

1. Create an HTML file that does nothing more than load the PNG design file
2. Load the HTML in your browser.
3. Set the width and height of your browser as precisely as possible to match the width and height of the PNG file.
4. Create your HTML file and load it in a separate tab.
5. Toggle your browser tabs back and forth between the files (Ctrl-Tab and Shift-Ctrl-Tab work with most browsers).
6. Observe the differences between the desiign file and your file. Make corrections in your file.
7. Return to step 5 until your files match as well as possible.

# 7:7 Improving Your HTML and CSS #

There is no "one true way" to achieve a result with HTML and CSS. Much of front-end development involves interpreting the information you wish to present and identifying common styles to make your CSS as concise as possible.

Read HTML5 for Web Designers by Jeremy Keith (2010).

Read up on the `role` attribute and ARIA.

The `cursor` property can be used to change the mouse cursor to change when a user is hovering over an element. For instance, `cursor: pointer` changes the mouse cursor to the icon that shows when we hover over an anchor link. The value can be a cursor type keyword, in which case the default icon for that type will be used, but you can also choose a particular icon, with fallback images and a final mandatory keyword for a type of cursor.

