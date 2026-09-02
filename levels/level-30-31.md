# Level 30 → 31

## 🎯 Objective

There is a Git repository available at:

```text
ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo
```

The repository is accessible through SSH on port:

```text
2220
```

The goal is to clone the repository and find the password for the next level.

---

## 📥 Cloning the Repository

As with the previous challenges, I needed to specify the non-standard SSH port while cloning the repository.

I used:

```bash
GIT_SSH_COMMAND='ssh -p 2220' git clone ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo
```

When prompted, I entered the current password for `bandit30`.

---

## 📂 Entering the Repository

After cloning the repository, I changed into the project directory:

```bash
cd repo
```

I then inspected the repository and checked the files present in the project.

```bash
ls -la
```

The repository appeared to be mostly empty, and the README or project files did not immediately contain the password.

---

## 🏷️ Checking Git Tags

I then checked the repository tags using:

```bash
git tag
```

This revealed a tag named:

```text
secret
```

This strongly suggested that the hidden password information might be stored in a Git tag object rather than in a tracked file.

---

## 🔍 Inspecting the Secret Tag

I used:

```bash
git show secret
```

The command displayed the contents of the tag object, which included the password for the next level.

```text
82NkymblpGBYmIXG6ZQ8YldBYstHpfUf
```

---

## 🔑 Password

```text
82NkymblpGBYmIXG6ZQ8YldBYstHpfUf
```

---

## 🧠 What I Learned

* Git repositories can hide information in tags, not just in files.
* `git tag` lists tags that may contain hidden metadata or references.
* `git show <tag>` can reveal the contents stored in a tag object.
* Sometimes the password is not in the repository files themselves but in Git metadata.
* Tag inspection is a useful technique when normal file exploration does not reveal the next credential.

---

## 📌 Key Takeaway

The password was not stored in the standard project files.

The important steps were:

```text
Clone Repository
        ↓
Inspect repository
        ↓
Check Git tags
        ↓
Find tag named secret
        ↓
Run git show secret
        ↓
Reveal next password
```

The main commands I used were:

```bash
GIT_SSH_COMMAND='ssh -p 2220' git clone ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo
```

```bash
cd repo
```

```bash
git tag
```

```bash
git show secret
```

This revealed the password for **Level 31**:

```text
82NkymblpGBYmIXG6ZQ8YldBYstHpfUf
```
