# HTML Cheatsheet

> Comprehensive quick reference for HTML elements, attributes, and best practices.

---

## 📄 Document Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Page description">
    <title>Page Title</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Content here -->
    <script src="script.js" defer></script>
</body>
</html>
```

### Essential Meta Tags
| Tag | Purpose |
|-----|---------|
| `<meta charset="UTF-8">` | Character encoding |
| `<meta name="viewport" content="width=device-width, initial-scale=1.0">` | Mobile responsive |
| `<meta name="description" content="...">` | SEO description |
| `<meta name="author" content="...">` | Author info |
| `<meta name="robots" content="index, follow">` | Search engines |
| `<link rel="canonical" href="...">` | Canonical URL |

---

## 📝 Text Elements

### Headings
```html
<h1>Main Title</h1>      <!-- One per page -->
<h2>Section Title</h2>
<h3>Subsection</h3>
<h4>Sub-subsection</h4>
<h5>Minor heading</h5>
<h6>Smallest heading</h6>
```

### Text Formatting
| Element | Purpose | Example |
|---------|---------|---------|
| `<p>` | Paragraph | `<p>Text</p>` |
| `<strong>` | Important (bold) | `<strong>Important</strong>` |
| `<em>` | Emphasis (italic) | `<em>Emphasis</em>` |
| `<mark>` | Highlight | `<mark>Highlighted</mark>` |
| `<small>` | Fine print | `<small>Copyright</small>` |
| `<del>` | Deleted text | `<del>Removed</del>` |
| `<ins>` | Inserted text | `<ins>Added</ins>` |
| `<sub>` | Subscript | `H<sub>2</sub>O` |
| `<sup>` | Superscript | `x<sup>2</sup>` |
| `<abbr>` | Abbreviation | `<abbr title="HyperText">HTML</abbr>` |
| `<code>` | Inline code | `<code>const x = 1;</code>` |
| `<pre>` | Preformatted | `<pre>Code block</pre>` |
| `<kbd>` | Keyboard input | `<kbd>Ctrl+C</kbd>` |
| `<samp>` | Sample output | `<samp>Error 404</samp>` |
| `<br>` | Line break | `Line 1<br>Line 2` |
| `<hr>` | Thematic break | `<hr>` |

### Quotations
```html
<blockquote cite="https://source.com">
    <p>Long quotation text.</p>
    <footer>— <cite>Author Name</cite></footer>
</blockquote>

<p>She said, <q>Inline quote</q>.</p>
```

---

## 📋 Lists

### Unordered List
```html
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
</ul>
```

### Ordered List
```html
<ol start="1" type="1">  <!-- type: 1, A, a, I, i -->
    <li>First</li>
    <li>Second</li>
</ol>
```

### Description List
```html
<dl>
    <dt>Term</dt>
    <dd>Definition</dd>
</dl>
```

---

## 🔗 Links

### Basic Links
```html
<a href="https://example.com">External Link</a>
<a href="/page.html">Internal Link</a>
<a href="#section-id">Anchor Link</a>
<a href="mailto:email@example.com">Email Link</a>
<a href="tel:+1234567890">Phone Link</a>
```

### Link Attributes
| Attribute | Purpose |
|-----------|---------|
| `href` | URL destination |
| `target="_blank"` | Open in new tab |
| `rel="noopener noreferrer"` | Security for _blank |
| `rel="nofollow"` | No SEO juice |
| `download` | Download file |
| `download="filename"` | Custom filename |

---

## 🖼️ Images

### Basic Image
```html
<img src="image.jpg" 
     alt="Description" 
     width="400" 
     height="300"
     loading="lazy">
```

### Figure with Caption
```html
<figure>
    <img src="photo.jpg" alt="Description">
    <figcaption>Image caption</figcaption>
</figure>
```

### Responsive Images
```html
<!-- Srcset for resolution -->
<img src="image.jpg"
     srcset="image-1x.jpg 1x, image-2x.jpg 2x"
     alt="Description">

