# HTML & CSS

## HTML5 Overview
HTML (HyperText Markup Language) provides the structure and content of web pages.

## Semantic HTML
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
</head>
<body>
  <header>
    <nav>
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h1>Article Title</h1>
      <section>
        <h2>Section Heading</h2>
        <p>Paragraph content...</p>
      </section>
    </article>
    <aside>Sidebar content</aside>
  </main>

  <footer>
    <p>&copy; 2024 Company</p>
  </footer>
</body>
</html>
```

## Common HTML Elements
```html
<!-- Text -->
<h1> to <h6>, <p>, <span>, <strong>, <em>, <br>, <hr>

<!-- Lists -->
<ul><li>Unordered</li></ul>
<ol><li>Ordered</li></ol>
<dl><dt>Term</dt><dd>Definition</dd></dl>

<!-- Links & Media -->
<a href="url" target="_blank">Link</a>
<img src="image.jpg" alt="Description">
<video src="video.mp4" controls></video>
<audio src="audio.mp3" controls></audio>

<!-- Forms -->
<form action="/submit" method="POST">
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" required>
  <textarea name="message"></textarea>
  <select name="option">
    <option value="1">Option 1</option>
  </select>
  <button type="submit">Submit</button>
</form>

<!-- Tables -->
<table>
  <thead><tr><th>Header</th></tr></thead>
  <tbody><tr><td>Data</td></tr></tbody>
</table>
```

---

## CSS Overview
CSS (Cascading Style Sheets) controls the visual presentation of HTML.

## Selectors
```css
/* Element */
p { }

/* Class */
.classname { }

/* ID */
#idname { }

/* Attribute */
[type="text"] { }
[href^="https"] { }  /* Starts with */
[href$=".pdf"] { }   /* Ends with */

/* Combinators */
div p { }       /* Descendant */
div > p { }     /* Direct child */
div + p { }     /* Adjacent sibling */
div ~ p { }     /* General sibling */

/* Pseudo-classes */
a:hover { }
li:first-child { }
li:nth-child(odd) { }
input:focus { }
input:valid { }

/* Pseudo-elements */
p::before { content: "→ "; }
p::after { }
p::first-letter { }
::selection { }
```

## Box Model
```css
.box {
  /* Content dimensions */
  width: 300px;
  height: 200px;
  
  /* Padding (inside) */
  padding: 20px;
  padding: 10px 20px;  /* vertical horizontal */
  
  /* Border */
  border: 1px solid #000;
  border-radius: 8px;
  
  /* Margin (outside) */
  margin: 20px auto;
  
  /* Box sizing */
  box-sizing: border-box;  /* Include padding/border in width */
}
```

## Flexbox
```css
.flex-container {
  display: flex;
  flex-direction: row;         /* row | column | row-reverse */
  justify-content: center;     /* flex-start | flex-end | space-between | space-around */
  align-items: center;         /* flex-start | flex-end | stretch | baseline */
  flex-wrap: wrap;
  gap: 16px;
}

.flex-item {
  flex: 1;                     /* grow shrink basis */
  flex-grow: 1;
  flex-shrink: 0;
  flex-basis: 200px;
  align-self: flex-start;
  order: 1;
}
```

## Grid
```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto 1fr auto;
  gap: 20px;
  
  /* Named areas */
  grid-template-areas:
    "header header header"
    "sidebar main main"
    "footer footer footer";
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }

.grid-item {
  grid-column: span 2;
  grid-row: 1 / 3;
}
```

## Responsive Design
```css
/* Mobile-first approach */
.container {
  width: 100%;
  padding: 16px;
}

/* Tablet */
@media (min-width: 768px) {
  .container {
    max-width: 720px;
    margin: 0 auto;
  }
}

/* Desktop */
@media (min-width: 1024px) {
  .container {
    max-width: 960px;
  }
}

/* Responsive units */
.text {
  font-size: clamp(1rem, 2.5vw, 2rem);
}
```

## CSS Variables
```css
:root {
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
}

.button {
  background: var(--primary-color);
  padding: var(--spacing-sm) var(--spacing-md);
}

/* Dark mode */
@media (prefers-color-scheme: dark) {
  :root {
    --primary-color: #5dade2;
  }
}
```

## Animations
```css
/* Transitions */
.button {
  transition: all 0.3s ease;
}
.button:hover {
  transform: scale(1.05);
}

/* Keyframe Animations */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animated {
  animation: fadeIn 0.5s ease-out forwards;
}
```

## Best Practices

1. Use **semantic HTML** elements
2. Ensure **accessibility** (ARIA, alt text)
3. Use **CSS custom properties** for theming
4. Prefer **Flexbox/Grid** over floats
5. Design **mobile-first**
6. Use **BEM naming** for classes
7. Minimize **specificity issues**

## Resources
- MDN Web Docs
- CSS-Tricks
- web.dev
