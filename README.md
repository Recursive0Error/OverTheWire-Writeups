# OverTheWire Bandit — Write-ups

My personal write-ups and notes while solving the **OverTheWire Bandit** wargame.

> **Goal:** Learn Linux, command-line usage, file handling, and basic cybersecurity concepts through hands-on challenges.

---

## 📚 Table of Contents

- [Connecting to Bandit](#-connecting-to-bandit)
- [Level 0 → 1](#level-0--1)
- [Level 1 → 2](#level-1--2)
- [Level 2 → 3](#level-2--3)
- [Level 3 → 4](#level-3--4)
- [Progress](#-progress)
- [Skills Practiced](#-skills-practiced)

---

# 🔐 Connecting to Bandit

The Bandit levels are accessed through SSH. To connect to a level, I used the following command:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

The command can be broken down as follows:

- `ssh` — Secure Shell, used to connect to a remote machine.
- `bandit0` — The username for the current Bandit level.
- `bandit.labs.overthewire.org` — The Bandit server.
- `-p 2220` — Specifies port `2220`, which is the port used by the Bandit game.

After completing a level, I used the password obtained from that level to log into the next one.

For example, after obtaining the password for Level 1:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

The same process is repeated for the following levels by changing the username.

---

# Level 0 → 1

## 🎯 Objective

Find the password for the next level.

## 🔎 Enumeration

After logging into the Bandit server, I first listed the files in the current directory using:

```bash
ls
```

This displayed the files available in the current directory.

I then used the `cat` command to read the contents of the file:

```bash
cat <filename>
```

The output contained the password required to log into **Level 1**:

```text
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

## 🔑 Password

```text
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

## 🧠 What I Learned

- `ls` is used to list files and directories.
- `cat` is used to display the contents of a file.
- `ssh` is used to securely connect to a remote Linux system.
- Basic Linux commands are important when navigating a Linux environment.

---

# Level 1 → 2

## 🎯 Objective

Find the password for the next level.

## 🔎 Enumeration

The password was stored in a file named:

```text
-
```

A normal attempt would be:

```bash
cat -
```

However, `-` has a special meaning in many Linux commands and can represent standard input.

## 💡 Solution

I explicitly specified that the file was located in the current directory:

```bash
cat ./-
```

Here, `./` tells the shell that `-` refers to a file in the current directory.

The command displayed the password required for **Level 2**:

```text
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

## 🔑 Password

```text
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

## 🧠 What I Learned

- `-` can have a special meaning when used with Linux commands.
- `./` can be used to explicitly reference a file in the current directory.
- Special filenames may require a different way of accessing them.
- Linux commands can interpret certain characters specially.

---

# Level 2 → 3

## 🎯 Objective

Find the password for the next level.

## 🔎 Enumeration

The password was stored in a file whose name contained spaces:

```text
--file with spaces--
```

If I tried to access it normally:

```bash
cat --file with spaces--
```

the shell would interpret the spaces as argument separators.

Instead of treating the filename as one argument, it would interpret it as multiple arguments.

## 💡 Solution

I enclosed the filename in double quotes:

```bash
cat "--file with spaces--"
```

The quotation marks tell the shell to treat the entire filename as a single argument.

The command displayed the password required for **Level 3**:

```text
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

## 🔑 Password

```text
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

## 🧠 What I Learned

- Spaces are normally used by the shell to separate arguments.
- Filenames containing spaces should be quoted.
- Double quotes allow the shell to treat the entire filename as one argument.
- The shell parses commands before passing arguments to programs.

---

# Level 3 → 4

## 🎯 Objective

Find the password for the next level stored in a hidden file inside the `inhere` directory.

## 🔎 Enumeration

First, I changed into the target directory:

```bash
cd inhere
```

A standard `ls` command did not show the password file because hidden files in Linux start with a dot (`.`).

To list all files, including hidden files, I used:

```bash
ls -a
```

This revealed a hidden file named:

```text
...Hiding-From-You
```

## 💡 Solution

I then read the contents of the hidden file using:

```bash
cat ./"...Hiding-From-You"
```

The command displayed the password required for **Level 4**.

## 🔑 Password

```text
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

## 🧠 What I Learned

- `cd` is used to change directories in Linux.
- Hidden files in Linux begin with a dot (`.`).
- `ls -a` lists all files, including hidden files.
- `./` can be used to reference a file in the current directory.
- Quoting can help when dealing with filenames containing special characters.

---


