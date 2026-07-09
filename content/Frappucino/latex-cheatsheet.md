---
title: LaTeX Cheatsheet
tags:
  - cheatsheet
  - latex
---

# Latex Cheat Sheet

> Inline math uses `$...$`
> 
> Display math uses:
> 
> ```latex
> $$
> ...
> $$
> ```

---

# Variables

| Output     | LaTeX      |
| ---------- | ---------- |
| $x$        | `x`        |
| $x_1$      | `x_1`      |
| $x_{long}$ | `x_{long}` |
| $x^2$      | `x^2`      |
| $x^{10}$   | `x^{10}`   |
| $x_i^2$    | `x_i^2`    |

---

# Fractions

| Output         | LaTeX          |
| -------------- | -------------- |
| $\frac{a}{b}$  | `\frac{a}{b}`  |
| $\dfrac{a}{b}$ | `\dfrac{a}{b}` |

---

# Square Roots

| Output        | LaTeX         |
| ------------- | ------------- |
| $\sqrt{x}$    | `\sqrt{x}`    |
| $\sqrt[n]{x}$ | `\sqrt[n]{x}` |

---

# Parentheses

Automatically sized delimiters:

| Output                     | LaTeX                      |
| -------------------------- | -------------------------- |
| $\left(x\right)$           | `\left(x\right)`           |
| $\left[\frac{a}{b}\right]$ | `\left[\frac{a}{b}\right]` |
| $\left{x\right}$           | `\left\{x\right\}`         |
| $x\right$                  | x\right                    |

---

# Greek Letters

|Output|LaTeX|
|---|---|
|$\alpha$|`\alpha`|
|$\beta$|`\beta`|
|$\gamma$|`\gamma`|
|$\delta$|`\delta`|
|$\epsilon$|`\epsilon`|
|$\theta$|`\theta`|
|$\lambda$|`\lambda`|
|$\mu$|`\mu`|
|$\pi$|`\pi`|
|$\rho$|`\rho`|
|$\sigma$|`\sigma`|
|$\tau$|`\tau`|
|$\phi$|`\phi`|
|$\omega$|`\omega`|
|$\Gamma$|`\Gamma`|
|$\Delta$|`\Delta`|
|$\Theta$|`\Theta`|
|$\Lambda$|`\Lambda`|
|$\Pi$|`\Pi`|
|$\Sigma$|`\Sigma`|
|$\Phi$|`\Phi`|
|$\Omega$|`\Omega`|

---

# Arithmetic

| Output        | LaTeX         |
| ------------- | ------------- |
| $a+b$         | `a+b`         |
| $a-b$         | `a-b`         |
| $a\cdot b$    | `a\cdot b`    |
| $a\times b$   | `a\times b`   |
| $\frac{a}{b}$ | `\frac{a}{b}` |

---

# Comparison

|Output|LaTeX|
|---|---|
|$=$|`=`|
|$\neq$|`\neq`|
|$<$|`<`|
|$>$|`>`|
|$\le$|`\le`|
|$\ge$|`\ge`|
|$\approx$|`\approx`|
|$\equiv$|`\equiv`|
|$\propto$|`\propto`|

---

# Logic

|Output|LaTeX|
|---|---|
|$\land$|`\land`|
|$\lor$|`\lor`|
|$\neg$|`\neg`|
|$\forall$|`\forall`|
|$\exists$|`\exists`|
|$\therefore$|`\therefore`|
|$\because$|`\because`|
|$\implies$|`\implies`|
|$\iff$|`\iff`|

---

# Sets

|Output|LaTeX|
|---|---|
|$\in$|`\in`|
|$\notin$|`\notin`|
|$\subset$|`\subset`|
|$\subseteq$|`\subseteq`|
|$\supseteq$|`\supseteq`|
|$\cup$|`\cup`|
|$\cap$|`\cap`|
|$\emptyset$|`\emptyset`|
|$\mathbb{N}$|`\mathbb{N}`|
|$\mathbb{Z}$|`\mathbb{Z}`|
|$\mathbb{Q}$|`\mathbb{Q}`|
|$\mathbb{R}$|`\mathbb{R}`|
|$\mathbb{C}$|`\mathbb{C}`|

