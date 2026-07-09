---
title: Shifting Bytes, Quicker Arithmetic
tags:
  - programming
  - memory
  - math
---

---
# Byte shifting

## Introduction

Shifting or byte shifting is a process of shifting bytes of a given [[binary|binary]] number in ether left or right direction. In programming shifting is marked by the shift operator:

- Right shifting, decalage a droite  **`>>`**
- Left shifting, decalage a gauche **`<<`**

> [!EXEMPLE]+
> Consider the octet / byte : `00111000`
> 
> `00111100 >> 1` -> `00011110`
>  `00111100 << 1` -> `01111000`

> In this exemple we shifted the binary `00111100` by one bit in both left and right direction.

> [!DANGER]
> shifting is a lossy operation **[[data|data]] can be lost** as it does NOT create more bit, it just move them in a direction `right/left` a cut of whatever fall out of the initial [[binary|encoding]].

## Arithmetic and byte shifting

In a given base `b`, where `b` represent the number of `symbol` used to count. **shifting by n** is equivalent to multiply by **$b^n$**.

**Formula** :

$$ 
\text{For } x \in \text{Base } b 
\implies
\begin{cases}
x \text{ >> }  n =  x \div b^n \\
x \text{ << }  n =  x \times b^n
\end{cases}
$$

It's more striking in [[binary|binary]] as with the naked eye, we can observe this formula.

| Decimal | Binary |
| ------- | ------ |
| 1       | 1      |
| 2       | 10     |
| 4       | 100    |
| 7       | 111    |
| 14      | 1110   |
| 28      | 11100  |

> [!NOTE]
> Multiplying by 2 is the same as shifting by left by one 