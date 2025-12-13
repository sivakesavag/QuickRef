# CSS Cheatsheet

> A comprehensive quick reference for CSS properties, selectors, and techniques.

## Quick Reference Summary

| Category | Topics |
|----------|--------|
| **Selectors** | Basic, combinator, attribute selectors |
| **Specificity** | Values, calculation examples |
| **Box Model** | Properties, reset, overflow |
| **Colors** | All formats (hex, rgb, hsl), opacity |
| **Typography** | Font properties, text styling, web fonts |
| **Backgrounds** | Properties, gradients, multiple backgrounds |
| **Borders** | Properties, radius, box-shadow |
| **Positioning** | Static, relative, absolute, fixed, sticky, z-index |
| **Display** | Block, inline, flex, grid, none |
| **Flexbox** | Container/item properties, common patterns |
| **CSS Grid** | Container/item properties, common patterns |
| **Responsive** | Media queries, container queries, fluid typography |
| **Transitions** | Properties, timing functions |
| **Animations** | Keyframes, properties, common animations |
| **Transforms** | 2D and 3D transforms |
| **Filters** | Filter, backdrop-filter, blend modes |
| **Variables** | Defining, using, theming |
| **Functions** | calc(), min(), max(), clamp() |
| **Pseudo-Classes** | User action, structural, form states |
| **Pseudo-Elements** | ::before, ::after, ::first-letter, etc. |
| **Units** | Absolute, relative, when to use |
| **Common Patterns** | Centering, sticky footer, truncate, aspect ratio |

---

## Table of Contents

