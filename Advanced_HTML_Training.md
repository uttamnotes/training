# 🧠 Advanced HTML Training Document

This document is designed for students who already have a basic understanding of HTML and wish to explore more advanced and modern HTML concepts.

---

## Module 1: HTML5 Deep Dive & Best Practices

### Concepts
- Understanding HTML5 doctype and structure
- Semantic HTML (vs. non-semantic)
- Importance of `<header>`, `<nav>`, `<article>`, `<section>`, `<aside>`, `<footer>`

### Example
```html
<article>
  <header><h2>Campus Tech Fest</h2></header>
  <section>
    <p>Annual college tech fest featuring coding, robotics, and AI challenges.</p>
  </section>
  <footer>Event Date: 20th October</footer>
</article>
```

### Explanation
Semantic HTML improves readability, accessibility, and SEO. Tags like `<section>` or `<article>` help browsers and assistive technologies understand content structure better than plain `<div>` elements.

---

## Module 2: Advanced Forms & Input Controls

### Concepts
- HTML5 input types: `email`, `url`, `date`, `color`, `range`, etc.
- Validation attributes: `required`, `pattern`, `min`, `max`, `step`
- Using `<datalist>` and `<output>`
- Form accessibility and user experience

### Example
```html
<form>
  <label>Email: <input type="email" required></label><br>
  <label>Age: <input type="number" min="18" max="60"></label><br>
  <label>Favorite Color: <input type="color"></label><br>
  <input type="submit">
</form>
```

### Explanation
HTML5 introduced various new form elements and attributes that make form validation and data collection more powerful and user-friendly without needing JavaScript.

---

## Module 3: Multimedia & Embedding

### Concepts
- Using `<audio>` and `<video>` with controls and multiple sources
- Adding captions via `<track>`
- Embedding YouTube or Google Maps responsibly
- Responsive images with `<picture>`

### Example
```html
<video controls width="400">
  <source src="intro.mp4" type="video/mp4">
  <track src="subtitles_en.vtt" kind="subtitles" srclang="en" label="English">
  Your browser does not support the video tag.
</video>
```

### Explanation
HTML5 supports multimedia elements natively. The `<track>` tag enhances accessibility by providing subtitles and captions.

---

## Module 4: Accessibility (a11y) & SEO

### Concepts
- Using ARIA roles and attributes: `role`, `aria-label`, `aria-hidden`
- Proper use of `alt`, `title`, and heading hierarchy
- SEO-related `<meta>` tags: `description`, `robots`, `og:title`

### Example
```html
<button aria-label="Play video">▶</button>
```

### Explanation
Accessibility ensures websites are usable by people with disabilities. ARIA attributes help assistive technologies describe the role or function of an element.

---

## Module 5: Advanced Linking & Metadata

### Concepts
- Internal and external linking best practices
- Anchor attributes: `target`, `download`, `rel`
- Social media meta tags (`og:title`, `og:image`, `og:description`)
- Favicons and web app manifests

### Example
```html
<a href="report.pdf" download="Student_Report">Download Report</a>
```

### Explanation
The `download` attribute allows users to download linked files directly instead of opening them. Metadata improves how your site is previewed on search engines and social media.

---

## Module 6: Tables, Lists, and Data Representation

### Concepts
- Table structure with `<thead>`, `<tbody>`, `<tfoot>`, and `<caption>`
- Styling and grouping columns using `<colgroup>` and `<col>`
- Creating nested and description lists for structured information

### Example
```html
<table>
  <caption>Course Schedule</caption>
  <thead><tr><th>Day</th><th>Topic</th></tr></thead>
  <tbody>
    <tr><td>Mon</td><td>Semantic HTML</td></tr>
    <tr><td>Tue</td><td>Forms</td></tr>
  </tbody>
</table>
```

### Explanation
Properly structured tables enhance both readability and accessibility. Captions and headers help describe the data context clearly.

---

## Module 7: Custom Data and Integration

### Concepts
- Using `data-*` attributes to store custom data
- How JavaScript can access and manipulate these attributes
- Progressive enhancement concept

### Example
```html
<div data-student="Ananya" data-score="92">Top Performer</div>
```

### Explanation
Custom data attributes provide a way to embed extra information in HTML elements, which can later be accessed via JavaScript to build dynamic web features.

---

## Module 8: Microdata & HTML APIs

### Concepts
- Structured data and `schema.org` markup
- HTML Drag-and-Drop API
- Overview of Web Storage (localStorage, sessionStorage)

### Example
```html
<div draggable="true" ondragstart="alert('Dragging started!')">Drag me!</div>
```

### Explanation
Microdata and structured data help search engines understand your content contextually. HTML APIs like drag-and-drop make web pages more interactive without external libraries.

---

## Mini Project Ideas

- Create a **college event registration page** with validation and semantic layout.
- Develop a **portfolio page** using `<picture>`, `<video>`, and metadata.
- Build a **mini dashboard** with tables and downloadable reports.

---

**End of Advanced HTML Training Document**
