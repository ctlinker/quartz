---
title: Polymorphism, Generic Programming
tags:
  - programming
---
# Polymorphism

## Introduction

One of the main goals of programming is to write code that is **generic**, **reusable**, and **easy to maintain**. Polymorphism is one of the core concepts that helps achieve this.

The word **polymorphism** comes from the Greek words:

- **poly** = many
- **morph** = forms

Literally, **"many forms."**

In programming, polymorphism means that **the same interface or operation can behave differently depending on the type it is used with.**

---

# A Simple Example

Imagine a function called `draw()`.

```text
draw(circle)
draw(square)
draw(triangle)
```

Although the function name never changes, the behavior does.

```
draw()
 ├── Circle   → draw a circle
 ├── Square   → draw a square
 └── Triangle → draw a triangle
```

The caller only knows it wants to **draw something**. The actual implementation depends on the object's type.

---

# Why Polymorphism?

Without polymorphism, programs quickly become full of type checks.

```text
if object is Circle
    ...
else if object is Square
    ...
else if object is Triangle
    ...
```

Every new type requires modifying existing code.
With polymorphism, new types simply provide their own implementation.

```text
object.draw()
```

The code using the object never needs to know which concrete type it is.
This makes software easier to extend and maintain.

---

# Different Forms of Polymorphism

Although programmers often speak of "polymorphism" as one concept, several mechanisms exist.

## 1. Ad-hoc Polymorphism (Function Overloading)

Multiple functions share the same name but accept different parameter types.

Example:

```text
print(42)
print("Hello")
print(3.14)
```

Each version is a different function chosen according to the argument types.

Languages like C++, Java, and C# support this directly.

---

## 2. Parametric Polymorphism (Generics)

The same implementation works for **any type**.

Example:

```text
List<T>
```

The list does not care whether `T` is:

- int
- float
- String
- User
- Animal

The implementation remains identical.

This is how containers like vectors, arrays, maps, and optional values are usually implemented.

Example:

```text
swap(a, b)
```

The algorithm is exactly the same regardless of the type.

Languages:

- Zig (`comptime`)
- Rust (`T`)
- C++ Templates
- Java Generics
- TypeScript Generics  

---

## 3. Subtype Polymorphism (Inheritance / Interfaces)

Different types share a common interface.

```text
Animal

Dog
Cat
Bird
```

Each implements:

```text
speak()
```

Calling

```text
animal.speak()
```

produces:

```
Dog  → Bark
Cat  → Meow
Bird → Tweet
```

The caller only knows it has an `Animal`.
This is the most common definition of polymorphism in object-oriented programming.

---

# Compile-Time vs Runtime Polymorphism

Not all polymorphism happens the same way.

## Compile-Time

The compiler already knows the concrete type.

Example:

```text
max(3, 5)
```

The compiler generates code specifically for integers.

Advantages:

- very fast
- zero runtime overhead
- often optimized away

Examples:

- Templates
- Generics
- Zig's `comptime`

---

## Runtime

The exact type is only known while the program is executing.

Example:

```text
Animal* animal = getAnimal();
animal.speak();
```

The program decides at runtime whether `animal` is a Dog, Cat, or Bird.

This typically requires:

- virtual tables (vtables)
- interfaces
- dynamic dispatch

Advantages:

- flexible
- extensible

Disadvantages:

- slight runtime cost

---

# Duck Typing

Some languages use another form of polymorphism called **Duck Typing**.

The famous expression is:

> _"If it walks like a duck and quacks like a duck, then it is a duck."_
> source: the duck test

Instead of checking the type, the language checks whether the required methods exist.

Example:

```text
move(entity)
```

Anything with a `move()` function works.
Python and JavaScript rely heavily on this style.

---

# Static vs Dynamic Languages

Static languages usually verify polymorphism during compilation.

Examples:

- Zig
- Rust
- C++
- Go

Dynamic languages resolve it while running.

Examples:

- Python
- JavaScript
- Ruby

Neither approach is universally better; they make different trade-offs between safety, flexibility, and performance.

---

# Real-World Analogy

Imagine a TV remote.

Every television exposes the same buttons:

- Power
- Volume
- Channel

Pressing **Power** works on every TV.

However, each manufacturer implements the electronics differently.
The user interacts with **one interface**, while each TV performs its own implementation.
That is polymorphism.

---

# Relationship with Other OOP Concepts

Polymorphism is often presented alongside three other concepts.

|Concept|Purpose|
|---|---|
|Encapsulation|Hide implementation details behind an interface.|
|Abstraction|Expose only what is necessary.|
|Inheritance|Reuse behavior between related types.|
|**Polymorphism**|Allow one interface to represent many concrete implementations.|

Notice that **inheritance is not required** for polymorphism. Modern languages such as Rust, Go, Zig, and TypeScript achieve polymorphism using interfaces, traits, generics, or structural typing without relying on classical inheritance.

---

# Summary

Polymorphism allows **one interface to represent many implementations**.
Depending on the language, this may be achieved through:

- Function overloading (ad-hoc polymorphism)
- Generics or templates (parametric polymorphism)
- Interfaces, traits, or inheritance (subtype polymorphism)
- Duck typing (structural polymorphism)

Its primary goal is to write code that is **more reusable**, **more extensible**, and **less dependent on concrete types**, allowing new types to integrate into existing code with minimal changes.