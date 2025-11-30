# Typst Basics

## What is Typst?

Typst is a modern markup language for creating professional documents (like LaTeX but simpler). It's great for reports, documentation, and academic papers.

## Installation

### Using Online Editor
- Go to https://typst.app
- No installation needed, works in browser

### Local Installation
```bash
brew install typst          # macOS
sudo apt install typst      # Linux
choco install typst         # Windows
```

## Your First Document

Create a file `document.typ`:

```typst
= My Document

Hello, world!

== Section

This is a paragraph.
This is another paragraph.
```

Compile to PDF:
```bash
typst compile document.typ
```

## Basic Syntax

### Headings
```typst
= Level 1 Heading
== Level 2 Heading
=== Level 3 Heading
```

### Text Formatting
```typst
*bold text*
_italic text_
`code`
#link("https://example.com")[Click here]
```

### Lists
```typst
- Item 1
- Item 2
  - Nested item
  
+ Ordered item 1
+ Ordered item 2
```

### Comments
```typst
// This is a comment
/* Multi-line
   comment */
```

## Document Metadata

```typst
#set document(
  title: "My Project Report",
  author: "Your Name",
)

#set page(margin: 2cm)
#set text(font: "New Computer Modern", size: 11pt)
```

## Output

After compiling, you get a PDF file with the same name:
```bash
typst compile document.typ
# Creates document.pdf
```

## Quick Commands

```bash
typst compile file.typ         # Compile to PDF
typst compile file.typ out/    # Output to directory
typst watch file.typ           # Auto-compile on changes
```

## Next Steps

- See `02-formatting.md` for text styling
- See `03-tables.md` for creating tables
- See `04-code-blocks.md` for displaying code
- See `05-images-figures.md` for images and figures
