---
title: Markdown Cheatsheet
tags:
  - markdown
  - cheatsheet
---
## Markdown Cheat-sheet

### Callouts

> [!NOTE]
> General information.
> ```markdown
> > [!NOTE]
> > TEXT
> ```

> [!TIP]
> Helpful advice.
> ```md
> > [!TIP]
> > Here's a tips
> ```

> [!IMPORTANT]
> Important information.
> ```md
> > [!IMPORTANT]
> > Something really important
> ```


> [!WARNING]
> Something requires caution.

> [!CAUTION]
> High risk or dangerous.

> [!SUCCESS]
> Success message.

> [!QUESTION]
> Question or prompt.

> [!FAILURE]
> Failure or error.

> [!BUG]
> Bug report.
> ```md
> > [!BUG]
> > That not a bug, that's a feature.
> ```

> [!EXAMPLE]
> Example.
> ```md
> > [!EXAMPLE]
> > An exemple of an exemple callout
> ```

> [!QUOTE]
> Quote or citation.
> ```md
> > [!QUOTE]
> > By Einstain - Time is relative 
> ```

### Foldable Callouts

> [!NOTE]- Closed by default
> Hidden content.
> ```md
> > [!NOTE]- Closed ...
> > Content
> ```

> [!TIP]+ Open by default
> Visible content.
> ```md
> > [!TIP]
> > Content
> ```

---

### Internal Links

\[\[Note]]
\[\[Note|Display Name]]

\[\[Note#Heading]]
\[\[Note#Heading|Display Name]]

\[\[Note#^block-id]]
\[\[Note#^block-id|Display Name]]

---

### Code Blocks

```zig
const x: u8 = 42;
```

Specify the language after the opening back-ticks for syntax highlighting.

---

### Tables

**Rendered**

| Name | Type  |
| ---- | ----- |
| data | []u8  |
| len  | usize |

**Code**

```md
| Heading 1 | ... | Heading N |
|:---------:| ... |:---------:|
| Content   | ... | Content   |
| Content   | ... | Content   |
```

---

### Check-boxes

**Rendered**

- [ ] To do
- [x] Done
- [-] Cancelled

**Code**

```md
- [ ] To do
- [x] Done
- [-] Cancelled  
```

---

Footnotes

Zig is fast.[^1]

[^1]: Because it compiles to native code.

---

### Escaping Markdown

\\\*Not italic\\\*
\\\# Not a heading
\\\`Not code\\\`