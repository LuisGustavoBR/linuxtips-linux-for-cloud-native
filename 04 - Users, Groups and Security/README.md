# Module 4: Users, Groups and Security

## Overview

This module covers Linux user and group administration: how the system identifies users and groups, the files that store that information, and the commands used to create, configure, and remove accounts.

Linux file permissions are built directly on top of these concepts, so a solid understanding of users and groups here sets up the permissions material covered in a later lesson of this module.

## Table of Contents

- [Lesson 1: Managing Linux Users](#lesson-1-managing-linux-users)
  - [1. Types of Users: Root, System Users, and Regular Users](#1-types-of-users-root-system-users-and-regular-users)
  - [2. The User ID (UID)](#2-the-user-id-uid)
  - [3. Inspecting Users with /etc/passwd](#3-inspecting-users-with-etcpasswd)
  - [4. Looking Up a User's Identity with `id`](#4-looking-up-a-users-identity-with-id)
  - [5. Primary and Secondary Groups](#5-primary-and-secondary-groups)
  - [6. Inspecting Groups with /etc/group](#6-inspecting-groups-with-etcgroup)
  - [7. Creating Users: `useradd` and `adduser`](#7-creating-users-useradd-and-adduser)
    - [`adduser`: Interactive and Fully Configured](#adduser-interactive-and-fully-configured)
    - [`useradd`: Bare and Scriptable](#useradd-bare-and-scriptable)
    - [Customizing a New User with `useradd` Options](#customizing-a-new-user-with-useradd-options)
  - [8. Managing Passwords with `passwd`](#8-managing-passwords-with-passwd)
    - [Setting a Password](#setting-a-password)
    - [Locking and Unlocking an Account](#locking-and-unlocking-an-account)
    - [Forcing a Password Change](#forcing-a-password-change)
    - [Removing a Password](#removing-a-password)
  - [9. Switching Users with `su`](#9-switching-users-with-su)
  - [10. Why Administrative Tasks Use `sudo`, Not a Root Login](#10-why-administrative-tasks-use-sudo-not-a-root-login)
  - [11. Password Storage and Aging in /etc/shadow](#11-password-storage-and-aging-in-etcshadow)
  - [12. Configuring Password Aging with `chage`](#12-configuring-password-aging-with-chage)
  - [13. Editing /etc/passwd Directly (and Why You Shouldn't)](#13-editing-etcpasswd-directly-and-why-you-shouldnt)
  - [14. Default Settings for New Users: /etc/adduser.conf](#14-default-settings-for-new-users-etcadduserconf)
  - [15. Pre-Populating New Home Directories with /etc/skel](#15-pre-populating-new-home-directories-with-etcskel)
  - [16. Removing Users with `userdel`](#16-removing-users-with-userdel)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson)
  - [Key Takeaways](#key-takeaways)
- [Lesson 2: Understanding sudo and the sudoers File](#lesson-2-understanding-sudo-and-the-sudoers-file)
  - [1. What `sudo` Does and Who Can Use It](#1-what-sudo-does-and-who-can-use-it)
  - [2. The /etc/sudoers File and Why You Must Use `visudo`](#2-the-etcsudoers-file-and-why-you-must-use-visudo)
  - [3. Choosing an Editor for `visudo`](#3-choosing-an-editor-for-visudo)
  - [4. Anatomy of a sudoers Rule](#4-anatomy-of-a-sudoers-rule)
  - [5. Restricting `sudo` to Specific Commands](#5-restricting-sudo-to-specific-commands)
  - [6. Command Execute Permission vs. Running as Root](#6-command-execute-permission-vs-running-as-root)
  - [7. Granting Full Admin Access via the sudo Group](#7-granting-full-admin-access-via-the-sudo-group)
  - [8. Modifying an Existing User with `usermod`](#8-modifying-an-existing-user-with-usermod)
  - [9. Locating a Command's Files with `whereis`](#9-locating-a-commands-files-with-whereis)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-1)
  - [Key Takeaways](#key-takeaways-1)
- [Lesson 3: Understanding and Changing File Permissions](#lesson-3-understanding-and-changing-file-permissions)
  - [1. Reading `ls -l` Permission Output](#1-reading-ls--l-permission-output)
  - [2. The File Type Character](#2-the-file-type-character)
  - [3. The Three Permission Sets: Owner, Group, and Others](#3-the-three-permission-sets-owner-group-and-others)
  - [4. Symbolic Mode: r, w, x, and What They Actually Allow](#4-symbolic-mode-r-w-x-and-what-they-actually-allow)
  - [5. Octal Mode: Converting Permissions to Numbers](#5-octal-mode-converting-permissions-to-numbers)
  - [6. Changing Permissions with `chmod` (Symbolic Mode)](#6-changing-permissions-with-chmod-symbolic-mode)
  - [7. Changing Permissions with `chmod` (Octal Mode)](#7-changing-permissions-with-chmod-octal-mode)
  - [8. Applying `chmod` Recursively with `-R`](#8-applying-chmod-recursively-with--r)
  - [9. Changing Ownership with `chown`](#9-changing-ownership-with-chown)
  - [10. Changing Just the Group with `chgrp`](#10-changing-just-the-group-with-chgrp)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-2)
  - [Key Takeaways](#key-takeaways-2)

---

# Lesson 1: Managing Linux Users

Before permissions can make sense, Linux needs a way to identify who is asking to do something — that's the job of users and groups. This lesson focuses entirely on users: the categories of accounts Linux recognizes, the files where account information lives, and the commands used to create, configure, and remove them. Permissions themselves — how ownership and access rules are actually enforced — are covered in a later lesson of this module.

## 1. Types of Users: Root, System Users, and Regular Users

Linux distinguishes three broad categories of accounts:

- **root** — the administrative superuser account, always identified by UID `0`.
- **System users** — created automatically by installed services and packages (a web server or the SSH daemon, for example) so those processes run under their own restricted identity instead of as root. These occupy a low range of UIDs, generally below `1000`.
- **Regular users** — human accounts. On Debian-based distributions (such as Ubuntu), the first regular user is assigned UID `1000`, with subsequent accounts incrementing from there.

> **Note:** Other distribution families (such as Red Hat-based ones) may reserve a different UID range for system vs. regular users. The exact numbers vary by distribution, but the three-tier structure — root, system users, regular users — applies everywhere.

## 2. The User ID (UID)

Every account is represented internally by a numeric UID rather than by its username — the username is just a human-readable label mapped to that number. root is always UID `0`, regardless of what the account happens to be named.

This matters because the kernel and the file-permission system check the UID, not the name. If two different usernames were ever assigned the same UID `0`, both would have root's exact privileges — root is special because of its UID, not because of the name "root". This will come up again later in this lesson.

## 3. Inspecting Users with /etc/passwd

Every account on the system has an entry in `/etc/passwd`:

```bash
cat /etc/passwd
```

Each line has seven colon-separated fields:

```
username:x:UID:GID:comment:home_directory:shell
```

| Field | Meaning |
|---|---|
| `username` | The account's login name. |
| `x` | A placeholder — the real password hash lives in `/etc/shadow`, not here. |
| `UID` | The account's numeric user ID. |
| `GID` | The account's primary group ID (see [Primary and Secondary Groups](#5-primary-and-secondary-groups)). |
| `comment` | Free-text descriptive info (the GECOS field) — often blank for system accounts, populated for accounts created interactively via `adduser`. |
| `home_directory` | The account's home directory path. |
| `shell` | The program launched when the user logs in — most regular users are set to `/bin/bash`. |

Some example rows worth recognizing:

- `root` — UID and GID both `0`, home `/root`, shell `/bin/bash`.
- Service accounts like `sshd`, `syslog`, or `www-data` — each has its own dedicated system account so its daemon doesn't need to run as root.
- Accounts belonging to the same service (for example, two web-server-related accounts) often share a home directory convention like `/var/www`, since they don't represent an interactive login — they exist purely to own and run a process.

## 4. Looking Up a User's Identity with `id`

The `id` command reports an account's UID, primary GID, and every group it belongs to:

```bash
id <username>
```

Run with no argument, `id` reports the identity of the currently logged-in session:

```bash
id
```

`id root` is a good example to try — it shows that root belongs only to its own group, with no secondary groups by default.

## 5. Primary and Secondary Groups

Every user has exactly one **primary group** — the default group used for files they create — and can additionally belong to any number of **secondary (supplementary) groups**.

By default, on Debian-based systems, a new user's primary group is a dedicated group created with the same name and the same numeric ID as the user. For example, a user with UID `1000` typically also has primary GID `1000`, in a group named after that user.

Secondary groups grant additional access without changing the user's primary identity — membership in a group like `adm` or `cdrom`, for instance, grants whatever access is associated with that group.

## 6. Inspecting Groups with /etc/group

Every group is listed in `/etc/group`:

```bash
cat /etc/group
```

Each line follows:

```
group_name:x:GID:member_list
```

The `x` placeholder plays the same role as in `/etc/passwd` (group passwords are essentially unused in practice). `member_list` is a comma-separated list of usernames who belong to that group as a **secondary** group — a user does not need to be listed here for a group that is already their primary group.

## 7. Creating Users: `useradd` and `adduser`

Linux provides two different tools for creating a user account, and it's easy to confuse their names. Both require `sudo`, since creating an account is an administrative action.

### `adduser`: Interactive and Fully Configured

`adduser` is Debian/Ubuntu's higher-level, interactive tool:

```bash
sudo adduser <username>
```

It immediately prompts for a password, then interactively asks for profile details — full name, room number, work phone, home phone, and an "other" free-text field — which get stored in the comment (GECOS) field of `/etc/passwd`. It also creates the user's home directory automatically, pre-populated from `/etc/skel` (see [Pre-Populating New Home Directories with /etc/skel](#15-pre-populating-new-home-directories-with-etcskel)).

### `useradd`: Bare and Scriptable

`useradd` is the low-level tool available on virtually every Linux distribution:

```bash
sudo useradd <username>
```

By default it only writes an entry to `/etc/passwd` (and `/etc/shadow`) — it does **not** create a home directory and does **not** prompt for or set a password. Because it takes no interactive input, it's well suited to scripting: every aspect of the new account has to be specified explicitly via flags, or is left at a bare default.

> **Note:** A user created with bare `useradd` has no password set at all until `passwd` is run for that account separately (see [Managing Passwords with `passwd`](#8-managing-passwords-with-passwd)).

### Customizing a New User with `useradd` Options

| Flag | Meaning |
|---|---|
| `-u <uid>` | Set a specific UID instead of the next available default. |
| `-g <group>` | Set the primary group, by name or GID. |
| `-d <path>` | Set a custom home directory path. |
| `-s <shell>` | Set the login shell. |
| `-m` | Create the home directory (copying its starter contents from `/etc/skel`) — without this flag, `useradd` does not create the home directory even when `-d` is given. |

For example:

```bash
sudo useradd -u 1234 -g 1000 -d /home/giros -s /bin/sh -m giros
```

This creates `giros` with UID `1234`, primary group `1000`, home directory `/home/giros` (actually created, because of `-m`), and shell `/bin/sh`.

> **Warning:** Setting `-g` to GID `0` (root's group) gives the new account root's group membership. This is only useful to demonstrate that group membership is just a number the kernel checks — never do this for a real account.

## 8. Managing Passwords with `passwd`

### Setting a Password

```bash
sudo passwd <username>
```

Only root (or `sudo`) can set another user's password this way. A user changing their **own** password just runs `passwd` with no arguments — subject to any password-aging restrictions in place (see [Configuring Password Aging with `chage`](#12-configuring-password-aging-with-chage)).

### Locking and Unlocking an Account

```bash
sudo passwd -l <username>   # lock
sudo passwd -u <username>   # unlock
```

A locked account cannot log in at all, regardless of whether the correct password is entered, until it's unlocked again.

### Forcing a Password Change

```bash
sudo passwd -e <username>
```

This immediately expires the account's password, so the next login (or `su`) forces the user to set a new one before proceeding.

### Removing a Password

```bash
sudo passwd -d <username>
```

This clears the account's password entirely.

> **Warning:** This can leave the account able to log in with no password prompted at all, depending on the system's authentication configuration. Use this only for controlled testing, never on a real account.

## 9. Switching Users with `su`

```bash
su - <username>
```

The trailing `-` loads that user's full login environment, rather than switching identity while keeping the previous user's environment variables. `su` is commonly said to stand for "substitute user" — not "super user," despite the common assumption.

## 10. Why Administrative Tasks Use `sudo`, Not a Root Login

By default, root frequently has **no password set at all**, so a plain `su - root` fails. Day-to-day administrative work is instead done via `sudo` from a regular user account, authenticating with that user's own password rather than root's.

It's possible to work around this by explicitly setting a password for root (`sudo passwd root`) and then logging in directly with `su - root`, but doing so works against the point of using `sudo` in the first place — every `sudo` command is tied to the user who ran it, which is lost the moment you're logged in as root itself.

> **Warning:** Setting a password for root and logging into it directly is shown here only to explain why `sudo` exists — it isn't the normal way to do administrative work.

## 11. Password Storage and Aging in /etc/shadow

The `x` placeholder in `/etc/passwd` corresponds to a real entry in `/etc/shadow`, readable only by root:

```bash
sudo cat /etc/shadow
```

Each line holds the account's password hash plus its password-aging fields — last change date, minimum age, maximum age, warning period, inactivity period, and expiration date. These are the same fields `chage` configures (see next section).

In place of a hash, you'll sometimes see:

- `*` — the account intentionally has no password set.
- `!` — the account is locked.

Both are common on system accounts, which aren't meant to be logged into interactively at all.

## 12. Configuring Password Aging with `chage`

```bash
sudo chage <username>
```

Run this way, `chage` interactively walks through each password-aging field for that account:

- **Minimum password age** — days that must pass before the password can be changed again.
- **Maximum password age** — days before a password change is required.
- **Last password change date** — can be left at its recorded default.
- **Warning period** — days before expiration that the user starts seeing a warning.
- **Inactivity period** — days after expiration before the account is disabled entirely.
- **Account expiration date** — an explicit date after which the account stops working, independent of the password fields above.

> **Note:** Leaving the inactivity period enabled can lock a user out entirely if they're away longer than that many days past their password's expiration — for example, someone returning from vacation. Set it deliberately.

> **Note:** A restrictive minimum password age can block a user from changing a compromised password immediately, since they'd have to wait it out. Weigh this against the security benefit before enabling it.

## 13. Editing /etc/passwd Directly (and Why You Shouldn't)

Hand-editing a field in `/etc/passwd` — for example, changing a user's UID — does not take effect for a session that's already logged in under the old UID: a bare `id` in that already-open session still reflects the stale, previously-loaded identity.

Looking the account up by name instead (`id <username>`) correctly shows the new UID, since that reads fresh from the file every time.

> **Warning:** Never hand-edit `/etc/passwd` directly on a real system. Changing account attributes should always go through the proper user-management commands — a mistake made by hand in this file can lock every account out.

## 14. Default Settings for New Users: /etc/adduser.conf

`adduser` reads its defaults from `/etc/adduser.conf`, including:

- The default login shell and home-directory path template for new accounts.
- The `SKEL` directory to copy starter files from (see next section).
- The UID/GID ranges reserved for system users vs. regular users.
- Default supplementary group(s) that every new user is automatically added to (for example, a group called `users`).

Editing this file changes `adduser`'s behavior for accounts created **afterward** — it has no effect on accounts that already exist.

## 15. Pre-Populating New Home Directories with /etc/skel

`/etc/skel` is a template directory. Its contents — mostly hidden dotfiles, so list it with `ls -a` — are copied automatically into every new home directory created by `adduser` (or `useradd -m`):

- **`.bash_logout`** — commands run automatically when a login shell exits.
- **`.bashrc`** — interactive shell configuration (aliases, prompt customization, and similar).
- **`.bash_profile`** — configuration applied for a login shell.

Anything placed in `/etc/skel` — a welcome message, a starter script, a shared config file — will automatically appear in every future user's home directory from then on.

## 16. Removing Users with `userdel`

```bash
sudo userdel <username>
```

This removes the account but leaves its home directory untouched on disk — the directory becomes orphaned.

```bash
sudo userdel -r <username>
```

The `-r` flag also deletes the home directory and everything in it.

> **Warning:** `-r` permanently deletes the contents of that user's home directory. There is no undo — double-check the username before running it.

## Important Commands from This Lesson

| Command | Description |
|---|---|
| `id [username]` | Show the UID, primary GID, and group memberships for the given user, or the current session if omitted. |
| `cat /etc/passwd` | List all user accounts and their basic attributes. |
| `cat /etc/group` | List all groups and their supplementary members. |
| `sudo cat /etc/shadow` | List password hashes and password-aging fields (root only). |
| `sudo adduser <username>` | Interactively create a user: prompts for a password and profile fields, creates the home directory automatically. |
| `sudo useradd [options] <username>` | Bare, low-level user creation. No password, no home directory unless configured via flags. |
| `sudo passwd <username>` | Set or change a user's password. |
| `sudo passwd -l` / `-u <username>` | Lock or unlock an account. |
| `sudo passwd -e <username>` | Expire a password, forcing a change at next login. |
| `sudo passwd -d <username>` | Remove a user's password entirely. |
| `su - <username>` | Switch to another user, loading their full login environment. |
| `sudo chage <username>` | Interactively configure password-aging settings for a user. |
| `sudo userdel <username>` | Delete a user account, leaving their home directory in place. |
| `sudo userdel -r <username>` | Delete a user account and their home directory. |

## Key Takeaways

- Linux identifies accounts by numeric UID, not by username — root is root because its UID is `0`, not because of its name.
- Accounts fall into three categories: root, system users (low UIDs, run services), and regular users (starting at `1000` on Debian-based systems).
- `/etc/passwd` holds account attributes; the actual password hash and aging settings live in `/etc/shadow`, readable only by root.
- Every user has one primary group plus any number of secondary groups, listed together in `/etc/group`.
- `useradd` is bare and scriptable; `adduser` is interactive and handles password, profile fields, and home-directory creation automatically.
- `useradd` never creates a home directory unless `-m` is passed, even when `-d` specifies a path.
- `passwd`'s flags (`-l`, `-u`, `-e`, `-d`) cover locking, unlocking, forcing a change, and removing a password entirely.
- Day-to-day administrative work uses `sudo` from a regular account rather than logging in directly as root, which frequently has no password set at all.
- `chage` configures password aging; overly strict settings (a long inactivity period, a high minimum age) can lock out legitimate users, so set them deliberately.
- `/etc/adduser.conf` controls `adduser`'s future defaults; `/etc/skel` is copied into every new home directory, making it the place to put files that should exist for every user.
- Account attributes should always be changed through proper commands, never by hand-editing `/etc/passwd` — permissions and identity are covered further in the next lesson.

---

# Lesson 2: Understanding sudo and the sudoers File

This lesson looks at how `sudo` actually works under the hood: the file that decides who can use it and for what, the safe way to edit that file, and the command used to grant a user administrative access after their account already exists.

## 1. What `sudo` Does and Who Can Use It

`sudo` lets a regular user run a single command with root's identity, without logging in as root directly. For example, `sudo vi /etc/passwd` succeeds where a plain `vi /etc/passwd` as a regular user would fail with a permissions error. `sudo su -` is one common way to use that access to fully switch into a root shell.

A newly created user does not have `sudo` access by default. On Ubuntu specifically, the account created during installation is automatically granted `sudo` access; any user created afterward has to be explicitly granted it (covered later in this lesson).

## 2. The /etc/sudoers File and Why You Must Use `visudo`

Who can use `sudo`, and what they're allowed to do with it, is defined in `/etc/sudoers`. Although the file can technically be opened directly, the correct way to edit it is with the dedicated command:

```bash
sudo visudo
```

`visudo` edits a temporary copy of the file and validates its syntax before saving. This is the same principle already covered for `/etc/passwd` earlier in this module: whenever a dedicated tool exists for editing a configuration file, use it instead of hand-editing the file directly.

> **Warning:** A syntax mistake made by hand-editing `/etc/sudoers` directly can leave the entire system without any way to use `sudo` at all. `visudo` exists specifically to prevent that.

## 3. Choosing an Editor for `visudo`

By default, `visudo` opens the system's default editor (commonly `nano`). To use a different one, set the `EDITOR` environment variable **as part of the same command**:

```bash
sudo EDITOR=vim visudo
```

This has to be done inline rather than with a plain `export EDITOR=vim` beforehand, because of a setting near the top of `/etc/sudoers` itself: `Defaults env_reset`. It resets/strips inherited environment variables for every command run through `sudo`, for security — including an `EDITOR` value exported ahead of time. Setting it inline, together with the `sudo` call, survives that reset because it's scoped to that one invocation.

Two other `Defaults` lines worth recognizing while looking at the top of the file:

- **`Defaults mail_badpass`** — emails the system administrator (normally root, whose local mail is stored under `/var/mail`) whenever someone enters a wrong password for `sudo`. This is an internal, local message, not something sent out over the internet.
- **`Defaults secure_path`** — defines the fixed list of directories `sudo` searches for a binary, regardless of the invoking user's own `PATH`. This prevents someone from tricking `sudo` into running a malicious binary by manipulating their own `PATH` beforehand.

## 4. Anatomy of a sudoers Rule

A typical rule, such as the default one granting root itself full access, looks like this:

```
root    ALL=(ALL:ALL) ALL
```

The format is:

```
who   host=(run_as_user:run_as_group)   command
```

| Field | Meaning |
|---|---|
| `who` | A username, or a group prefixed with `%` (for example, `%sudo`). |
| `host` | Which machine(s) this rule applies to. Usually `ALL` — this matters more when a single sudoers-style ruleset is distributed across many machines from a central directory service, rather than on one standalone machine. |
| `(run_as_user:run_as_group)` | The identity the command is executed as. `ALL:ALL` allows running the command as any user and group; leaving this out defaults to root. This is also what makes `sudo -u <username> <command>` work — it runs a command as a specific non-root user, as long as the rule permits it. |
| `command` | Which command(s) this rule grants. `ALL` means unrestricted; a specific path (like `/usr/bin/apt`) restricts the rule to just that program. |

## 5. Restricting `sudo` to Specific Commands

A rule doesn't have to grant unrestricted access. Adding a line like this through `visudo` grants a specific user permission to run only `apt` as root, on any host:

```
luisgustavo    ALL=(ALL:ALL) /usr/bin/apt
```

## 6. Command Execute Permission vs. Running as Root

Granting a `sudo` rule for a command is not the same as giving a user direct execute rights on that command as themselves. Even after adding the rule above, running the command **without** `sudo` still fails partway through — the command executes (the user does have execute permission on the `apt` binary itself), but it hits a permissions error trying to write to root-owned files it needs (such as a lock file under `/var/lib/dpkg`), because the process is still running as the user, not as root.

Running the same command **with** `sudo` works completely, because `sudo` assumes root's full identity for that invocation — not just execute permission on one binary.

The distinction: a sudoers rule grants permission to use `sudo` to run a given command as root. It does not by itself grant that command's normal execute permission bits to the user directly — those are a separate mechanism, covered later in this module.

## 7. Granting Full Admin Access via the sudo Group

Rather than writing individual command-restricted rules for every user, the common way to grant full administrative access is to add the user to the `sudo` group. `/etc/sudoers` already includes a rule granting that group unrestricted access:

```
%sudo    ALL=(ALL:ALL) ALL
```

Membership in this group is what makes Ubuntu's installation-time user — and any user added to the group afterward — able to use `sudo` for anything.

## 8. Modifying an Existing User with `usermod`

`usermod` changes an existing user's account attributes — the same categories of settings `useradd` sets at creation time.

| Flag | Meaning |
|---|---|
| `-u <uid>` | Change the UID. |
| `-g <group>` | Change the primary group. |
| `-d <path>` | Change the home directory. |
| `-s <shell>` | Change the login shell. |
| `-aG <group>` | Append the user to an additional (secondary) group. |

> **Warning:** Always combine `-a` (append) with `-G`. Using `-G` alone replaces the user's *entire* list of secondary groups with the one(s) given, removing them from every other group they were previously in.

For example, adding an existing user to the `sudo` group grants them full administrative access:

```bash
sudo usermod -aG sudo <username>
```

Confirm the change with `cat /etc/group` (the username now appears in the `sudo` group's member list) or `id <username>`.

## 9. Locating a Command's Files with `whereis`

```bash
whereis apt
```

Reports every file associated with a command: its binary location, any libraries, its configuration, and its documentation/man page — useful for finding exactly where a command lives before writing a sudoers rule for it.

## Important Commands from This Lesson

| Command | Description |
|---|---|
| `sudo <command>` | Run a single command with root's identity. |
| `sudo su -` | Use `sudo` access to fully switch into a root shell. |
| `sudo visudo` | Safely edit `/etc/sudoers` — validates syntax before saving. |
| `sudo EDITOR=<editor> visudo` | Edit sudoers with a specific editor for that invocation (needed because `Defaults env_reset` strips a plain exported `EDITOR`). |
| `sudo -u <username> <command>` | Run a command as a specific user instead of root. |
| `sudo usermod -aG <group> <username>` | Add a user to an additional group without removing their existing ones. |
| `whereis <command>` | Show the binary, library, config, and man-page paths for a command. |

## Key Takeaways

- `sudo` lets a user run a command with root's identity for that one invocation, without logging in as root.
- `sudo` permissions are defined in `/etc/sudoers`, always edited with `visudo`, which validates syntax and prevents locking yourself out.
- A sudoers rule reads as `who host=(run_as_user:run_as_group) command` — `ALL` in any field means unrestricted for that dimension.
- Granting a sudoers rule for a command is not the same as giving a user direct execute rights on that command as themselves — it still has to be run through `sudo` to gain root's identity.
- The `sudo` group already has an unrestricted `ALL` rule in `/etc/sudoers` by default — adding a user to it (`usermod -aG sudo <username>`) is the standard way to grant full admin access.
- `usermod -aG` must always combine `-a` with `-G`, or the user's other secondary groups get wiped out.
- `Defaults env_reset`, `mail_badpass`, and `secure_path` in sudoers exist for security: they strip inherited environment variables, alert the administrator on failed `sudo` password attempts, and lock down which directories `sudo` searches for binaries.

---
