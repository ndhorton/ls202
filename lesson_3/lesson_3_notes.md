# 3:1 Images Introduction #

Image types:
* Understand the primary differences between `jpg`, `png`, and `gif` images.
* Explain when to use which image type.

HTML and CSS for images:
* Add foreground and background images to a web page.
* Use figures and captions.
* Use images as links.

# 3:2 Image Types #

The three types of images you'll see most often are **jpg**, **png**, and **gif**.

## JPG ##

The jpg format is the most common image format for images used in web documents.

Jpgs provide an exceptional balance of image quality and compression. Jpgs use a **lossy** form of compression; they lose information in exchange for a file size reduction. In some cases, you can compress and image down to 10% of its original size or less. However, lossiness sacrifices quality in return for compression.

If you edit a jpg, the resulting file has less detail than the original. If you update the file again, the result loses more detail. If you repeat this process often enough, you can end up with an image that you no longer recognize. Even if you never edit a jpg file, you can see some **JPEG artifacts** on close examination. However, most people don't notice these on well-handled jpgs, so they work well with most photographs.

You can set the amount of compression and associated lossiness when you save a jpg file. Low lossiness levels lead to better image quality but larger files; likewise, high lossiness yields lower image quality but smaller files. As a rule of thumb, you shouold aim to reduce the size of the jpg as much as possible without losing noticeable detail or introducing visible artifacts, which requires experimentation for every image.

## PNG ##

In general, jpgs don't work well as CSS background images. Photographs are too intricate visually for use as a background, and most suitable non-photographic graphics show visible results of compression even at the highest quality. Thus, the png format is often the best choiced for backgrounds and non-photographic images.

Like jpgs, pngs use compression to reduce the size of the file, but png compression is non-lossy. However, the lack of lossiness means larger file sizes --- considerably larger in some cases.

Pngs also provide both single-color and alpha transparency, which lets you see the background behind an image while still viewing the image's main subject. Single-color transparency allows part of an image to be entirely clear by reserving a single color --- any pixel that matches that color in the png reveals the content (typically a background color) behind the image. Alpha transparency adds an alpha channel to images, which allows up to 65,536 different levels of transparency tinted by color.

Pngs are ideal for images that need all their detail, transparency, or that must support more than 16.7 million colors.

## GIF ##

Gifs are suitable for small images used as user interface icons in an application. They hae a limited color range (256 colors), but this allows for minuscule file sizes, which makes them perfect for images where size, detail, and a broad color palette aren't significant.


# 3:3 Adding Images to Web Pages #

## `<img>` ##

`<img>` is a self-closing tag that tells the browser to load and display a foreground image from a separate resource. It has four attributes of particular interest.

### `src` ###

The `src` attribute is required. It tells the browser where to find the image. It uses the same URL format as links in the `<a>` tag and can be relative, root-relative, or absolute.

### `alt` ###

The `alt` attribute is optional, but you should almost always use it. It describes the content of the image as an aid for users who cannot see it or that have images disabled. If you have a picture of Da Vinci's smarter sister, Lucrezia, you should say so in the `alt` attribute value. Most browsers display the alt text when an image is unavailable or when images have been disabled.

Screen readers, specialized browsers that read web pages aloud for people with vision problems, use the `alt` attribute to tell the user about image content. Without `alt`, the user has no idea what the image shows. They may not even know it is present: some reader software treats images with no `alt` text as non-essential, so they skip over them while reading the screen.

Search engines use `alt` to index images, which makes it relevant for search engine optimization (SEO).

If you omit the `alt` attribute, your browser can still render the image. Existing standards require the `alt` attribute *in most cases* to provide text that the browser can display when the image is unavailable. Your HTML won't validate on the W3C validator unless you use the `alt` attribute. If your image isn't significant enough to require an `alt` attribute, you can specify an empty value with `alt=""`. (There are some specific exceptions to this rule, but you should ignore them for this course.)

### `width` and `height` ###

The `width` and `height` attributes are also optional. They provide the width and height of the image in pixels. The CSS `width` and `height` properties override the HTML attributes in the rendered version of the page.

If you plan to almost always display images with a specific width and height, then you should use the attributes to specify those values. That lets your browser optimize the rendering speed by allocating room for your image before it finishes downloading.

In many cases, however, you won't know the specific width and height in advance, especially if the image's size is dependent on the output device. For instance, mobile devices often render images at a smaller size than in a desktop browser. In such cases, providing the `height` and `width` attributes may lead to worse overall performance. Instead, use the `height` and `width` CSS properties exclusively.

## Figure and Figcaption ##

