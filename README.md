# Slideshows using Remark

To make a new html slidedeck:

* Write a new slidedeck in markdown using `---` to seperate slides.
* Give it the attribute `layout: presentation` in the yaml header

Then github pages should properly render the slides pages, and the JTD theme should index the slides and enable search.


## Issues

[The markdown parser for Remark tries to render markdown within a latex equation](https://github.com/gnab/remark/issues/336).

This means that if a latex equation has multiple `_`s, 
one of the following workarounds must be used:

- Escape each underscore by replacing each `_` with `\_`
- Wrap the equation in an html element so the markdown parser ignores it.

