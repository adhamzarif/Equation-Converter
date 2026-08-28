# Equation-Converter

A single-file, browser-based tool that turns an AI chat reply — from ChatGPT, Gemini, DeepSeek or Claude — into a clean document, and exports it to **.docx**, **.html** or **PDF**, with equations that stay **fully editable in Microsoft Word**.

No installation. No server. Open the file in any modern browser.

---

## Features

- **Live preview** — MathJax renders your equations as you type, with a short debounce
- **Paste-and-go** — accepts a reply exactly as you copied it, without reformatting
- **Every common math delimiter** — `$$...$$`, `\[...\]`, `$...$`, `\(...\)`, and bare `[` / `]` blocks for replies whose backslashes were stripped by Markdown
- **LaTeX environments** — `aligned`, `align`, `gather`, `split`, `cases`, `matrix`, `pmatrix`, `bmatrix`, `vmatrix`, `array`
- **Markdown** — headings, bold, italic, inline code, fenced code blocks, bullet and numbered lists, tables, dividers
- **Colour-coded sections** — named sections (Question, Given, Formula, Solution, Final Answer, Note…) each get a distinct accent
- **Unicode recovery** — if you paste already-rendered math (`x²`, `√5`, `≥`, `π`, `aₙ₊₁`, `½`), it is converted back to LaTeX
- **Three exports:**
  - `.docx` — native OMML equations, editable in Word's equation editor, not images
  - `.html` — standalone file with embedded MathJax
  - **PDF** — rendered in a new tab, then the print dialog opens on its own
- **Keyboard shortcut** — `Ctrl+Enter` (`Cmd+Enter` on Mac) forces a preview

---

## Requirements

- Any modern browser (Chrome, Firefox, Edge, Safari)
- An internet connection on first load — MathJax and JSZip come from a CDN
- Microsoft Word 2016 or later to edit the exported equations

---

## How to use

### 1. Open the file

Open `index.html` in your browser. Nothing to install.

### 2. Set a document title (optional)

The **Document title** field at the top becomes a centred bold heading in every export, and supplies the filename. Leave it blank and the file is named `document`.

### 3. Paste the reply

Click into the **Input** panel and paste. All of these work, and you can mix them freely in one document:

**Display math**

```
$$
\int_0^\infty e^{-x^2}\,dx = \frac{\sqrt{\pi}}{2}
$$
```

```
\[
\sum_{k=1}^{n} k = \frac{n(n+1)}{2}
\]
```

**Inline math**

```
The identity $E = mc^2$ still holds, and so does \(a^2 + b^2 = c^2\).
```

**Environments** — write them as usual, either bare or inside `$$`:

```
$$
\begin{cases}
x + y = 2 \\
x - y = 0
\end{cases}
$$
```

**Bare brackets** — when a reply loses its backslashes in copy-paste, a line containing only `[`, a body, and a line containing only `]` is read as display math:

```
[
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
]
```

**Already-rendered Unicode** — pasted from a chat window that showed the typeset result:

```
$$
x² + √5 ≥ π
$$
```

This is only rewritten when the block contains Unicode maths symbols *and* no LaTeX commands at all, so a block that is already valid LaTeX is never touched.

### 4. Formatting syntax

| Syntax | Result |
|---|---|
| `# Heading` … `###### Heading` | Colour-coded section header |
| `**Label**` or `*Label*` alone on a line | Colour-coded section header |
| `**bold**`, `*italic*` | Bold, italic |
| `` `code` `` | Inline monospace |
| ```` ```…``` ```` | Fenced code block |
| `- item` / `* item` / `+ item` | Bullet list |
| `1. item` | Numbered list |
| `\| a \| b \|` with a `\|---\|---\|` row | Table |
| `---` | Horizontal divider |

Inline math is allowed inside list items, table cells and headings.

**Section colours**

| Section name contains | Colour |
|---|---|
| Question | Blue |
| Given, Step, Check | Teal |
| Formula | Amber |
| Solution, Working | Purple |
| Final answer, Answer, Result | Red |
| Note | Violet |
| Anything else | Grey |

### 5. Preview

The preview refreshes automatically about half a second after you stop typing. To force it, press **Ctrl+Enter** or click **Preview**. **Load example** fills the input with a worked Fourier-coefficient problem that exercises most features.

### 6. Export

**Download .docx** — a Word document whose equations are native **OMML**. Click any equation in Word and the equation editor opens; the maths is real Word maths, not a picture. Body text is Times New Roman 12 pt; equations use Cambria Math, which is Word's default maths font. Bold and italic from your input are preserved, and tables and lists come through as real Word tables and paragraphs.

**Download .html** — a self-contained page with MathJax embedded. Opens in a browser, and Word will import it too.

**Save as PDF** — opens a new tab, waits for MathJax to finish typesetting, then opens the print dialog. Choose *Save as PDF* there. If nothing happens, your browser blocked the tab — allow pop-ups for this page and try again.

---

## Tips

- Blank lines separate paragraphs; use `---` when you want a visible rule
- A line like `**Given**` or `*Solution:*` becomes a section header, with the trailing colon dropped. A short italic sentence alone on a line will also be read as a header — put it in a paragraph with other text if that is not what you want
- Prices are safe: `it costs $5 and then $10` is not parsed as maths, because a `$` maths span must have no space just inside either delimiter. Write `\$` if you want to be certain
- Zero-width and non-breaking characters pasted from web pages are stripped automatically

---

## Known limitations

- `\int`, `\sum` and `\lim` decide where their operand ends by scanning to the next relation sign. `\int f(x)\,dx + C` therefore pulls the `+ C` inside the integral — wrap the integrand in braces (`\int {f(x)\,dx} + C`) if that matters
- The DOCX converter covers a large subset of LaTeX, not all of it. An unrecognised command is written as upright text rather than dropped, so nothing disappears silently, but exotic packages will not survive
- Word has no blackboard-bold maths style, so `\mathbb{R}` and friends are mapped to the Unicode characters ℝ, ℕ, ℤ, ℚ, ℂ
- Nested `\left…\right` inside a matrix cell is handled, but a matrix that spans a `\left…\right` boundary is not
- PDF fidelity depends on the browser's print engine; Chrome gives the most consistent result
- Very long single-line equations scroll horizontally in the preview rather than wrapping

---

## Built with

| Library | Purpose |
|---|---|
| [MathJax 3.2.2](https://www.mathjax.org/) | Typesets equations in the preview and the HTML/PDF exports |
| [JSZip 3.10.1](https://stuk.github.io/jszip/) | Packages the `.docx`, loaded on demand |

Both load from `cdnjs.cloudflare.com` and are cached by the browser after the first visit.

---

## Privacy

Everything runs in your browser. Nothing you paste is uploaded anywhere. The only network requests are for the two CDN libraries above.

---

## License

Provided as-is.
