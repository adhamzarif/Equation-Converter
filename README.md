# Equation-Converter

A single-file, browser-based tool that converts math content (LaTeX, Unicode, or plain AI-generated text) into a live preview and exports it to **.docx**, **.html**, or **PDF** — with equations that remain **fully editable in Microsoft Word**.

No installation required. No server. Just open the URL in any modern browser.

---

## Features

- **Live preview** — renders equations using MathJax as you type or paste
- **Multiple input formats** — accepts LaTeX (`[...]`, `$$...$$`, `\[...\]`, `$...$`), Unicode math symbols, and plain AI-generated text
- **Smart preprocessing** — automatically detects stacked Unicode fractions, section headers, Markdown headings (`###`), emoji-prefixed lines, and horizontal rules
- **Color-coded sections** — recognizes named sections (Question, Given, Formula, Solution, Final Answer, Note) and styles each with a distinct color accent
- **Three export formats:**
  - `.docx` — Word document with native OMML equations (editable in Word, not images)
  - `.html` — standalone HTML file with embedded MathJax (ready to open in Word or any browser)
  - **PDF** — via the browser's print dialog
- **Keyboard shortcut** — `Ctrl+Enter` (or `Cmd+Enter` on Mac) triggers the preview
- **Custom document title** — set a title that appears as a heading in all exports
- **Print-ready** — hides the editor UI when printing, showing only the document

---

## Requirements

- Any modern browser (Chrome, Firefox, Edge, Safari)
- Internet connection (used to load MathJax and JSZip from CDN on first use)
- Microsoft Word 2016 or later (to open and edit exported `.docx` equations)

---

## How to Use

### 1. Open the file

Click the URL to open it in your browser. No installation or setup needed.

### 2. Set a document title *(optional)*

At the top of the page, there is a **Document title** field. Type your document name here (e.g., `Fourier Series — Problem Set 3`). This title will appear as a bold heading in all exported files.

### 3. Paste or type your content

Click inside the **Input** panel on the left and paste your math content. The tool accepts several formats:

#### Format A — LaTeX blocks (recommended)

Wrap each equation in square brackets `[` ... `]` on separate lines:

```
*Section Name*

[
\frac{1}{2} + \frac{\sqrt{3}}{4}
]

plain text goes here

---
```

#### Format B — Dollar-sign LaTeX (standard Markdown math)

```
$$\int_0^\infty e^{-x^2} dx = \frac{\sqrt{\pi}}{2}$$

Inline math also works: $E = mc^2$
```

#### Format C — Backslash bracket display math

```
\[
\sum_{k=1}^{n} k = \frac{n(n+1)}{2}
\]
```

#### Format D — Unicode math (copy-pasted from AI chat)

If you paste output from an AI tool that uses Unicode symbols instead of LaTeX, the converter will automatically detect and convert them:

```
α + β = γ
∫ f(x) dx ≈ 0.5
```

### 4. Use the formatting syntax

| Syntax | Result |
|---|---|
| `*Section Name*` | Color-coded section header |
| `[LaTeX here]` | Centered display equation |
| `---` | Horizontal divider line |
| `**bold text**` | **Bold** inline text |
| `*italic text*` | *Italic* inline text |
| `\(...\)` | Inline equation within a text line |
| `### Heading` | Converted to a section header automatically |

#### Named section colors

The following section names get a special color accent automatically:

| Section name | Color |
|---|---|
| Question | Blue |
| Given | Teal / Green |
| Formula / Formulas | Amber |
| Solution | Purple |
| Final Answer / Answer | Red |
| Note | Violet |
| Any other name | Gray |

### 5. Preview

Click the **Preview ↵** button (top-right of the Input panel), or press **Ctrl+Enter** (`Cmd+Enter` on Mac). The right panel will render your content with typeset equations.

You can also click **Load example** to see a fully worked signal analysis example.

### 6. Export

Once you are satisfied with the preview, export using one of the three buttons:

#### ⬇ Download .docx

Generates a proper Word document (`.docx`) with equations stored as native **OMML** (Office Math Markup Language). This means:
- Equations appear as real Word equations, not images
- You can click any equation in Word and edit it with the Equation Editor
- Font is Cambria Math (standard for Word equations)
- Uses Calibri 12pt body text

The file is named after your document title (e.g., `Signal_Analysis.docx`).

#### ⬇ HTML (Word-ready)

Downloads a self-contained `.html` file with MathJax-rendered equations. You can open this in Word, or share it as a web page.

#### 🖨 Save as PDF

Opens the browser's print dialog. The editor UI is hidden automatically, so only the document content is printed. Use "Save as PDF" in the print dialog.

---

## Input Tips

- You can mix LaTeX, Unicode, and plain text freely in the same document
- Blank lines between sections are ignored — use `---` for explicit dividers
- A line like `*Given*` or `*Solution:*` (with or without a trailing colon) is treated as a section header
- Markdown headings (`## Title`) are automatically converted to section headers
- Zero-width characters (often invisibly pasted from web pages) are stripped automatically
- Emoji bullet points (`👉`, `✅`, `💡`, etc.) are converted to plain text lines

---

## Example Input

```
*Question*
Draw magnitude and phase plots of c_k.

---

*Given*
[
c_0 = 1, \quad c_{\pm1} = \frac{1}{2} \mp j
]

---

*Solution*
[
|c_0| = 1, \quad \angle c_0 = 0
]

The magnitude and phase are computed using standard formulas.

---

*Final Answer*
[
(-1,\ \tfrac{\sqrt{5}}{2}),\ (0,\ 1),\ (1,\ \tfrac{\sqrt{5}}{2})
]
```

---

## File Structure

The entire tool is a **single `.html` file** with no external dependencies beyond CDN-loaded libraries:

| Library | Purpose |
|---|---|
| [MathJax 3.2.2](https://www.mathjax.org/) | Renders LaTeX equations in the preview |
| [JSZip](https://stuk.github.io/jszip/) | Packages the `.docx` file (loaded on demand) |

Both libraries are loaded from `cdnjs.cloudflare.com`. An internet connection is needed for the first load; after that, they may be cached by the browser.

---

## Limitations

- Complex LaTeX commands that are not supported by MathJax may not render correctly in preview
- The DOCX exporter converts a subset of LaTeX to OMML; very advanced or non-standard LaTeX may fall back to displaying as plain monospace text in Word
- Unicode-to-LaTeX conversion is heuristic — ambiguous stacked symbols may not always parse as intended; use explicit `[LaTeX]` blocks for critical equations
- PDF quality depends on the browser's print engine

---

## License

This tool is provided as-is. It runs entirely in your browser and sends no data anywhere.