<!-- Srcset with sizes -->
<img src="default.jpg"
     srcset="small.jpg 400w, medium.jpg 800w, large.jpg 1200w"
     sizes="(max-width: 600px) 400px, (max-width: 1200px) 800px, 1200px"
     alt="Description">

<!-- Picture element for art direction -->
<picture>
    <source media="(min-width: 800px)" srcset="large.webp" type="image/webp">
    <source media="(min-width: 800px)" srcset="large.jpg">
    <source srcset="small.webp" type="image/webp">
    <img src="small.jpg" alt="Description">
</picture>
```

---

## 🏗️ Semantic Structure

```html
<body>
    <header>
        <nav aria-label="Main">
            <ul>
                <li><a href="/">Home</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <article>
            <header>
                <h1>Article Title</h1>
                <time datetime="2024-01-15">Jan 15, 2024</time>
            </header>
            
            <section>
                <h2>Section Title</h2>
                <p>Content...</p>
            </section>
            
            <footer>
                <address>
                    By <a href="mailto:author@email.com">Author</a>
                </address>
            </footer>
        </article>
        
        <aside>
            <h2>Related</h2>
        </aside>
    </main>
    
    <footer>
        <p>&copy; 2024 Company</p>
    </footer>
</body>
```

### Semantic Elements Summary
| Element | Purpose |
|---------|---------|
| `<header>` | Introductory content |
| `<nav>` | Navigation links |
| `<main>` | Main content (one per page) |
| `<article>` | Self-contained content |
| `<section>` | Thematic grouping |
| `<aside>` | Tangential content |
| `<footer>` | Closing content |
| `<figure>` | Self-contained illustration |
| `<figcaption>` | Figure caption |
| `<time>` | Date/time |
| `<address>` | Contact info |

---

## 📊 Tables

```html
<table>
    <caption>Table Title</caption>
    <thead>
        <tr>
            <th scope="col">Header 1</th>
            <th scope="col">Header 2</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Row Header</th>
            <td>Data</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <th scope="row">Total</th>
            <td>Sum</td>
        </tr>
    </tfoot>
</table>
```

### Table Attributes
| Attribute | Purpose |
|-----------|---------|
| `scope="col"` | Column header |
| `scope="row"` | Row header |
| `colspan="2"` | Span columns |
| `rowspan="2"` | Span rows |
| `headers="id1 id2"` | Complex associations |

---

## 📝 Forms

### Form Structure
```html
<form action="/submit" method="POST" enctype="multipart/form-data">
    <fieldset>
        <legend>Personal Info</legend>
        
        <label for="name">Name *</label>
        <input type="text" id="name" name="name" required>
        
        <label for="email">Email</label>
        <input type="email" id="email" name="email">
    </fieldset>
    
    <button type="submit">Submit</button>
</form>
```

### Input Types
| Type | Purpose |
|------|---------|
| `text` | Single-line text |
| `email` | Email address |
| `password` | Password |
| `number` | Numeric value |
| `tel` | Telephone |
| `url` | URL |
| `date` | Date picker |
| `time` | Time picker |
| `datetime-local` | Date and time |
| `color` | Color picker |
| `range` | Slider |
| `file` | File upload |
| `checkbox` | Multiple choice |
| `radio` | Single choice |
| `hidden` | Hidden data |
| `search` | Search field |

### Input Attributes
| Attribute | Purpose |
|-----------|---------|
| `required` | Must fill |
| `placeholder` | Hint text |
| `pattern="[A-Z]+"` | Regex validation |
| `minlength="5"` | Min characters |
| `maxlength="100"` | Max characters |
| `min="0"` | Min value |
| `max="100"` | Max value |
| `step="5"` | Value increment |
| `disabled` | Not editable |
| `readonly` | Display only |
| `autofocus` | Focus on load |
| `autocomplete="email"` | Autofill hint |

### Other Form Elements
```html
<!-- Textarea -->
<textarea id="msg" name="msg" rows="4" cols="50"></textarea>

