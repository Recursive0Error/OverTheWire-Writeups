# Level 31 → 32

## 🎯 Objective

The repository README provided the following task:

```text
This time your task is to push a file to the remote repository.

File name: key.txt
Content: 'May I come in?'
Branch: master
```

The goal was to create `key.txt`, commit it to the `master` branch, and push it to the remote repository to obtain the password for the next level.

## 📥 Inspecting the Repository

After cloning the repository and entering it, I read the README and listed all files:

```bash
cat README.md
ls -a
```

The repository contained a `.gitignore` file. I checked its contents:

```bash
cat .gitignore
```

It contained:

```text
*.txt
```

This meant that `key.txt` would be ignored by Git unless I explicitly forced it into the index.

## 🗝️ Creating and Staging the File

I created the required file with the exact content from the instructions:

```bash
echo "May I come in?" > key.txt
```

Because the file matched the `.gitignore` rule, I staged it with `git add -f`:

```bash
git add -f key.txt
```

The `-f` option forces Git to add an otherwise ignored file.

## 💾 Committing the File

The first commit attempt used an invalid option:

```bash
git commit -f
```

For commits, `-m` supplies the commit message. Git also required a local author identity, so I configured one for this repository:

```bash
git config user.email "bandit31@bandit.labs.overthewire.org"
git config user.name "bandit31"
```

I then committed the staged file:

```bash
git commit -m "Add key file"
```

## 🚀 Pushing to the Remote Repository

I pushed the `master` branch with:

```bash
git push origin master
```

The first password prompt was rejected, but the retry succeeded and the remote pre-receive hook validated the submitted file. The push itself was then rejected because the challenge hook intentionally reports the password instead of accepting the branch update.

The hook returned:

```text
Well done! Here is the password for the next level:
pWuj5jBQ6IgV0NXwiH6g1pXRF8S1YvbT
```

## 🔑 Password

```text
pWuj5jBQ6IgV0NXwiH6g1pXRF8S1YvbT
```

## 🧠 What I Learned

* `.gitignore` can prevent required files from being staged.
* `git add -f <file>` stages a file even when it matches an ignore rule.
* `git commit -m "message"` creates a commit with a message.
* Git requires a configured author name and email before creating commits.
* A remote pre-receive hook can inspect pushed content and return challenge information.
* A rejected push does not necessarily mean the challenge failed; the server hook may have already displayed the password.

## 📌 Key Takeaway

The important steps were:

```text
Read README.md
        ↓
Inspect .gitignore
        ↓
Create key.txt with the required content
        ↓
Force-add the ignored file
        ↓
Configure Git identity
        ↓
Commit the file
        ↓
Push master to origin
        ↓
Read the password from the server response
```

The main commands were:

```bash
cat README.md
cat .gitignore
echo "May I come in?" > key.txt
git add -f key.txt
git config user.email "bandit31@bandit.labs.overthewire.org"
git config user.name "bandit31"
git commit -m "Add key file"
git push origin master
```

This revealed the password for **Level 32**:

```text
pWuj5jBQ6IgV0NXwiH6g1pXRF8S1YvbT
```
