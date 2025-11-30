# Text Formatting in Typst

## Basic Text Styling

```typst
*bold text*
_italic text_
*_bold and italic_*
`inline code`
#strike[strikethrough]
```

## Sizes and Colors

### Font Size
```typst
#set text(size: 12pt)

#text(size: 14pt)[Larger text]
#text(size: 10pt)[Smaller text]
```

### Colors
```typst
#text(fill: red)[Red text]
#text(fill: rgb("#0066cc"))[Custom color]

// Common colors: red, blue, green, black, white, etc.
```

## Headings with Styling

```typst
= Main Title
#set heading(numbering: "1.1")  // Enable numbering

#heading(level: 1, numbering: "I.")[Custom heading]
```

## Text Alignment

```typst
#align(left)[Left aligned]
#align(center)[Centered text]
#align(right)[Right aligned]

// Change default alignment:
#set align(center)
```

## Quotes and Emphasis

```typst
> This is a block quote.
> It can span multiple lines.

#quote[Important citation goes here]
```

## Spacing

```typst
Space between paragraphs is automatic.

#v(1em)      // Vertical space
#h(2em)text  // Horizontal space

#linebreak() // New line
```

## Subscript and Superscript

```typst
H#sub[2]O              // H₂O
E = mc#sup[2]          // E = mc²
```

## Boxes and Highlighting

```typst
#box(fill: yellow)[Highlighted text]
#box(stroke: 1pt + black)[Bordered box]
```

## Line Breaks and Paragraphs

```typst
Line break with #linebreak()

Two returns create a new paragraph.

#parbreak() // Force paragraph break
```

## Example Document

```typst
#set text(font: "New Computer Modern", size: 11pt)
#set align(left)

= My Report

== Introduction

This is an _important_ introduction with *emphasis*.

#text(fill: blue, size: 14pt)[
  Highlighted section
]

> "Remember to cite your sources properly"

The section continues here.
```