<!-- Select -->
<select id="country" name="country">
    <option value="">Choose...</option>
    <optgroup label="North America">
        <option value="us">USA</option>
        <option value="ca">Canada</option>
    </optgroup>
</select>

<!-- Datalist -->
<input list="browsers" name="browser">
<datalist id="browsers">
    <option value="Chrome">
    <option value="Firefox">
</datalist>

<!-- Output -->
<output name="result" for="a b">0</output>
```

---

## 🎬 Multimedia

### Audio
```html
<audio controls preload="metadata">
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    <p>Your browser doesn't support audio.</p>
</audio>
```

### Video
```html
<video controls width="640" height="360" poster="thumbnail.jpg">
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    <track kind="captions" src="captions.vtt" srclang="en" label="English" default>
    <p>Your browser doesn't support video.</p>
</video>
```

### Track Kinds
| Kind | Purpose |
|------|---------|
| `captions` | Deaf/hard of hearing |
| `subtitles` | Translation |
| `descriptions` | Audio description |
| `chapters` | Navigation |
| `metadata` | Script data |

### Iframe
```html
<iframe src="https://example.com"
        width="600" 
        height="400"
        title="Embedded content"
        loading="lazy"
        sandbox="allow-scripts allow-same-origin">
</iframe>
```

---

## ♿ Accessibility (ARIA)

### Landmark Roles
```html
<header role="banner">
<nav role="navigation">
<main role="main">
<aside role="complementary">
<footer role="contentinfo">
<form role="search">
```

### Common ARIA Attributes
| Attribute | Purpose |
|-----------|---------|
| `aria-label="..."` | Accessible name |
| `aria-labelledby="id"` | Name from element |
| `aria-describedby="id"` | Description |
| `aria-hidden="true"` | Hide from AT |
| `aria-expanded="false"` | Disclosure state |
| `aria-current="page"` | Current item |
| `aria-live="polite"` | Dynamic content |
| `aria-required="true"` | Required field |
| `aria-invalid="true"` | Validation state |

### Skip Link
```html
<a href="#main-content" class="skip-link">Skip to content</a>
<!-- ...navigation... -->
<main id="main-content">
```

### Accessible Images
```html
<!-- Informative -->
<img src="chart.png" alt="Sales increased 25% in Q4">

<!-- Decorative -->
<img src="divider.png" alt="" role="presentation">

<!-- Functional (link/button) -->
<a href="/"><img src="logo.png" alt="Go to homepage"></a>
```

---

## 🔍 SEO Metadata

### Essential Meta Tags
```html
<title>Page Title - Brand Name</title>
<meta name="description" content="Page description (150-160 chars)">
<link rel="canonical" href="https://example.com/page">
```

### Open Graph (Social)
```html
<meta property="og:title" content="Page Title">
<meta property="og:description" content="Description">
<meta property="og:image" content="https://example.com/image.jpg">
<meta property="og:url" content="https://example.com/page">
<meta property="og:type" content="website">
```

### Twitter Cards
```html
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Page Title">
<meta name="twitter:description" content="Description">
<meta name="twitter:image" content="https://example.com/image.jpg">
```

### Structured Data (JSON-LD)
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Article Title",
  "author": {
    "@type": "Person",
    "name": "Author Name"
  },
  "datePublished": "2024-01-15"
}
</script>
```

---

## ⚡ Performance

### Resource Hints
```html
<!-- DNS prefetch -->
<link rel="dns-prefetch" href="//cdn.example.com">

<!-- Preconnect -->
<link rel="preconnect" href="https://fonts.googleapis.com">

<!-- Preload critical resource -->
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin>

<!-- Prefetch next page -->
<link rel="prefetch" href="/next-page.html">
```

### Script Loading
```html
<!-- Defer (execute after parsing) -->
<script src="app.js" defer></script>

<!-- Async (execute when ready) -->
<script src="analytics.js" async></script>

<!-- Module -->
<script type="module" src="module.js"></script>
```

### Lazy Loading
```html
<img src="image.jpg" alt="..." loading="lazy">
<iframe src="..." loading="lazy"></iframe>
```

