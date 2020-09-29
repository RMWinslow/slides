# Slideshows using Remark

To make a new html5 slidedeck:

* Write a new slidedeck in markdown using `---` to seperate slides.
* copy the remark_template.html file and 
    * edit the external markdown link to point towards the slides you just made
    * give it a nice title.

Then on the website, 
you'll have a jekyll-rendered "blog" version of the slides, with the url being derived from the markdown source
and a html file which contains the remark-rendered slides.



I'm doing it this way because trying to use the jekyll template for remark.js failed to properly render the 

---

as a new slide.
Instead it was just a horizontal rule.

Github's parser makes `\(\)` and `\[\]` finicky:

Double dollar notation for display mode `$$x^2_i  \times \beta $$`: 
$$x^2_i \times \beta $$

Slash bracket display mode `\[x^2_i + u_u  \times \beta \]`: 
\[x^2_i + u_u  \times \beta \]

Slash bracket display mode `\\[x^2_i + u_u \times \beta \\]`: 
\\[x^2_i + u_u  \times \beta \\]


Inline latext how you doin? `\(x^3\)` \(x^2\)    ; `\\(x^4\\)` \\(x^4\\)   ;  `$x^5$` $x^6$
