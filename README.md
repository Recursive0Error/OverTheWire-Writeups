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

The output contained the password required to log into **Level 1** which was 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR

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

The command displayed the password required for **Level 2** which was PK8fYLZg2hnHSz83plBL1iEPKdD3QToB

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

The command displayed the password required for **Level 3** which was 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

