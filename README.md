# crossref-adapt

A Pandoc-Lua Filter to change the internal IDs for cross-references as produced by `pandoc-crossref`.

Michael Cysouw <cysouw@mac.com>

# Rationale

[Pandoc](https:pandoc.org) is a system for converting between different markup formats. The [`pandoc-crossref`](https://github.com/lierdakil/pandoc-crossref) filter (extensions to Pandoc are called 'filter' in Pandoc-parlance) allows for easy and flexible internal cross-reference to sections, figures, tables and equations. The current `crossref-adapt` filter adds a cosmetic change to the IDs of these cross-references.

The effect of `crossref-adapt` is that the internal IDs are harmonized with the IDs as they are type-set in the final text. In this way it is possible to use these IDs to transparently refer to each individual item. For example, in the [HTML-version](https://cysouw.github.io/crossref-adapt/README.html) of this README this section is numbered as Section 2. By adding the [fragment-identifier](https://en.wikipedia.org/wiki/URI_fragment) `#sec2` to the URL a direct link to this section is made (e.g. [cysouw.github.io/crossref-adapt/README.html#sec2](https://cysouw.github.io/crossref-adapt/README.html#sec2)).

This functionality is intended for stable (scientific) publications on the open web. Instead of circuitous and cumbersome current practice of page numbering inside of PDFs, this allows for direct scientific cross-references to specific element of a scientific work, e.g. (Cysouw 2021: [#sec2.5](https://cysouw.github.io/diathesis/fulltext.html#sec2.5)). 

# Cross-referencing

Currently, the IDs as produced by this filter can be referred to as follows:

- **`#sec2`** for numbered sections
- **`#tbl2`** for numbered tables
- **`#fig3`** for numbered figures
- **`#eq4`** for numbered equations

The format is deliberately somewhat cryptic and short, but easy to type and parse. The hash is the URL-standard for fragments. The numbers are the actual numbers as produced in the final output. No punctuation is added inside these IDs to make automatic parsing easier.

The format is harmonized with the IDs for footnotes as produces natively by Pandoc, with linguistic examples as produced by the Pandoc-filter `pandoc-ling` and with paragraph numbers as added to Pandoc with the filter `count-para`:

- **`#fn3`** for [Pandoc footnotes](https://pandoc.org/MANUAL.html#footnotes)
- **`#ex7`** for examples as produced by [`pandoc-ling`](https://github.com/cysouw/pandoc-ling)
- **`#8`** for paragraph numbers as produced by [`count-para`](https://github.com/cysouw/count-para)

# Usage

As an example, this `readme` is converted into HTML with the following Pandoc command. It can be directly accessed at [cysouw.github.io/crossref-adapt](https://cysouw.github.io/crossref-adapt/readme.html).

```
pandoc README.md \
    --to html \
    --output README.html \
    --standalone \
    --number-sections \
    --filter pandoc-crossref \
    --metadata linkReferences=true \
    --metadata setLabelAttribute=true \
    --lua-filter crossref-adapt.lua \
    --metadata title="Introducing crossref-adapt"
```
