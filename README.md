# About
This repo contains the source I use to automatically generate
my curriculum vitae as a [PDF](/build/cv.pdf) from YAML and BibTeX input.

+ [generate.py](generate.py) reads from [cv.yaml](cv.yaml) and
[publications](publications) and outputs LaTeX and Markdown
by using Jinja templates.
+ The publications are rendered from a single
  [BibTeX](publications/all.bib) file.
+ The [YAML source](cv.yaml) links to all author websites,
  which will automatically be added to the
  publication lists the PDF.

This originated from [here](https://github.com/bamos/cv).
I heavily modified it to work with the [moderncv](https://ctan.org/pkg/moderncv?lang=en) LaTeX class.
The underlying template files use standard functionality from `moderncv` such that you can switch between styles.

As of yet, I have **not** modified the template files for the markdown generator as in [here](https://github.com/bamos/cv).
So the current changes are only reflected in the .tex files (and consequent PDF file).
More work is needed if you intend to use this to generate a website as well. 

I use a modified `classic` style, which looks something like this:
![Alt text](/build/preview.png?raw=true)

# Building and running
This requires a Python 3 installation,
and the hashbang of `generate.py` assumes an executable named
`python3` is available on the path.
Dependencies are included in `requirements.txt` and can be installed
using `pip` with `pip3 install -r requirements.txt`.
On Mac or Linux, `make` will call [generate.py](generate.py) and
build the LaTeX documents with `latexmk` and `biber`.

The Makefile will also:

1. Stage to my website with `make stage`,
2. Start a local jekyll server of my website with updated
  documents with `make jekyll`, and
3. Push updated documents to my website with `make push`.

# What to modify
Change the content in `cv.yaml`.
You should also look through the template files to make sure there isn't any
special-case code that needs to be modified.
The `Makefile` can also start a Jekyll server and push the
new documents to another repository.
To use the Jekyll integration,
review the `BLOG_DIR` variable and the `jekyll` and `push` targets.

## Warnings
1. Strings in `cv.yaml` should be LaTeX (though, the actual LaTeX formatting
   should be in the left in the templates as much as possible).
2. If you do include any new LaTeX commands, make sure that one of the
   `REPLACEMENTS` in `generate.py` converts them properly.
3. The LaTeX templates use modified Jinja delimiters to avoid overlaps with
   normal LaTeX. See `generate.py` for details.

# Licensing
This work is distributed under the MIT license (`LICENSE.mit`)
with significant portions copyright [Brandon Amos](https://github.com/bamos/cv) and 
Ellis Michael from
[emichael/resume](https://github.com/emichael/resume).
Amos' and Ellis' portions are also distributed under the MIT license and this version includes template restructuring.
