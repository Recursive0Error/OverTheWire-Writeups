# Bandit Level 28 → Level 29

## 🎯 Objective

There is a Git repository available at:

```text
ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo
```

The repository is accessible through SSH on port:

```text
2220
```

The password for the `bandit28-git` user is the same password I obtained for **bandit28**.

The goal is to clone the repository onto my **local machine** and find the password for the next level.

The interesting part of this level is that the password is not visible in the current version of the repository. However, Git keeps track of previous changes, so I can inspect the repository's history to find the password that was previously stored in the file.

## 📥 Cloning the Repository

I first cloned the repository from my local machine using:

```bash
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo bandit28-repo
```

The final argument:

```text
bandit28-repo
```

specifies the name of the directory where Git should place the cloned repository.

I then entered the repository:

```bash
cd bandit28-repo
```

When Git requested the password, I entered the password for **bandit28** that I obtained from the previous level.

## 📂 Checking the Current Files

I listed the files in the repository:

```bash
ls -la
```

I then examined the main README file:

```bash
cat README.md
```

The password was not directly visible in the current version of the file.

Instead, the credentials section contained something similar to:

```text
## credentials

- username: bandit29
- password: <TBD>
```

This indicated that the password had been removed or replaced in a later commit.

## 🕐 Inspecting Git History

Since this is a Git repository, previous versions of files may still exist in the repository's history.

I used:

```bash
git log -p
```

The `git log` command displays the commit history.

The `-p` option is particularly useful because it displays the **patch**, or the exact changes made by each commit.

This allowed me to see not only the commit messages but also the actual changes made to the files.

## 🔍 Finding the Removed Password

While examining the commit history, I found a commit that changed the password in `README.md`.

The relevant part of the diff was:

```text
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: <TBD>
+- password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

The `-` line represents the previous version:

```text
- password: <TBD>
```

The `+` line represents the new version introduced by that commit:

```text
+ password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

Therefore, Git's history revealed the password that had previously been stored in the repository.

## 🧠 Understanding Git Diff

The important part of the output was:

```text
- password: <TBD>
+ password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

In a Git diff:

```text
-
```

means the line was removed or replaced.

While:

```text
+
```

means the line was added.

Therefore, the added line revealed the password.

The important concept is that **removing information from the current version of a Git repository does not necessarily remove it from Git history**.

Previous commits can still contain older versions of files.

## 🔑 Retrieving the Password

The command I used to inspect the Git history was:

```bash
git log -p
```

Inside the output, I found:

```text
- password: <TBD>
+ password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

The password for the next level was therefore:

```text
Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

## 🔑 Password

```text
Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

## 🧠 What I Learned

* **Git** is a version control system that keeps track of changes to files.
* `git clone` downloads a remote repository to the local machine.
* `git log` displays the commit history of a repository.
* `git log -p` displays the commit history along with the actual changes made in each commit.
* Git diffs use `-` to indicate removed lines.
* Git diffs use `+` to indicate added lines.
* Information removed from the current version of a file may still exist in previous commits.
* Git history can therefore reveal information that is no longer visible in the latest version of a file.
* Looking through commit history is an important technique when analyzing Git repositories.

---

## 📌 Key Takeaway

The main idea of this level was to realize that the password had been removed from the current version of `README.md`, but Git still had the previous version stored in its history.

The complete process was:

```text
Local Machine
      ↓
Clone bandit28-git repository
      ↓
cd bandit28-repo
      ↓
ls -la
      ↓
cat README.md
      ↓
Password is hidden/replaced
      ↓
git log -p
      ↓
Inspect previous commits
      ↓
Find the previous password
      ↓
Password for Level 29
```

The important commands I used were:

```bash
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo bandit28-repo
```

```bash
cd bandit28-repo
```

```bash
ls -la
```

```bash
cat README.md
```

and finally:

```bash
git log -p
```

The relevant Git diff was:

```text
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: <TBD>
+- password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

which gave me the password for **Level 29**:

```text
Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```