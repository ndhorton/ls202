# 1. #

image width = (`width`) 500px + (`padding`) 20px * 2 + (`margin`) (19 + 11) + (`border`) 4px * 2
    = 500 + 40 + 30 + 8 pixels
    = 578px width

image height = 300px + 10px * 2 + (20 + 10) + 4 * 2
    = 358px height

So the `div` must have a content area of at least 578x358 pixels

x incorrect

The `div` itself is `border-box` with a `1px` border, so the `div` dimensions need to be increased to account for the borders

Thus, it would need to be at least 578 + 1px * 2 by 358 + 1px * 2, or 580 by 360 pixels

# 2. #

The `div` would have to be 580 by 360 pixels. The only difference from the first question is that the `section` element is declared `block` instead of `inline-block` and this does not affect the box size in this instance.

From the answer: "The chief difference is that other elemnets may appear adjacent to the `img` in problem 1, while the `section` in this problem will always be on a line by itself within the `div` no matter its width."

# 3. #

The `em` element is declared `inline` (the same as the default). This means that the `width` and `height` properties are ignored for the `em`, and its size will depend on the text content. It is therefore difficult to give a precise answer as to how big the `div` would need to be.

We can say that we need to account for the left and right margins (`19px` and `11px` respectively), since these are actually rendered. The width and height depend on the text content. We could also leave room for the `4px` border on all sides. And we could leave room for the padding as well. The reason we include these things that the browser "ignores" is that the browser only ignores these things relative to the surrounding inline content, but if we have colored padding and borders the browser will render them over and under the surrounding text; we are interested in containing it within the `div`, though, so we need to include the padding, borders, and left and right margins. We ignore the top and bottom margins since these

# 4. #

Since the `article` is set to `box-sizing: border box`, the `width` and `height` include the padding and borders. Since the `display` is set to `inline-block`, we can simply add the `margin` values to these values and the `div`'s border value (since the `div` is also set to `border-box`).

necessary width = 500 + 19 + 11 + 2 = 532
necessary height = 300 + 20 + 10 + 2 = 332

# 5. #

2, 3, 6

# 6. #

The `article` element is block-level by default and there is no `display` property set to change this. Therefore, the `article`s will not display side by side.

To change this, we could add `display: inline-block` to the `article` selector's ruleset.

However, the `width` of each `article` is set to `50%`, and since we are using the default visual display model (`content-box`) the `10px` of `padding` and `1px` of `border` is added to this. Therefore, we would need to either adjust the `width` (or the `border` and `padding`) of the `article`, or set the `display` property of `article` to `border-box`.

# 7. #

Placing the `article` elements on different lines might add a single space of text content, but since there is no other text content in the `section` (except in the `article` children), I genuinely don't know if this will be rendered. If it is, this could displace the second `article` onto the next line, since each `article` takes up 50% of the `section` parent's available content area.

My guess is that it will not displace the second article.

x incorrect

I guessed wrong. Apparently, the significant single space caused by a line-break is often the cause of problems for `inline-block` elements. There are techniques to deal with this problem.
