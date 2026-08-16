---
title: What is a factorial
tags:
  - math
---
## Formula

The formula that express the concept of factorial is simple in practice, scary in design.

$$
\text{n!} = \prod_{k=1}^{n}k
$$
> [!EXAMPLE]+ For the unintimate of loops see [[loops-in-math| loops in math]]
>$$
>\begin{aligned}
>\text{for } &n = 5 \\ 
>&n! =  1 \times 2 \times 3 \times 4 \times 5 
>\end{aligned}$$

**But what does it mean ?**

A factorial expresses a simple idea: **how many ways are there to order a set[^1] without repeating any of its elements?**

The answer is straightforward. If you have a set of `n` distinct elements, you have `n` possibilities for the first position. Once one element has been chosen, `n-1` remain for the second position, then `n-2`, and so on.

For example, if you have to arrange 5 elements:

- first pick: 5 possibilities
- second pick: 4 possibilities
- third pick: 3 possibilities
- fourth pick: 2 possibilities
- last pick: 1 possibility

Therefore:

$$
5! = 5 \times 4 \times 3 \times 2 \times 1 = 120
$$

That's it. Nothing magical is happening here.

> [!EXAMPLE]- How many ways is there to shuffle a deck of fifty-two cards ?
> $$
> \begin{aligned}
> \text{for } &n = 52 \\
> &n! =  1 \times 2 \times 3 \times 4 \times 5 \times \text{...} \times 52 \\
> &n! \approx 8.07 \times 10^67
> \end{aligned}
> $$
>  That's a little more than $8\times10^{67}$ possible arrangements — a number so large that even if the entire human population shuffled cards 24 hours a day, 7 days a week, for generations, there would still be plays that had never been played.

[^1]: A collection of **distinct** elements