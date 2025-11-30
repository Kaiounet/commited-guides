# Typst for Technical Documentation

## What is Typst?

Typst is a modern document preparation system (like LaTeX, but easier). Use it for:
- Project reports
- Architecture documentation
- API specifications
- Technical proposals
- Meeting minutes

**Why not Word/Google Docs for technical stuff?**
- Version control in Git ✅
- Code syntax highlighting ✅
- Mathematical formulas ✅
- Automatic tables of contents ✅
- Reproducible layouts ✅

## Project Structure

```
project/
├─ docs/
│  ├─ 00-main.typ          (Table of contents)
│  ├─ 01-introduction.typ
│  ├─ 02-architecture.typ
│  ├─ 03-api.typ
│  ├─ 04-database.typ
│  ├─ images/
│  │  ├─ architecture.png
│  │  ├─ database-schema.png
│  │  └─ flowchart.svg
│  ├─ code-examples/
│  │  ├─ example1.js
│  │  └─ example2.rs
│  └─ typst.toml           (Configuration)
└─ README.md               (Quick reference)
```

## Basic Structure

### Main Document (00-main.typ)
```typst
#set document(
  title: "Project Architecture & Design",
  author: "Development Team",
  date: datetime.today().display("[year]-[month]-[day]"),
)

#set page(numbering: "1")
#set text(font: "New Computer Modern")

// Customize heading styles
#show heading.where(level: 1): it => {
  text(size: 24pt, weight: "bold", it.body)
}

// Title page
#align(center)[
  #text(size: 28pt, weight: "bold")[
    Our Amazing Project
  ]
  
  Architecture & Technical Documentation
  
  #text(size: 12pt, fill: gray)[
    Version 1.0
    
    Generated: #datetime.today().display("[month]/[day]/[year]")
  ]
]

#pagebreak()

// Table of contents
#outline(depth: 2)

#pagebreak()

// Include sections
#include "01-introduction.typ"
#include "02-architecture.typ"
#include "03-api.typ"
#include "04-database.typ"
```

### Individual Sections

**01-introduction.typ**:
```typst
= Introduction

== Project Overview

This is a web application for managing student projects.

Key features:
- User authentication
- Real-time collaboration
- Version control integration
- Progress tracking

== Team

- *Alex*: Backend Lead
- *Jamie*: Frontend Lead
- *Morgan*: DevOps
- *Riley*: QA

== Timeline

/ Sprint 1: Foundation (Oct 1-15)
/ Sprint 2: Core Features (Oct 16-31)
/ Sprint 3: Polish & Deploy (Nov 1-15)
```

## Common Elements

### Headings
```typst
= Level 1 Heading (Section)
== Level 2 Heading (Subsection)
=== Level 3 Heading (Subsubsection)
```

### Text Formatting
```typst
*bold text*
_italic text_
`monospace code`
#text(color: red)[colored text]
#text(size: 14pt)[bigger text]
```

### Lists
```typst
// Unordered list
- Item 1
- Item 2
  - Nested item 2a
  - Nested item 2b

// Ordered list
+ First
+ Second
+ Third

// Description list
/ Term 1: Definition
/ Term 2: Another definition
```

### Code Blocks
```typst
```javascript
function login(email, password) {
  return fetch('/api/auth/login', {
    method: 'POST',
    body: JSON.stringify({ email, password })
  })
}
```‌
```

Or include from file:
```typst
```javascript
#include "code-examples/example1.js"
```‌
```

### Tables
```typst
#table(
  columns: (1fr, 2fr, 1fr),
  [*Endpoint*], [*Description*], [*Method*],
  
  [`/auth/login`], 
  [Authenticate user with email and password], 
  [POST],
  
  [`/auth/logout`], 
  [End user session], 
  [POST],
  
  [`/users/@{id}`], 
  [Get user profile], 
  [GET],
)
```

### Images
```typst
== Architecture Diagram

#figure(
  image("images/architecture.png", width: 100%),
  caption: [System architecture overview],
)
```

