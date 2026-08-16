---
title: Markdown How To Write Table
tags:
  - markdown
  - cheatsheet
---
## Syntax

The syntax is straightforward and stand as follow : 

```md
| Column 1 | ... | Column N |
|----------|-----|----------|
| Content  | ... | Content  |
```

## Text Alignment

Text can be aligned in the table by using the row below the column headers.

- `:------` align to the left
- `------:` align to the right
- `:-----:` center the text

## Exemples

### A simple table

**Code**

```md
| Column 1 | ... | Column N |
|----------|-----|----------|
| Content  | ... | Content  |
```

**Illustration**

| Column 1 | ... | Column N |
|----------|-----|----------|
| Content  | ... | Content  |


### A table with it's last column right aligned

**Code**

```md
| Column 1 | ... | Column N  |
|----------|-----|----------:|
| Content  | ... | Content   |
```

**Illustration**

| Column 1 | ... | Column N  |
|----------|-----|----------:|
| Content  | ... | Content   |

### A table with it's middle column centered

**Code**

```md
| Column 1 | ... | Column N  |
|----------|:---:|-----------|
| Content  | ... | Content   |
```

**Illustration**

| Column 1 | ... | Column N  |
|----------|:---:|-----------|
| Content  | ... | Content   |
