# Document Structure and Organization

## Basic Structure

```typst
#set document(
  title: "My Project Report",
  author: "Student Name",
)

= Main Title

== Section 1
Content here.

=== Subsection 1.1
More content.

== Section 2
Different content.
```

## Table of Contents

```typst
#outline()

= Section 1
Content...

== Subsection
More content...
```

## Heading Numbering

```typst
#set heading(numbering: "1.1.1")

= Chapter 1
== Section 1.1
=== Subsection 1.1.1
```

## Page Breaks

```typst
= Chapter 1

Content of chapter 1.

#pagebreak()

= Chapter 2

Content of chapter 2.
```

## Chapters/Multi-File Structure

For large documents, split into files:

**main.typ**
```typst
#set document(title: "My Report")
#include "chapters/01-intro.typ"
#include "chapters/02-methods.typ"
#include "chapters/03-results.typ"
```

**chapters/01-intro.typ**
```typst
= Introduction

This is the introduction section...
```

## Header and Footer

```typst
#set page(
  header: [My Document],
  footer: [#align(right, text(size: 9pt, [Page #counter(page).display()]))],
)
```

## Margins and Page Size

```typst
#set page(
  margin: (top: 2cm, bottom: 2cm, left: 2.5cm, right: 2.5cm),
  paper: "a4",  // or "letter", "a3", etc.
)
```

## Bibliography

**main.typ**
```typst
#bibliography("references.yml")
```

**references.yml**
```yaml
- id: smith2020
  type: article
  title: Great Research
  author: John Smith
  date: 2020-01-01
```

Use in text:
```typst
According to @smith2020, this is true.
```

## Complete Example

```typst
#set document(title: "Student Project Report", author: "Jane Doe")
#set page(margin: 2cm)
#set heading(numbering: "1.1")
#set text(font: "New Computer Modern", size: 11pt)

#align(center, text(size: 24pt, weight: "bold")[
  Student Project Report
])

#align(center)[Jane Doe | University Name | Dec 2024]

#outline()

#pagebreak()

= Introduction

This project explores...

= Methods

We used the following approach...

= Results

The results show that...

= Conclusion

In conclusion...
```

## Tips

- Use `#outline()` for automatic table of contents
- `#pagebreak()` for page breaks
- Heading levels: `=` (h1), `==` (h2), `===` (h3)
- Include files for better organization
- Numbering can be disabled: `#set heading(numbering: none)`
