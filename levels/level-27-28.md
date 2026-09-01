# Bandit Level 27 → Level 28

## 🎯 Objective

There is a Git repository available at:

```text
ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo
```

The repository is accessible through SSH on port:

```text
2220
```

The password for the `bandit27-git` user is the same password I obtained for **bandit27**.

The goal is to clone the repository onto my **local machine** and find the password for the next level.

This level introduces the basics of working with **Git repositories** and cloning a remote repository over SSH.

> **Important:** The repository needs to be cloned from my local machine, not from the OverTheWire Bandit machine.

## 🗂️ Creating a Working Directory

I first created a directory on my local machine to store the Git repository:

```bash
mkdir bandit_git
```

I then moved into the directory:

```bash
cd bandit_git
```

This gives me a clean workspace for the challenge.

## 📥 Cloning the Git Repository

I used the following command to clone the repository:

```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

Here is what each part means:

```text
git clone
```

tells Git to make a local copy of a remote repository.

The SSH URL is:

```text
ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

It contains several important parts:

```text
bandit27-git
        ↓
Username used for authentication

bandit.labs.overthewire.org
        ↓
OverTheWire server

2220
        ↓
SSH port

/home/bandit27-git/repo
        ↓
Location of the Git repository
```

When prompted for a password, I entered the password I obtained from the previous level:

```text
STJLJBRRphMxKB392CT4iOr5CbzPU9ER
```

Git then downloaded the repository to my local machine.

## 📂 Entering the Repository

After cloning the repository, Git created a directory named:

```text
repo
```

I entered it using:

```bash
cd repo
```

I then listed the files, including hidden files:

```bash
ls -la
```

This allowed me to inspect the contents of the repository.

## 🔍 Inspecting the Repository

The repository contained a `README` file.

I read it using:

```bash
cat README
```

The file contained:

```text
The password to the next level is: y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
```

Therefore, the password for the next level was directly stored inside the repository's README file.

## 🔑 Password

```text
y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
```

## 🧠 What I Learned

* **Git** is a distributed version control system used to manage source code and other files.
* `git clone` creates a local copy of a remote Git repository.
* Git repositories can be accessed over **SSH**.
* SSH URLs can specify a custom port.
* The syntax:

  ```text
  ssh://username@host:port/path
  ```

  specifies the username, host, port, and remote path.
* `ls -la` displays normal and hidden files.
* `cat` can be used to read text files such as `README`.
* Git repositories can be cloned and inspected from a local computer.
* The password for `bandit27-git` was the same as the password for `bandit27`.

---

## 📌 Key Takeaway

The main idea of this level was to clone a remote Git repository over SSH and inspect its contents.

The complete process was:

```text
Local Machine
      ↓
Create working directory
      ↓
git clone
      ↓
SSH connection to bandit.labs.overthewire.org:2220
      ↓
Authenticate as bandit27-git
      ↓
Repository downloaded
      ↓
cd repo
      ↓
ls -la
      ↓
cat README
      ↓
Password for Level 28
```

The important commands I used were:

```bash
mkdir bandit_git
```

```bash
cd bandit_git
```

```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

```bash
cd repo
```

```bash
ls -la
```

```bash
cat README
```

which gave me the password for **Level 28**:

```text
y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
```