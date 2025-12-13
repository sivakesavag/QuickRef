# CSS Mastery Curriculum: Beginner to Expert

> A comprehensive, self-contained CSS curriculum with 240+ assignments designed to systematically build mastery from fundamentals to professional-level expertise.

---

## Table of Contents

1. [Beginner Level](#beginner-level-css-fundamentals) (Assignments 1-60)
2. [Intermediate Level](#intermediate-level-layouts--responsive-design) (Assignments 61-120)
3. [Advanced Level](#advanced-level-animations--modern-techniques) (Assignments 121-180)
4. [Expert Level](#expert-level-complex-designs--optimization) (Assignments 181-240)

---

# BEGINNER LEVEL: CSS Fundamentals

> **Goal**: Master CSS syntax, selectors, colors, typography, box model, and basic styling techniques.

---

## Module 1: CSS Syntax and Basic Selectors (Assignments 1-10)

### Assignment 1: Your First CSS Rule
**Objective**: Write your first CSS rule to change paragraph text color.

**HTML Provided**:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>First CSS</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <p>Hello, CSS World!</p>
</body>
</html>
```

**Requirements**:
- Create `styles.css` file
- Change paragraph text to blue using element selector
- Use proper CSS syntax: `selector { property: value; }`

**Expected Outcome**: Blue paragraph text

**Key Concepts**: CSS rule structure, element selector, color property

**Common Pitfalls**:
- Missing semicolon after property value
- Incorrect file linking in HTML
- Typos in property names

---

### Assignment 2: Multiple Properties
**Objective**: Apply multiple CSS properties to a single element.

**HTML Provided**:
```html
<h1>Welcome to My Website</h1>
<p>This is a paragraph with multiple styles.</p>
```

**Requirements**:
- Style `h1`: color navy, font-size 32px
- Style `p`: color gray, font-size 16px, font-family Arial

**Expected Outcome**: Styled heading and paragraph with distinct appearances

**Key Concepts**: Multiple property declarations, font properties

---

### Assignment 3: Class Selectors
**Objective**: Use class selectors to style specific elements.

**HTML Provided**:
```html
<p class="intro">This is the introduction paragraph.</p>
<p>This is a regular paragraph.</p>
<p class="intro">Another introduction paragraph.</p>
```

**Requirements**:
- Create `.intro` class with: font-weight bold, color darkgreen, font-size 18px
- Regular paragraphs remain unstyled

**Expected Outcome**: Only elements with class="intro" are styled

**Key Concepts**: Class selector syntax (.), reusable styles

---

### Assignment 4: ID Selectors
**Objective**: Use ID selectors for unique element styling.

**HTML Provided**:
```html
<header id="main-header">Site Header</header>
<nav id="primary-nav">Navigation</nav>
<main id="content">Main Content</main>
```

**Requirements**:
- `#main-header`: background-color #333, color white, padding 20px
- `#primary-nav`: background-color #666, color white, padding 10px
- `#content`: padding 20px

**Expected Outcome**: Each section uniquely styled

**Key Concepts**: ID selector syntax (#), unique identifiers

---

### Assignment 5: Universal Selector
**Objective**: Apply global styles using the universal selector.

**HTML Provided**:
```html
<h1>Heading</h1>
<p>Paragraph text</p>
<ul>
  <li>List item 1</li>
  <li>List item 2</li>
</ul>
```

**Requirements**:
- Use `*` selector to set: margin 0, padding 0, box-sizing border-box
- Add specific styles for each element after reset

**Expected Outcome**: All default browser margins/padding removed

**Key Concepts**: Universal selector, CSS reset basics

---

### Assignment 6: Grouping Selectors
**Objective**: Apply same styles to multiple selectors efficiently.

**HTML Provided**:
```html
<h1>Main Title</h1>
<h2>Section Title</h2>
<h3>Subsection Title</h3>
```

**Requirements**:
- Group h1, h2, h3 with: font-family Georgia, serif; color #2c3e50
- Add individual font-size for each (h1: 36px, h2: 28px, h3: 22px)

**Expected Outcome**: All headings share font-family/color, unique sizes

**Key Concepts**: Selector grouping with commas, DRY principle

---

### Assignment 7: Descendant Selectors
**Objective**: Style elements based on their parent context.

**HTML Provided**:
```html
<article>
  <p>Paragraph inside article</p>
</article>
<p>Paragraph outside article</p>
<div class="sidebar">
  <p>Paragraph inside sidebar</p>
</div>
```

**Requirements**:
- `article p`: color #333, line-height 1.6
- `.sidebar p`: color #666, font-size 14px
- Outside paragraph: unstyled

**Expected Outcome**: Context-specific paragraph styling

**Key Concepts**: Descendant combinator (space), contextual styling

---

### Assignment 8: Comments and Organization
**Objective**: Write well-organized, commented CSS code.

**Requirements**:
Create a stylesheet with:
- Header comment with file description, author, date
- Section comments for: Typography, Colors, Layout
- Inline comments explaining complex rules
- Minimum 10 CSS rules across sections

**Expected Outcome**: Professional, maintainable CSS file structure

**Key Concepts**: `/* comment */` syntax, code organization

---

### Assignment 9: Combining Class and Element Selectors
**Objective**: Create more specific selectors by combining types.

**HTML Provided**:
```html
<p class="highlight">Highlighted paragraph</p>
<span class="highlight">Highlighted span</span>
<div class="highlight">Highlighted div</div>
```

**Requirements**:
- `p.highlight`: yellow background, padding 10px
- `span.highlight`: red text, font-weight bold
- `div.highlight`: border 2px solid blue

**Expected Outcome**: Same class, different element styling

**Key Concepts**: Combining selectors without space

---

### Assignment 10: Specificity Basics
**Objective**: Understand how CSS specificity determines which rules apply.

**HTML Provided**:
```html
<p id="special" class="text">What color am I?</p>
```

**CSS to Analyze**:
```css
p { color: blue; }
.text { color: green; }
#special { color: red; }
p.text { color: purple; }
```

**Requirements**:
- Predict the color (answer: red - ID has highest specificity)
- Create examples demonstrating specificity order
- Document specificity values for each selector

**Expected Outcome**: Understanding of specificity hierarchy

**Key Concepts**: Specificity calculation (ID > Class > Element)

---

## Module 2: Colors and Units (Assignments 11-20)

### Assignment 11: Named Colors
**Objective**: Use CSS named colors effectively.

**Requirements**:
Create a color palette display with 20 different named colors:
- Display as colored boxes with labels
- Include: red, blue, green, yellow, purple, orange, pink, brown, gray, black, white, navy, teal, coral, crimson, gold, indigo, lime, maroon, olive

**Expected Outcome**: Visual color palette reference

**Key Concepts**: 147 named CSS colors

---

### Assignment 12: Hexadecimal Colors
**Objective**: Master hexadecimal color notation.

**Requirements**:
- Convert these colors to hex: red, lime, blue, yellow, cyan, magenta
- Create 6-digit and 3-digit shorthand examples
- Build a gradient-like display from #000000 to #FFFFFF using 10 shades

**Expected Outcome**: Hex color proficiency

**Key Concepts**: #RRGGBB format, shorthand (#RGB)

---

### Assignment 13: RGB and RGBA Colors
**Objective**: Use RGB notation with transparency.

**Requirements**:
- Create solid colors using rgb(r, g, b)
- Create transparent overlays using rgba(r, g, b, a)
- Build overlapping circles showing transparency (alpha: 0.3, 0.5, 0.7)

**Expected Outcome**: Understanding of RGB and alpha transparency

**Key Concepts**: rgb() function, alpha channel (0-1)

---

### Assignment 14: HSL and HSLA Colors
**Objective**: Use HSL for intuitive color manipulation.

**Requirements**:
- Create a hue wheel showing colors at 30° intervals (0, 30, 60...330)
- Show saturation variations (0%, 50%, 100%) for same hue
- Show lightness variations (10%, 50%, 90%) for same hue

**Expected Outcome**: HSL color model understanding

**Key Concepts**: Hue (0-360), Saturation (%), Lightness (%)

---

### Assignment 15: Pixel Units
**Objective**: Use pixel units for precise sizing.

**Requirements**:
- Create boxes of exact sizes: 50px, 100px, 200px, 400px
- Style text at: 12px, 14px, 16px, 18px, 24px, 32px
- Create border widths: 1px, 2px, 4px, 8px

**Expected Outcome**: Pixel-perfect sizing understanding

**Key Concepts**: Absolute units, px for precision

---

### Assignment 16: Em Units
**Objective**: Use relative em units for scalable typography.

**Requirements**:
- Set base font-size on body (16px)
- Create headings using em: h1 (2em), h2 (1.5em), h3 (1.25em)
- Demonstrate em compounding in nested elements

**Expected Outcome**: Understanding em relativity to parent

**Key Concepts**: em relative to parent font-size

---

### Assignment 17: Rem Units
**Objective**: Use root-relative rem units.

**Requirements**:
- Set html font-size (16px)
- Create consistent spacing using rem (0.5rem, 1rem, 1.5rem, 2rem)
- Compare behavior vs em in nested contexts

**Expected Outcome**: Understanding rem consistency

**Key Concepts**: rem relative to root, avoiding compounding

---

### Assignment 18: Percentage Units
**Objective**: Use percentages for fluid layouts.

**Requirements**:
- Create a container with width: 80%
- Create child elements: 50%, 25%, 25% widths
- Make images responsive with max-width: 100%

**Expected Outcome**: Fluid, percentage-based layout

**Key Concepts**: Percentage relative to parent

---

### Assignment 19: Viewport Units (vh, vw)
**Objective**: Size elements relative to viewport.

**Requirements**:
- Create a full-screen hero section (100vh, 100vw)
- Create font-size responsive to viewport (5vw)
- Use vmin and vmax for aspect-ratio-independent sizing

**Expected Outcome**: Viewport-responsive elements

**Key Concepts**: vh, vw, vmin, vmax

---

### Assignment 20: Mixed Units Practice
**Objective**: Combine different units appropriately.

**Requirements**:
Create a card component using:
- rem for typography
- px for borders
- % for widths
- em for padding relative to font-size
- Justify each unit choice in comments

**Expected Outcome**: Strategic unit selection

**Key Concepts**: When to use which unit

---

## Module 3: Typography (Assignments 21-30)

### Assignment 21: Font Families
**Objective**: Implement proper font stacks.

**Requirements**:
- Create font stacks for: serif, sans-serif, monospace
- Include 3+ fallback fonts in each stack
- Apply to appropriate content types

**Example**:
```css
body { font-family: 'Segoe UI', Roboto, Arial, sans-serif; }
code { font-family: 'Fira Code', Consolas, monospace; }
```

**Expected Outcome**: Robust typography with fallbacks

---

### Assignment 22: Font Size and Weight
**Objective**: Control text size and thickness.

**Requirements**:
- Create a type scale: 12, 14, 16, 18, 20, 24, 30, 36, 48, 60px
- Show all font-weights: 100-900 (if font supports)
- Create bold, normal, and light text variations

**Expected Outcome**: Complete typography hierarchy

---

### Assignment 23: Font Style and Variant
**Objective**: Apply italic and special text styles.

**Requirements**:
- Use font-style: italic for emphasis
- Use font-variant: small-caps for headings
- Style quotes and definitions appropriately

**Expected Outcome**: Rich typographic variety

---

### Assignment 24: Line Height
**Objective**: Master vertical rhythm with line-height.

**Requirements**:
- Compare line-height: 1, 1.2, 1.5, 1.8, 2
- Create readable body text (line-height: 1.6)
- Adjust line-height for headings (tighter: 1.2)

**Expected Outcome**: Optimal reading experience

---

### Assignment 25: Text Alignment
**Objective**: Align text horizontally.

**Requirements**:
- Create sections with: left, center, right, justify alignment
- Center a heading, left-align body text
- Use justify for newspaper-style columns

**Expected Outcome**: Proper text alignment usage

---

### Assignment 26: Text Decoration
**Objective**: Add decorative text effects.

**Requirements**:
- Remove default link underlines
- Add custom underlines with text-decoration-color
- Use overline, underline, line-through
- Style strikethrough for deleted prices

**Expected Outcome**: Custom text decorations

---

### Assignment 27: Text Transform
**Objective**: Change text capitalization.

**Requirements**:
- Create uppercase headings
- Use capitalize for title case
- Use lowercase for email normalization display
- Style buttons with uppercase text

**Expected Outcome**: Controlled text casing

---

### Assignment 28: Letter and Word Spacing
**Objective**: Adjust horizontal spacing in text.

**Requirements**:
- Create dramatic letter-spacing for logo text (0.2em)
- Subtle letter-spacing for uppercase text (0.05em)
- Adjust word-spacing for justified text readability

**Expected Outcome**: Fine-tuned text spacing

---

### Assignment 29: Web Fonts (Google Fonts)
**Objective**: Integrate custom web fonts.

**Requirements**:
- Add Google Font to HTML (`<link>`)
- Select fonts: one serif, one sans-serif, one display
- Apply appropriate font-display property

**Example fonts**: Inter, Playfair Display, Roboto Mono

**Expected Outcome**: Custom typography implementation

---

### Assignment 30: Typography System
**Objective**: Build a complete typography system.

**Requirements**:
Create a modular type system with:
- Base font settings on body
- Heading styles (h1-h6)
- Paragraph styles
- List styles
- Inline elements (strong, em, code)
- Link styles

**Expected Outcome**: Reusable typography foundation

---

## Module 4: Backgrounds (Assignments 31-40)

### Assignment 31: Background Colors
**Objective**: Apply solid background colors.

**Requirements**:
- Style sections with distinct background colors
- Create light and dark theme sections
- Use transparent background for overlays

**Expected Outcome**: Color-blocked layout

---

### Assignment 32: Background Images
**Objective**: Add images as backgrounds.

**Requirements**:
- Add hero section with background-image
- Use url() syntax correctly
- Handle image paths (relative and absolute)

**Expected Outcome**: Image-based backgrounds

---

### Assignment 33: Background Repeat
**Objective**: Control background pattern tiling.

**Requirements**:
- Create repeating pattern background
- Use no-repeat for single images
- Use repeat-x and repeat-y for borders

**Expected Outcome**: Controlled background patterns

---

### Assignment 34: Background Position
**Objective**: Position background images precisely.

**Requirements**:
- Center a background image
- Position at: top left, bottom right, center
- Use percentage positioning
- Use exact pixel positions

**Expected Outcome**: Precisely positioned backgrounds

---

### Assignment 35: Background Size
**Objective**: Scale background images.

**Requirements**:
- Use cover for full-coverage backgrounds
- Use contain for complete image visibility
- Use exact sizes (px or %)
- Compare auto behavior

**Expected Outcome**: Properly sized backgrounds

---

### Assignment 36: Background Attachment
**Objective**: Create fixed/parallax backgrounds.

**Requirements**:
- Create fixed background that doesn't scroll
- Compare scroll (default) vs fixed
- Use local for scrolling containers

**Expected Outcome**: Fixed background effect

---

### Assignment 37: Background Shorthand
**Objective**: Use background shorthand property.

**Requirements**:
Write backgrounds using shorthand:
```css
background: color image position/size repeat attachment;
```
- Convert multiple properties to shorthand
- Maintain readability

**Expected Outcome**: Efficient background declarations

---

### Assignment 38: Multiple Backgrounds
**Objective**: Layer multiple backgrounds.

**Requirements**:
- Layer pattern over color
- Layer transparent overlay over image
- Create complex layered effects

**Example**:
```css
background: 
  linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
  url('image.jpg') center/cover;
```

**Expected Outcome**: Layered background compositions

---

### Assignment 39: Background Clip and Origin
**Objective**: Control background boundaries.

**Requirements**:
- Use background-clip: padding-box, border-box, content-box
- Create text-filled backgrounds (background-clip: text)
- Understand background-origin differences

**Expected Outcome**: Advanced background control

---

### Assignment 40: Background Blend Mode
**Objective**: Blend backgrounds together.

**Requirements**:
- Blend color with image (multiply, overlay, screen)
- Create artistic effects
- Combine with multiple backgrounds

**Expected Outcome**: Creative background blending

---

## Module 5: Box Model (Assignments 41-50)

### Assignment 41: Content Box
**Objective**: Understand the content area.

**Requirements**:
- Create boxes with explicit width/height
- Observe content area behavior
- Add content exceeding dimensions

**Expected Outcome**: Content area understanding

---

### Assignment 42: Padding
**Objective**: Add internal spacing.

**Requirements**:
- Use padding shorthand: 1 value, 2 values, 4 values
- Use individual properties (padding-top, etc.)
- Create consistent internal spacing

**Expected Outcome**: Controlled internal spacing

---

### Assignment 43: Borders
**Objective**: Add and style borders.

**Requirements**:
- Use border shorthand: width style color
- Create different border styles: solid, dashed, dotted, double
- Use individual side borders
- Create partial borders (bottom only, etc.)

**Expected Outcome**: Various border implementations

---

### Assignment 44: Border Radius
**Objective**: Create rounded corners.

**Requirements**:
- Create rounded buttons (border-radius: 4px, 8px, 20px)
- Create pill shapes (border-radius: 50px or 9999px)
- Create circles (border-radius: 50%)
- Use individual corner radii

**Expected Outcome**: Rounded element corners

---

### Assignment 45: Margin
**Objective**: Add external spacing.

**Requirements**:
- Use margin shorthand and individual properties
- Center elements with margin: 0 auto
- Create consistent vertical rhythm
- Understand margin collapse

**Expected Outcome**: Controlled external spacing

---

### Assignment 46: Box Sizing
**Objective**: Compare content-box vs border-box.

**Requirements**:
- Create two identical boxes
- Apply border-box to one, content-box to other
- Add same padding and borders
- Observe width/height differences

**Expected Outcome**: Box-sizing model understanding

---

### Assignment 47: Width and Height
**Objective**: Control element dimensions.

**Requirements**:
- Use min-width, max-width
- Use min-height, max-height
- Create responsive containers with constraints
- Handle content overflow

**Expected Outcome**: Flexible dimensioning

---

### Assignment 48: Overflow
**Objective**: Handle content overflow.

**Requirements**:
- Use overflow: visible, hidden, scroll, auto
- Apply overflow-x and overflow-y separately
- Create scrollable containers
- Hide overflowing images properly

**Expected Outcome**: Controlled content overflow

---

### Assignment 49: Box Shadow
**Objective**: Add depth with shadows.

**Requirements**:
- Create subtle shadows (cards, buttons)
- Create dramatic drop shadows
- Use multiple shadows
- Create inset shadows
- Spread radius effects

**Example**:
```css
box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), 0 2px 4px rgba(0, 0, 0, 0.06);
```

**Expected Outcome**: Depth through shadows

---

### Assignment 50: Outline
**Objective**: Use outlines vs borders.

**Requirements**:
- Create focus outlines for accessibility
- Show outline doesn't affect layout
- Use outline-offset
- Style custom focus states

**Expected Outcome**: Accessible focus indicators

---

## Module 6: Basic Layout and Components (Assignments 51-60)

### Assignment 51: Display Property
**Objective**: Control element display type.

**Requirements**:
- Convert inline elements to block
- Convert block elements to inline
- Use inline-block for layout
- Hide elements with display: none

**Expected Outcome**: Display type mastery

---

### Assignment 52: Centered Container
**Objective**: Create a standard centered layout container.

**Requirements**:
- Create container with max-width (1200px)
- Center with margin: 0 auto
- Add responsive padding
- Use box-sizing: border-box

**Expected Outcome**: Standard page container pattern

---

### Assignment 53: Simple Button
**Objective**: Style a complete button component.

**Requirements**:
- Reset default button styles
- Add padding, border-radius, colors
- Create hover and active states
- Make keyboard-focusable

**Expected Outcome**: Styled, accessible button

---

### Assignment 54: Navigation Menu
**Objective**: Create a horizontal navigation menu.

**Requirements**:
- Reset list styles (list-style: none)
- Make links inline or inline-block
- Style link states (hover, active)
- Add visual active indicator

**Expected Outcome**: Functional navigation bar

---

### Assignment 55: Simple Card
**Objective**: Build a basic card component.

**Requirements**:
- Card container with shadow
- Image at top
- Content padding
- Title and text styling
- Border radius

**Expected Outcome**: Reusable card pattern

---

### Assignment 56: Profile Card
**Objective**: Create a user profile card.

**Requirements**:
- Circular avatar image
- Centered layout
- Name and bio text
- Social links
- Hover effects

**Expected Outcome**: Social profile card

---

### Assignment 57: Styled Article
**Objective**: Style a complete text article.

**Requirements**:
- Article container
- Headline hierarchy (h1, h2, h3)
- Body text with proper line-height
- Styled lists and blockquotes
- Inline code styling

**Expected Outcome**: Readable article layout

---

### Assignment 58: Basic Form
**Objective**: Style a contact form.

**Requirements**:
- Style input fields and textareas
- Add focus states
- Style labels
- Submit button styling
- Form layout (labels above inputs)

**Expected Outcome**: Styled form interface

---

### Assignment 59: Footer Component
**Objective**: Create a page footer.

**Requirements**:
- Dark background, light text
- Multiple columns (links, contact, social)
- Copyright text
- Padding and spacing

**Expected Outcome**: Standard footer pattern

---

### Assignment 60: Beginner Capstone - Landing Page
**Objective**: Combine all beginner skills into a complete landing page.

**Requirements**:
Create a single-page website with:
- Header with navigation
- Hero section with background
- Features section with cards
- About section with text
- Contact form
- Footer

**Assessment Criteria**:
- Proper selector usage
- Consistent color scheme
- Typography hierarchy
- Box model application
- Clean code organization

**Expected Outcome**: Complete, styled landing page

---

# INTERMEDIATE LEVEL: Layouts & Responsive Design

> **Goal**: Master Flexbox, CSS Grid, positioning, responsive design, and intermediate components.

---

## Module 7: Positioning (Assignments 61-70)

### Assignment 61: Static Positioning (Default)
**Objective**: Understand default document flow.

**Requirements**:
- Create elements in normal flow
- Observe block vs inline behavior
- Document how position: static works (default)

**Expected Outcome**: Normal flow understanding

---

### Assignment 62: Relative Positioning
**Objective**: Offset elements from normal position.

**Requirements**:
- Use position: relative with top/left/right/bottom
- Create overlapping elements
- Observe space preservation in normal flow
- Use negative offsets

**Expected Outcome**: Relative positioning mastery

---

### Assignment 63: Absolute Positioning
**Objective**: Position elements relative to ancestor.

**Requirements**:
- Create positioned parent (position: relative)
- Position child absolutely
- Create corner badges
- Center with absolute + transform

**Expected Outcome**: Absolute positioning control

---

### Assignment 64: Fixed Positioning
**Objective**: Create viewport-fixed elements.

**Requirements**:
- Create fixed header/navigation
- Create fixed "back to top" button
- Handle content spacing for fixed elements
- Create fixed sidebar

**Expected Outcome**: Fixed UI elements

---

### Assignment 65: Sticky Positioning
**Objective**: Create scroll-aware sticky elements.

**Requirements**:
- Create sticky header that sticks on scroll
- Create sticky sidebar
- Set appropriate top value
- Handle sticky within containers

**Expected Outcome**: Sticky element behavior

---

### Assignment 66: Z-Index and Stacking
**Objective**: Control element stacking order.

**Requirements**:
- Create overlapping elements
- Control order with z-index
- Understand stacking context creation
- Debug z-index issues

**Expected Outcome**: Stacking context mastery

---

### Assignment 67: Dropdown Menu
**Objective**: Build a dropdown with positioning.

**Requirements**:
- Parent has position: relative
- Dropdown has position: absolute
- Show on hover
- Proper z-index layering

**Expected Outcome**: CSS dropdown menu

---

### Assignment 68: Tooltip
**Objective**: Create positioned tooltips.

**Requirements**:
- Hidden by default
- Show on hover
- Position above/below/left/right of trigger
- Add arrow using pseudo-element

**Expected Outcome**: Pure CSS tooltips

---

### Assignment 69: Modal Overlay
**Objective**: Create a centered modal design.

**Requirements**:
- Full-screen fixed overlay
- Centered modal box
- Close button positioning
- Background darkening

**Expected Outcome**: Modal component structure

---

### Assignment 70: Badge Positioning
**Objective**: Position notification badges.

**Requirements**:
- Create icon with badge
- Position badge at top-right corner
- Handle badge sizing
- Animate badge appearance

**Expected Outcome**: Notification badge pattern

---

## Module 8: Flexbox (Assignments 71-85)

### Assignment 71: Flex Container Basics
**Objective**: Create first flex container.

**Requirements**:
- Apply display: flex
- Observe default behavior
- Compare with block layout

**Expected Outcome**: Flex container understanding

---

### Assignment 72: Flex Direction
**Objective**: Control main axis direction.

**Requirements**:
- Use row, row-reverse, column, column-reverse
- Understand main axis vs cross axis
- Create horizontal and vertical layouts

**Expected Outcome**: Flex direction control

---

### Assignment 73: Justify Content
**Objective**: Align items along main axis.

**Requirements**:
- Use: flex-start, flex-end, center, space-between, space-around, space-evenly
- Create navigation with space-between
- Center items horizontally

**Expected Outcome**: Main axis alignment

---

### Assignment 74: Align Items
**Objective**: Align items along cross axis.

**Requirements**:
- Use: stretch, flex-start, flex-end, center, baseline
- Create vertically centered content
- Align items with different heights

**Expected Outcome**: Cross axis alignment

---

### Assignment 75: Flex Wrap
**Objective**: Handle wrapping in flex containers.

**Requirements**:
- Use flex-wrap: wrap, nowrap, wrap-reverse
- Create responsive card grid
- Control item widths for wrapping

**Expected Outcome**: Wrapping flex layouts

---

### Assignment 76: Align Content
**Objective**: Align multiple flex lines.

**Requirements**:
- Create wrapped flex container
- Use align-content values
- Distribute space between rows

**Expected Outcome**: Multi-line flex alignment

---

### Assignment 77: Flex Grow
**Objective**: Control how items grow.

**Requirements**:
- Use flex-grow: 0, 1, 2
- Create sidebar + main layout
- Proportional growth

**Expected Outcome**: Flex growing behavior

---

### Assignment 78: Flex Shrink
**Objective**: Control how items shrink.

**Requirements**:
- Use flex-shrink: 0, 1, 2
- Prevent sidebar from shrinking
- Handle overflow with shrinking

**Expected Outcome**: Flex shrinking behavior

---

### Assignment 79: Flex Basis
**Objective**: Set initial item size.

**Requirements**:
- Use flex-basis: auto, 0, fixed values
- Combine with grow/shrink
- Create fixed-width columns

**Expected Outcome**: Flex basis understanding

---

### Assignment 80: Flex Shorthand
**Objective**: Use flex shorthand property.

**Requirements**:
- Use flex: grow shrink basis
- Common patterns: flex: 1, flex: 0 0 auto
- Refactor longhand to shorthand

**Expected Outcome**: Flex shorthand mastery

---

### Assignment 81: Order Property
**Objective**: Reorder flex items visually.

**Requirements**:
- Change visual order without HTML changes
- Create mobile-first layout with reordering
- Use negative order values

**Expected Outcome**: Visual reordering

---

### Assignment 82: Align Self
**Objective**: Override alignment for individual items.

**Requirements**:
- Override align-items for specific children
- Create varied item alignments
- Center one item, stretch others

**Expected Outcome**: Individual item alignment

---

### Assignment 83: Flexbox Navigation
**Objective**: Build responsive navigation with flexbox.

**Requirements**:
- Logo left, links right (space-between)
- Vertically centered items
- Responsive wrapping
- Active link indicator

**Expected Outcome**: Flexbox navigation bar

---

### Assignment 84: Flexbox Card Layout
**Objective**: Create a card grid using flexbox.

**Requirements**:
- Responsive card grid (wrapping)
- Equal height cards
- Card content layout (image, text, button)
- Gap spacing (or margin fallback)

**Expected Outcome**: Responsive card grid

---

### Assignment 85: Holy Grail with Flexbox
**Objective**: Build classic layout with flexbox.

**Requirements**:
- Header, footer (full width)
- Main content + two sidebars
- Sticky footer
- Responsive collapse

**Expected Outcome**: Holy grail layout pattern

---

## Module 9: CSS Grid (Assignments 86-100)

### Assignment 86: Grid Container Basics
**Objective**: Create first grid container.

**Requirements**:
- Apply display: grid
- Define columns with grid-template-columns
- Define rows with grid-template-rows

**Expected Outcome**: Basic grid understanding

---

### Assignment 87: Fr Unit
**Objective**: Use fractional units for flexible sizing.

**Requirements**:
- Create equal columns with 1fr 1fr 1fr
- Mix fr with fixed values (200px 1fr 1fr)
- Understand fr distribution

**Expected Outcome**: Fr unit mastery

---

### Assignment 88: Gap Property
**Objective**: Add spacing between grid items.

**Requirements**:
- Use gap (shorthand)
- Use row-gap and column-gap
- Compare with margin approach

**Expected Outcome**: Grid spacing control

---

### Assignment 89: Repeat Function
**Objective**: Simplify repetitive track definitions.

**Requirements**:
- Use repeat(3, 1fr)
- Combine repeat with other values
- Create 12-column grid

**Expected Outcome**: Efficient grid definitions

---

### Assignment 90: Grid Line Placement
**Objective**: Place items by grid lines.

**Requirements**:
- Use grid-column-start, grid-column-end
- Use grid-row-start, grid-row-end
- Span multiple tracks
- Use negative line numbers

**Expected Outcome**: Precise item placement

---

### Assignment 91: Grid Column/Row Shorthand
**Objective**: Use shorthand placement.

**Requirements**:
- Use grid-column: start / end
- Use grid-row: start / end
- Span syntax: span 2

**Expected Outcome**: Shorthand placement

---

### Assignment 92: Grid Template Areas
**Objective**: Name grid areas for layout.

**Requirements**:
- Define grid-template-areas
- Assign items with grid-area
- Create semantic layouts
- Use dots (.) for empty cells

**Expected Outcome**: Named area layouts

---

### Assignment 93: Auto-Fill and Auto-Fit
**Objective**: Create responsive grids automatically.

**Requirements**:
- Use repeat(auto-fill, minmax(200px, 1fr))
- Compare auto-fill vs auto-fit behavior
- Create responsive gallery

**Expected Outcome**: Responsive grid patterns

---

### Assignment 94: Minmax Function
**Objective**: Set flexible track constraints.

**Requirements**:
- Use minmax(min, max)
- Combine with auto-fill
- Create responsive sidebar layouts

**Expected Outcome**: Flexible grid tracks

---

### Assignment 95: Grid Alignment
**Objective**: Align grid items and content.

**Requirements**:
- Use justify-items, align-items
- Use justify-content, align-content
- Use justify-self, align-self

**Expected Outcome**: Complete grid alignment

---

### Assignment 96: Implicit Grid
**Objective**: Handle auto-generated tracks.

**Requirements**:
- Understand implicit vs explicit grid
- Use grid-auto-rows, grid-auto-columns
- Control auto-flow direction

**Expected Outcome**: Implicit grid control

---

### Assignment 97: Dense Grid Packing
**Objective**: Use dense packing algorithm.

**Requirements**:
- Use grid-auto-flow: dense
- Fill gaps in grid
- Create masonry-like layouts

**Expected Outcome**: Dense grid packing

---

### Assignment 98: Dashboard Layout
**Objective**: Build a dashboard with CSS Grid.

**Requirements**:
- Header spanning full width
- Sidebar navigation
- Main content with widget grid
- Responsive collapse

**Expected Outcome**: Dashboard layout

---

### Assignment 99: Magazine Layout
**Objective**: Create editorial-style layout.

**Requirements**:
- Large featured article
- Mixed article sizes
- Overlapping elements
- Named grid areas

**Expected Outcome**: Magazine-style grid

---

### Assignment 100: Photo Gallery
**Objective**: Build responsive image gallery.

**Requirements**:
- Auto-fill responsive grid
- Mixed image sizes (spanning)
- Hover effects
- Lightbox-ready structure

**Expected Outcome**: Responsive gallery grid

---

## Module 10: Responsive Design (Assignments 101-115)

### Assignment 101: Mobile-First Approach
**Objective**: Write mobile-first CSS.

**Requirements**:
- Start with mobile styles (no media query)
- Add min-width breakpoints for larger screens
- Document mobile-first benefits

**Expected Outcome**: Mobile-first methodology

---

### Assignment 102: Basic Media Queries
**Objective**: Write standard media queries.

**Requirements**:
- Use @media (min-width: value)
- Create breakpoints: 576px, 768px, 992px, 1200px
- Change layout at each breakpoint

**Expected Outcome**: Media query basics

---

### Assignment 103: Responsive Typography
**Objective**: Scale text responsively.

**Requirements**:
- Use clamp() for fluid typography
- Scale headings appropriately
- Adjust line-height for different sizes

**Example**:
```css
h1 { font-size: clamp(1.5rem, 5vw, 3rem); }
```

**Expected Outcome**: Fluid typography

---

### Assignment 104: Responsive Images
**Objective**: Make images responsive.

**Requirements**:
- Use max-width: 100%
- Maintain aspect ratio
- Use object-fit for cropping
- Handle different orientations

**Expected Outcome**: Flexible images

---

### Assignment 105: Responsive Navigation
**Objective**: Build adaptive navigation.

**Requirements**:
- Mobile: hamburger menu (structure)
- Tablet: simplified layout
- Desktop: full horizontal nav
- Use media queries for transitions

**Expected Outcome**: Adaptive navigation

---

### Assignment 106: Breakpoint Strategy
**Objective**: Implement consistent breakpoints.

**Requirements**:
- Define breakpoint CSS variables
- Create reusable breakpoint pattern
- Document breakpoint usage
- Test at each breakpoint

**Expected Outcome**: Systematic breakpoints

---

### Assignment 107: Responsive Cards
**Objective**: Create adaptive card layouts.

**Requirements**:
- Mobile: single column
- Tablet: two columns
- Desktop: three or four columns
- Smooth transitions

**Expected Outcome**: Responsive card grid

---

### Assignment 108: Aspect Ratio Property
**Objective**: Use CSS aspect-ratio.

**Requirements**:
- Create 16:9 video containers
- Create 1:1 avatar containers
- Handle content within aspect ratio

**Expected Outcome**: Intrinsic aspect ratios

---

### Assignment 109: Container Queries Basics
**Objective**: Introduction to container queries.

**Requirements**:
- Define container with container-type
- Write @container queries
- Compare with media queries

**Expected Outcome**: Container query introduction

---

### Assignment 110: Viewport Units for Layout
**Objective**: Use vh/vw for responsive layouts.

**Requirements**:
- Full-height sections (100vh)
- Calculate with calc(100vh - header)
- Handle mobile browser issues (dvh)

**Expected Outcome**: Viewport-based layouts

---

### Assignment 111: Responsive Table
**Objective**: Make tables usable on mobile.

**Requirements**:
- Horizontal scroll wrapper
- Data-label approach for mobile
- Card-based transformation
- Maintain accessibility

**Expected Outcome**: Mobile-friendly tables

---

### Assignment 112: Print Stylesheet
**Objective**: Create print-optimized styles.

**Requirements**:
- Use @media print
- Hide navigation, footer
- Adjust typography for print
- Handle page breaks

**Expected Outcome**: Print-ready styles

---

### Assignment 113: Responsive Form
**Objective**: Create adaptive form layout.

**Requirements**:
- Stack on mobile
- Side-by-side labels on desktop
- Touch-friendly input sizes
- Responsive button sizing

**Expected Outcome**: Adaptive form layout

---

### Assignment 114: CSS Custom Properties for Responsive
**Objective**: Use variables for responsive values.

**Requirements**:
- Change variable values in media queries
- Create responsive spacing systems
- Theme-like responsive adjustments

**Expected Outcome**: Variable-based responsive CSS

---

### Assignment 115: Intermediate Capstone - Blog Layout
**Objective**: Build complete responsive blog.

**Requirements**:
- Responsive header with navigation
- Blog post cards (responsive grid)
- Sidebar (collapses on mobile)
- Footer with columns
- Working at all breakpoints

**Expected Outcome**: Complete responsive blog

---

## Module 11: Transitions and Transforms (Assignments 116-125)

### Assignment 116: Basic Transitions
**Objective**: Add smooth property changes.

**Requirements**:
- Use transition-property, transition-duration
- Transition colors on hover
- Transition multiple properties

**Expected Outcome**: Basic transitions

---

### Assignment 117: Timing Functions
**Objective**: Control transition easing.

**Requirements**:
- Use: ease, linear, ease-in, ease-out, ease-in-out
- Create custom cubic-bezier
- Compare different easings visually

**Expected Outcome**: Transition easing understanding

---

### Assignment 118: Transition Shorthand
**Objective**: Use transition shorthand.

**Requirements**:
- Combine all transition properties
- Multiple transitions in one declaration
- Use transition: all cautiously

**Expected Outcome**: Efficient transition declarations

---

### Assignment 119: 2D Transforms - Translate
**Objective**: Move elements with translate.

**Requirements**:
- Use translateX, translateY, translate
- Center with transform: translate(-50%, -50%)
- Combine with transitions for animation

**Expected Outcome**: Translation transforms

---

### Assignment 120: 2D Transforms - Scale
**Objective**: Resize elements with scale.

**Requirements**:
- Grow on hover with scale
- Use scaleX, scaleY separately
- Combine scale with translate

**Expected Outcome**: Scale transforms

---

### Assignment 121: 2D Transforms - Rotate
**Objective**: Rotate elements.

**Requirements**:
- Rotate images on hover
- Create spinning animation
- Use different angle units (deg, turn)

**Expected Outcome**: Rotation transforms

---

### Assignment 122: 2D Transforms - Skew
**Objective**: Skew elements.

**Requirements**:
- Create slanted sections
- Use skewX, skewY
- Compensate child skew

**Expected Outcome**: Skew transforms

---

### Assignment 123: Transform Origin
**Objective**: Change transformation pivot point.

**Requirements**:
- Rotate from corner vs center
- Scale from different origins
- Use keyword, percentage, and length values

**Expected Outcome**: Transform origin control

---

### Assignment 124: Combining Transforms
**Objective**: Apply multiple transforms.

**Requirements**:
- Combine translate, rotate, scale
- Understand transform order importance
- Create complex hover effects

**Expected Outcome**: Combined transforms

---

### Assignment 125: Animated Button
**Objective**: Build button with transition effects.

**Requirements**:
- Hover: scale up, shadow, color change
- Active: scale down (pressed)
- Smooth transitions
- Focus state

**Expected Outcome**: Polished interactive button

---

## Module 12: Intermediate Components (Assignments 126-140)

### Assignment 126: Accordion Component
**Objective**: Build expandable accordion.

**Requirements**:
- Use :checked pseudo-class
- Hide/show content panels
- Rotate arrow indicator
- Smooth height transition (limited)

**Expected Outcome**: CSS-only accordion

---

### Assignment 127: Tabs Component
**Objective**: Create tab interface.

**Requirements**:
- Radio button technique
- Styled tab buttons
- Content panel switching
- Active tab indicator

**Expected Outcome**: CSS-only tabs

---

### Assignment 128: Timeline Layout
**Objective**: Build vertical timeline.

**Requirements**:
- Alternating left/right entries
- Connecting line (pseudo-element)
- Circle markers
- Responsive (single column mobile)

**Expected Outcome**: Event timeline design

---

### Assignment 129: Pricing Table
**Objective**: Create pricing comparison.

**Requirements**:
- Multiple pricing tiers
- Feature lists
- Highlighted "recommended" tier
- Responsive stack

**Expected Outcome**: Pricing table component

---

### Assignment 130: Testimonial Slider Structure
**Objective**: Design testimonial layout.

**Requirements**:
- Quote styling
- Avatar and author info
- Star rating display
- Card-based layout

**Expected Outcome**: Testimonial component

---

### Assignment 131: Feature List
**Objective**: Style feature highlight section.

**Requirements**:
- Icon + text layout
- Grid or flex for multiple features
- Hover effects
- Responsive behavior

**Expected Outcome**: Feature section

---

### Assignment 132: Statistics Counter Display
**Objective**: Design stats showcase.

**Requirements**:
- Large numbers prominently displayed
- Labels and icons
- Clean grid layout
- Visual separators

**Expected Outcome**: Stats display component

---

### Assignment 133: Team Member Cards
**Objective**: Create team section.

**Requirements**:
- Photo with overlay on hover
- Social links revealed on hover
- Bio text styling
- Grid layout

**Expected Outcome**: Team section design

---

### Assignment 134: Call-to-Action Section
**Objective**: Design compelling CTA.

**Requirements**:
- Background (color/image)
- Centered content
- Prominent button
- Responsive text sizing

**Expected Outcome**: CTA component

---

### Assignment 135: Newsletter Signup
**Objective**: Style email signup form.

**Requirements**:
- Input + button inline
- Responsive stack on mobile
- Focus states
- Success/error states

**Expected Outcome**: Newsletter form

---

### Assignment 136: Breadcrumb Navigation
**Objective**: Create breadcrumb trail.

**Requirements**:
- Separator styling (/ or >)
- Current page styling
- Hover effects
- Responsive truncation

**Expected Outcome**: Breadcrumb component

---

### Assignment 137: Pagination
**Objective**: Build page navigation.

**Requirements**:
- Number buttons
- Active page indicator
- Previous/next buttons
- Disabled states

**Expected Outcome**: Pagination component

---

### Assignment 138: Progress Bar
**Objective**: Create progress indicator.

**Requirements**:
- Track and fill elements
- Percentage width
- Animated fill
- Label overlay

**Expected Outcome**: Progress bar component

---

### Assignment 139: Tags/Chips
**Objective**: Style tag components.

**Requirements**:
- Pill-shaped tags
- Remove button styling
- Color variations
- Hover/active states

**Expected Outcome**: Tag component set

---

### Assignment 140: Intermediate Capstone - E-commerce Product Grid
**Objective**: Build product listing page.

**Requirements**:
- Responsive product grid
- Product cards (image, title, price, rating)
- Hover effects for cards
- Filter sidebar (static)
- Pagination
- Mobile responsive

**Expected Outcome**: E-commerce product listing

---

# ADVANCED LEVEL: Animations & Modern Techniques

> **Goal**: Master CSS animations, 3D transforms, modern CSS features, filters, and advanced layout patterns.

---

## Module 13: CSS Animations (Assignments 141-155)

### Assignment 141: Keyframe Basics
**Objective**: Create first keyframe animation.

**Requirements**:
- Define @keyframes with from/to
- Apply animation-name to element
- Set animation-duration

**Expected Outcome**: Basic keyframe understanding

---

### Assignment 142: Multi-Step Keyframes
**Objective**: Create animations with percentages.

**Requirements**:
- Use 0%, 25%, 50%, 75%, 100%
- Create complex motion paths
- Animate multiple properties

**Expected Outcome**: Multi-step sequences

---

### Assignment 143: Animation Timing Functions
**Objective**: Control animation easing.

**Requirements**:
- Apply different timing functions
- Create custom cubic-bezier
- Use steps() for frame-by-frame

**Expected Outcome**: Easing control mastery

---

### Assignment 144: Animation Iteration
**Objective**: Control loop behavior.

**Requirements**:
- Use infinite for continuous animations
- Set specific iteration counts
- Understand iteration behavior

**Expected Outcome**: Loop control

---

### Assignment 145: Animation Direction
**Objective**: Control playback direction.

**Requirements**:
- Use: normal, reverse, alternate, alternate-reverse
- Create ping-pong effects
- Combine with iteration

**Expected Outcome**: Direction control

---

### Assignment 146: Animation Fill Mode
**Objective**: Control before/after animation states.

**Requirements**:
- Use: none, forwards, backwards, both
- Maintain end state with forwards
- Pre-apply start state with backwards

**Expected Outcome**: Fill mode understanding

---

### Assignment 147: Animation Shorthand
**Objective**: Use animation shorthand property.

**Requirements**:
- Combine all animation properties
- Multiple animations on one element
- Proper value ordering

**Expected Outcome**: Efficient animation declarations

---

### Assignment 148: Loading Spinner
**Objective**: Create animated loading indicator.

**Requirements**:
- Spinning circle animation
- Pulsing dots variation
- Bouncing bar variation

**Expected Outcome**: Loading animation components

---

### Assignment 149: Fade Animations
**Objective**: Create fade-in/fade-out effects.

**Requirements**:
- Fade in from transparent
- Fade out animation
- Combine with translate for entrance

**Expected Outcome**: Fade animation effects

---

### Assignment 150: Slide Animations
**Objective**: Create sliding entrance effects.

**Requirements**:
- Slide in from left/right/top/bottom
- Slide with fade combination
- Staggered slide animations

**Expected Outcome**: Slide animations

---

### Assignment 151: Scale Pulse
**Objective**: Create attention-grabbing pulse.

**Requirements**:
- Scale up and down infinitely
- Ring pulse effect (expanding border)
- Heartbeat animation

**Expected Outcome**: Pulse effects

---

### Assignment 152: Animation Play State
**Objective**: Pause and resume animations.

**Requirements**:
- Use animation-play-state
- Pause on hover
- Toggle with checkboxes (CSS-only)

**Expected Outcome**: Animation control

---

### Assignment 153: Animated Menu Icon
**Objective**: Create hamburger to X animation.

**Requirements**:
- Three-line hamburger icon
- Transform to X on active
- Smooth line transitions

**Expected Outcome**: Animated menu toggle icon

---

### Assignment 154: Typewriter Effect
**Objective**: Create typing animation.

**Requirements**:
- Reveal text character by character
- Blinking cursor
- Use width animation with steps()

**Expected Outcome**: Typewriter text effect

---

### Assignment 155: Animated Background
**Objective**: Animate background properties.

**Requirements**:
- Moving gradient background
- Color cycling
- Parallax-like movement

**Expected Outcome**: Animated backgrounds

---

## Module 14: 3D Transforms (Assignments 156-165)

### Assignment 156: Perspective
**Objective**: Understand 3D perspective.

**Requirements**:
- Apply perspective to parent
- Compare different perspective values
- Use perspective-origin

**Expected Outcome**: 3D perspective understanding

---

### Assignment 157: RotateX and RotateY
**Objective**: Rotate in 3D space.

**Requirements**:
- Flip cards using rotateY
- Create door-opening rotateX
- Combine rotations

**Expected Outcome**: 3D rotations

---

### Assignment 158: TranslateZ
**Objective**: Move along Z-axis.

**Requirements**:
- Bring elements forward/back
- Create depth effect
- Combine with other transforms

**Expected Outcome**: Z-axis movement

---

### Assignment 159: Transform Style
**Objective**: Preserve 3D for children.

**Requirements**:
- Use transform-style: preserve-3d
- Create nested 3D elements
- Build 3D objects

**Expected Outcome**: 3D transform preservation

---

### Assignment 160: 3D Flip Card
**Objective**: Create interactive flip card.

**Requirements**:
- Front and back faces
- Use backface-visibility: hidden
- Flip on hover with rotateY(180deg)

**Expected Outcome**: 3D flip card component

---

### Assignment 161: 3D Button
**Objective**: Create button with 3D effect.

**Requirements**:
- Pseudo-element for depth
- Press down on active
- Light/shadow simulation

**Expected Outcome**: 3D button effect

---

### Assignment 162: 3D Cube
**Objective**: Build a CSS cube.

**Requirements**:
- Six faces positioned correctly
- Spin animation
- Interactive rotation

**Expected Outcome**: 3D rotating cube

---

### Assignment 163: Card Stack
**Objective**: Create stacked card effect.

**Requirements**:
- Multiple cards with z-offset
- Spread on hover
- 3D rotation on spread

**Expected Outcome**: 3D card stack

---

### Assignment 164: Page Flip
**Objective**: Create book page flip effect.

**Requirements**:
- Page rotation around edge
- Reveal next page
- Realistic curve simulation

**Expected Outcome**: Page flip animation

---

### Assignment 165: 3D Gallery
**Objective**: Build 3D image carousel.

**Requirements**:
- Images arranged in circle
- Rotate to show different images
- Navigation controls

**Expected Outcome**: 3D image carousel

---

## Module 15: Modern CSS Functions (Assignments 166-175)

### Assignment 166: CSS Variables (Custom Properties)
**Objective**: Define and use CSS variables.

**Requirements**:
- Define variables on :root
- Use var() to apply
- Override in nested scopes

**Expected Outcome**: Variable fundamentals

---

### Assignment 167: Variable Theming
**Objective**: Create theme system with variables.

**Requirements**:
- Define color palette variables
- Light and dark theme variables
- Toggle themes with class

**Expected Outcome**: Theme system

---

### Assignment 168: Calc() Function
**Objective**: Perform calculations in CSS.

**Requirements**:
- Combine units with calc()
- Full width minus margin: calc(100% - 40px)
- Dynamic column widths

**Expected Outcome**: Dynamic calculations

---

### Assignment 169: Min() and Max()
**Objective**: Use comparison functions.

**Requirements**:
- Responsive widths with min()
- Max font sizes
- Combine with calc()

**Expected Outcome**: Comparison function usage

---

### Assignment 170: Clamp() Function
**Objective**: Create fluid responsive values.

**Requirements**:
- Fluid typography: clamp(1rem, 4vw, 2rem)
- Responsive spacing
- Constrained containers

**Expected Outcome**: Fluid value clamping

---

### Assignment 171: CSS Counters
**Objective**: Auto-number with CSS counters.

**Requirements**:
- Use counter-reset, counter-increment
- Number headings automatically
- Nested list numbering

**Expected Outcome**: CSS automatic numbering

---

### Assignment 172: Attr() Function
**Objective**: Use HTML attributes in CSS.

**Requirements**:
- Display tooltip text from data-attribute
- Create custom badges
- Dynamic content insertion

**Expected Outcome**: Attribute value usage

---

### Assignment 173: Filter Property
**Objective**: Apply visual filters to elements.

**Requirements**:
- Use: blur, brightness, contrast, grayscale
- Use: saturate, hue-rotate, invert, sepia
- Combine multiple filters

**Expected Outcome**: CSS filter effects

---

### Assignment 174: Backdrop Filter
**Objective**: Apply filters to background.

**Requirements**:
- Create frosted glass effect
- Blur background behind modal
- Combine with semi-transparent backgrounds

**Expected Outcome**: Backdrop filter effects

---

### Assignment 175: Blend Modes
**Objective**: Blend elements with background.

**Requirements**:
- Use mix-blend-mode
- Use background-blend-mode
- Create overlay effects

**Expected Outcome**: Blend mode mastery

---

## Module 16: Advanced Selectors (Assignments 176-185)

### Assignment 176: Attribute Selectors
**Objective**: Select elements by attributes.

**Requirements**:
- Use [attr], [attr=value], [attr^=], [attr$=], [attr*=]
- Style external links differently
- Target specific input types

**Expected Outcome**: Attribute selector mastery

---

### Assignment 177: Nth-Child Patterns
**Objective**: Select elements by position.

**Requirements**:
- Use :nth-child(odd/even)
- Use :nth-child(3n), :nth-child(3n+1)
- Create striped tables

**Expected Outcome**: Nth-child selection

---

### Assignment 178: Nth-of-type Selectors
**Objective**: Type-specific position selection.

**Requirements**:
- Compare :nth-child vs :nth-of-type
- Select every 3rd paragraph
- Complex patterns

**Expected Outcome**: Nth-of-type understanding

---

### Assignment 179: Negation Pseudo-Class (:not)
**Objective**: Exclude elements from selection.

**Requirements**:
- Style all paragraphs except .intro
- Exclude last-child from margins
- Combine :not with other selectors

**Expected Outcome**: Negation selection

---

### Assignment 180: Form State Pseudo-Classes
**Objective**: Style forms based on state.

**Requirements**:
- Style :valid, :invalid inputs
- Style :required vs optional
- Style :checked checkboxes/radios
- Style :disabled, :enabled

**Expected Outcome**: Form state styling

---

### Assignment 181: Focus Pseudo-Classes
**Objective**: Handle focus states properly.

**Requirements**:
- Use :focus, :focus-visible, :focus-within
- Create accessible focus rings
- Parent styling with :focus-within

**Expected Outcome**: Focus state handling

---

### Assignment 182: Pseudo-Element ::before/::after
**Objective**: Create decorative pseudo-elements.

**Requirements**:
- Add quote marks with ::before/::after
- Create decorative shapes
- Create custom list markers

**Expected Outcome**: Pseudo-element decorations

---

### Assignment 183: Advanced Pseudo-Elements
**Objective**: Use specialized pseudo-elements.

**Requirements**:
- Style ::first-letter for drop caps
- Style ::first-line differently
- Customize ::selection colors
- Style ::placeholder

**Expected Outcome**: Specialized pseudo-elements

---

### Assignment 184: :has() Relational Selector
**Objective**: Select parent based on child.

**Requirements**:
- Style cards that contain images
- Style forms with invalid inputs
- Parent-child relationship styling

**Expected Outcome**: Relational selection

---

### Assignment 185: Complex Selector Combinations
**Objective**: Build sophisticated selectors.

**Requirements**:
- Combine multiple selector types
- Create highly specific selections
- Document specificity values

**Expected Outcome**: Complex selector mastery

---

## Module 17: Advanced Layouts (Assignments 186-195)

### Assignment 186: CSS Multi-Column Layout
**Objective**: Create newspaper-style columns.

**Requirements**:
- Use column-count
- Use column-gap, column-rule
- Handle column-span

**Expected Outcome**: Multi-column text layout

---

### Assignment 187: Subgrid
**Objective**: Use CSS subgrid for nested alignment.

**Requirements**:
- Create parent grid
- Child uses subgrid for tracks
- Align nested elements to parent grid

**Expected Outcome**: Subgrid alignment

---

### Assignment 188: Masonry-like Layout
**Objective**: Create masonry layout with CSS.

**Requirements**:
- Use columns for simple masonry
- Use Grid with auto-rows variation
- Handle content of different heights

**Expected Outcome**: Masonry-style layouts

---

### Assignment 189: Sticky Sidebar
**Objective**: Create sidebar that scrolls with sections.

**Requirements**:
- Position: sticky sidebar
- Handle overflow properly
- Multiple sticky elements

**Expected Outcome**: Scroll-aware sidebar

---

### Assignment 190: Centering Everything
**Objective**: Master all centering techniques.

**Requirements**:
- Flexbox centering
- Grid centering
- Absolute + transform centering
- Margin auto centering
- Table-cell (legacy) method

**Expected Outcome**: Complete centering mastery

---

### Assignment 191: Full-Bleed Layout
**Objective**: Break out of container for full-width elements.

**Requirements**:
- Centered content container
- Full-width sections breaking out
- Use calc() or Grid techniques

**Expected Outcome**: Full-bleed sections

---

### Assignment 192: Overlapping Elements
**Objective**: Create intentional overlaps.

**Requirements**:
- Use negative margins
- Use Grid overlapping
- Use absolute positioning
- Create design-forward overlaps

**Expected Outcome**: Controlled element overlaps

---

### Assignment 193: Scroll Snap
**Objective**: Create snap points for scrolling.

**Requirements**:
- Use scroll-snap-type
- Use scroll-snap-align
- Create fullscreen section scrolling
- Horizontal carousel snap

**Expected Outcome**: Scroll snap layouts

---

### Assignment 194: Logical Properties
**Objective**: Use writing-mode-aware properties.

**Requirements**:
- Replace margin-left with margin-inline-start
- Use block-size, inline-size
- Handle RTL languages

**Expected Outcome**: Logical property usage

---

### Assignment 195: Advanced Capstone - Dashboard with Grid
**Objective**: Build complex dashboard layout.

**Requirements**:
- Named grid areas
- Responsive grid changes
- Nested grids for widgets
- Sidebar navigation
- Collapsible panels
- Charts/stats areas

**Expected Outcome**: Complete dashboard layout

---

## Module 18: Advanced Components (Assignments 196-210)

### Assignment 196: Custom Checkbox
**Objective**: Style custom checkbox with CSS.

**Requirements**:
- Hide default checkbox
- Create custom indicator with pseudo-elements
- Animate check mark
- Handle focus and disabled states

**Expected Outcome**: Custom checkbox component

---

### Assignment 197: Custom Radio Buttons
**Objective**: Style custom radio buttons.

**Requirements**:
- Hide default radio
- Create circular indicator
- Inner dot animation
- Group behavior preservation

**Expected Outcome**: Custom radio buttons

---

### Assignment 198: Toggle Switch
**Objective**: Create iOS-style toggle.

**Requirements**:
- Track and thumb elements
- Slide animation
- Color change on toggle
- Label association

**Expected Outcome**: Toggle switch component

---

### Assignment 199: Range Slider Styling
**Objective**: Customize range input.

**Requirements**:
- Style track and thumb
- Cross-browser compatibility
- Visual feedback on interaction

**Expected Outcome**: Custom range slider

---

### Assignment 200: Custom Select Dropdown
**Objective**: Style select element appearance.

**Requirements**:
- Override default appearance
- Custom arrow indicator
- Styled options (limited)
- Focus states

**Expected Outcome**: Styled select element

---

### Assignment 201: File Upload Button
**Objective**: Style file input.

**Requirements**:
- Hide default input
- Create custom button
- Show selected filename area
- Drag-drop zone styling

**Expected Outcome**: Custom file upload UI

---

### Assignment 202: Glassmorphism Card
**Objective**: Create frosted glass effect.

**Requirements**:
- backdrop-filter: blur
- Semi-transparent background
- Subtle border
- Background gradient visible

**Expected Outcome**: Glassmorphism component

---

### Assignment 203: Neumorphism Component
**Objective**: Create soft UI (neumorphism).

**Requirements**:
- Soft inset shadows
- Subtle outset shadows
- Pressed/unpressed states
- Color matching shadows

**Expected Outcome**: Neumorphism UI elements

---

### Assignment 204: Ribbon Banner
**Objective**: Create corner ribbon effect.

**Requirements**:
- Positioned ribbon with transform
- Folded edge effect with pseudo-elements
- Text inside ribbon

**Expected Outcome**: Corner ribbon badge

---

### Assignment 205: Notification Badge
**Objective**: Create animated notification indicator.

**Requirements**:
- Positioned badge on icon
- Pulse animation
- Counter display
- Show/hide logic

**Expected Outcome**: Notification badge component

---

### Assignment 206: Animated Underline
**Objective**: Create expanding underline on hover.

**Requirements**:
- Underline grows from center/left/right
- Use pseudo-element
- Smooth transition

**Expected Outcome**: Animated link underlines

---

### Assignment 207: Image Comparison Slider
**Objective**: Create before/after slider (structure).

**Requirements**:
- Two overlapping images
- Divider styling
- Clip-path for reveal
- Handle styling

**Expected Outcome**: Image comparison UI structure

---

### Assignment 208: Tooltip Variations
**Objective**: Create multiple tooltip styles.

**Requirements**:
- Top, bottom, left, right positioning
- Arrow variations
- Animated appearance
- Different color schemes

**Expected Outcome**: Tooltip component library

---

### Assignment 209: Skeleton Loading
**Objective**: Create content placeholder effect.

**Requirements**:
- Gray placeholder shapes
- Shimmer animation
- Match content structure
- Smooth fade out

**Expected Outcome**: Skeleton loading screens

---

### Assignment 210: Advanced Capstone - Portfolio Gallery
**Objective**: Build animated portfolio gallery.

**Requirements**:
- Filterable grid (structure ready)
- Hover reveal details
- Lightbox structure
- Smooth animations throughout
- Responsive design

**Expected Outcome**: Complete portfolio gallery

---

# EXPERT LEVEL: Complex Designs & Optimization

> **Goal**: Master professional CSS architecture, performance optimization, complex CSS-only components, accessibility, and modern CSS features.

---

## Module 19: CSS Architecture (Assignments 211-220)

### Assignment 211: BEM Methodology
**Objective**: Implement BEM naming convention.

**Requirements**:
- Structure: Block__Element--Modifier
- Build component using BEM
- Document class hierarchy
- Create style guidelines

**Expected Outcome**: BEM implementation mastery

---

### Assignment 212: CSS File Organization
**Objective**: Structure large CSS projects.

**Requirements**:
- Create folder structure (base, components, layouts, utilities)
- Main entry file with imports
- Logical file separation
- Documentation for organization

**Expected Outcome**: Scalable CSS architecture

---

### Assignment 213: Utility Classes
**Objective**: Build utility class system.

**Requirements**:
- Spacing utilities (m-1, p-2, etc.)
- Color utilities
- Typography utilities
- Display utilities
- Responsive prefixes

**Expected Outcome**: Utility-first CSS system

---

### Assignment 214: Component Library Structure
**Objective**: Organize component-based CSS.

**Requirements**:
- Isolated component files
- Consistent naming conventions
- Documented component API
- Variation patterns

**Expected Outcome**: Component library architecture

---

### Assignment 215: CSS Reset vs Normalize
**Objective**: Implement and compare resets.

**Requirements**:
- Create custom reset
- Implement Normalize.css approach
- Document differences
- Choose appropriate approach

**Expected Outcome**: Understanding of CSS resets

---

### Assignment 216: Cascade Layers (@layer)
**Objective**: Use CSS cascade layers.

**Requirements**:
- Define layer order
- Organize styles into layers (reset, base, components, utilities)
- Manage specificity with layers
- Create scalable architecture

**Expected Outcome**: Cascade layer mastery

---

### Assignment 217: CSS Nesting
**Objective**: Use native CSS nesting.

**Requirements**:
- Nest selectors properly
- Nest media queries
- Follow nesting best practices
- Compare with preprocessor nesting

**Expected Outcome**: Native nesting proficiency

---

### Assignment 218: Critical CSS Strategy
**Objective**: Implement critical CSS extraction concept.

**Requirements**:
- Identify above-the-fold styles
- Inline critical CSS
- Load remaining CSS asynchronously
- Document process

**Expected Outcome**: Critical CSS understanding

---

### Assignment 219: CSS Documentation
**Objective**: Document CSS for teams.

**Requirements**:
- Create style guide documentation
- Document variables and mixins
- Usage examples
- Browser support notes

**Expected Outcome**: Professional CSS documentation

---

### Assignment 220: Refactoring Poor CSS
**Objective**: Improve existing poorly-written CSS.

**Provided CSS**: Messy, duplicated, over-specific CSS

**Requirements**:
- Identify issues (specificity battles, duplication, !important abuse)
- Refactor to clean architecture
- Reduce file size
- Maintain functionality

**Expected Outcome**: CSS refactoring skills

---

## Module 20: Performance Optimization (Assignments 221-230)

### Assignment 221: Selector Performance
**Objective**: Write performant selectors.

**Requirements**:
- Avoid deep nesting
- Reduce universal/attribute selectors where possible
- Benchmark selector strategies
- Document best practices

**Expected Outcome**: Efficient selector writing

---

### Assignment 222: Hardware Acceleration
**Objective**: Trigger GPU acceleration.

**Requirements**:
- Use transform for movement (not top/left)
- Use opacity for fade (not filter)
- Understand composite layers
- Measure performance difference

**Expected Outcome**: GPU acceleration knowledge

---

### Assignment 223: Will-Change Property
**Objective**: Properly hint browser for animations.

**Requirements**:
- Use will-change correctly
- Apply before animation starts
- Remove after animation ends
- Avoid overuse

**Expected Outcome**: Will-change best practices

---

### Assignment 224: CSS Containment
**Objective**: Use contain property for optimization.

**Requirements**:
- Use contain: layout, paint, size
- Isolate component rendering
- Reduce layout recalculation
- Measure impact

**Expected Outcome**: CSS containment usage

---

### Assignment 225: Reducing Repaints
**Objective**: Minimize expensive style operations.

**Requirements**:
- Identify repaint-triggering properties
- Batch style changes
- Use class toggling vs style manipulation
- Profile with DevTools

**Expected Outcome**: Repaint optimization

---

### Assignment 226: Font Loading Optimization
**Objective**: Optimize web font loading.

**Requirements**:
- Use font-display property
- Subset fonts
- Preload critical fonts
- Provide appropriate fallbacks

**Expected Outcome**: Optimized font loading

---

### Assignment 227: CSS Minification
**Objective**: Minimize CSS file size.

**Requirements**:
- Remove unused CSS concept
- Minification strategies
- Combine files appropriately
- Gzip consideration

**Expected Outcome**: CSS minification understanding

---

### Assignment 228: Lazy Loading CSS
**Objective**: Load CSS only when needed.

**Requirements**:
- Split CSS by route/component
- Load critical CSS first
- Lazy load below-fold styles
- Print stylesheet lazy loading

**Expected Outcome**: Strategic CSS loading

---

### Assignment 229: Animation Performance
**Objective**: Create 60fps animations.

**Requirements**:
- Animate only transform and opacity
- Reduce animation complexity
- Use reduced-motion media query
- Profile animation performance

**Expected Outcome**: Performant animations

---

### Assignment 230: Performance Audit
**Objective**: Complete CSS performance audit.

**Requirements**:
- Analyze existing stylesheet
- Identify performance bottlenecks
- Create optimization recommendations
- Implement improvements
- Measure before/after

**Expected Outcome**: CSS audit capability

---

## Module 21: Accessibility (Assignments 231-235)

### Assignment 231: Focus Indicators
**Objective**: Create accessible focus styles.

**Requirements**:
- Visible focus for all interactive elements
- Avoid outline: none without replacement
- Use :focus-visible appropriately
- Meet WCAG contrast requirements

**Expected Outcome**: Accessible focus management

---

### Assignment 232: Color Accessibility
**Objective**: Ensure color-accessible designs.

**Requirements**:
- Check text contrast ratios
- Don't rely on color alone
- Test with color blindness simulators
- Meet WCAG AA/AAA standards

**Expected Outcome**: Color accessibility compliance

---

### Assignment 233: Responsive Text
**Objective**: Ensure readable text at all sizes.

**Requirements**:
- Avoid tiny text
- Test 200% zoom functionality
- Use relative units
- Maintain readability

**Expected Outcome**: Text accessibility

---

### Assignment 234: Reduced Motion
**Objective**: Support motion-sensitive users.

**Requirements**:
- Use prefers-reduced-motion media query
- Provide alternative to animations
- Simplify rather than remove
- Test results

**Expected Outcome**: Motion accessibility

---

### Assignment 235: High Contrast Mode
**Objective**: Support high contrast preferences.

**Requirements**:
- Use prefers-contrast media query
- Test forced-colors mode
- Ensure UI remains usable
- System color keywords

**Expected Outcome**: Contrast mode support

---

## Module 22: Cross-Browser Compatibility (Assignments 236-240)

### Assignment 236: Feature Detection (@supports)
**Objective**: Use CSS feature detection.

**Requirements**:
- Write @supports queries
- Provide fallbacks
- Progressive enhancement
- Test in multiple browsers

**Expected Outcome**: Feature detection mastery

---

### Assignment 237: Vendor Prefixes
**Objective**: Handle vendor prefixes properly.

**Requirements**:
- Identify properties still needing prefixes
- Proper prefix ordering
- Autoprefixer concept
- Test cross-browser

**Expected Outcome**: Prefix management

---

### Assignment 238: Fallback Values
**Objective**: Provide graceful fallbacks.

**Requirements**:
- Fallback color values (rgb before hsl)
- Fallback for custom properties
- Layout fallbacks (Grid to Flexbox to block)
- Progressive enhancement

**Expected Outcome**: Robust fallback strategies

---

### Assignment 239: Browser Testing
**Objective**: Test CSS across browsers.

**Requirements**:
- Test in Chrome, Firefox, Safari, Edge
- Document browser differences
- Create cross-browser solutions
- Mobile browser testing

**Expected Outcome**: Cross-browser validation

---

### Assignment 240: Debugging CSS
**Objective**: Debug CSS issues systematically.

**Requirements**:
- Use DevTools effectively
- Identify specificity issues
- Debug layout problems
- Create reproducible test cases

**Expected Outcome**: CSS debugging skills

---

## Module 23: Expert Components (Assignments 241-248)

### Assignment 241: CSS-Only Dropdown Menu
**Objective**: Build accessible dropdown without JS.

**Requirements**:
- Keyboard-navigable
- Multiple levels
- Smooth animations
- Accessible structure

**Expected Outcome**: CSS-only navigation

---

### Assignment 242: CSS-Only Modal
**Objective**: Create accessible modal with CSS.

**Requirements**:
- Open/close with :target or checkbox
- Focus trapping consideration
- Overlay and centering
- Transition animations

**Expected Outcome**: CSS-only modal

---

### Assignment 243: CSS-Only Carousel
**Objective**: Build image carousel without JS.

**Requirements**:
- Scroll-snap based
- Navigation dots/arrows
- Smooth scrolling
- Responsive design

**Expected Outcome**: CSS-only carousel

---

### Assignment 244: Advanced Data Table
**Objective**: Create feature-rich table styling.

**Requirements**:
- Sticky header
- Alternating rows
- Responsive behavior
- Sortable appearance
- Accessible structure

**Expected Outcome**: Advanced table styling

---

### Assignment 245: Complex Form Validation Styling
**Objective**: Style form validation states.

**Requirements**:
- Untouched, valid, invalid states
- Error message styling
- Success indicators
- Accessible feedback

**Expected Outcome**: Form validation UI

---

### Assignment 246: Mega Menu
**Objective**: Build large navigation menu.

**Requirements**:
- Multiple columns
- Image/icon support
- Smooth transitions
- Accessible structure

**Expected Outcome**: Mega menu component

---

### Assignment 247: Animated Charts (CSS only)
**Objective**: Create simple chart visualizations.

**Requirements**:
- Bar chart with animation
- Pie/donut chart with conic-gradient
- Progress indicators
- Responsive sizing

**Expected Outcome**: CSS chart components

---

### Assignment 248: Design System Implementation
**Objective**: Build mini design system.

**Requirements**:
- Color tokens
- Typography system
- Spacing scale
- Component library
- Documentation page

**Expected Outcome**: Complete design system

---

## Module 24: Capstone Projects (Assignments 249-260)

### Assignment 249: E-commerce Product Page
**Objective**: Build complete product page.

**Requirements**:
- Product image gallery
- Product details and variants
- Add to cart section
- Related products
- Reviews section
- Fully responsive
- Performance optimized

**Expected Outcome**: Professional e-commerce page

---

### Assignment 250: SaaS Landing Page
**Objective**: Create modern SaaS marketing page.

**Requirements**:
- Animated hero section
- Features showcase
- Pricing tables
- Testimonials
- FAQ accordion
- Call to action sections
- Responsive design
- Dark/light mode

**Expected Outcome**: Complete SaaS landing page

---

### Assignment 251: Admin Dashboard
**Objective**: Build complete admin interface.

**Requirements**:
- Sidebar navigation
- Header with user menu
- Widget grid
- Data tables
- Cards and stats
- Form elements
- Responsive collapse
- Dark theme

**Expected Outcome**: Complete admin dashboard

---

### Assignment 252: Blog Theme
**Objective**: Create complete blog design.

**Requirements**:
- Homepage with featured posts
- Post listing grid
- Single post layout
- Author pages
- Category pages
- Sidebar widgets
- Comments section styling
- Print stylesheet

**Expected Outcome**: Complete blog theme

---

### Assignment 253: Portfolio Website
**Objective**: Build creative portfolio.

**Requirements**:
- Animated introduction
- Project gallery with filters
- Case study layouts
- About section
- Contact form
- Smooth scrolling
- Micro-interactions

**Expected Outcome**: Creative portfolio site

---

### Assignment 254: Restaurant Website
**Objective**: Create restaurant website design.

**Requirements**:
- Hero with background
- Menu display layouts
- Gallery section
- Reservation form styling
- Location/contact section
- Opening hours display
- Mobile-optimized

**Expected Outcome**: Restaurant website design

---

### Assignment 255: Event/Conference Site
**Objective**: Build event website.

**Requirements**:
- Countdown display
- Speaker cards
- Schedule timeline
- Ticket selection UI
- Venue information
- FAQ section
- Registration form

**Expected Outcome**: Event website design

---

### Assignment 256: News/Magazine Layout
**Objective**: Create editorial layout.

**Requirements**:
- Complex grid layout
- Featured article areas
- Category columns
- Breaking news ticker
- Sidebar with widgets
- Article templates
- Print optimization

**Expected Outcome**: Magazine-style layout

---

### Assignment 257: Mobile App UI (Web)
**Objective**: Create app-like web interface.

**Requirements**:
- Bottom navigation
- Card-based UI
- Pull-to-refresh visual
- Gesture-friendly sizing
- Native-like transitions
- Status bar consideration
- PWA-ready styling

**Expected Outcome**: Mobile app-style interface

---

### Assignment 258: Email Template
**Objective**: Create HTML email design.

**Requirements**:
- Table-based layout (email compatibility)
- Inline styles (email requirement)
- Responsive email techniques
- Button styling for email
- Image handling
- Footer with unsubscribe

**Expected Outcome**: Email-compatible design

---

### Assignment 259: CSS Art Challenge
**Objective**: Create complex illustration with CSS.

**Requirements**:
- Create recognizable image/character
- Use shapes and pseudo-elements
- Shadows and gradients
- Optional animation
- Well-organized code

**Expected Outcome**: CSS artwork

---

### Assignment 260: Performance-Optimized Large Site
**Objective**: Build optimized large-scale design.

**Requirements**:
- Multiple page templates
- Critical CSS implementation
- Lazy-loaded components
- Efficient selectors
- Minimal file size
- Full accessibility
- Cross-browser tested
- Documented architecture

**Expected Outcome**: Production-ready CSS architecture

---

# Appendix: Quick Reference

## CSS Specificity Values

| Selector Type | Specificity |
|---------------|-------------|
| !important | Overrides all |
| Inline style | 1,0,0,0 |
| ID (#id) | 0,1,0,0 |
| Class (.class) | 0,0,1,0 |
| Pseudo-class | 0,0,1,0 |
| Attribute [attr] | 0,0,1,0 |
| Element | 0,0,0,1 |
| Pseudo-element | 0,0,0,1 |
| Universal (*) | 0,0,0,0 |

## Common Breakpoints

```css
/* Mobile First Breakpoints */
@media (min-width: 576px) { /* Small devices */ }
@media (min-width: 768px) { /* Tablets */ }
@media (min-width: 992px) { /* Desktops */ }
@media (min-width: 1200px) { /* Large desktops */ }
@media (min-width: 1400px) { /* Extra large */ }
```

## Essential Box Model Reset

```css
*, *::before, *::after {
  box-sizing: border-box;
}

* {
  margin: 0;
  padding: 0;
}

html {
  font-size: 16px;
  -webkit-text-size-adjust: 100%;
}

body {
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
}

img, picture, video, canvas, svg {
  display: block;
  max-width: 100%;
}

input, button, textarea, select {
  font: inherit;
}
```

## Flexbox Centering

```css
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

## Grid Centering

```css
.center {
  display: grid;
  place-items: center;
}
```

## Fluid Typography

```css
h1 {
  font-size: clamp(2rem, 5vw + 1rem, 4rem);
}
```

## Theme Variables Template

```css
:root {
  /* Colors */
  --color-primary: #3b82f6;
  --color-secondary: #6366f1;
  --color-accent: #f59e0b;
  
  --color-text: #1f2937;
  --color-text-light: #6b7280;
  --color-background: #ffffff;
  --color-surface: #f3f4f6;
  
  /* Typography */
  --font-sans: 'Inter', system-ui, sans-serif;
  --font-mono: 'Fira Code', monospace;
  
  /* Spacing */
  --space-xs: 0.25rem;
  --space-sm: 0.5rem;
  --space-md: 1rem;
  --space-lg: 1.5rem;
  --space-xl: 2rem;
  --space-2xl: 3rem;
  
  /* Borders */
  --radius-sm: 0.25rem;
  --radius-md: 0.5rem;
  --radius-lg: 1rem;
  --radius-full: 9999px;
  
  /* Shadows */
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
  
  /* Transitions */
  --transition-fast: 150ms ease;
  --transition-normal: 300ms ease;
}

/* Dark Theme */
[data-theme="dark"] {
  --color-text: #f9fafb;
  --color-text-light: #9ca3af;
  --color-background: #111827;
  --color-surface: #1f2937;
}
```

---

## Curriculum Summary

| Level | Assignments | Focus Areas |
|-------|-------------|-------------|
| Beginner | 1-60 | Syntax, selectors, colors, typography, box model, basic components |
| Intermediate | 61-140 | Positioning, Flexbox, Grid, responsive design, transitions |
| Advanced | 141-210 | Animations, 3D transforms, modern functions, advanced selectors |
| Expert | 211-260 | Architecture, performance, accessibility, capstone projects |

**Total Assignments: 260**

---

*This curriculum provides a complete progression from CSS beginner to professional-level expertise. Complete assignments in order for the best learning experience.*
