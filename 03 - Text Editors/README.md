# Module 3: Text Editors

## Overview

Working with Linux day to day means constantly reading, inspecting, comparing, and editing plain text files: configuration files, logs, scripts, and code. This module covers the command-line tools Linux provides for that job, starting with the lightweight utilities used to view and compare files, then moving into full text editors — with a strong focus on Vim, since some vi-compatible editor ships with virtually every Linux distribution and is the one tool you can always rely on being available, even on a minimal server with no graphical environment.

This module also covers modern editor options such as VS Code, which is common in DevOps, SRE, and development workflows, but the emphasis stays on terminal-based editing, since that is the skill that matters most when working directly on remote servers.

## Table of Contents

- [Lesson 1: Viewing and Comparing Text Files](#lesson-1-viewing-and-comparing-text-files)
  - [1. Text Editors in Linux: An Overview](#1-text-editors-in-linux-an-overview)
  - [2. Viewing File Content with `cat`](#2-viewing-file-content-with-cat)
  - [3. Counting Lines, Words, and Characters with `wc`](#3-counting-lines-words-and-characters-with-wc)
  - [4. Numbering Lines with `cat -n`](#4-numbering-lines-with-cat--n)
  - [5. Viewing Multiple Files at Once with `cat`](#5-viewing-multiple-files-at-once-with-cat)
  - [6. Creating and Overwriting Files with `cat` and Redirection](#6-creating-and-overwriting-files-with-cat-and-redirection)
  - [7. Appending to a File with `cat >>`](#7-appending-to-a-file-with-cat-)
  - [8. Paging Through Long Files with `more`](#8-paging-through-long-files-with-more)
  - [9. Paging and Searching with `less`](#9-paging-and-searching-with-less)
  - [10. Generating Test Data with `seq`](#10-generating-test-data-with-seq)
  - [11. Viewing the End of a File with `tail`](#11-viewing-the-end-of-a-file-with-tail)
  - [12. Viewing the Beginning of a File with `head`](#12-viewing-the-beginning-of-a-file-with-head)
  - [13. Comparing Files with `diff`](#13-comparing-files-with-diff)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson)
  - [Key Takeaways](#key-takeaways)

---

# Lesson 1: Viewing and Comparing Text Files

This lesson covers the command-line tools Linux provides for reading, counting, paging through, and comparing text files. These tools are the foundation for everything that follows: before editing a file with Vim, you almost always need to inspect it first.

## 1. Text Editors in Linux: An Overview

Linux offers two broad categories of tools for working with text. The first is graphical, editor-style tools such as VS Code, Cursor, or Antigravity — common in DevOps, SRE, and development work, but dependent on having a desktop environment or a remote editing connection. The second category is terminal-based editors: Vim, Nano, Emacs, and file-manager-style tools like Midnight Commander (`mc`). These run entirely inside a terminal session, which makes them the only option when you are connected to a remote server over SSH with no graphical interface.

Vim is the recommended default for this reason: some vi-compatible editor ships with essentially every Linux distribution, and the full Vim is preinstalled on the large majority of them. If a system doesn't have Vim, it can be installed with the distribution's package manager — on Debian and Ubuntu:

```bash
sudo apt install vim
```

On other distributions, use the equivalent package manager (`dnf`, `pacman`, `apk`, etc.). macOS also ships with Vim by default, so the same skills transfer directly to a Mac terminal.

> **Note:**
> The course lab environment includes a dedicated Vim practice tool (the "Vim Dojo") with a series of hands-on challenges for building muscle memory with Vim commands, plus a ready-to-use VS Code instance. Both are available directly from the lab's toolbar, so Vim skills can be practiced without any local setup — a plain Debian or other Linux terminal from the lab environment works just as well for following along with the examples in this lesson.

## 2. Viewing File Content with `cat`

`cat` (short for *concatenate*) prints the entire content of a file to standard output. It's the simplest way to look inside a file:

```bash
cat chapter03.md
```

For a short file this works well, but for a large file it dumps everything at once, scrolling past faster than it can be read — which is the motivation for the paging tools covered later in this lesson.

## 3. Counting Lines, Words, and Characters with `wc`

`wc` (word count) reports the size of a file in three dimensions at once: lines, words, and bytes/characters. Run without any flags, it prints all three:

```bash
wc chapter03.md
```

Each measurement can also be requested individually:

```bash
wc -l chapter03.md   # line count
wc -w chapter03.md   # word count, e.g. "4397 chapter03.md"
wc -c chapter03.md   # byte/character count
```

This is useful for quickly gauging how large a file is — for example, confirming a file is around 27 KB and roughly 4,400 words before deciding whether to `cat` it directly or use a pager.

## 4. Numbering Lines with `cat -n`

Adding `-n` numbers every line of the output:

```bash
cat -n chapter03.md
```

This is helpful when you need to reference a specific line — for example, checking what content sits at line 300 of a file, which would otherwise require counting manually.

## 5. Viewing Multiple Files at Once with `cat`

`cat` accepts more than one filename and concatenates them in the order given, printing the first file's content immediately followed by the second's:

```bash
cat chapter03.md arquivo.txt
```

This is a quick way to inspect two related files together without switching between separate commands.

## 6. Creating and Overwriting Files with `cat` and Redirection

`cat` can also be used in reverse: instead of reading a file, it reads from standard input (the keyboard) and writes whatever is typed to a file, using output redirection with `>`:

```bash
cat > giropops.txt
```

After running this, everything typed is written to `giropops.txt` once the input is terminated. The correct way to signal the end of input is **Ctrl+D**, which sends an end-of-file (EOF) signal that `cat` is waiting for. Pressing Ctrl+C instead sends an interrupt signal that kills the `cat` process — it happens to also leave the already-typed lines in the file, because `cat` writes each line to disk as it's read rather than buffering the whole input in memory, but Ctrl+D is the correct and intentional way to end the input.

> **Warning:**
> A single `>` always truncates the target file first, before anything new is written — even if the file already had content. Running `cat > giropops.txt` a second time discards everything that was in the file previously. If the goal is to add content without losing what's already there, use `>>` instead (see the next section).

## 7. Appending to a File with `cat >>`

Using two redirection symbols (`>>`) appends the new content to the end of the file instead of replacing it:

```bash
cat >> giropops.txt
```

Anything typed after this command is added after the file's existing content, leaving what was already there untouched. Mixing up `>` and `>>` is one of the most common ways to accidentally destroy file content, since a single missing character silently changes "add to this file" into "erase this file and start over."

## 8. Paging Through Long Files with `more`

`more` displays a file one screen at a time instead of dumping the whole thing like `cat` does:

```bash
more chapter03.md
```

Inside `more`: **Space** advances a full page, **Enter** advances a single line, `/pattern` searches forward for text, and `q` quits. Its main limitation is that navigation only moves forward through the file — there's no way to scroll back up to a previous page.

## 9. Paging and Searching with `less`

`less` is a more capable pager that solves `more`'s biggest limitation: it supports free movement through the file using the arrow keys, in both directions, not just forward.

```bash
less chapter03.md
```

Searching works the same way as `more`, with `/pattern` searching forward from the current position and highlighting matches. From there:

- `n` jumps to the next match.
- `N` (uppercase) jumps to the previous match, searching backward instead of forward.
- Typing a line number followed by `g` jumps directly to that line. If the number is larger than the total number of lines in the file, `less` jumps to the last line instead of producing an error.
- `q` quits.

Because it supports backward navigation and doesn't require re-reading the whole file for every movement, `less` is generally the better default choice over `more` for exploring a file interactively.

## 10. Generating Test Data with `seq`

`seq` prints a sequence of numbers, which is a convenient way to generate predictable sample data for testing other commands:

```bash
seq 1 50 > numbers.txt
```

This writes the numbers 1 through 50 to `numbers.txt`, one per line. The `numbers.txt` file created here is used in the following sections to demonstrate `tail`, `head`, and `diff`.

## 11. Viewing the End of a File with `tail`

`tail` prints the end ("tail") of a file. By default, it shows the last 10 lines:

```bash
tail numbers.txt
```

The number of lines can be controlled with `-n`:

```bash
tail -n 15 numbers.txt
```

The most important use of `tail` in daily operations is its follow mode, `-f`, which keeps the file open and prints new lines to the terminal as they are appended — instead of exiting once the current content has been displayed:

```bash
tail -f numbers.txt
```

This is exactly how log files are monitored in real time: running `tail -f` against an authentication log or application log lets new entries appear on screen the moment they're written, which is essential for watching a system as it happens rather than repeatedly re-running `cat` or `tail` to check for updates.

## 12. Viewing the Beginning of a File with `head`

`head` is the counterpart to `tail`: it prints the beginning of a file instead of the end. By default, it shows the first 10 lines:

```bash
head numbers.txt
```

Like `tail`, the count can be adjusted with `-n`:

```bash
head -n 15 numbers.txt
```

## 13. Comparing Files with `diff`

`diff` compares two files line by line and reports what's different between them. This is heavily used across the Linux ecosystem — Git, for example, relies on the same kind of comparison to show what changed between commits.

Given two files, `numbers.txt` (containing 1 through 50) and `numbers2.txt` (containing 1 through 45):

```bash
diff numbers.txt numbers2.txt
```

`diff` treats the first argument as the "original" and the second as the version being compared against it. The output reports that lines 46 through 50 exist in `numbers.txt` but not in `numbers2.txt`. Swapping the argument order reverses the framing: `diff numbers2.txt numbers.txt` reports that lines 46 through 50 are missing from `numbers2.txt` and need to be added to match `numbers.txt`. The direction of the arguments changes which file is treated as the baseline, so it always matters which file is listed first.

Adding `-u` switches to unified diff format, which is easier to read and is the format used by Git and most code review tools:

```bash
diff -u numbers.txt numbers2.txt
```

In unified format, lines that exist only in the first file are prefixed with `-`, and lines that exist only in the second file are prefixed with `+`, shown alongside a few lines of unchanged context. Comparing in the opposite direction (`diff -u numbers2.txt numbers.txt`) simply flips which side the `-` and `+` lines belong to.

`diff` never modifies either file — it only reports the difference between them. Run `diff --help` or `man diff` for the full list of options; it supports many more comparison modes than covered here, including comparing entire directories at once.

## Important Commands from This Lesson

| Command | Purpose |
|---|---|
| `cat FILE` | Print a file's entire content to the terminal. |
| `cat -n FILE` | Print a file's content with line numbers. |
| `cat FILE1 FILE2` | Print two files' content one after the other. |
| `cat > FILE` | Write typed input to `FILE`, overwriting any existing content. |
| `cat >> FILE` | Write typed input to `FILE`, appending to existing content. |
| `wc FILE` | Show line, word, and byte counts for a file. |
| `wc -l` / `-w` / `-c` | Show only the line / word / byte count. |
| `more FILE` | Page through a file forward only. |
| `less FILE` | Page through a file with free forward/backward navigation and search. |
| `seq 1 N > FILE` | Generate a file containing the numbers 1 through N. |
| `tail FILE` | Show the last 10 lines of a file. |
| `tail -n N FILE` | Show the last N lines of a file. |
| `tail -f FILE` | Follow a file and print new lines as they are appended. |
| `head FILE` | Show the first 10 lines of a file. |
| `head -n N FILE` | Show the first N lines of a file. |
| `diff FILE1 FILE2` | Show line differences between two files. |
| `diff -u FILE1 FILE2` | Show line differences in unified (Git-style) format. |

## Key Takeaways

* Terminal-based editors (Vim, Nano, Emacs, `mc`) are the only editing option on a server without a graphical environment, which is why Vim — installed by default on nearly every distribution — is the recommended default to learn well.
* `cat` both reads files (printing their content) and writes them (via `>`/`>>` redirection), but a single `>` always truncates the target file first — use `>>` to append instead of overwrite.
* `more` and `less` both page through long files instead of dumping them all at once; `less` is generally preferable because it supports backward navigation and jumping to a specific line.
* `tail -f` is the standard way to watch a file for new content in real time, most commonly used to monitor logs as they're written.
* `head` and `tail` show the beginning and end of a file, respectively, defaulting to 10 lines and accepting `-n` to change that count.
* `diff` reports the differences between two files line by line, treating the first argument as the baseline; `-u` produces the more readable unified format used by Git.
