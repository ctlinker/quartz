---
title: How To Peg
tags:
  - programming
  - parser
---
# PEG (Parsing Expression Grammar)

## Overview

**PEG (Parsing Expression Grammar)** is a formal grammar notation used to describe parsers. It was introduced by Bryan Ford in 2004 as an alternative to traditional **context-free grammars (CFGs)** used in tools like Yacc and Bison.

A PEG describes how a sequence of characters should be recognized and transformed into a structured representation, usually an **Abstract Syntax Tree (AST)**.

Unlike CFGs, PEG grammars are **deterministic**: when multiple rules could match, PEG always chooses the first successful alternative.

---

# Core Idea

A PEG grammar is composed of:

- **Rules**: named parsing expressions
- **Terminals**: literal characters or tokens
- **Combinators**: operators that combine expressions

Example:

```peg
Expression <- Number "+" Number

Number <- [0-9]+
```

This grammar recognizes:

```
12+34
```

---

# Parsing Expression Operators

## Sequence

Match expressions in order.

Syntax:

```peg
A B
```

Example:

```peg
Greeting <- "hello" " " "world"
```

Matches:

```
hello world
```

---

## Ordered Choice

Try alternatives from left to right.

Syntax:

```peg
A / B
```

Example:

```peg
Value <- "true" / "false"
```

If `"true"` matches, PEG stops and does not try `"false"`.

This differs from CFGs where alternatives are usually unordered.

---

## Repetition

### Zero or more

```peg
A*
```

Example:

```peg
Digits <- [0-9]*
```

Matches:

```
12345
```

or an empty string.

---

### One or more

```peg
A+
```

Example:

```peg
Digits <- [0-9]+
```

Requires at least one digit.

---

### Optional

```peg
A?
```

Example:

```peg
Sign <- "+"?
```

Matches:

```
+
```

or nothing.

---

# Predicates

PEG supports lookahead without consuming input.

## Positive lookahead

```peg
&A
```

Succeeds if `A` matches.

Example:

```peg
Keyword <- &"if" Identifier
```

Checks that `"if"` exists but does not consume it.

---

## Negative lookahead

```peg
!A
```

Succeeds if `A` does not match.

Example:

```peg
Identifier <- !Keyword [a-z]+
```

Prevents keywords from being parsed as identifiers.

---

# PEG vs Context-Free Grammar

|Feature|PEG|CFG|
|---|---|---|
|Ambiguity|Impossible by design|Possible|
|Choice|Ordered|Unordered|
|Parser type|Usually recursive descent|Often generated parsers|
|Backtracking|Built-in|Usually not|
|Implementation|Directly executable|Requires parser construction|

Example ambiguity:

CFG:

```
A -> "a" | "ab"
```

PEG:

```
A <- "a" / "ab"
```

PEG always chooses `"a"` because it appears first.

---

# PEG and Programming Languages

PEG is commonly used for:

- Programming language parsers
- Configuration formats
- DSLs
- Command interpreters
- Data serialization formats

Examples:

- Tree-sitter uses grammar descritions inspired by parsing expression techniques.
- ANTLR supports grammar-based language tooling, though its approach is based on CFG-style grammars.

Popular PEG tools:

- pest — PEG parser framework for Rust
- pigeon — PEG parser for go
- PEG.js — generates JavaScript parsers
- Ohm — grammar-based language toolkit

---

# PEG in Compiler Design

A typical compiler pipeline:

```
Source Code
     |
     v
Lexer
     |
     v
Parser (PEG)
     |
     v
AST
     |
     v
Semantic Analysis
     |
     v
Code Generation
```

PEG can replace the lexer/parser separation in small languages because lexical rules can also be expressed directly.

---

# PEG and DSL Design

PEG is especially useful when creating a custom language.

A DSL can define:

```
program <- statement*

statement <- assignment / function / import

assignment <- identifier "=" expression
```

The grammar becomes the specification of the language itself.

This makes PEG attractive for:

- configuration languages
    
- build systems
    
- protocol definitions
    
- code generation tools
    

---

# Limitations

PEG is not perfect:

- Backtracking can become expensive.
- Poorly designed grammars can cause performance issues.
- Left recursion is usually not supported directly.

Example:

```peg
Expression <- Expression "+" Number
```

This causes infinite recursion.

It must be rewritten:

```peg
Expression <- Number ("+" Number)*
```

---

# Summary

PEG is a **deterministic grammar formalism** where:

- rules describe how input is recognized,
- choices are ordered,
- the first successful match wins,
- grammars can directly become parsers.

Its simplicity makes it a strong choice for building custom languages, parsers, and DSLs.