The `figure` element is a semantic HTML element; it designates an item as a representation of information discussed in the content. The tag customarily encloses some media, such as an image, video, or audio file, that illustrates the surrounding content. You can also supply a caption with the optional `<figcaption>` tag, short for "figure caption".

You should only use `figure` and `figcaption` with images that reference the surrounding content or vice versa, or that need a caption; otherwise a `figure` element is not needed. For instance, logos, fancy bullets, background images, and the like are decoration, not content.

## Images as Links ##

 You can use any non-interactive HTML element as a link, including images. (The non-interactive requirement means e.g. form controls cannot be wrapped in an `a` tag.)
 
 To make an image clickable and have it link to another page, place the `img` tag inside an `a` tag.
 
If we want to make an image clickable so that the browser will display the image in a page by itself when clicked on, we can set the `href` of the `a` element to the same value as the `src` of the `img` element.

## Background Images ##

You can also add background images to a page or element by applying the CSS `background` or `background-image` property. Background images appear behind the content for the element that requested the background and its descendents.

Most background images apply to an entire page, so in this situation we can use the `body` selector specify them. However, you can apply backgrounds to any selector, such as a tag, class, or id selector.

There are several other background properties you can provide with a background image, including the size of the image, the positioning, and repeat counts.

# 3:6 Summary #

We discussed the three main types of images found on the Web (jpg, png, and gif).

We learned how to use images as foreground images and background images, and we saw how CSS interacts with them. We also learned a crucial lesson; nearly anything can be a link on a Web page.

Topics for further research:
* The technical aspects of images: color depth, images size, compression, etc.
* Background images: positioning and sizing, gradients

Start with MDN. There are also links in the second pinned conversation in the Lesson 2 Forum section.

# Mind The Gap forum post #

The following HTML displays a picture against a yellow background. The background annoyingly extends just below the image. To get rid, uncomment any single line in the CSS code for `figure` or `image`. N.B. adjusting the `font-size` property seems to affect the margin slightly, while adjusting `line-height` doesn't.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Mind the Gap</title>
    <meta charset="utf-8">
    <style>
      
      /* n.b. font-size affects the margin
        slightly, line-height doesn't.
        It may be line-height is harder
        to reset in the child elements, idk */

      figure {
        background-color: yellow;
        /* line-height: 0; */
        /* font-size: 0; */
      }

      img {
        /* vertical-align: bottom; */
        /* vertical-align: top; */
        /* vertical-align: middle; */
        
        /* display: block; */
        /* display: flex; */
        /* display: grid; */

      }

    </style>
  </head>
  <body>
    <figure>
      <img src="cats.jpg" alt="two fluffy cats">
    </figure>
  </body>
