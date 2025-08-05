# Nutrition Label #

## Fonts ##

- Franklin Gothic Heavy --- main heading
- Helvetica Black
- Helvetica
- Arial

## Challenge ##

Attempt to limit classes to 1. No IDs. Use adjacent siblings, pseudo-classes (e.g `:first-of-type`), highly specific selectors.

Be mindful of semantics; avoid `div` and `span.

## Notes ##

When duplicating the thickness of the `<hr>`, remember that
the horizontal rule gets its thickness from double the border.
So for the bottom border of a table row, we need to double the
border value, e.g. `border: 0.451rem solid black;` becomes
`border-bottom: 0.92rem solid black;`.