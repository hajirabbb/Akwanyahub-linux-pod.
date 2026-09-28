# Week 2: Open Source, the Command Line, and Getting Help


This week covered three chapters:

1. Chapter 4: Open Source Software and Licensing
2. Chapter 5: Command Line Skills
3. Chapter 6: Getting Help

---

## Chapter 4: Open Source Software and Licensing

### What is open source?

Open source software is software whose **source code** is available for anyone to view, study, and modify. Source code is the set of instructions written by programmers that is used to create software. Open source makes those instructions accessible, which encourages collaboration. **Linux** is the classic example. The Linux kernel is written mainly in C, with small parts in assembly.

### Software licences

A licence defines what users are allowed to do with software:

- Use it
- Copy it
- Modify it
- Share it
- Redistribute it

Without a licence, you cannot assume you have any of these rights.

### Free software vs open source

| | Free Software | Open Source |
|---|---|---|
| Focus | User freedom | Access to source code and better development |
| Core question | Does this respect the user's freedom? | Does open collaboration produce better software? |
| Tone | Ethical / philosophical | Practical / commercial |
| Championed by | FSF | OSI |

Free software rests on **four essential freedoms**:

- **Freedom 0:** run the program for any purpose
- **Freedom 1:** study how it works and change it
- **Freedom 2:** redistribute copies
- **Freedom 3:** distribute modified copies

"Free" here means *freedom*, not *price* ("free as in freedom, not free as in beer"). In practice, licences such as GPL, MIT, Apache and BSD satisfy both definitions. The difference is mostly the reasoning behind the rules, not the rules themselves.

### Important organisations

- **FSF (Free Software Foundation):** promotes software freedom and free software principles. Founded by Richard Stallman in 1985.
- **OSI (Open Source Initiative):** promotes open source software and defines the criteria a licence must meet to count as open source (the Open Source Definition).

### Open source vs closed source

| | Open Source | Closed Source |
|---|---|---|
| Source code | Visible to everyone | Hidden, owned by a company |
| Who can modify it | Anyone, within the licence | Only the owner |
| Support | Community, or paid services | Official vendor support |
| Transparency | High, code can be audited | Low, you trust the vendor |
| Examples | Linux, Firefox, Python | Windows, Photoshop |

Key points:

- Open source is about the **code**, not the **price**. Companies such as Red Hat make money from support, hosting and enterprise features built around open source software.
- Closed source offers support, accountability and a consistent experience. Open source offers transparency and freedom. Neither is universally better.
- Visible code is not the same as open source. "Source available" licences let you read the code but restrict modification or commercial use, so they fail both definitions.

### Why standards matter

Standards are agreed specifications that let independent companies build products that still work together.

- **Different systems work together:** email sent from Android opens on Windows because both follow shared standards (SMTP, MIME).
- **Common specifications:** USB defines the voltage, data rules and connector, so any USB device works with any USB port.
- **Better compatibility:** a PDF opens the same on Linux, Windows and macOS.
- **Collaboration across companies:** Wi-Fi (IEEE 802.11) is why a TP-Link router works with Dell laptops and Samsung phones.
- **Easier to maintain and develop:** HTML and CSS standards let developers write one website that renders in Chrome, Firefox and Safari.

---

## Chapter 5: Command Line Skills

### The Linux command line (CLI)

CLI stands for Command Line Interface. It lets you interact with Linux by typing commands. It is:

- Powerful, fast and precise
- Automatable through scripts
- Consistent across Linux distributions

Most servers have no graphical interface at all, so the CLI is often the only way in.

### Terminal, shell and Bash

| Term | Role |
|---|---|
| **Terminal** | The window where commands are typed |
| **Shell** | The program that interprets the commands |
| **Bash** | One of the most common Linux shells ("Bourne Again SHell") |

Bash supports command history, scripting, aliases and variables.

Example prompt:

```bash
sysadmin@localhost:~$
```