</html>
```




When we have a background color in a container that contains an image, the default behavior causes a sliver of the background color to appear below the picture. This happens because `img` is an `inline` element and inline elements are generally expected to contain text. Fonts are displayed along a **baseline**, somewhat like the lines on lined writing paper. The baseline is not at the lowest point at which text appears. Rather, it allows for a descender space beneath which is contained the descent of a letter like 'p' or 'q'. This is why a gap appears beneath an image --- the bottom of the image lines up with the baseline and the baseline is not quite the bottom of the space allotted for inline elements. In the case of an image, of course, the space is quite useless.

This explains why the solutions involving reducing the `font-size` or `line-height` to `0` work: the descender space is also reduced to zero.

Of course, you have to be careful about text size in the child and descendent elements of the container if you use this solution, since they will inherit the zero value. Children in particular cannot use `em` for `font-size` in this situation since regardless of the value given, the value will be multiplying zero.

The reason the `vertical-align` solutions work is that the `inline` element is designed for text, and, when we have some text after the image within the same container, we can see that the image is equivalent to a single line of text with the following text being aligned along the baseline with the descending characters descending below it. If we vertically align the inline `img` element, the following text is shifted. When the value is `bottom`, the text is realigned upward slightly so that the descending characters descend only as far as the baseline, so there is no need to have the background descend below it. And the other values for `vertical-align` move the text even higher.

The `display` solutions work because, of course, the `img` element ceases to be `inline`.

The exact proportion of the line space given over to the descending space is dependent on the specific font in use for the inline element.


# Articles linked in second forum post #


## Understanding the Most Popular Image File Types and Formats ##

The five most popular web and computer graphics image formats:

* JPEG
* GIF
* BMP
* TIFF
* PNG

### JPEG ###

JPEG stands for Joint Photographic Experts Group and is the most popular image format used for the web. It is a lossy compression format. Since 1994, JPEG has taken over from GIF as the most popular format, since it is better for providing decent-looking photographs in a small file size.

Pros:
* 24-bit color, with up to 16 million colors
* Rich colors, great for photographs that need fine attention to color detail
* Most used and most widely accepted image format
* Compatible in most OS (Mac, Windows, Linux)
Cons:
* Tends to discard a lot of data
* After compression, JPEG tends to leave artifacts
* Cannot be animated
* Does not support transparency

### GIF ###

GIF, short for Graphics Interchange Format, is limited to the 8 bit palette with only 256 colors. GIF is still a popular image format on the internet because image size is relatively small compared to other image compression types.

GIF compresses images in two ways: first, by reducing the number of colors in rich color images, thus reducing the number of bits per pixel. Second, GIF replaces multiple occurring patterns (large patterns) into one. So instead of storing five kinds of blue, it stores only one blue.

GIF is most suitable for graphics, diagrams, cartoos and logos with relatively few colors. GIF is still the chosen format for animation effects.

Compared to JPEG, it is lossless for images with 256 colors and below, but may leave color-dithering artifacts in rich color images and is poor when representing detailed pictures. For a full-color image it may lose up to 99.998% of its colors.

One edge of the GIF image format is the interlacing feature, giving the illusion of fast loading graphics. When it loads in a browser, the GIF first appears to be blurry and fuzzy, but as soon as more data is downloaded, the image becomes more defined until all the data has been downloaded.

Pros:
* Can support transparency
* Can do small animation effects
* 'Lossless' quality for images of 256 colors or fewer
* Great for images with limited colors, or with flat regions of color

Cons:
* Only supports 256 colors
* Oldest format in the web and has never been updated
* Sometimes, the file size is larger than PNG

### BMP ###

The Windows Bitmap or BMP files are image files within the Microsoft Windows operating system. In fact, it was at one point one of the few image formats.

These files are large and uncompressed, but the images are rich in color, high in quality, simple and compatible in all Windows OS and programs. BMP files are also called raster or paint images.

BMP files are made of millions and millions of dots called 'pixels', with different colors and arrangements to come up with an image or pattern.

A BMP may be 8-bit, 16-bit, or 24-bit. Thus when you make a BMP image larger, you are making the individual pixels larger, and thus making the shapes look fuzzy and jagged.

BMP files are not great for the web and not very popular. Being very large, bitmap files are not web friendly, and they are not compatible with all platforms. They do not scale well.

Pros of BMP:  
* Works well with most Windows programs and OS, you can use it as a Windows wallpaper

Cons:
* Does not scale or compress well
* Again, very huge image files making it not web friendly
* No real advantage over other image formats

### TIFF ###

TIFF was created by Aldus for 'desktop publishing', and by 2009 it was transferred to the control of Adobe Systems. TIFF is popular among common users, but has gained recognition in the graphic design, publishing and photography industry. It is also popular among Apple users.

TIFF images are not compatible for all systems. However, TIFF offers crisp quality and rich colors for photographs.

The TIFF (Tage Image File Format) image format is easy to use with software that deals with page layout, publishing and photo manipulation via fax, scanning, word processing, etc. TIFF is very flexible, it can be lossy or lossless. TIFF is a rich format and supported by many imaging programs.

It is capable of recording halftone image data with different pixel intensities, thus is the perfect format for graphic storage, processing and printing. This makes TIFF the superior raster image format.

Pros of TIFF:
* Very flexible format, it supports several types of compression like JPEG, LZW, ZIP, or no compression at all.
* High quality image format, all color and data information are stored
* TIFF format can now be saved with layers

Cons:
* Very large file size, long transfer time, huge disk space consumption, and slow loading time.

### PNG ###

PNG (or Portable Network Graphics) is a recently introduced format, so not everyone is familiar with it. But PNG has been approved as a standard since 1996. It is an image format specifically designed for the web. PNG is, in all aspects, the superior version of the GIF.

Like the GIF format, the PNG *can* be saved with 256 colors maximum (PNG-8 mode), but it saves the color information more efficiently. It also supports an 8-bit transparency.

PNG was actually created with the intent to replace the GIF as an image format that doesn't require a patent license. PNG can support 24 bit RGB color images, grayscale images, both with and without alpha channels.

Pros:
* Lossless, so it does not lose quality and detail after image compression
* In a lot of ways better than GIF --- often has smaller files sizes
* Supports transparency better than GIF

Cons:  
* Not good for large images because they tend to generate a very large file, sometimes creating larger files than JPEG
* Unlike GIF, cannot be animated
* Not all web browsers can support PNG

### Which is best for what? ###

* Print Graphics: TIFF is the best and only choice for professionals when images are intended for print. Its ability to read CMYK and YcbCr color, and its high pixel intensity means it is the only serious choice for designers, photographers and publishers
* Web Graphics: PNG, JPEG and GIF are the most web friendly image formats: JPEG for files where data loss is unimportant; PNG for files where detail matters; GIF has animation.
* Logos & Line Art: JPEG is the worst choice, adding artifacts and blurring text, lines, and edges. JPEG cannot support transparency, which is often needed for logos and icons. GIF is a good choice, but PNG is better. TIFF is an option for small images like these.
* Clip Art: GIF is the best for clipart and drawn graphics that only use a few colors with precise lines and shapes.

JPEG is the most compatible between PC and Mac.

# Web.Dev Image Performance article #

## `srcset` and `sizes` attributes for `<img>` ##

The `img` element supports the `srcset` attribute, which lets you specify a list of possible image sources the browser may use. Each image source specified must include the image URL, and a width *or* pixel density descriptor.

E.g.
```html
<img
  alt="An image"
  width="500"
  height="500"
  src="/image-500.jpg"
  srcset="/image-500.jpg 1x, /image-1000.jpg 2x, /image-1500.jpg 3x"
