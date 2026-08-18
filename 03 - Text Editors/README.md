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
- [Lesson 2: Getting Started with Vim](#lesson-2-getting-started-with-vim)
  - [1. Vi, Vim, and Why Editor Fluency Matters](#1-vi-vim-and-why-editor-fluency-matters)
  - [2. Opening Vim and Its Modes](#2-opening-vim-and-its-modes)
  - [3. Movement in Normal Mode](#3-movement-in-normal-mode)
  - [4. Yanking (Copying) and Pasting Text](#4-yanking-copying-and-pasting-text)
  - [5. Deleting and Cutting Text](#5-deleting-and-cutting-text)
  - [6. Entering Insert Mode from Different Positions](#6-entering-insert-mode-from-different-positions)
  - [7. Visual Mode: Selecting Text](#7-visual-mode-selecting-text)
  - [8. Saving and Quitting a File](#8-saving-and-quitting-a-file)
  - [9. Undo and Redo](#9-undo-and-redo)
  - [10. Searching for Text](#10-searching-for-text)
  - [11. Find and Replace with the Substitute Command](#11-find-and-replace-with-the-substitute-command)
  - [12. Customizing Behavior with `:set`](#12-customizing-behavior-with-set)
  - [13. Persisting Settings with `~/.vimrc`](#13-persisting-settings-with-vimrc)
  - [14. Editing Multiple Files: Splits, `:e`, and `:r`](#14-editing-multiple-files-splits-e-and-r)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-1)
  - [Key Takeaways](#key-takeaways-1)
- [Lesson 3: Getting Started with VS Code and Remote-SSH](#lesson-3-getting-started-with-vs-code-and-remote-ssh)
  - [1. GUI Code Editors: VS Code and Alternatives](#1-gui-code-editors-vs-code-and-alternatives)
  - [2. Downloading VS Code](#2-downloading-vs-code)
  - [3. Extensions: Making the Editor Smarter](#3-extensions-making-the-editor-smarter)
  - [4. Determining Your System's Architecture Before Downloading](#4-determining-your-systems-architecture-before-downloading)
  - [5. Installing VS Code on Linux with `dpkg`](#5-installing-vs-code-on-linux-with-dpkg)
  - [6. Why VS Code Doesn't Belong on a Headless Server](#6-why-vs-code-doesnt-belong-on-a-headless-server)
  - [7. Installing VS Code on Windows and macOS](#7-installing-vs-code-on-windows-and-macos)
  - [8. Touring the VS Code Interface](#8-touring-the-vs-code-interface)
  - [9. Installing the Remote-SSH Extension](#9-installing-the-remote-ssh-extension)
  - [10. How Remote-SSH Uses Your SSH Config](#10-how-remote-ssh-uses-your-ssh-config)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-2)
  - [Key Takeaways](#key-takeaways-2)
- [Lesson 4: Connecting to a Remote Host with VS Code Remote-SSH](#lesson-4-connecting-to-a-remote-host-with-vs-code-remote-ssh)
  - [1. Opening the Command Palette](#1-opening-the-command-palette)
  - [2. Connecting to a Host with Remote-SSH](#2-connecting-to-a-host-with-remote-ssh)
  - [3. Browsing and Opening Files on the Remote Host](#3-browsing-and-opening-files-on-the-remote-host)
  - [4. Using the Integrated Terminal on a Remote Connection](#4-using-the-integrated-terminal-on-a-remote-connection)
  - [5. Adding a New Host from Within VS Code](#5-adding-a-new-host-from-within-vs-code)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-3)
  - [Key Takeaways](#key-takeaways-3)

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

---

# Lesson 2: Getting Started with Vim

Vim's reputation for being hard to exit is common enough that it has become a running joke among people who have used it for years without ever really learning it. This lesson closes that gap: it covers Vim's editing modes, the core commands for moving, copying, deleting, and searching text, how to save and quit properly (including the case where a file was opened without a name), and how to customize and persist Vim's behavior so it fits the way you work.

## 1. Vi, Vim, and Why Editor Fluency Matters

Vim (Vi IMproved) is built on top of the much older `vi` editor. The original `vi` dates back to a time when keyboards didn't have dedicated arrow keys, and its source code was historically tied to AT&T Unix's restrictive licensing terms. Vim, by contrast, is free and open source, and adds substantial usability improvements on top of the original `vi` behavior — including support for the arrow keys, which `vi` never had.

Some `vi`-compatible editor ships by default with nearly every Linux distribution, which makes baseline fluency with it essential — it's often the only text editor guaranteed to be available on a minimal server with no graphical environment. The full Vim is preinstalled on most distributions as well; if it isn't, it can be installed with the distribution's package manager:

```bash
sudo apt install vim   # Debian, Ubuntu
sudo dnf install vim   # Fedora, RHEL-based
sudo apk add vim       # Alpine
```

> **Note:**
> macOS also ships with Vim by default, so the same commands and workflow covered in this lesson apply directly to a Mac terminal, not just Linux.

## 2. Opening Vim and Its Modes

Running `vim` with no arguments opens an unnamed buffer and shows a welcome screen with information about the editor, since there's no file content to display yet:

```bash
vim
```

To open (or create) a specific file instead, pass its name as an argument. If the file already exists, Vim opens it for editing; if it doesn't, Vim creates it:

```bash
vim giropops.txt
```

Vim has two modes that matter from the very start:

- **Normal mode** is the default mode. Keystrokes in this mode are interpreted as commands, not as text to type — this is the mode all the editing and movement commands in this lesson run in.
- **Insert mode** is where typing actually enters text into the file, the way a typical text editor behaves. Press **i** from Normal mode to enter Insert mode, and press **Esc** to leave Insert mode and return to Normal mode.

Whether the current mode is being shown at the bottom of the screen (e.g. `-- INSERT --`) depends on a setting covered later in this lesson.

## 3. Movement in Normal Mode

In Normal mode, the arrow keys work as expected, but Vim also supports movement with four letter keys — **h** (left), **j** (down), **k** (up), and **l** (right) — sitting in a row on a standard keyboard. This dates back to when `vi` was created for keyboards without dedicated arrow keys, and the convention has stuck ever since; using `hjkl` instead of reaching for the arrow keys is significantly faster once it becomes muscle memory.

## 4. Yanking (Copying) and Pasting Text

Vim calls copying "yanking." From Normal mode:

- **`yy`** yanks (copies) the entire current line.
- **`p`** pastes whatever was last yanked or deleted, after the cursor's current position.

Yanking isn't limited to a single line. A count placed before the command tells Vim how many times to apply it:

```text
y2y   " yank the current line plus the next one (2 lines total)
y10y  " yank 10 lines starting from the current one
```

The same count-plus-motion pattern applies to yanking by word instead of by line, using the **`w`** (word) motion — **`yw`** yanks from the cursor's current position up to the start of the next word, and a count before it advances that many words further:

```text
yw    " yank from the cursor to the start of the next word
y3w   " yank from the cursor to the start of the word 3 words ahead
```

Because `yw` yanks up to the *start* of the next word rather than a whole word by itself, the exact result depends on where the cursor sits: at the beginning of a word, it yanks that entire word plus the whitespace after it; from the middle of a word, it only yanks the remaining letters of that word plus the trailing whitespace.

After yanking, moving the cursor to the desired location and pressing **`p`** pastes the yanked text there. Pressing `p` repeatedly pastes the same yanked content again each time.

## 5. Deleting and Cutting Text

**`d`** deletes text, following the same count-plus-motion pattern as yanking:

```text
dd    " delete (cut) the current line
d2d   " delete 2 lines
dw    " delete one word
d3w   " delete 3 words
```

Deleted text isn't simply discarded — like yanked text, it's placed in Vim's default register, so pressing **`p`** right after a `dd` pastes the line that was just deleted. This is what makes `dd` + `p` behave like cut-and-paste rather than plain deletion. Only the most recently deleted or yanked text is kept this way, so deleting several times in a row before pasting only makes the last deletion available to paste.

## 6. Entering Insert Mode from Different Positions

Besides plain **`i`**, which starts inserting text at the cursor's exact position, Vim offers several other ways to enter Insert mode depending on where the new text should go:

| Key | Where insertion starts |
| --- | --- |
| `i` | At the cursor's current position |
| `I` (uppercase) | At the beginning of the current line |
| `a` | One character after the cursor |
| `A` (uppercase) | At the end of the current line |
| `o` | On a new line opened below the current one |
| `O` (uppercase) | On a new line opened above the current one |

All six exit back to Normal mode with **Esc**, the same as plain `i`. Learning these saves the extra movement commands that would otherwise be needed to reposition the cursor before every edit.

## 7. Visual Mode: Selecting Text

Visual mode lets you select a specific range of text with the movement keys before acting on it, instead of guessing at a count for `y` or `d`. Vim has three variants:

### Character-wise Visual Mode

Pressing **`v`** enters Visual mode starting at the cursor. Moving the cursor from there extends the selection character by character, in any direction. With text selected, the usual commands apply to the selection instead of a line or word — **`y`** yanks exactly the selected text, **`d`** deletes it, and **`p`** pastes it elsewhere afterward. Pressing **Esc** exits Visual mode without acting on the selection.

### Line-wise Visual Mode

Pressing **Shift+V** (uppercase `V`) enters Visual Line mode, which selects whole lines as the cursor moves up or down, instead of individual characters. This is useful when the unit you want to copy or delete is naturally "N lines," similar to `y2y` or `d2d`, but selected visually instead of counted.

### Block-wise Visual Mode

Pressing **Ctrl+V** enters Visual Block mode, which selects a rectangular block of text across multiple lines and columns, rather than whole lines. This is the mode to use when the edit only applies to a specific column of text across several lines — for example, yanking (`y`) a block from one place and pasting (`p`) that exact rectangle somewhere else, without touching the rest of each line.

## 8. Saving and Quitting a File

Vim's save and quit commands are typed in command-line mode, entered by pressing **`:`** from Normal mode — a colon prompt appears at the bottom of the screen, distinct from the Normal-mode keystroke commands covered so far.

```text
:w              " write (save) the file
:w filename.txt " write (save) as filename.txt — required if the buffer has no name yet
:q              " quit
:wq             " write and quit in one step
```

If Vim was opened with no filename (`vim` with no arguments), `:w` alone fails because there's no name to save to yet — `:w filename.txt` must be used to give it one.

> **Warning:**
> `:q!` quits without saving, discarding every change made since the file was last saved. Vim refuses a plain `:q` on a modified buffer specifically to prevent this — the `!` is an explicit confirmation that any unsaved changes should be thrown away.

Two shortcuts combine saving and quitting into a single keystroke sequence:

- **Shift+Z Shift+Z** (`ZZ`, both uppercase) saves and quits, equivalent to `:wq`.
- **`:x`** also saves and quits.

## 9. Undo and Redo

- **`u`** undoes the last change. Pressing it repeatedly keeps undoing further back through the edit history.
- **Ctrl+R** redoes a change that was just undone.

## 10. Searching for Text

Typing **`/`** followed by a pattern and pressing Enter searches forward from the cursor's current position for the first match:

```text
/vim
```

From there:

- **`n`** jumps to the next match, continuing in the same direction as the search.
- **`N`** (uppercase) jumps to the match in the opposite direction.

Typing **`?`** instead of `/` runs the same kind of search but starting backward from the cursor instead of forward — in that case `n` continues backward and `N` continues forward, since both keys always follow the direction the search was originally issued in. Using `/` as the default is simpler to reason about, since forward is the more natural reading direction.

## 11. Find and Replace with the Substitute Command

The substitute command, entered in command-line mode, replaces text matching a pattern:

```text
:%s/vim/Santos/g
```

This command has three parts:

- A **range**, specifying which lines to apply the substitution to: `%` means every line in the file; a single number like `3` restricts it to just that line; a range like `3,5` applies it to lines 3 through 5.
- The **pattern and replacement**, `/old/new/` — the text to find and what to replace it with.
- The optional **`g`** flag: without it, only the first match on each targeted line is replaced; with `g`, every match on each targeted line is replaced.

For example, `:3s/vim/Santos/` replaces only the first occurrence of "vim" on line 3, while `:3,5s/vim/Santos/g` replaces every occurrence of "vim" across lines 3 through 5. Like any other change, a substitution can be undone with `u` if it doesn't produce the expected result.

## 12. Customizing Behavior with `:set`

The `:set` command changes Vim's behavior for the current session. A few of the most useful options:

| Command | Effect |
| --- | --- |
| `:set number` / `:set nonumber` | Show or hide line numbers in the left margin. These numbers are for on-screen reference only — they're never written to the file or included when it's printed or sent elsewhere. |
| `:set hlsearch` / `:set nohlsearch` | Highlight every match of the current search pattern, instead of only positioning the cursor on the first one. |
| `:set showmode` / `:set noshowmode` | Show or hide the current mode name (e.g. `-- INSERT --`) at the bottom of the screen. |
| `:set ignorecase` / `:set noignorecase` | Make searches case-insensitive, or restore the default case-sensitive behavior. |
| `:set incsearch` | Show matches incrementally as the search pattern is typed, before pressing Enter. |
| `:syntax on` | Enable syntax highlighting, coloring code based on the language Vim detects from the file's extension. |
| `:set tabstop=N` | Set how many spaces a Tab keypress inserts — for example, `:set tabstop=2` for the 2-space indentation conventionally used in YAML files. |
| `:set shiftwidth=N` | Set the indentation width Vim uses when auto-indenting a line, independent of the Tab key's own width. |

> **Note:**
> `:set ignorecase` treats uppercase and lowercase as identical when searching. The default, case-sensitive behavior is generally the safer choice, since it avoids unintentionally matching text that only looks similar.

## 13. Persisting Settings with `~/.vimrc`

Every `:set` option covered in the previous section only lasts for the current Vim session — closing and reopening Vim resets them. To make settings permanent, add them to `~/.vimrc`, a per-user configuration file in the home directory that Vim automatically loads every time it starts:

```bash
vim ~/.vimrc
```

Inside it, each desired setting is written on its own line, without the leading colon:

```text
set number
set hlsearch
set incsearch
```

Because `~/.vimrc` lives in each user's home directory, it's personal to that user — it doesn't affect Vim's behavior for other accounts on the same machine.

> **Note:**
> Get in the habit of backing up a configuration file like `~/.vimrc` (for example, a copy with a `.bkp` extension) before making changes to it, so it's easy to revert if something goes wrong. Once a workflow involves Git, version-controlling configuration files like this is a more reliable long-term solution than manual backups.

## 14. Editing Multiple Files: Splits, `:e`, and `:r`

Vim can show more than one file on screen at once, or switch between files entirely, without leaving the editor:

```text
:split filename.txt    " open filename.txt in a horizontal split (stacked panes)
:vsplit filename.txt   " open filename.txt in a vertical split (side-by-side panes)
```

**Ctrl+W** followed by **W** (two separate keypresses in sequence) moves focus between the open panes. Content yanked or deleted in one pane can be pasted directly into the other, since both panes share the same yank/delete registers as any other part of Vim.

To replace the current window's file entirely instead of opening a split, use `:e` (edit):

```text
:e filename.txt
```

> **Warning:**
> If the current buffer has unsaved changes, `:e filename.txt` is refused, the same way `:q` is refused on a modified buffer. Forcing it with `:e! filename.txt` discards those unsaved changes — the same kind of unrecoverable loss as `:q!`.

`:r` (read) works differently: instead of switching to another file, it inserts that file's entire content into the current file at the cursor's position, merging the two:

```text
:r otherfile.txt
```

## Important Commands from This Lesson

| Command | Purpose |
| --- | --- |
| `vim FILE` | Open (or create) FILE for editing. |
| `i` / `I` / `a` / `A` / `o` / `O` | Enter Insert mode at cursor / line start / one char ahead / line end / new line below / new line above. |
| `Esc` | Return to Normal mode from any other mode. |
| `h` `j` `k` `l` | Move left / down / up / right in Normal mode. |
| `yy`, `y{N}y` | Yank the current line, or N lines. |
| `yw`, `y{N}w` | Yank from the cursor to the start of the next word, or N words ahead. |
| `dd`, `d{N}d` | Delete (cut) the current line, or N lines. |
| `dw`, `d{N}w` | Delete (cut) the current word, or N words. |
| `p` | Paste the last yanked or deleted text. |
| `v` | Enter character-wise Visual mode. |
| `Shift+V` | Enter line-wise Visual mode. |
| `Ctrl+V` | Enter block-wise Visual mode. |
| `u` | Undo the last change. |
| `Ctrl+R` | Redo the last undone change. |
| `:w`, `:w FILE` | Save the file (as FILE if it has none yet). |
| `:q`, `:q!` | Quit; force-quit discarding unsaved changes. |
| `:wq`, `ZZ`, `:x` | Save and quit in one step. |
| `/pattern`, `?pattern` | Search forward / backward for pattern. |
| `n`, `N` | Jump to the next / previous match, relative to search direction. |
| `:%s/old/new/g` | Replace every match of old with new, across the whole file. |
| `:N,Ms/old/new/g` | Replace every match on lines N through M. |
| `:set number` / `nonumber` | Show / hide line numbers. |
| `:set hlsearch` / `ignorecase` / `incsearch` | Highlight matches / case-insensitive search / incremental search. |
| `:syntax on` | Enable syntax highlighting. |
| `:set tabstop=N`, `:set shiftwidth=N` | Set Tab width / auto-indent width. |
| `:split FILE`, `:vsplit FILE` | Open FILE in a horizontal / vertical split. |
| `Ctrl+W` then `W` | Switch focus between split panes. |
| `:e FILE`, `:e! FILE` | Switch to editing FILE; force-switch discarding unsaved changes. |
| `:r FILE` | Insert FILE's content at the cursor. |

## Key Takeaways

* Vim is built on the older `vi`, ships with virtually every Linux distribution, and is often the only editor available on a server without a graphical environment — which is why baseline fluency with it matters.
* Normal mode is where keystrokes act as commands; Insert mode is where they're typed as text. `Esc` always returns to Normal mode from anywhere else.
* Copy (`y`) and delete (`d`) both combine with a count and a motion — a word (`w`) or a line (doubling the letter, e.g. `dd`, `yy`) — to act on exactly the amount of text needed.
* Saving and quitting have several equivalent shortcuts (`:wq`, `ZZ`, `:x`), but discarding unsaved changes always requires an explicit override (`:q!`, `:e!`), since Vim refuses to lose modifications silently.
* Visual mode (character-wise, line-wise, and block-wise) selects exact text before acting on it with the same yank/delete commands used elsewhere.
* The `:s` substitute command combines a line range (a number, a range, or `%` for the whole file) with the `g` flag to control exactly how much of the file a find-and-replace affects.
* Settings changed with `:set` only last for the current session; placing them in `~/.vimrc` makes them permanent across every future Vim session.

---

# Lesson 3: Getting Started with VS Code and Remote-SSH

The previous lesson covered Vim, a terminal-based editor available on virtually any Linux system. This lesson introduces graphical code editors such as VS Code, when they fit into a Linux workflow, and how to connect one to a remote Linux server that has no graphical interface at all.

## 1. GUI Code Editors: VS Code and Alternatives

VS Code (Visual Studio Code) is a graphical text editor created by Microsoft and released as open source. It runs on Linux, Windows, and macOS, which makes it usable regardless of which desktop operating system a developer works from. Because it's open source, other editors have been built on the same foundation — Cursor and Antigravity (from Google) are two examples.

Cursor became particularly popular because it shipped with a built-in AI chat assistant early on, enabling a workflow often called "vibe coding," where the AI writes a large portion of the code based on natural-language instructions. VS Code has since added similar AI features through extensions like Copilot. Since AI assistance changes quickly and each editor integrates it differently, it's worth trying more than one to see which one fits best into your workflow — keeping in mind that AI assistance is meant to improve productivity, not to replace understanding the code it produces.

> **Note:**
> Many learning platforms and cloud IDEs offer a browser-based, sandboxed version of VS Code so you can get familiar with the interface without installing anything. That sandboxed version is useful for practice, but it typically can't install extensions or connect to a real remote server over SSH — for that, a real, locally installed copy of VS Code is required.

## 2. Downloading VS Code

VS Code is downloaded from `code.visualstudio.com`. The site offers a web version, along with installers for Windows, Linux (`.deb` and `.rpm` packages), and macOS. For Linux and macOS, separate builds are available for different processor architectures — x86, ARM32, and ARM64 — since installing the wrong architecture's package will fail.

> **Note:**
> Pressing the **`.`** key while viewing a repository on GitHub opens that repository directly in the web version of VS Code (github.dev), without any local installation.

## 3. Extensions: Making the Editor Smarter

Extensions add language- or tool-specific intelligence to VS Code — autocomplete, syntax checking, and other productivity features tailored to a particular technology. For example, installing a Python extension adds Python-aware autocomplete and error checking, and installing a Docker extension adds recognition of `Dockerfile` syntax and highlights syntax errors in it. Extensions are installed from the Extensions panel inside VS Code itself, covered in more detail later in this lesson.

## 4. Determining Your System's Architecture Before Downloading

Since Linux and macOS builds are split by processor architecture, it's important to confirm which architecture a machine uses before downloading a package. On Linux, `cat /proc/cpuinfo` prints processor details, though the output can be inconclusive on some virtualized environments. When that happens, the architecture can usually be found in the virtualization platform's own settings — for example, VirtualBox shows it in a virtual machine's Properties/description (e.g. "Ubuntu (ARM64)").

```bash
cat /proc/cpuinfo
```

## 5. Installing VS Code on Linux with `dpkg`

Once the correct `.deb` package has been downloaded, it needs to reach the target Linux machine. If it was downloaded through a browser on a separate desktop machine, `scp` copies it over to the remote server:

```bash
scp code_<version>_arm64.deb user@remote-host:~
```

From there, connect to the remote machine over SSH and install the package with `dpkg`, using `sudo` since installing a package system-wide requires root privileges:

```bash
sudo dpkg -i code_<version>_arm64.deb
```

On a Linux desktop with a graphical file manager, double-clicking the `.deb` file triggers the same installation through the GUI package manager instead of the command line.

`dpkg` does not resolve missing dependencies on its own — if the installation reports missing libraries, running `sudo apt-get install -f` fixes broken dependencies by installing whatever `dpkg` was missing.

## 6. Why VS Code Doesn't Belong on a Headless Server

Installing VS Code directly on a minimal Linux server without a graphical environment fails, because VS Code depends on graphical (X11) libraries — such as `libxrandr` — that a headless system doesn't have installed, and `apt-get install -f` can't make a genuinely headless server capable of running a graphical application. This isn't a problem to work around: a server with no graphical environment isn't a place to run VS Code directly in the first place.

The correct approach is to install VS Code on your own desktop machine — Linux, Windows, or macOS — and use it to edit files on the remote server over SSH instead, which is exactly what the Remote-SSH extension, covered later in this lesson, is for.

## 7. Installing VS Code on Windows and macOS

On Windows, the downloaded installer runs through a standard step-by-step wizard (Next, Next, Finish).

On macOS, there is no installer wizard: the download is an application bundle that needs to be dragged into the `Applications` folder manually. Once it's there, the installation is complete, and the editor can be launched either from Applications or by typing `code` in a terminal.

## 8. Touring the VS Code Interface

The sidebar on the left side of the VS Code window gives access to its main panels:

| Icon | Panel | Purpose |
| --- | --- | --- |
| Explorer | File browser | Browse and open files in the current folder. |
| Search | Find in files | Search for text across every file in the project. |
| Source Control | Git integration | Stage, commit, and manage Git changes without leaving the editor. |
| Run and Debug | Debugger | Run and step through code with breakpoints. |
| Extensions | Extension marketplace | Search for and install extensions. |

## 9. Installing the Remote-SSH Extension

The Remote-SSH extension, published by Microsoft, is what makes it possible to open VS Code locally and edit files on a remote Linux server as if they were local — without needing a graphical environment on the server itself. It's installed from the Extensions panel by searching for "Remote SSH" and choosing the official Microsoft extension from the results.

## 10. How Remote-SSH Uses Your SSH Config

Remote-SSH connects using the same SSH configuration already set up for command-line SSH access — the host aliases defined in `~/.ssh/config`, each specifying a hostname, user, and identity file. Running `cat ~/.ssh/config` confirms the file and its host entries are in place before trying to connect through the extension.

```bash
cat ~/.ssh/config
```

## Important Commands from This Lesson

| Command | Purpose |
| --- | --- |
| `cat /proc/cpuinfo` | Check the processor architecture of the current machine. |
| `scp FILE user@host:~` | Copy FILE to a remote host's home directory over SSH. |
| `sudo dpkg -i FILE.deb` | Install a `.deb` package, such as VS Code's Linux build. |
| `sudo apt-get install -f` | Resolve missing dependencies left over from a `dpkg -i` installation. |
| `cat ~/.ssh/config` | View configured SSH host aliases, used by both `ssh` and the Remote-SSH extension. |

## Key Takeaways

* VS Code, Cursor, and Antigravity are all graphical code editors built on the same open-source foundation, available on Linux, Windows, and macOS — the choice between them mostly comes down to which one's AI integration fits your workflow best.
* Extensions add language- and tool-specific intelligence (autocomplete, syntax checking) to the editor, and are installed from the Extensions panel.
* Linux and macOS builds of VS Code are split by processor architecture, so confirm the target machine's architecture (`cat /proc/cpuinfo`, or the hypervisor's VM settings) before downloading.
* VS Code depends on a graphical environment and can't run on a headless Linux server — installing it there fails on missing X11 libraries that a headless system will never have.
* The right setup for editing files on a headless remote server is to install VS Code locally and connect to the server through the Remote-SSH extension, not to install VS Code on the server itself.
* Remote-SSH connects using the same host aliases already defined in `~/.ssh/config`, so a working SSH config is a prerequisite for using it.

---

# Lesson 4: Connecting to a Remote Host with VS Code Remote-SSH

The previous lesson installed VS Code and the Remote-SSH extension; this lesson uses that extension to actually connect to a remote Linux server, browse and edit its files, and open a terminal that's already connected to it — completing the remote editing workflow.

## 1. Opening the Command Palette

**Ctrl+Shift+P** (Windows/Linux) or **Cmd+Shift+P** (macOS) opens VS Code's Command Palette, a search box for running any of VS Code's commands by typing its name instead of hunting through menus.

## 2. Connecting to a Host with Remote-SSH

Typing "Remote-SSH" into the Command Palette lists the extension's available commands, including **Remote-SSH: Connect to Host**. Selecting it shows the host aliases VS Code already knows about — read from `~/.ssh/config`, including any hosts brought in through an `Include` directive in that file. Picking one of these aliases opens a new VS Code window connected to that host.

Once connected, a status indicator in the bottom-left corner of the window shows the name of the host currently connected to, confirming the remote session is active.

## 3. Browsing and Opening Files on the Remote Host

With a Remote-SSH connection active, using **Open** (from the File menu or the Welcome screen) browses the remote machine's filesystem instead of the local one, letting you pick a folder there to open — for example, the remote user's home directory. The first time a given folder is opened, VS Code asks for confirmation that its author and contents are trusted before opening it.

Once opened, every file inside that remote folder appears in the Explorer sidebar exactly as if it were local. Files can be created, edited, and saved directly from VS Code, with the extension handling the transfer of changes to the remote machine transparently.

## 4. Using the Integrated Terminal on a Remote Connection

Opening **Terminal > New Terminal** from the menu while connected through Remote-SSH opens a terminal panel that is already connected to the remote host over that same connection, with no separate manual `ssh` command required. This makes it possible to run commands directly on the remote server without leaving the editor.

## 5. Adding a New Host from Within VS Code

Besides connecting to a host already defined in `~/.ssh/config`, a new one can be added directly from VS Code: **Remote-SSH: Add New Host** in the Command Palette prompts for a connection string in the same format used for a plain SSH command, such as `ssh user@remote-ip`. Once entered, the host is saved and appears in the "Connect to Host" list from then on.

> **Note:**
> Rather than relying only on this quick-add flow, add the new host properly to `~/.ssh/config` instead — that keeps every connection detail (hostname, user, identity file) in one place shared by both the command line and Remote-SSH.

## Important Commands from This Lesson

| Shortcut / Command | Purpose |
| --- | --- |
| `Ctrl+Shift+P` / `Cmd+Shift+P` | Open the Command Palette. |
| Remote-SSH: Connect to Host | Open a new VS Code window connected to a host from `~/.ssh/config`. |
| Remote-SSH: Add New Host | Add a new SSH host from a connection string, e.g. `ssh user@remote-ip`. |
| Terminal > New Terminal | Open an integrated terminal on the current (local or remote) connection. |

## Key Takeaways

* The Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`) is the fastest way to reach any VS Code command by name.
* Remote-SSH: Connect to Host lists the aliases already defined in `~/.ssh/config` and opens a new window connected to whichever one is chosen.
* Once connected, files and folders on the remote host open, edit, and save exactly like local ones, with VS Code handling the transfer transparently.
* The integrated terminal opened while connected through Remote-SSH is already on the remote host — no manual `ssh` needed.
* New hosts can be added on the fly through Remote-SSH: Add New Host, but adding them to `~/.ssh/config` directly keeps the configuration consistent between the command line and VS Code.
* Between Vim for direct terminal editing and VS Code with Remote-SSH for graphical remote editing, this module covers both core approaches to editing files on a Linux server.
