---
tags:
  - memory
  - programming
title: Heap And Stack Memory
---
# Heap and Stack Memory, In a Nutshell

## Introduction

When a program runs, it needs memory to store values: variables, function calls, temporary data, objects, etc.

To manage this, most systems split runtime memory into two major regions:

- **Stack memory** → fast, structured, automatic
- **Heap memory** → flexible, dynamic, manual (or semi-manual depending on language)

They serve different purposes, and the key difference is not _what_ they store, but _how and when_ memory is allocated and freed.

---

## 1. Stack Memory (The Structured One)

### What it is

The **stack** is a region of memory used for **function calls and local variables**.
It works like a real stack (LIFO: Last In, First Out).
Every time a function is called:

A **stack frame** is created, It stores:

- Local variables
- Function parameters
- Return address

When the function ends:

- The stack frame is automatically removed

---

### Key properties

- Very fast allocation/deallocation
- Managed automatically by the compiler/runtime
- Fixed size per thread (limited memory)
- Follows function scope strictly

---

### Example (conceptual)

```c
void foo() {
    int x = 10;   // stored in stack
} // x disappears here automatically
```

When `foo()` finishes, `x` is gone instantly.

---

### Mental model

Think of the stack like a pile of plates:

- You only add/remove from the top 
- Everything is temporary and scoped

---

## 2. Heap Memory (The Growable Memory)

### What it is

The **heap** is a large pool of memory used for **dynamic allocation**.
You use the heap when:

- You don’t know the size at compile time
- You need data to live beyond a function
- You want to share data across parts of a program

---

### Key properties

- Flexible size allocation
- Slower than stack (allocation + lookup overhead)
- Requires manual management (or GC in some languages)
- Data can outlive the function that created it

---

### Example (conceptual)

```c
int* x = malloc(sizeof(int));
*x = 10;
```

Here:

- The pointer `x` is on the stack
- The actual integer (`10`) is on the heap

---

### Important idea

The heap does NOT automatically clean itself (in low-level languages).

So you must explicitly free memory:

```c
free(x);
```

If you forget → **memory leak**

If you free incorrectly → **dangling pointer / undefined behavior**

---

### Mental model

Think of the heap like a warehouse:

- You request space
- You get a reference (address)
- You are responsible for returning it

---

## 3. Stack vs Heap — Core Differences

| Feature    | Stack                           | Heap                           |
| ---------- | ------------------------------- | ------------------------------ |
| Speed      | Very fast                       | Slower                         |
| Lifetime   | Automatic (scope-based)         | Manual / GC-based              |
| Size       | Limited                         | Large (system-dependent)       |
| Allocation | Implicit                        | Explicit                       |
| Use case   | Local variables, function calls | Dynamic data, large structures |
| Risk       | Stack overflow                  | Memory leaks, fragmentation    |

---

## 4. The Most Important Mental Model

A clean way to think about it:

- **Stack = execution flow**
- **Heap = data persistence**

Or more intuitively:

- Stack answers: _“What am I doing right now?”_
- Heap answers: _“What do I need to keep alive?”_

---

## 5. Common Pitfalls

### Stack overflow

Happens when:

- Too deep recursion
- Too many large local variables

---

### Memory leak

Happens when:

- You allocate heap memory
- You lose all references to it without freeing it

---

### Dangling pointer

Happens when:

- You free memory
- But still try to use the [[pointer|pointer]] afterward

---

## 6. Modern Languages Note

Not all languages expose heap/stack directly:

- **C / C++ / Zig** → explicit control
- **Rust** → ownership system manages heap safety
- **Java / Python / JS** → garbage-collected heap
- **Go** → hybrid GC + escape analysis (some stack allocation is optimized)

Even in high-level languages:

> The stack still exists, it is just hidden.