1. [Selectors](#selectors)
2. [Specificity](#specificity)
3. [Box Model](#box-model)
4. [Colors](#colors)
5. [Typography](#typography)
6. [Backgrounds](#backgrounds)
7. [Borders](#borders)
8. [Positioning](#positioning)
9. [Display](#display)
10. [Flexbox](#flexbox)
11. [CSS Grid](#css-grid)
12. [Responsive Design](#responsive-design)
13. [Transitions](#transitions)
14. [Animations](#animations)
15. [Transforms](#transforms)
16. [Filters & Effects](#filters--effects)
17. [CSS Variables](#css-variables)
18. [Functions](#functions)
19. [Pseudo-Classes](#pseudo-classes)
20. [Pseudo-Elements](#pseudo-elements)
21. [Units](#units)
22. [Common Patterns](#common-patterns)

---

## Selectors

### Basic Selectors

| Selector | Example | Description |
|----------|---------|-------------|
| Element | `p` | All `<p>` elements |
| Class | `.intro` | All elements with `class="intro"` |
| ID | `#header` | Element with `id="header"` |
| Universal | `*` | All elements |
| Grouping | `h1, h2, h3` | All h1, h2, and h3 elements |

### Combinator Selectors

| Selector | Example | Description |
|----------|---------|-------------|
| Descendant | `div p` | All `<p>` inside `<div>` |
| Child | `div > p` | Direct `<p>` children of `<div>` |
| Adjacent sibling | `h1 + p` | First `<p>` after `<h1>` |
| General sibling | `h1 ~ p` | All `<p>` after `<h1>` |

### Attribute Selectors

| Selector | Example | Description |
|----------|---------|-------------|
| `[attr]` | `[disabled]` | Has attribute |
| `[attr=value]` | `[type="text"]` | Exact match |
| `[attr^=value]` | `[href^="https"]` | Starts with |
| `[attr$=value]` | `[href$=".pdf"]` | Ends with |
| `[attr*=value]` | `[class*="btn"]` | Contains |
| `[attr~=value]` | `[class~="active"]` | Word in list |

---

## Specificity

### Specificity Values

| Selector Type | Value | Example |
|---------------|-------|---------|
| Inline styles | 1,0,0,0 | `style="..."` |
| ID | 0,1,0,0 | `#header` |
| Class, attribute, pseudo-class | 0,0,1,0 | `.btn`, `[type]`, `:hover` |
| Element, pseudo-element | 0,0,0,1 | `div`, `::before` |
| Universal | 0,0,0,0 | `*` |

### Calculation Examples

```css
/* Specificity: 0,0,1,1 */
p.intro { }

/* Specificity: 0,1,1,1 */
#main p.intro { }

/* Specificity: 0,2,1,0 */
#nav #logo .brand { }
```

> ⚠️ `!important` overrides all specificity (avoid when possible)

---

## Box Model

### Properties

```css
.box {
  /* Content dimensions */
  width: 300px;
  height: 200px;
  min-width: 100px;
  max-width: 500px;
  min-height: 50px;
  max-height: 400px;
  
  /* Padding (inside border) */
  padding: 10px;                    /* all sides */
  padding: 10px 20px;               /* vertical | horizontal */
  padding: 10px 20px 15px;          /* top | horizontal | bottom */
  padding: 10px 20px 15px 25px;     /* top | right | bottom | left */
  
  /* Margin (outside border) */
  margin: 10px;                     /* same shorthand as padding */
  margin: 0 auto;                   /* center horizontally */
  
  /* Box sizing */
  box-sizing: content-box;          /* default: width = content only */
  box-sizing: border-box;           /* width = content + padding + border */
}
```

### Box Model Reset

```css
*, *::before, *::after {
  box-sizing: border-box;
}

* {
  margin: 0;
  padding: 0;
}
```

### Overflow

```css
.container {
  overflow: visible;   /* default */
  overflow: hidden;    /* clip content */
  overflow: scroll;    /* always show scrollbars */
  overflow: auto;      /* scrollbars when needed */
  overflow-x: scroll;  /* horizontal only */
  overflow-y: auto;    /* vertical only */
}
```

---

## Colors

### Color Formats

```css
.element {
  /* Named colors */
  color: red;
  color: cornflowerblue;
  
  /* Hexadecimal */
  color: #ff0000;        /* red */
  color: #f00;           /* shorthand */
  color: #ff000080;      /* with alpha (50%) */
  
  /* RGB / RGBA */
  color: rgb(255, 0, 0);
  color: rgba(255, 0, 0, 0.5);
  color: rgb(255 0 0 / 50%);     /* modern syntax */
  
  /* HSL / HSLA */
  color: hsl(0, 100%, 50%);      /* hue, saturation, lightness */
  color: hsla(0, 100%, 50%, 0.5);
  color: hsl(0 100% 50% / 50%);  /* modern syntax */
  
  /* Special values */
  color: transparent;
  color: currentColor;           /* inherits from color property */
  color: inherit;
}
```

### Opacity

```css
.element {
  opacity: 1;      /* fully visible */
  opacity: 0.5;    /* 50% transparent */
  opacity: 0;      /* invisible */
}
```

---

## Typography

### Font Properties

```css
.text {
  /* Font family (with fallbacks) */
  font-family: 'Helvetica Neue', Arial, sans-serif;
  font-family: Georgia, 'Times New Roman', serif;
  font-family: 'Fira Code', Consolas, monospace;
  
  /* Font size */
  font-size: 16px;
  font-size: 1rem;
  font-size: 1.2em;
  font-size: clamp(1rem, 2vw + 0.5rem, 2rem);  /* fluid */
  
  /* Font weight */
  font-weight: normal;     /* 400 */
  font-weight: bold;       /* 700 */
  font-weight: 100;        /* thin */
  font-weight: 900;        /* black */
  
  /* Font style */
  font-style: normal;
  font-style: italic;
  font-style: oblique;
  
  /* Line height */
  line-height: 1.5;        /* unitless (recommended) */
  line-height: 24px;
  line-height: 150%;
  
  /* Shorthand */
  font: italic bold 16px/1.5 Arial, sans-serif;
}
```

### Text Properties

```css
.text {
  /* Alignment */
  text-align: left;
  text-align: center;
  text-align: right;
  text-align: justify;
  
  /* Decoration */
  text-decoration: none;
  text-decoration: underline;
  text-decoration: line-through;
  text-decoration: underline wavy red;
  
  /* Transform */
  text-transform: none;
  text-transform: uppercase;
  text-transform: lowercase;
  text-transform: capitalize;
  
  /* Spacing */
  letter-spacing: 0.05em;
  word-spacing: 0.1em;
  
  /* Indentation */
  text-indent: 2em;
  
  /* Shadow */
  text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
  
  /* Overflow */
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

### Web Fonts

```css
/* Google Fonts (in HTML) */
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap" rel="stylesheet">

/* @font-face */
@font-face {
  font-family: 'CustomFont';
  src: url('font.woff2') format('woff2'),
       url('font.woff') format('woff');
  font-weight: normal;
  font-style: normal;
  font-display: swap;  /* fallback behavior */
}
```

---

## Backgrounds

### Background Properties

```css
.element {
  /* Color */
  background-color: #f0f0f0;
  
  /* Image */
  background-image: url('image.jpg');
  background-image: linear-gradient(to right, #ff0000, #0000ff);
  
  /* Position */
  background-position: center;
  background-position: top left;
  background-position: 50% 50%;
  background-position: 20px 100px;
  
  /* Size */
  background-size: cover;      /* fill, may crop */
  background-size: contain;    /* fit, may show gaps */
  background-size: 100% auto;
  background-size: 200px 100px;
  
  /* Repeat */
  background-repeat: repeat;
  background-repeat: no-repeat;
  background-repeat: repeat-x;
  background-repeat: repeat-y;
  
  /* Attachment */
  background-attachment: scroll;  /* default */
  background-attachment: fixed;   /* parallax effect */
  background-attachment: local;
  
  /* Shorthand */
  background: #f0f0f0 url('img.jpg') center/cover no-repeat fixed;
}
```

### Gradients

```css
.element {
  /* Linear gradient */
  background: linear-gradient(to right, red, blue);
  background: linear-gradient(45deg, red, yellow, green);
  background: linear-gradient(to bottom, red 0%, blue 50%, green 100%);
  
  /* Radial gradient */
  background: radial-gradient(circle, red, blue);
  background: radial-gradient(ellipse at top left, red, blue);
  
  /* Conic gradient */
  background: conic-gradient(red, yellow, green, blue, red);
  background: conic-gradient(from 90deg, red 0deg, blue 180deg, red 360deg);
  
  /* Multiple backgrounds */
  background: 
    linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
    url('image.jpg') center/cover;
}
```

---

## Borders

### Border Properties

```css
.element {
  /* Full border */
  border: 1px solid #333;
  
  /* Individual properties */
  border-width: 1px;
  border-style: solid;     /* solid, dashed, dotted, double, none */
  border-color: #333;
  
  /* Individual sides */
  border-top: 2px solid red;
  border-right: 1px dashed blue;
  border-bottom: 3px double green;
  border-left: none;
  
  /* Border radius */
  border-radius: 8px;                    /* all corners */
  border-radius: 8px 16px;               /* top-left/bottom-right | top-right/bottom-left */
  border-radius: 8px 16px 24px 32px;     /* clockwise from top-left */
  border-radius: 50%;                    /* circle */
  border-radius: 9999px;                 /* pill shape */
  
  /* Individual corners */
  border-top-left-radius: 8px;
  border-top-right-radius: 16px;
  
  /* Outline (doesn't affect layout) */
  outline: 2px solid blue;
  outline-offset: 4px;
}
```

### Box Shadow

```css
.element {
  /* box-shadow: offset-x offset-y blur spread color */
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1), 0 8px 16px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.2);  /* inner shadow */
  box-shadow: none;
}
```

---

## Positioning

### Position Property

```css
.element {
  /* Static (default) - normal document flow */
  position: static;
  
  /* Relative - offset from normal position */
  position: relative;
  top: 10px;
  left: 20px;
  
  /* Absolute - removed from flow, relative to positioned ancestor */
  position: absolute;
  top: 0;
  right: 0;
  
  /* Fixed - relative to viewport */
  position: fixed;
  bottom: 20px;
  right: 20px;
  
  /* Sticky - hybrid of relative/fixed */
  position: sticky;
  top: 0;  /* sticks when reaching this position */
}
```

### Z-Index

```css
.element {
  position: relative;  /* or absolute/fixed/sticky */
  z-index: 1;          /* positive = above */
  z-index: -1;         /* negative = below */
  z-index: 9999;       /* common for modals */
  z-index: auto;       /* default */
}
```

---

## Display

### Display Values

```css
.element {
  display: block;         /* full width, new line */
  display: inline;        /* inline, no width/height */
  display: inline-block;  /* inline, respects width/height */
  display: none;          /* hidden, removed from flow */
  display: flex;          /* flexbox container */
  display: inline-flex;   /* inline flexbox */
  display: grid;          /* grid container */
  display: inline-grid;   /* inline grid */
  display: contents;      /* removes box, keeps children */
}
```

### Visibility

```css
.element {
  visibility: visible;   /* default */
  visibility: hidden;    /* hidden but takes space */
  visibility: collapse;  /* for table elements */
}
```

---

## Flexbox

### Container Properties

```css
.flex-container {
  display: flex;
  
  /* Direction */
  flex-direction: row;            /* default: left to right */
  flex-direction: row-reverse;    /* right to left */
  flex-direction: column;         /* top to bottom */
  flex-direction: column-reverse; /* bottom to top */
  
  /* Wrapping */
  flex-wrap: nowrap;    /* default: single line */
  flex-wrap: wrap;      /* wrap to new lines */
  flex-wrap: wrap-reverse;
  
  /* Shorthand */
  flex-flow: row wrap;
  
  /* Main axis alignment */
  justify-content: flex-start;    /* default */
  justify-content: flex-end;
  justify-content: center;
  justify-content: space-between; /* even space between items */
  justify-content: space-around;  /* even space around items */
  justify-content: space-evenly;  /* equal space everywhere */
  
  /* Cross axis alignment */
  align-items: stretch;     /* default: fill height */
  align-items: flex-start;
  align-items: flex-end;
  align-items: center;
  align-items: baseline;    /* text baseline alignment */
  
  /* Multi-line alignment */
  align-content: flex-start;
  align-content: center;
  align-content: space-between;
  
  /* Gap */
  gap: 20px;           /* both row and column */
  row-gap: 20px;
  column-gap: 10px;
}
```

### Item Properties

```css
.flex-item {
  /* Growth */
  flex-grow: 0;    /* default: don't grow */
  flex-grow: 1;    /* grow to fill space */
  flex-grow: 2;    /* grow twice as much */
  
  /* Shrink */
  flex-shrink: 1;  /* default: shrink if needed */
  flex-shrink: 0;  /* don't shrink */
  
  /* Base size */
  flex-basis: auto;   /* default: use width/content */
  flex-basis: 200px;  /* starting size */
  flex-basis: 0;      /* ignore content size */
  
  /* Shorthand */
  flex: 1;            /* grow: 1, shrink: 1, basis: 0 */
  flex: 0 0 auto;     /* don't grow, don't shrink, auto basis */
  flex: 1 1 200px;    /* grow, shrink, 200px basis */
  
  /* Order */
  order: 0;    /* default */
  order: -1;   /* move to start */
  order: 1;    /* move to end */
  
  /* Individual alignment */
  align-self: auto;
  align-self: flex-start;
  align-self: center;
  align-self: flex-end;
  align-self: stretch;
}
```

### Common Flexbox Patterns

```css
/* Center everything */
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Space between nav */
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Equal columns */
.columns {
  display: flex;
  gap: 20px;
}
.columns > * {
  flex: 1;
}

/* Sidebar layout */
.layout {
  display: flex;
}
.sidebar {
  flex: 0 0 250px;  /* fixed width */
}
.main {
  flex: 1;  /* fill remaining */
}
```

---

## CSS Grid

### Container Properties

```css
.grid-container {
  display: grid;
  
  /* Columns and rows */
  grid-template-columns: 200px 1fr 200px;        /* fixed + flexible */
  grid-template-columns: repeat(3, 1fr);          /* 3 equal columns */
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));  /* responsive */
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); /* responsive */
  
  grid-template-rows: 100px auto 100px;
  grid-template-rows: repeat(3, minmax(100px, auto));
  
  /* Gap */
  gap: 20px;
  row-gap: 20px;
  column-gap: 10px;
  
  /* Named areas */
  grid-template-areas:
    "header header header"
    "sidebar main main"
    "footer footer footer";
  
  /* Alignment */
  justify-items: stretch;   /* horizontal alignment of items */
  justify-items: start;
  justify-items: center;
  justify-items: end;
  
  align-items: stretch;     /* vertical alignment of items */
  align-items: start;
  align-items: center;
  align-items: end;
  
  justify-content: start;   /* grid within container (horizontal) */
  align-content: start;     /* grid within container (vertical) */
  
  place-items: center;      /* shorthand for align + justify items */
  place-content: center;    /* shorthand for align + justify content */
  
  /* Implicit grid */
  grid-auto-rows: minmax(100px, auto);
  grid-auto-columns: 1fr;
  grid-auto-flow: row;      /* default */
  grid-auto-flow: column;
  grid-auto-flow: dense;    /* fill gaps */
}
```

### Item Properties

```css
.grid-item {
  /* Placement by line */
  grid-column-start: 1;
  grid-column-end: 3;
  grid-column: 1 / 3;       /* shorthand */
  grid-column: 1 / span 2;  /* start at 1, span 2 columns */
  grid-column: span 2;      /* span 2 from auto position */
  
  grid-row-start: 1;
  grid-row-end: 4;
  grid-row: 1 / 4;
  
  /* Placement by area name */
  grid-area: header;
  
  /* Shorthand: row-start / column-start / row-end / column-end */
  grid-area: 1 / 1 / 3 / 4;
  
  /* Individual alignment */
  justify-self: start;
  justify-self: center;
  justify-self: end;
  justify-self: stretch;
  
  align-self: start;
  align-self: center;
  align-self: end;
  align-self: stretch;
  
  place-self: center;       /* shorthand */
}
```

### Common Grid Patterns

```css
/* Holy Grail Layout */
.layout {
  display: grid;
  grid-template-areas:
    "header header header"
    "nav    main   aside"
    "footer footer footer";
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
}
.header { grid-area: header; }
.nav    { grid-area: nav; }
.main   { grid-area: main; }
.aside  { grid-area: aside; }
.footer { grid-area: footer; }

/* Responsive card grid */
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}

/* 12-column grid */
.grid-12 {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
}
.col-6 { grid-column: span 6; }
.col-4 { grid-column: span 4; }
```

---

## Responsive Design

### Media Queries

```css
/* Mobile first approach (recommended) */
.element {
  /* Base styles for mobile */
  font-size: 14px;
}

@media (min-width: 576px) {
  /* Small devices and up */
}

@media (min-width: 768px) {
  /* Tablets and up */
  .element { font-size: 16px; }
}

@media (min-width: 992px) {
  /* Desktops and up */
}

@media (min-width: 1200px) {
  /* Large desktops */
}

/* Other media features */
@media (max-width: 767px) { }
@media (orientation: landscape) { }
@media (prefers-color-scheme: dark) { }
@media (prefers-reduced-motion: reduce) { }
@media print { }
```

### Container Queries

```css
.card-container {
  container-type: inline-size;
  container-name: card;
}

@container card (min-width: 400px) {
  .card {
    flex-direction: row;
  }
}

@container (min-width: 300px) {
  /* Works without named container */
}
```

### Responsive Images

```css
img {
  max-width: 100%;
  height: auto;
  display: block;
}

/* Object fit for fixed containers */
.image-container {
  width: 300px;
  height: 200px;
}
.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;      /* fill, may crop */
  object-fit: contain;    /* fit, may letterbox */
  object-position: center;
}
```

### Fluid Typography

```css
/* Using clamp() */
h1 {
  font-size: clamp(1.5rem, 4vw + 1rem, 3rem);
  /* min: 1.5rem, preferred: 4vw + 1rem, max: 3rem */
}

body {
  font-size: clamp(1rem, 0.5vw + 0.9rem, 1.25rem);
}
```

---

## Transitions

### Transition Properties

```css
.element {
  /* Individual properties */
  transition-property: all;           /* what to transition */
  transition-property: background-color, transform;
  transition-duration: 0.3s;          /* how long */
  transition-timing-function: ease;   /* easing curve */
  transition-delay: 0.1s;             /* wait before start */
  
  /* Shorthand */
  transition: all 0.3s ease;
  transition: background-color 0.3s ease, transform 0.2s ease-out;
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

/* Apply on hover */
.button {
  background: blue;
  transition: background 0.3s ease;
}
.button:hover {
  background: darkblue;
}
```

### Timing Functions

```css
.element {
  transition-timing-function: linear;
  transition-timing-function: ease;        /* default */
  transition-timing-function: ease-in;     /* slow start */
  transition-timing-function: ease-out;    /* slow end */
  transition-timing-function: ease-in-out;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-timing-function: steps(4);    /* stepped animation */
}
```

---

## Animations

### Keyframes

```css
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideIn {
  0% {
    transform: translateX(-100%);
    opacity: 0;
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}
```

### Animation Properties

```css
.element {
  /* Individual properties */
  animation-name: fadeIn;
  animation-duration: 0.5s;
  animation-timing-function: ease;
  animation-delay: 0.2s;
  animation-iteration-count: 1;        /* or infinite */
  animation-direction: normal;         /* reverse, alternate */
  animation-fill-mode: forwards;       /* none, backwards, both */
  animation-play-state: running;       /* paused */
  
  /* Shorthand */
  animation: fadeIn 0.5s ease 0.2s 1 normal forwards;
  
  /* Multiple animations */
  animation: fadeIn 0.5s ease, slideIn 0.3s ease-out;
}
```

### Common Animations

```css
/* Fade in */
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

/* Slide up */
@keyframes slideUp {
  from { transform: translateY(20px); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}

/* Spin */
@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

/* Pulse */
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

/* Shake */
@keyframes shake {
  0%, 100% { transform: translateX(0); }
  25% { transform: translateX(-5px); }
  75% { transform: translateX(5px); }
}
```

---

## Transforms

### 2D Transforms

```css
.element {
  /* Translate (move) */
  transform: translateX(50px);
  transform: translateY(-20px);
  transform: translate(50px, -20px);
  transform: translate(-50%, -50%);    /* useful for centering */
  
  /* Scale (resize) */
  transform: scaleX(1.5);
  transform: scaleY(0.5);
  transform: scale(1.5);               /* both axes */
  transform: scale(1.5, 0.5);
  
  /* Rotate */
  transform: rotate(45deg);
  transform: rotate(-90deg);
  transform: rotate(0.5turn);
  
  /* Skew */
  transform: skewX(10deg);
  transform: skewY(-5deg);
  transform: skew(10deg, -5deg);
  
  /* Combine multiple */
  transform: translate(-50%, -50%) rotate(45deg) scale(1.2);
  
  /* Transform origin */
  transform-origin: center;            /* default */
  transform-origin: top left;
  transform-origin: 50% 100%;
}
```

### 3D Transforms

```css
.container {
  perspective: 1000px;          /* depth of 3D effect */
  perspective-origin: center;
}

.element {
  transform: rotateX(45deg);    /* rotate around X axis */
  transform: rotateY(45deg);    /* rotate around Y axis */
  transform: rotateZ(45deg);    /* same as rotate() */
  transform: rotate3d(1, 1, 0, 45deg);
  
  transform: translateZ(50px);  /* move toward/away */
  transform: translate3d(10px, 20px, 50px);
  
  transform-style: preserve-3d; /* keep 3D for children */
  backface-visibility: hidden;  /* hide back of element */
}
```

---

## Filters & Effects

### Filter Property

```css
.element {
  filter: blur(5px);
  filter: brightness(1.2);      /* >1 brighter, <1 darker */
  filter: contrast(1.5);
  filter: grayscale(100%);
  filter: saturate(2);
  filter: sepia(100%);
  filter: hue-rotate(90deg);
  filter: invert(100%);
  filter: opacity(50%);
  filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.3));
  
  /* Multiple filters */
  filter: contrast(1.2) brightness(1.1) saturate(1.3);
  
  /* None */
  filter: none;
}
```

### Backdrop Filter

```css
.frosted-glass {
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  backdrop-filter: blur(10px) saturate(180%);
}
```

### Blend Modes

```css
.element {
  /* Mix with background */
  mix-blend-mode: multiply;
  mix-blend-mode: screen;
  mix-blend-mode: overlay;
  mix-blend-mode: darken;
  mix-blend-mode: lighten;
  mix-blend-mode: color-dodge;
  mix-blend-mode: difference;
  
  /* Background layers */
  background-blend-mode: multiply;
}
```

### Clip Path

```css
.element {
  clip-path: circle(50%);
  clip-path: ellipse(50% 30% at 50% 50%);
  clip-path: polygon(50% 0%, 100% 100%, 0% 100%);  /* triangle */
  clip-path: inset(10px 20px 30px 40px round 10px);
}
```

---

## CSS Variables

### Defining and Using Variables

```css
/* Define on :root for global access */
:root {
  --primary-color: #3b82f6;
  --secondary-color: #6366f1;
  --text-color: #1f2937;
  --font-size-base: 16px;
  --spacing-unit: 8px;
  --border-radius: 8px;
}

/* Use with var() */
.element {
  color: var(--primary-color);
  font-size: var(--font-size-base);
  padding: calc(var(--spacing-unit) * 2);
  
  /* With fallback */
  color: var(--undefined-color, #333);
}
```

### Scoped Variables

```css
.card {
  --card-padding: 20px;
  padding: var(--card-padding);
}

.card.compact {
  --card-padding: 10px;
}
```

### Theme Switching

```css
:root {
  --bg-color: #ffffff;
  --text-color: #1f2937;
}

[data-theme="dark"] {
  --bg-color: #1f2937;
  --text-color: #f9fafb;
}

body {
  background: var(--bg-color);
  color: var(--text-color);
}
```

---

## Functions

### Mathematical Functions

```css
.element {
  /* calc() - calculations with mixed units */
  width: calc(100% - 40px);
  height: calc(100vh - 80px);
  font-size: calc(1rem + 0.5vw);
  
  /* min() - smallest value */
  width: min(90%, 1200px);
  
  /* max() - largest value */
  width: max(300px, 50%);
  
  /* clamp() - value between min and max */
  font-size: clamp(1rem, 2.5vw, 2rem);
  width: clamp(200px, 50%, 800px);
}
```

### Color Functions

```css
.element {
  /* Modern color functions */
  color: rgb(255 0 0);
  color: rgb(255 0 0 / 50%);
  color: hsl(120 100% 50%);
  color: hsl(120 100% 50% / 50%);
  
  /* Color-mix (modern browsers) */
  background: color-mix(in srgb, red, blue);
  background: color-mix(in srgb, red 30%, blue);
}
```

---

## Pseudo-Classes

### User Action

```css
a:hover { }       /* mouse over */
a:active { }      /* being clicked */
a:focus { }       /* keyboard focus */
a:focus-visible { } /* keyboard focus only */
a:visited { }     /* visited link */
```

### Structural

```css
:first-child { }
:last-child { }
:nth-child(2) { }         /* 2nd element */
:nth-child(odd) { }       /* 1st, 3rd, 5th... */
:nth-child(even) { }      /* 2nd, 4th, 6th... */
:nth-child(3n) { }        /* every 3rd */
:nth-child(3n+1) { }      /* 1st, 4th, 7th... */
:nth-last-child(2) { }    /* 2nd from end */
:only-child { }
:first-of-type { }
:last-of-type { }
:nth-of-type(2) { }
:only-of-type { }
:empty { }                /* no children */
:root { }                 /* html element */
```

### Form States

```css
:enabled { }
:disabled { }
:checked { }
:indeterminate { }
:valid { }
:invalid { }
:required { }
:optional { }
:in-range { }
:out-of-range { }
:read-only { }
:read-write { }
:placeholder-shown { }
:focus-within { }  /* parent has focused child */
```

### Negation and Matching

```css
:not(.class) { }
:not(:first-child) { }
:is(h1, h2, h3) { }       /* matches any */
:where(h1, h2, h3) { }    /* like :is but 0 specificity */
:has(.child) { }          /* parent selector */
:has(> img) { }           /* has direct img child */
```

---

## Pseudo-Elements

```css
/* Before and after */
.element::before {
  content: "";           /* required */
  display: block;
}

.element::after {
  content: "→";
  content: attr(data-label);  /* from attribute */
  content: counter(item);
}

/* First letter and line */
p::first-letter {
  font-size: 2em;
  float: left;
}

p::first-line {
  font-weight: bold;
}

/* Selection and placeholder */
::selection {
  background: yellow;
  color: black;
}

input::placeholder {
  color: #999;
}

/* Marker (list bullets) */
li::marker {
  color: red;
}
```

---

## Units

### Absolute Units

| Unit | Description |
|------|-------------|
| `px` | Pixels (1/96 of 1 inch) |
| `pt` | Points (1/72 of 1 inch) |
| `cm` | Centimeters |
| `mm` | Millimeters |
| `in` | Inches |

### Relative Units

| Unit | Relative To |
|------|-------------|
| `em` | Parent element's font size |
| `rem` | Root element's font size |
| `%` | Parent element's dimension |
| `vw` | 1% of viewport width |
| `vh` | 1% of viewport height |
| `vmin` | 1% of smaller viewport dimension |
| `vmax` | 1% of larger viewport dimension |
| `dvh` | Dynamic viewport height (mobile) |
| `svh` | Small viewport height |
| `lvh` | Large viewport height |
| `ch` | Width of "0" character |
| `ex` | Height of "x" character |
| `lh` | Line height of element |

### When to Use What

```css
/* px: borders, shadows, exact sizes */
border: 1px solid #ccc;
box-shadow: 0 2px 4px rgba(0,0,0,0.1);

/* rem: typography, spacing (consistent) */
font-size: 1rem;
padding: 1.5rem;
margin-bottom: 2rem;

/* em: component-relative sizing */
button { padding: 0.5em 1em; }

/* %: fluid widths, responsive layouts */
.container { width: 90%; max-width: 1200px; }

/* vw/vh: viewport-relative */
.hero { height: 100vh; }
.full-width { width: 100vw; }
```

---

## Common Patterns

### Center Horizontally

```css
/* Block element */
.center { margin: 0 auto; }

/* Flexbox */
.parent { display: flex; justify-content: center; }

/* Grid */
.parent { display: grid; justify-items: center; }

/* Text */
.text { text-align: center; }
```

### Center Vertically

```css
/* Flexbox */
.parent { display: flex; align-items: center; }

/* Grid */
.parent { display: grid; align-items: center; }

/* Absolute + transform */
.child {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```

### Center Both

```css
/* Flexbox */
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Grid */
.parent {
  display: grid;
  place-items: center;
}

/* Absolute + transform */
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

### Sticky Footer

```css
body {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

main {
  flex: 1;
}

footer {
  margin-top: auto;
}
```

### Truncate Text

```css
.truncate {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* Multi-line truncate */
.truncate-multi {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

### Aspect Ratio Container

```css
.aspect-16-9 {
  aspect-ratio: 16 / 9;
}

.aspect-square {
  aspect-ratio: 1;
}

/* Legacy padding trick */
.aspect-container {
  position: relative;
  padding-bottom: 56.25%; /* 16:9 */
}
.aspect-container > * {
  position: absolute;
  inset: 0;
}
```

### Visually Hidden (Accessible)

```css
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

### Custom Scrollbar

```css
.scrollable::-webkit-scrollbar {
  width: 8px;
}

.scrollable::-webkit-scrollbar-track {
  background: #f1f1f1;
}

.scrollable::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 4px;
}

.scrollable::-webkit-scrollbar-thumb:hover {
  background: #555;
}
```

---

## Quick Reference Tables

### Flexbox Alignment Summary

| Property | Axis | Values |
|----------|------|--------|
| `justify-content` | Main | flex-start, flex-end, center, space-between, space-around, space-evenly |
| `align-items` | Cross | flex-start, flex-end, center, stretch, baseline |
| `align-content` | Cross (multi-line) | Same as justify-content + stretch |
| `align-self` | Cross (single item) | auto, flex-start, flex-end, center, stretch, baseline |

### Grid Alignment Summary

| Property | Applies To | Direction |
|----------|------------|-----------|
| `justify-items` | Grid items | Inline (horizontal) |
| `align-items` | Grid items | Block (vertical) |
| `justify-content` | Grid tracks | Inline (horizontal) |
| `align-content` | Grid tracks | Block (vertical) |
| `place-items` | Shorthand | Both (align then justify) |
| `place-content` | Shorthand | Both (align then justify) |

### Common Easing Functions

```css
/* Standard easings */
linear
ease           /* default, slow start and end */
ease-in        /* slow start */
ease-out       /* slow end */
ease-in-out    /* slow start and end */

/* Custom cubic-bezier */
cubic-bezier(0.4, 0, 0.2, 1)    /* standard */
cubic-bezier(0, 0, 0.2, 1)      /* decelerate */
cubic-bezier(0.4, 0, 1, 1)      /* accelerate */
cubic-bezier(0.0, 0, 0.2, 1)    /* sharp */
```

---

*Keep this cheatsheet handy while working through the CSS assignments!*