### Equations (Math)
```typst
== Algorithm Complexity

The time complexity is:

$ O(n log n) $

Where _n_ is the input size.
```

### Callouts/Highlights
```typst
#block(
  fill: rgb("#e3f2fd"),
  inset: 10pt,
  radius: 5pt,
  [
    *Important:* All endpoints require authentication headers.
  ]
)
```

## Documentation Examples

### API Documentation
```typst
= API Reference

== Authentication

=== POST /api/auth/login

Authenticate a user and receive a JWT token.

*Request:*
```json
{
  "email": "user@example.com",
  "password": "secret123"
}
```‌

*Response (200):*
```json
{
  "token": "eyJhbG...",
  "user": {
    "id": "123",
    "email": "user@example.com",
    "role": "student"
  }
}
```‌

*Errors:*
- 401: Invalid credentials
- 422: Missing required fields
```

### Architecture Document
```typst
= System Architecture

== Overview

The system follows a three-tier architecture:

#align(center)[
  #text(size: 12pt)[
    Client Layer | API Layer | Data Layer
  ]
]

== Frontend (React)

- Built with React 18
- State management: Redux
- Styling: Tailwind CSS

Key pages:
- Dashboard
- Project Management
- Team Collaboration

== Backend (Node.js)

#table(
  columns: (auto, 1fr),
  [*Service*], [*Responsibility*],
  [Auth], [User authentication & authorization],
  [Projects], [Project CRUD operations],
  [Teams], [Team management & roles],
  [Notifications], [Real-time updates],
)

== Database (PostgreSQL)

Tables:
- users
- projects
- teams
- project_members
```

## Team Documentation Workflow

### Who Maintains What
```
Architecture.typ
  ├─ 02-architecture.typ (Tech Lead)
  ├─ 03-api.typ (Backend Lead)
  └─ 04-database.typ (Database Owner)
```

### Updating Documentation

**In your PR description**, link to documentation updates:
```
## Code Changes
- Added POST /api/users endpoint

## Documentation Updated
- docs/03-api.typ: New endpoint specification
```

**When reviewing**, check:
- [ ] Docs match code changes
- [ ] Examples are correct and up-to-date
- [ ] No outdated information

### Building/Viewing

```bash
# Install Typst (if not already)
# macOS: brew install typst
# Ubuntu: sudo apt install typst

# Watch for changes and compile
typst watch docs/00-main.typ output.pdf

# One-time compile
typst compile docs/00-main.typ output.pdf

# View PDF
open output.pdf
```

### Version Control

```bash
# Commit Typst files
git add docs/**/*.typ
git commit -m "docs: update API specification"

# Usually don't commit PDFs (use CI to generate)
# Add to .gitignore:
docs/output.pdf
*.pdf
```

## Best Practices

- **Keep sections modular**: One feature per file
- **Update with code**: Change docs when code changes
- **Use version numbers**: Change when schema/API changes
- **Include examples**: Show real code from codebase
- **Diagrams > Words**: Use images for complex concepts
- **Review together**: Docs deserve code review too

## Common Mistakes

- ❌ Docs separate from code - they diverge
- ✅ Update docs in same PR as code

- ❌ Dense paragraphs - hard to scan
- ✅ Headings, bullet points, tables

- ❌ Outdated code examples
- ✅ Link or include from actual code

- ❌ Typos and grammar errors
- ✅ One person reviews for writing

## Resources

- **Typst Docs**: https://typst.app/docs/
- **Typst Gallery**: https://typst.app/gallery/
- **Official Tutorial**: https://typst.app/docs/tutorial/
- **Community**: Discord and GitHub discussions

## Checklist for Documentation

Before committing documentation:

- [ ] Spellcheck and grammar
- [ ] Code examples are current
- [ ] All images present
- [ ] Headings are clear
- [ ] Table of contents accurate
- [ ] PDF compiles without errors
- [ ] Links work (relative paths)
- [ ] Reviewed by teammate
