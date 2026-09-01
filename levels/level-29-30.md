# Level 29 → 30

## 🎯 Objective

There is a Git repository available at:

```text
ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo
```

The repository is accessible through SSH on port:

```text
2220
```

The goal is to clone the repository and find the password for the next level.

---

## 📥 Cloning the Repository

Since the OverTheWire Git server uses the non-standard SSH port `2220`, I needed to tell Git to use this port while cloning the repository.

I used:

```bash
GIT_SSH_COMMAND='ssh -p 2220' git clone ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo
```

### 🔍 Command Breakdown

```bash
GIT_SSH_COMMAND='ssh -p 2220'
```

`GIT_SSH_COMMAND` is an environment variable that allows us to specify which SSH command Git should use.

In this case:

```bash
ssh -p 2220
```

tells SSH to connect using port `2220` instead of the default SSH port `22`.

The complete command:

```bash
GIT_SSH_COMMAND='ssh -p 2220' git clone ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo
```

clones the remote Git repository onto my local machine.

When prompted, I entered the current password for `bandit29`.

---

## 📂 Entering the Repository

After cloning the repository, I changed into the newly created directory:

```bash
cd repo
```

I then checked the files in the repository and read the `README.md` file:

```bash
cat README.md
```

The file contained a message indicating that the password was not available in the production version of the repository.

This suggested that the password might exist in another Git branch.

---

## 🌿 Checking Available Branches

I checked all available local and remote branches using:

```bash
git branch -a
```

The `-a` option displays both:

* Local branches
* Remote branches

Among the branches, I found a development branch:

```text
remotes/origin/dev
```

This indicated that the repository contained another version of the project that could potentially contain the password.

---

## 🔄 Switching to the Development Branch

I switched to the development branch using:

```bash
git checkout dev
```

The `git checkout` command changes the currently active branch.

After switching branches, the files in my working directory were updated to match the version stored in the `dev` branch.

---

## 🔑 Retrieving the Password

I read the `README.md` file again:

```bash
cat README.md
```

This time, the file contained the credentials for the next level:

```text
username: bandit30
password: jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX
```

---

## 🔑 Password

```text
jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX
```

---

## 🧠 What I Learned

* Git repositories can contain multiple branches with different versions of files.
* `git clone` is used to download a remote Git repository.
* `GIT_SSH_COMMAND` can be used to specify custom SSH options when Git connects to a remote repository.
* `ssh -p 2220` specifies a non-default SSH port.
* `git branch -a` displays both local and remote branches.
* Remote branches can contain information that is not present in the currently checked-out branch.
* `git checkout <branch>` switches to another branch.
* Examining different branches is important when analyzing a Git repository.

---

## 📌 Key Takeaway

The password was not available in the default production branch.

The important steps were:

```text
Clone Repository
        ↓
Check README.md
        ↓
Password not present
        ↓
List all Git branches
        ↓
Find development branch
        ↓
Switch to dev branch
        ↓
Read README.md again
        ↓
Retrieve password
```

The main commands I used were:

```bash
GIT_SSH_COMMAND='ssh -p 2220' git clone ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo
```

```bash
cd repo
```

```bash
cat README.md
```

```bash
git branch -a
```

```bash
git checkout dev
```

Finally:

```bash
cat README.md
```

This revealed the password for **Level 30**:

```text
jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX
```
