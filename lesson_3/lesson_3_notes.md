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