---

# Calculus

|Output|LaTeX|
|---|---|
|$\lim_{x\to0}$|`\lim_{x\to0}`|
|$\sum_{i=0}^{n}$|`\sum_{i=0}^{n}`|
|$\prod_{i=1}^{n}$|`\prod_{i=1}^{n}`|
|$\int_a^b$|`\int_a^b`|
|$\oint$|`\oint`|
|$\partial$|`\partial`|
|$\nabla$|`\nabla`|
|$\infty$|`\infty`|

---

# Derivatives

|Output|LaTeX|
|---|---|
|$\frac{dy}{dx}$|`\frac{dy}{dx}`|
|$\frac{\partial f}{\partial x}$|`\frac{\partial f}{\partial x}`|
|$\dot{x}$|`\dot{x}`|
|$\ddot{x}$|`\ddot{x}`|

---

# Vectors

|Output|LaTeX|
|---|---|
|$\vec{v}$|`\vec{v}`|
|$\overrightarrow{AB}$|`\overrightarrow{AB}`|
|$\mathbf{v}$|`\mathbf{v}`|
|$\hat{x}$|`\hat{x}`|
|$\bar{x}$|`\bar{x}`|

---

# Matrices

```latex
$$
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
$$
```

Produces

$$  
\begin{bmatrix}  
1 & 2\  
3 & 4  
\end{bmatrix}  
$$

Other environments:

- `pmatrix` → ()
- `bmatrix` → []
- `Bmatrix` → {}
- `vmatrix` → |
- `Vmatrix` → ||

---

# Cases

```latex
$$
f(x)=
\begin{cases}
x^2 & x>0\\
0 & x=0\\
-x & x<0
\end{cases}
$$
```

$$
f(x)=
\begin{cases}
x^2 & x>0\\
0 & x=0\\
-x & x<0
\end{cases}
$$
---

# Alignment

```latex
$$
\begin{aligned}
a+b &= c\\
x+y &= z
\end{aligned}
$$
```

$$
\begin{aligned}
a+b &= c\\
x+y &= z
\end{aligned}
$$

---

# Decorations

|Output|LaTeX|
|---|---|
|$\overline{AB}$|`\overline{AB}`|
|$\underline{x}$|`\underline{x}`|
|$\widehat{ABC}$|`\widehat{ABC}`|
|$\widetilde{f}$|`\widetilde{f}`|
|$\cancel{x}$*|`\cancel{x}`|

*Requires the `cancel` package (not available in all renderers).

---

# Common Functions

|Output|LaTeX|
|---|---|
|$\sin$|`\sin`|
|$\cos$|`\cos`|
|$\tan$|`\tan`|
|$\log$|`\log`|
|$\ln$|`\ln`|
|$\exp$|`\exp`|
|$\max$|`\max`|
|$\min$|`\min`|

---

# Spacing

|Output|LaTeX|
|---|---|
|$a,b$|`a\,b`|
|$a;b$|`a\;b`|
|$a\quad b$|`a\quad b`|
|$a\qquad b$|`a\qquad b`|

---

# Text Inside Math

```latex
\text{Speed}
```

Example:

$$  
v = 10\text{ m/s}  
$$

---

# Useful Symbols

|Output|LaTeX|
|---|---|
|$\rightarrow$|`\rightarrow`|
|$\Rightarrow$|`\Rightarrow`|
|$\leftarrow$|`\leftarrow`|
|$\leftrightarrow$|`\leftrightarrow`|
|$\mapsto$|`\mapsto`|
|$\circ$|`\circ`|
|$\bullet$|`\bullet`|
|$\angle$|`\angle`|
|$\perp$|`\perp`|
|$\parallel$|`\parallel`|
|$\degree$*|`^\circ`|

---

# Most Used Commands

```latex
^        Superscript

_        Subscript

\frac{}{}

\sqrt{}

\sum

\prod

\int

\lim

\partial

\nabla

\vec{}

\mathbf{}

\mathbb{}

\left ... \right

\begin{cases}

\begin{aligned}

\begin{bmatrix}
```

> Inline math uses `$...$`
> 
> Display math uses:
> 
> ```latex
> $$
> ...
> $$
> ```