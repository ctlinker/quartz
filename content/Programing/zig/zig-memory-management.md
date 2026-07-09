---
title: Zig Memory Management
tags:
  - zig
  - memory
  - programming
---
## Zig How to deal with memory

## Introduction

Zig is a C-like modern programming language. It's memory managenent requiere one to understand :

- [[pointer|pointer]]
- value lifetime
- And type it's constrain

> [!IMPORTANT]
> Do not get me wrong zig does not enforce data ownership instead it nudge us programmarers to properly:
>
>- manage
>- ask
>- free
>
>memory through [[pointer|pointer]], allocator, and memory location.

## Using and freeing memory

In common language allocating memory and it's location are abstracted as the same thing.

- C as `malloc`, `realloc` and `free` 
```c
int *val = (int *)malloc(10 * sizeof(int)); 
free(val);
```

- Go has the `make` function
```go
var val []int8 = make([]int8, 0); // cree une liste d'entier sur 8 bit
```

- Rust as dedicated [[heap&stack|Heap/Stack]] type datastructure
```rust
let val = Vec<i8>; // cree une vecteur/list d'entier sur 8bit
```

All of these have in common that memory location and it's allcoation are abstracted under a default model.

> Zig does not. Zig is explicit. There'more than one way to allocate memory and to manage it.


## Memory Allocators

### 1. Raw Vs Managed Allocator

Zig In order to allocate memory zig put at our dispostion two kind of allocator :

- Raw Allocator
- Managed Allocator

Each kind implement the "std.mem.Allocator" interface. The gimick being that raw allocator are allocator that directly implement it :

- `std.heap.page_allocator`
- `std.heap.c_allocator`
- `std.heap.wasm_allocator`

And managed allocator are allocator that manage fized memory or another allocator.

- `std.heap.ArenaAllocator.init(allocator)`
- `std.heap.FixedBufferAllocator.init(&buffer) // buffer is typeof [size]type`

>[!NOTE] 
> Managed allocator expose there `std.mem.Allocator` interface under the .allocator() method

### 2. Differentiating an Allocator

Managed allocators usually expose a `std.mem.Allocator` through their `.allocator()` method. Raw allocators already are `std.mem.Allocator` implementations, so no conversion is necessary.

As well, the naming convention for allocators goes as: 
- **CamelCase** for **managed allocator**
- **snake_case** for **raw allocator**

> [!IMPORTANT]
> Beware that naming may still be ambiguous eg: `std.heap.FixedBufferAllocator`.
> Be sure to read the lsp tooltip on each imported func from the std.heap

### 3. Choosing an allocator

Allocator Implement the `std.mem.Allocator` interface. the std library provide built in allocator under `std.heap`.

#### Page Allocator

The page allocator is the global allocator 

#### FixedSizeBuffer


#### Arena Allocator

The arena allocator is a managed allocator, it's perk being that on call for `.deinit()` all allocate memory by it is freed.

> It's particularly usefull when you've a lot of data to allocate / deallocate and don't want to keep track of everything you may have done. 

```zig
const page = std.heap.page_allocator;
var arena = std.heap.ArenaAllocator.init(page);
defer arena.deinit();
const allocator = arena.allocator();
```

Here:

- `page_allocator` already satisfies the allocator interface.
- `ArenaAllocator` is a manager object with additional state.
- `.allocator()` returns the allocator interface that clients use.

## Asking for Data

One of Zig's design principles is making ownership and mutation explicit.
When a function needs access to data, it can ask for it in three different ways.
### Read-only access

If a function only needs to inspect a value, it usually accepts a constant [[pointer|pointer]].

```zig
fn doSomething(value: *const MyType) void {
	std.debug.print("{}\n", .{value.field});
}
```

Here the function promises not to modify the pointed value.

> [!NOTE]  
> `*const T` means "read-only access through this [[pointer|pointer]]."

---

### Mutable access

If a function needs to modify an existing object, it accepts a mutable pointer.

```zig
fn reset(counter: *Counter) void { 
	counter.value = 0;
}
```

Changes are applied directly to the caller's object.

---

### By value

Sometimes the function simply needs its own copy.

```
fn distance(a: Vec2, b: Vec2) f32 {...}
```

The caller's values are copied (or optimized by the compiler when possible), allowing the function to modify its local copies without affecting the originals.

> [!TIP]  
> Passing by value is often preferred for small structs because it keeps APIs simple and can be just as efficient.

