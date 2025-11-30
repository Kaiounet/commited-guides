# Images and Figures

## Inserting Images

### Basic Image

```typst
#image("path/to/image.png")
```

### Image with Width

```typst
#image("logo.png", width: 50%)
#image("screenshot.jpg", width: 150mm)
```

### Centered Image

```typst
#align(center)[
  #image("diagram.png", width: 80%)
]
```

## Figure with Caption

```typst
#figure(
  image("screenshot.png", width: 100%),
  caption: [This is a screenshot of the login page],
)
```

## Numbered Figures

Enable figure numbering:

```typst
#set figure(numbering: "1")

#figure(
  image("diagram.png", width: 80%),
  caption: [Architecture diagram showing system components],
)

// Later in document
In @fig1, we can see the architecture.
```

## Figure Placement

```typst
#figure(
  image("chart.png", width: 100%),
  caption: [Performance metrics over time],
  kind: "figure",
  supplement: [Figure],
)
```

## Side-by-Side Images

```typst
#grid(
  columns: (1fr, 1fr),
  gutter: 10pt,
  image("before.png"),
  image("after.png"),
)
```

## Image with Borders

```typst
#box(
  stroke: 1pt + black,
  [#image("photo.jpg", width: 100%)]
)
```

## Table of Figures

```typst
#outline(title: [List of Figures], target: figure.where(kind: "figure"))
```

## Image File Paths

```typst
// Same directory as .typ file
#image("image.png")

// Subdirectory
#image("images/screenshot.png")

// Parent directory
#image("../shared/logo.png")

// Full path (use relative when possible)
#image("/absolute/path/to/image.png")
```

## Supported Formats

- PNG (recommended)
- JPG/JPEG
- SVG (vector graphics)
- GIF (first frame)

## Tips

- Use `width: 80%` for full-bleed figures
- Use `width: 150mm` or `width: 3in` for specific sizes
- Keep images in a dedicated `images/` folder
- Use high-quality images (at least 72 DPI)
- PNG for charts/diagrams, JPG for photos
- SVG for scalable graphics (logos, diagrams)

## Example Document

```typst
#set figure(numbering: "1")

= Project Report

== Architecture

#figure(
  image("architecture.svg", width: 100%),
  caption: [System architecture overview],
)

== Screenshots

#figure(
  image("screenshots/dashboard.png", width: 100%),
  caption: [Dashboard interface],
)

As shown in @<fig>, the dashboard displays...
```