>
```

This HTML snippet uses the pixel density descriptor to hint the browser to use `image-500.png` on devices with a Device Pixel Ratio (DPR) of 1, `image-1000.jpg` for a DPR of 2, etc.

In combination with `srcset`, we can use the `sizes` attribute to further adjust the size depending on media conditions.

E.g.
```html

<img
  alt="An image"
  with="500"
  height="500"
  src="/image-500.jpg"
  srcset="/image-500.jpg 500w, /image-1000.jpg 1000w, /image-1500.jpg 1500w"
  sizes="(min-width: 768px) 500px, 100vw"
>
```

In this snippet, the `srcset` attribute specifies a list of image candidates the browser can choose from, separated by commas. Each candidate in the list consists of the image's URL, followed by a syntax that denotes the intrinsic width of the image. An image's *intrinsic size* is its dimensions. For example, a descriptor of `1000w` denotes that the image's intrinsic width is 1000 pixels wide.

Using this information, the browser evaluates the media condition in the `sizes` attribute, and --- in this case --- is instructed that if the device's viewport width exceeds 768 pixels, the image is displayed at a width of 500 pixels. On smaller devices, the image is displayed at `100vw` -- or, the full viewport width.

The browser can then combine this information with the list of `srcset` image sources to find the optimal image. For example, if the user is on a mobile device with a screen width of 320 pixels with a DPR of 3, the closest sized image would be `image-1000.jpg` which has an intrinsic width of 1000 pixels (`1000w`).

`srcset` width descriptors (`w`) don't work without the `sizes` attribute. Similarly, if you omit the `srcset` width descriptors, the `sizes` attribute doesn't do anything.

## File Formats ##

Modern image formats like WebP and AVIF may provide better compression than PNG or JPEG, making your image file size smaller therefore taking less time to download. By serving images in modern formats, you can reduce a resource's load time, which may result in a lower Largest Contentful Paint (LCP).

WebP is a widely supported format that works on all modern browsers. WebP often has better compression than JPEG, PNG, or GIF, offering both lossy and lossless compression. WebP also supports alpha channel transparency even when using lossy compression --- a feature the JPEG codec doesn't offer.

The 'P' in WebP simply signifies its origins as a picture format. WebP was developed at Google and released in 2010.

AVIF is a newer image format, and while it isn't as widely supported as WebP, it does enjoy a reasonably decent support across browsers. AVIF supports both lossy and lossless compression, and tests have shown greater than 50% savings when compared to JPEG in some cases. AVIF also offers Wide Color Gamut (WCG) and High Dynamic Range (HDR) features.

AVIF stands for AV1 Image File Format. AVIF is open and royalty-free and can store images or image sequences compressed with AV1 in the HEIF container format. It competes with HEIC, which uses the same container format built upon ISOBMFF, but uses HEVC for compression. Version 1.0 of the AVIF spec was finalized in 2019.

Both WebP and AVIF support animation.

## The `<picture>` element ##

The `<picture>` element gives you greater flexibility in specifying multiple image candidates.

When you use `<source>` element(s) within the `<picture>` element, you can add support for, say, AVIF or WebP images, but fall back to more widely supported image formats if the browser cannot support more modern ones. With this approach, the browser picks the first `<source>` element that matches its supported image file formats. If it can render the image given in a source, it uses that image; otherwise, the browser moves on to the next specified `<source>`. So the preferred `<source>` is placed first, and the rest are given in order of preference, with reliable but aging formats placed toward the bottom.

A `<picture>` element requires an `<img>` element nested inside of it. The `alt`, `width`, and `height` attributes are defined on the `<img>` and used regardless of which `<source>` is selected.

The `<source>` element also supports the `media`, `srcset`, and `sizes` attributes. Similarly to the `<img>` example earlier, these indicate to the browser which image to select on different viewports.

