---
title: Les Pointeur
tags:
  - memory
  - programming
---
## Pointer: How to find [[data|Data]] in Memory

### Introduction

Un pointer est un type de donnée qui stocke uniquement **une adresse mémoire**.

On les retrouve principalement dans les langages de programmation bas niveau ou compilés, où la gestion de la mémoire est explicite.

> [!IMPORTANT]  
> A pointer only holds a memory address and an expected interpretation of what is stored there.
> 
> It does NOT guarantee that:
> 
> - the memory is still allocated
>     
> - the value at that address is valid
>     
> 
> This leads to cases like **dangling pointers**, which point to freed or invalid memory.

---

## Types of pointers

### 1. Pointeur vers valeur unique (Scalar / Raw Pointer)

Pointer vers une seule valeur en mémoire.

```plaintext
{
    addr: memory_address
}
```

---

### 2. Pointeur de liste (Slice / Fat Pointer)

Used to represent a sequence of values in memory.

Memory can be contiguous or represented as a view depending on the system.

```plaintext
{
    addr: memory_address,
    len: number_of_elements,
    stride: bytes_between_elements
}
```

> Metadata depends on the language and memory model.

---

### 3. Pointeur Null (Null Pointer)

A null pointer is a special pointer value that explicitly represents **no valid memory address**.
It does not point to unknown memory; it points to nothing.
It is often used to indicate:

- absence of value
- uninitialized pointer state
- optional data

---

## Dereferencing

A pointer has one key operation: **dereferencing**.

> Dereferencing means accessing the value stored at the memory address pointed to by the pointer.

```plaintext
*ptr → value at addr(ptr)
```

Depending on the language, dereferencing may allow:

- read access
- write access
- ownership / memory deallocation (in ownership systems)

---

## TL;DR

- **pointer** → GPS coordinate
- **dereference** → arriving at the location
- **slice pointer **→ GPS + size (and possibly stride metadata)
- **null pointer** → “no location”

> A pointer is not “data”, it is a **tag that indicate where you could* find it in memory**































