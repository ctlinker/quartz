---
title: Vector, Geometric Intuition
tags:
  - math
  - ai
---
# Mathematical Vector In Geometry

## Introduction

### 1. Contexte

What is a *vector* ?
From early days of school we tend to think of vector arrow on 2D grid/plane.

```plaintext
y
↑
│        • (3,2)
│      ↗
│    ↗
│  ↗
O────────────→ x
```

With notation: $\vec{u} = \begin{pmatrix} 3 \\ 2 \end{pmatrix}$
### 2. Interpretation 

That is the basic overview of the subject.

But truly, a vector is less about the arrow and more about what the vector *describes*. If we look closely, what is actually happening in the 1st example? What does $\vec{u}$ represent? 

> [!IMPORTANT] 
> A vector is a **displacement** (movement). 
> In our example, it represents moving **3 units along $x$** and **2 units along $y$**. 
> * When this displacement starts from the origin $O$, we use it to define a specific position (a *position vector*). 
> * When it can start from *any* arbitrary point in the space[^1], we call it a **free vector**. It represents the pure concept of movement, regardless of where you start.

## Vector & Free Vector, Geometrical Intuition

### 1. Point vs Free Vector vs Vector in Space

A **point** answer the where are you are exactly in said space[^1], where a Vector answer how do you move in the said space[^1].

> [!IMPORTANT]+
> By default, the textbook/school taught to us that vector start at the origin of
> space. for convenience as it's simpler to reason about. but again a vector is **movement**. and any mouvement as invariable that are it's **direction** and it' **magnitude**.
> more on that in next sections.

A free vector is a mouvement in space[^1] transposed to some point in space[^1].

Eg : 
```plaintext
		   • A(2,2)
		    \ 
		     \
		      \ 
		       \
		        \
		         \> • B(4,-1)
```

Here we observe a *free vector* that we'll name $\vec{u}$ going from the points `A(2,2)` to `B(4,-1)`.
Notice that `A` & `B` are just points the actual vector vector is how do we get from a A to B ?

Simple : A + (2, -3)
So our vector's $\vec{u} = \begin{pmatrix} 2\\-3\end{pmatrix}$

> [!IMPORTANT]+
> I insist $\vec{u}$ is pure movement, not a value, it's transformation that can be realized at any point in space[^1].
> 
> As well it's symmetrical meaning we can B - $\vec{u}$ = A

### 2. Characteristic of a Vector

### 2.1 Geometric Vector

A vector or more precisely in this case a `geometric` vector that characterized by a :

- a sens
- an angle
- a direction
- and a magnitude

it's important to differentiate a `geometric` vector, from non geometric one. reason being that not every space require all characteristic given to vector.






[^1]: **Intuition (State/Parameter Space):** Much like a sample space $\Omega$ in probability theory represents the universe of all possible outcomes, a vector space here acts as the universe of all possible parameter configurations. Each vector is a specific "point" or snapshot in this universe, uniquely defined by a tuple of parameters (coordinates) spanning across the available dimensions. 