
# ✍️ `vi` / `vim` Editor Cheat Sheet

A quick reference guide to effectively use the `vi` or `vim` text editor on Linux.

---

## 🚀 Opening a File

```bash
vi filename
# or
vim filename
```

---

## 🛠️ Modes in `vi`

| Mode        | Description                            |
|-------------|----------------------------------------|
| Normal      | Default mode for navigation/commands   |
| Insert      | For inserting text                     |
| Visual      | For selecting text                     |
| Command     | For entering commands (starts with `:`)|

---

## 🔄 Switching Modes

- **Insert Mode**: Press `i`, `I`, `a`, `A`, `o`, or `O`
- **Visual Mode**: Press `v` (character), `V` (line), or `Ctrl+v` (block)
- **Command Mode**: Press `:` from Normal mode
- **Normal Mode**: Press `ESC`

---

## ✏️ Insert Commands

| Command | Action                     |
|---------|----------------------------|
| `i`     | Insert before cursor       |
| `I`     | Insert at line start       |
| `a`     | Append after cursor        |
| `A`     | Append at line end         |
| `o`     | Open new line below        |
| `O`     | Open new line above        |

---

## 💾 Save & Exit

| Command | Description             |
|---------|-------------------------|
| `:w`    | Save                    |
| `:q`    | Quit                    |
| `:wq`   | Save and quit           |
| `:x`    | Save and quit           |
| `:q!`   | Quit without saving     |

---

## 📦 Navigation

| Key | Description         |
|-----|---------------------|
| `h` | Move left           |
| `l` | Move right          |
| `j` | Move down           |
| `k` | Move up             |
| `0` | Start of line       |
| `^` | First non-space char|
| `$` | End of line         |
| `gg`| Start of file       |
| `G` | End of file         |
| `:n`| Go to line number `n` |

---

## 🔍 Search

```bash
/pattern       # Forward search
?pattern       # Backward search
n              # Next match
N              # Previous match
```

---

## 📋 Copy, Cut, Paste

| Command | Description         |
|---------|---------------------|
| `yy`    | Copy (yank) line    |
| `dd`    | Cut (delete) line   |
| `p`     | Paste after cursor  |
| `P`     | Paste before cursor |
| `u`     | Undo                |
| `Ctrl + r` | Redo             |

---

## 🧹 Deleting Text

| Command | Description               |
|---------|---------------------------|
| `x`     | Delete character          |
| `dd`    | Delete current line       |
| `d$`    | Delete to end of line     |
| `d^`    | Delete to beginning of line |
| `dG`    | Delete to end of file     |

---

## ⚙️ Configuration and Tools

| Command        | Description                      |
|----------------|----------------------------------|
| `:set nu`      | Show line numbers                |
| `:set nonu`    | Hide line numbers                |
| `:syntax on`   | Enable syntax highlighting       |
| `:syntax off`  | Disable syntax highlighting      |
| `:help`        | Open help                        |

---

## 📚 Learn `vim`

Start the interactive tutorial:
```bash
vimtutor
```
