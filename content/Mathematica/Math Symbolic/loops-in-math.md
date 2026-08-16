---
tags:
  - math
  - programming
title: Loops in mathematica
---
## Concept

A mathematical summation or product can be understood as a compact way of repeating an operation over a sequence of values.

For example:

$$\sum_{k=1}^{5} k$$

means: $1+2+3+4+5$

while:

$$
\prod_{k=1}^{5} k
$$

means:

$$
1\times2\times3\times4\times5
$$

The variable \(k\) is the index. It starts at \(1\) and increases by \(1\) until it reaches \(5\).

In programming terms, the product could be thought of roughly as:

result = 1

```p
for k = 1 to 5:
    result = result × k
```

The important distinction is that mathematical notation describes what is being computed, rather than necessarily specifying how it must be computed. A compiler or programmer could implement the same mathematical expression using a loop, recursion, parallel operations, or another method.

The general forms are:

$$\sum_{k=a}^{b} f(k)$$

for repeatedly adding values, and

$$\prod_{k=a}^{b} f(k)$$

for repeatedly multiplying values.

Here:

- \(k\) — the index

- \(a\) — the starting value

- \(b\) — the ending value

- \(f(k)\) — the expression evaluated for each \(k\)


So:

$$\prod_{k=1}^{n} k$$

can be read informally as:

> “For every \(k\) from 1 to \(n\), multiply \(k\) into the result.”

This is the notation used to express factorial:

$$
n! = \prod_{k=1}^{n} k
$$