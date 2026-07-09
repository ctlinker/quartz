---
title: Compile-Time Type Generation
tags:
  - zig
  - programming
aliases:
---
---

## Compile-Time Type Generation: A Generics Alternative

### Introduction

Zig doesn't have dedicated [[polymorphism|generic]] syntax. Instead, it achieves generic programming through **compile-time type generation**.

Because code can execute during compilation, functions can build and return entirely new types. This form of [[meta-programming#Introduction|meta-programming]] makes Zig extremely flexible while keeping the language simple.

### Example: Custom Type Generator

**`MyGenerator`** takes a compile-time type "T" and returns a new struct type containing a single field named "data".

```zig
fn MyGenerator(comptime T: type) type {
    return struct {
        data: T,
    };
}
```


> [!NOTE]
> `T` must be known at compile time. In fact any **comptime variable must be known at compile time**.

### Usage: Creating Type Constants

```zig
const myu8data: type = MyGenerator(u8); // struct { data: u8 }
const myi8data: type = MyGenerator(i8); // struct { data: i8 }
```

Creating simple type aliases is useful, but compile-time [[expression#Introduction|expression]] allow much more dynamic type generation.

```zig
pub fn List(comptime T: type, comptime is_view: bool) type {
    const Datatype = if (is_view) []const T else []T;
    const AllocatorType = if (is_view) void else std.mem.Allocator;

    return struct {
        allocator: AllocatorType,
        data: Datatype,
        len: usize,

        pub fn init(
            allocator: AllocatorType,
            data: Datatype,
        ) @This() {
            return @This(){
                .allocator = allocator,
                .data = data,
                .len = data.len,
            };
        }
    };
}

const ls = List(u8, true);

// struct {
//     allocator: void,
//     data: []const u8,
//     len: usize,
// }
```


> [!NOTE]
>`Datatype` and `AllocatorType` are computed at compile time because they depend only on compile-time parameters.

Compile-time execution is not limited to selecting types. It can also compute values used to define a type.

```zig
pub fn StaticTensor(comptime T: type, comptime dim: []const usize) type {
    comptime {
        if (dim.len == 0) {
            @compileError("Static dim cannot be 0");
        }
    }

    const size = comptime block: {
        var result: usize = 1;
        for (dim) |value| {
            result *= value;
        }
        break :block result;
    };

    return struct {
        data: [size]T,
        len: usize,
    };
}
```

>[!NOTE]
>A function returning `type` acts as a type factory. Each unique set of compile-time arguments produces a distinct concrete type.