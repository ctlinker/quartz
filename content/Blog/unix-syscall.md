---
title: Unix Syscall
tags:
  - unix
---
Unix Syscall

### 1. Context

Unix syscall philosophy is of the following

```plaintext
syscall(
	RAX = syscall number,
	RDI = argument 1,
	RSI = argument 2,
	RDX = argument 3,
)
```

RAX: "I want operation #1"
RDI: "first parameter"
RSI: "second parameter"
RDX: "third parameter"
- kind: which kind of syscall do you need ?
- fd : file descriptor
- request: which question question/command are you asking the kernel for 
- argument: where in memory to write the response (see [[pointer|pointer]])

> [!IMPORTANT]
> Unix like operating system eg (linux, free bsd). describe everything as file. from te save of your game, to your mouse/keyboard, network socket and even your ram and drive. see the content of **/dev** folder.
> 
> A file descriptor give us the unix kernel's index related to a given file. 

> [!NOTE]+
> A **`uintptr`** is **NOT** a pointer, it's an **unsigned integer type large enough to store the numeric value of a pointer address**.
> So on a typical machine:
> - 32-bit system → `uintptr` is usually 32 bits
> - 64-bit system → `uintptr` is usually 64 bits
>
> Why do we need a `uintptr ` ?
> 
> For the simple reason that cpu/gpu architecture differ from machine to another. and so does the bytes length the said cpu/gpu can handle, as it's pointer length.



