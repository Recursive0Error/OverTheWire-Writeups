# OverTheWire Bandit — Write-ups

My personal write-ups and notes while solving the **OverTheWire Bandit** wargame.

> **Goal:** Learn Linux, command-line usage, file handling, and basic cybersecurity concepts through hands-on challenges.

---

## 📚 Table of Contents

- [Level 0 → 1](#level-0--1)
- [Level 1 → 2](#level-1--2)
- [Level 2 → 3](#level-2--3)
- [Progress](#-progress)
- [Skills Practiced](#-skills-practiced)

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

The output contained the password required to log into **Level 1**.

## 🧠 What I Learned

- `ls` is used to list files and directories.
- `cat` is used to display the contents of a file.
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

The command displayed the password required for **Level 2**.

## 🧠 What I Learned

- `-` can have a special meaning when used with Linux commands.
- `./` can be used to explicitly reference a file in the current directory.
- Special filenames may require a different way of accessing them.

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

The command displayed the password required for **Level 3**.

## 🧠 What I Learned

- Spaces are normally used by the shell to separate arguments.
- Filenames containing spaces should be quoted.
- Double quotes allow the shell to treat the entire filename as one argument.

---

# 📌 Summary

| Level | Challenge | Technique |
|-------|-----------|-----------|
| 0 → 1 | Find the password in a file | `ls`, `cat` |
| 1 → 2 | Filename is `-` | `cat ./-` |
| 2 → 3 | Filename contains spaces | `cat "--file with spaces--"` |

---

# 🚀 Progress

- [x] Level 0 → 1
- [x] Level 1 → 2
- [x] Level 2 → 3
- [ ] Level 3 → 4
- [ ] Level 4 → 5
- [ ] Level 5 → 6
- [ ] Level 6 → 7
- [ ] Level 7 → 8
- [ ] Level 8 → 9
- [ ] Level 9 → 10
- [ ] Level 10 → 11
- [ ] Level 11 → 12
- [ ] Level 12 → 13
- [ ] Level 13 → 14
- [ ] Level 14 → 15
- [ ] Level 15 → 16
- [ ] Level 16 → 17
- [ ] Level 17 → 18
- [ ] Level 18 → 19
- [ ] Level 19 → 20
- [ ] Level 20 → 21
- [ ] Level 21 → 22
- [ ] Level 22 → 23
- [ ] Level 23 → 24
- [ ] Level 24 → 25
- [ ] Level 25 → 26
- [ ] Level 26 → 27
- [ ] Level 27 → 28
- [ ] Level 28 → 29
- [ ] Level 29 → 30
- [ ] Level 30 → 31
- [ ] Level 31 → 32
- [ ] Level 32 → 33
- [ ] Level 33 → 34

---

# 🧠 Skills Practiced

So far, I have practiced:

- Linux command line
- File and directory navigation
- `ls`
- `cat`
- Handling special filenames
- Handling filenames containing spaces
- Understanding shell arguments
- Basic Linux filesystem concepts

---

## ⚠️ Disclaimer

This repository contains my personal learning notes from the **OverTheWire Bandit** wargame.

Passwords are intentionally not stored in this repository. The focus is on documenting the techniques and concepts learned while solving each challenge.

---

**More levels will be added as I progress. 🚀**
