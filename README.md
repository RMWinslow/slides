# Slideshows using [Remark](https://github.com/gnab/remark)

To make a new html slidedeck:

* Write a new slidedeck in markdown using `---` to seperate slides.
* Give it the attribute `layout: presentation` or `layout: presentation_solar`  in the yaml header

Then github pages should properly render the slides pages, and the JTD theme should index the slides and enable search.


## Issues

[The markdown parser for Remark tries to render markdown within a latex equation](https://github.com/gnab/remark/issues/336).

This causes at least two problems:
- underscores must be escaped `\_` if more than one appears in an equation.
- multiline equation elements need a `\\\\` instead of a `\\` to go to a new line.

The `presentation_solar` template attempts to deal with this by replacing 
each `_` with `\_`,
and each `\\` with `\\\\\\\\` (because the escapes must be escaped too).

The upside of this fix is that the equations in the source files need not be modified.
The downside is that these replacements apply to the entire markdown source, not just equations.
As such, filenames like `food_bar.png` will be broken.

