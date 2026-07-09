---
title: Neovim Cheatsheet
tags:
  - nvim
  - vim
  - cheatsheet
publish: true
---
## Neovim Cheat-sheet

### Modes

- "n" → Normal mode
- "i" → Insert mode
- "v" → Visual mode
- "V" → Visual line mode
- "Ctrl+v" → Visual block mode
- ":" → Command mode
- "R" → Replace mode

---

### Movement

- "h j k l" → left / down / up / right
- "w" → next word
- "b" → previous word
- "e" → end of word
- "0" → start of line
- "$" → end of line
- "gg" → top of file
- "G" → bottom of file
- ":n" → go to line n

---

### Editing

- "i" → insert before cursor

- "a" → insert after cursor

- "I" → insert at line start

- "A" → insert at line end

- "o" → new line below

- "O" → new line above

- "x" → delete character

- "dd" → delete line

- "dw" → delete word

- "d$" → delete to end of line

- "u" → undo

- "Ctrl+r" → redo

---

### Copy / Paste

- "yy" → copy line
- "yw" → copy word
- "y$" → copy to end of line
- "p" → paste after cursor
- "P" → paste before cursor

---

### Visual Mode

- "v" → select text
- "V" → select line
- "y" → copy selection
- "d" → delete selection
- ">" → indent
- "<" → unindent

---

### Search

- "/text" → search forward
- "?text" → search backward
- "n" → next match
- "N" → previous match
- ":%s/a/b/g" → replace all

---

### Buffers / Files

- ":e file" → open file
- ":w" → save
- ":q" → quit
- ":wq" → save & quit
- ":bd" → close buffer
- ":ls" → list buffers
- ":b n" → switch buffer

---

### Windows

- ":vsp" → vertical split
- ":sp" → horizontal split
- "Ctrl+w h/j/k/l" → move between splits
- "Ctrl+w =" → equalize splits

---

### Macros

- "qa" → start recording macro into register a
- "q" → stop recording
- "@a" → run macro a
- "@@" → repeat last macro

---

### Useful tricks

- "." → repeat last action
- ":%norm! ..." → run normal command on all lines
- "Ctrl+o" → go back in jump list
- "Ctrl+i" → go forward in jump list

---

### Mental model

- Normal mode = operations
- Insert mode = typing
- Visual mode = selecting
- Command mode = scripting

Neovim is just: verbs + motions + repetition