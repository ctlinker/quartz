---
title: Makfile Cheatsheet
tags:
  - cheatsheet
  - programming
---
# Makefile Cheat Sheet

> A **Makefile** is a build automation file used by `make` to define rules for compiling, building, and running projects efficiently.

---

# Basic Structure

```makefile
target: dependencies
<TAB> command
```

Example:

```makefile
main:
	gcc main.c -o main
```

> [!IMPORTANT]
> Commands MUST start with a **TAB**, not spaces.

---

# Simple Example

```makefile
all: build

build:
	gcc main.c utils.c -o app

clean:
	rm -f app
```

Usage:

```bash
make        # runs "all" by default
make build
make clean
```

---

# Variables

Define reusable values.

```makefile
CC = gcc
CFLAGS = -Wall -Wextra -O2
TARGET = app
```

Use them:

```makefile
build:
	$(CC) $(CFLAGS) main.c -o $(TARGET)
```

---

# Automatic Variables

|Variable|Meaning|
|---|---|
|`$@`|Target name|
|`$<`|First dependency|
|`$^`|All dependencies|

Example:

```makefile
app: main.c utils.c
	$(CC) $^ -o $@
```

Equivalent to:

```bash
gcc main.c utils.c -o app
```

---

# Pattern Rules

Compile many files automatically.

```makefile
%.o: %.c
	$(CC) -c $< -o $@
```

Explanation:

- `%.c` → any C file
    
- `%.o` → corresponding object file
    

---

# Full Build Example

```makefile
CC = gcc
CFLAGS = -Wall -Wextra -O2
SRC = main.c utils.c
OBJ = $(SRC:.c=.o)

app: $(OBJ)
	$(CC) $(OBJ) -o app

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(OBJ) app
```

---

# Phony Targets

Used for commands, not files.

```makefile
.PHONY: clean run all
```

Example:

```makefile
run:
	./app
```

---

# Multiple Targets

```makefile
all: build test

build:
	gcc main.c -o app

test:
	./app --test
```

---

# Conditionals

```makefile
ifeq ($(OS),Windows_NT)
	RM = del
else
	RM = rm -f
endif
```

---

# Functions

## String substitution

```makefile
FILES = main.c utils.c
OBJ = $(FILES:.c=.o)
```

---

## Wildcard

```makefile
SRC = $(wildcard *.c)
```

---

## Notdir

Remove directories:

```makefile
SRC = src/main.c src/utils.c
FILES = $(notdir $(SRC))
```

---

# Include Other Makefiles

```makefile
include config.mk
```

---

# Default Target

First target is default:

```makefile
all:
	echo "default"
```

Or explicitly:

```makefile
.DEFAULT_GOAL := all
```

---

# Silent Commands

```makefile
all:
	@echo "Building project"
```

`@` prevents command echoing.

---

# Export Variables

```makefile
export PATH := $(PATH):/custom/bin
```

---

# Recursive Make

```makefile
make -C subdir
```

---

# Debugging Makefiles

Print variable:

```bash
make -p
```

Dry run:

```bash
make -n
```

Verbose output:

```bash
make --debug
```

---

# Common Build Flow

```makefile
all: build run

build:
	gcc main.c -o app

run:
	./app

clean:
	rm -f app
```

---

# Directory-Based Project Example

```makefile
SRC = src
BIN = bin
CC = gcc

all:
	mkdir -p $(BIN)
	$(CC) $(SRC)/main.c -o $(BIN)/app

clean:
	rm -rf $(BIN)
```

---

# Dependency Example

```makefile
main.o: main.c main.h utils.h
```

Meaning:

- rebuild `main.o` if any header changes
    

---

# Recursive Pattern Build

```makefile
SRCS = $(wildcard *.c)
OBJS = $(SRCS:.c=.o)

app: $(OBJS)
	$(CC) $^ -o $@
```

---

# Key Concepts

- **Target** → what you want to build
    
- **Dependency** → what it needs
    
- **Recipe** → commands to build it
    
- **Variables** → reusable values
    
- **Pattern rules** → generic compilation rules
    
- **Phony targets** → commands like `clean`, `run`

---

# Mental Model

```text
file.c  → compile → file.o
file.o  → link    → executable

Make tracks timestamps:
If dependency is newer → rebuild target
```

---

# Most Used Commands

```text
make
make clean
make all
make run
make -j4
make -n
make -B
```

---

# Parallel Build

```bash
make -j4
```

Builds using 4 threads (faster compilation).

---

# Golden Rule

A good Makefile should:

- avoid repetition
- use variables
- use pattern rules
- include `clean`
- be readable, not clever