---

## 🧩 Modern HTML5 Features

### Details/Summary
```html
<details>
    <summary>Click to expand</summary>
    <p>Hidden content here.</p>
</details>
```

### Dialog
```html
<dialog id="modal">
    <h2>Modal Title</h2>
    <p>Content...</p>
    <button onclick="this.closest('dialog').close()">Close</button>
</dialog>
```

### Template
```html
<template id="card-template">
    <div class="card">
        <h3></h3>
        <p></p>
    </div>
</template>
```

### Data Attributes
```html
<div data-id="123" data-category="tech" data-user-name="john">
    <!-- JS: element.dataset.id, element.dataset.userName -->
</div>
```

### Progress & Meter
```html
<progress value="70" max="100">70%</progress>
<meter value="0.7" min="0" max="1" low="0.3" high="0.7" optimum="0.8">70%</meter>
```

---

## 🔤 HTML Entities

| Character | Entity | Code |
|-----------|--------|------|
| `<` | `&lt;` | `&#60;` |
| `>` | `&gt;` | `&#62;` |
| `&` | `&amp;` | `&#38;` |
| `"` | `&quot;` | `&#34;` |
| `'` | `&apos;` | `&#39;` |
| ` ` (nbsp) | `&nbsp;` | `&#160;` |
| `©` | `&copy;` | `&#169;` |
| `®` | `&reg;` | `&#174;` |
| `™` | `&trade;` | `&#8482;` |
| `€` | `&euro;` | `&#8364;` |
| `£` | `&pound;` | `&#163;` |
| `—` | `&mdash;` | `&#8212;` |
| `–` | `&ndash;` | `&#8211;` |
| `…` | `&hellip;` | `&#8230;` |
| `×` | `&times;` | `&#215;` |
| `÷` | `&divide;` | `&#247;` |
| `←` | `&larr;` | `&#8592;` |
| `→` | `&rarr;` | `&#8594;` |
| `↑` | `&uarr;` | `&#8593;` |
| `↓` | `&darr;` | `&#8595;` |

---

## ✅ Best Practices Checklist

### Document
- [ ] DOCTYPE declared
- [ ] lang attribute on html
- [ ] charset meta tag
- [ ] viewport meta tag
- [ ] title tag (50-60 chars)
- [ ] meta description (150-160 chars)

### Semantic HTML
- [ ] One h1 per page
- [ ] Logical heading hierarchy
- [ ] Semantic elements over divs
- [ ] Lists for list content
- [ ] Tables for tabular data only

### Accessibility
- [ ] All images have alt text
- [ ] All form inputs have labels
- [ ] Color not sole indicator
- [ ] Keyboard navigable
- [ ] Skip link present
- [ ] Focus visible
- [ ] ARIA used correctly

### Performance
- [ ] Images have width/height
- [ ] Below-fold images lazy loaded
- [ ] Scripts deferred
- [ ] Critical resources preloaded
- [ ] Resource hints used

### SEO
- [ ] Unique title per page
- [ ] Meta description unique
- [ ] Canonical URL set
- [ ] Open Graph tags
- [ ] Structured data where applicable

### Forms
- [ ] All inputs have labels
- [ ] Required fields marked
- [ ] Input types appropriate
- [ ] Error messages accessible
- [ ] Fieldsets for grouping

### Links
- [ ] Descriptive link text
- [ ] External links have rel="noopener"
- [ ] Internal links work
- [ ] No broken links

### Validation
- [ ] W3C HTML valid
- [ ] No duplicate IDs
- [ ] Proper nesting
- [ ] All tags closed

---

## 🛠️ Validation Tools

| Tool | URL |
|------|-----|
| W3C HTML Validator | validator.w3.org |
| WAVE Accessibility | wave.webaim.org |
| aXe DevTools | Browser extension |
| Lighthouse | Chrome DevTools |
| Schema.org Validator | validator.schema.org |
| Rich Results Test | search.google.com/test/rich-results |

---

*Quick reference for HTML development — from basics to advanced.*