- `sysadmin` is the user
- `localhost` is the machine
- `~` is the current directory (the user's **home directory**, not the root directory `/`)
- `$` means a regular user (`#` would mean the root user)

### Command structure

```bash
command [options] [arguments]
```

Example:

```bash
ls -lh /usr/bin
```

- `ls` is the command (list directory contents)
- `-l` is an option for long format
- `-h` is an option for human-readable sizes
- `/usr/bin` is the argument, the thing being acted on

Options change **how** a command behaves. Arguments say **what** it acts on.

### Reading `ls -l` output

```
-rw-r--r--  1 hajira hajira  4096 Sep 26 10:15 notes.txt
```

| Column | Meaning |
|---|---|
| `-rw-r--r--` | Permissions |
| `1` | Number of hard links |
| `hajira` (first) | Owner |
| `hajira` (second) | Group |
| `4096` | Size (`-h` turns this into values like `4.0K`) |
| `Sep 26 10:15` | Last modified date and time |
| `notes.txt` | Filename |

### File permissions

Three permission types:

- **r (read):** view a file, or list a directory
- **w (write):** modify a file, or add and remove files in a directory
- **x (execute):** run a file, or enter a directory

They are set for three categories: **owner**, **group** and **others**.

The 10-character string splits into a file type (`-` file, `d` directory, `l` link) followed by three sets of `rwx` for owner, group and others.

Numeric shorthand: `r=4`, `w=2`, `x=1`, added up per category. For example, `chmod 755 file` gives the owner `rwx`, and the group and others `r-x`.

### Command history

| Method | What it does |
|---|---|
| `!!` | Rerun the last command (for example `sudo !!`) |
| Up / Down arrows | Step through history |
| `history` then `!n` | Rerun a command by its number |
| `!string` | Rerun the latest command starting with that text |
| `Ctrl + R` | Search history as you type |

### Variables

```bash
NAME="Shola"
echo $NAME
```

Output:

```
Shola
```

`NAME=` sets the variable and `$NAME` reads it. Two important built-in variables:

- **PATH:** a list of directories the shell searches to find commands
- **HOME:** the path to the user's home directory

### How the shell finds a command

**PATH does not contain commands. It contains directory locations.** The executables live inside those directories.

1. You type a command such as `ls`
2. The shell checks whether it is a builtin, alias or function
3. If not, the shell searches each directory in `PATH`, in order
4. When it finds a matching file (for example `/usr/bin/ls`), it executes it

View your PATH:

```bash
echo $PATH
```

---

## Chapter 6: Getting Help

Linux has thousands of commands, and nobody memorises them all. What matters is knowing how to look them up quickly. Built-in help tells us what a command does, what options it has, and how to use it.

| Tool | Example | Best for |
|---|---|---|
| `man` | `man ls` | Full manual: purpose, usage, options, examples |
| `--help` | `ls --help` | A quick overview of usage and common options |
| `info` | `info ls` | Detailed documentation organised into sections (nodes) |

Think of `man` as a textbook chapter, `--help` as a cheat sheet, and `info` as a reference manual with a table of contents.

### Finding where a command comes from

```bash
which ls
type ls
```

- `which` shows the location of an executable by searching the directories in `PATH` (for example `/usr/bin/ls`)
- `type` also reveals whether the command is a builtin, alias or function

This is useful when several versions of a tool are installed and you need to know which one is actually running.

---

## Command cheat sheet

| Command | Purpose |
|---|---|
| `ls -lh /usr/bin` | Detailed, readable directory listing |
| `echo $NAME` | Print a variable's value |
| `echo $PATH` | Show the directories the shell searches |
| `!!` | Rerun the last command |
| `history` | Show numbered command history |
| `man ls` | Full manual page for `ls` |
| `ls --help` | Quick usage summary |
| `info ls` | Detailed info documentation |
| `which ls` | Location of the executable |
| `type ls` | What kind of command it is, and where it comes from |

---

## Key takeaways

- Open source is about access to code, while free software is about user freedom. The licences overlap heavily, but the reasoning differs.
- Open source does not mean no money. Businesses build on it through support, hosting and enterprise features.
- The CLI is fast, precise and scriptable, and it is often the only interface on a server.
- The terminal is where you type, the shell interprets, and Bash is one specific shell.
- PATH stores search locations, not commands.
- Nobody memorises every command. `man`, `--help` and `info` are how you find what you need.

## Reflection

<!-- Add your own words here: what surprised you this week, what clicked, and how presenting with Team Zuri went. -->