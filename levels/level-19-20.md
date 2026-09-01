# Level 19 → 20

## 🎯 Objective

To gain access to the next level, I needed to use the **SetUID binary** in the home directory.

The password for the next level is stored in the usual location:

```text
/etc/bandit_pass/bandit20
```

However, I needed to use the provided SetUID binary to access it.

## 🔎 Initial Attempt

I first tried to read the password file directly:

```bash
cat /etc/bandit_pass/bandit20
```

This returned:

```text
Permission denied
```

This happened because the `bandit19` user did not have sufficient permissions to read the `bandit20` password file.

## 🔍 Finding the SetUID Binary

I used:

```bash
ls
```

to list the files in the home directory.

I found the SetUID binary:

```text
bandit20-do
```

I first executed it without arguments as suggested by the challenge:

```bash
./bandit20-do
```

This displayed information about how to use the binary.

## 💡 Solution

The SetUID binary allows a command to be executed with the privileges of the user who owns the binary.

I used it to execute the `cat` command:

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

Here:

- `./bandit20-do` executes the SetUID binary from the current directory.
- `cat` is the command that I want the binary to execute.
- `/etc/bandit_pass/bandit20` is the password file I want to read.

This time, the command was successful and returned:

```text
4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

## 🔑 Password

```text
4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

## 🧠 What I Learned

- Linux uses file permissions to control access to files.
- `Permission denied` means the current user does not have the required permissions.
- **SetUID (SUID)** is a Linux permission mechanism that allows an executable to run with the privileges of its owner.
- `./` is used to execute a program located in the current directory.
- A SetUID binary can execute commands with the privileges associated with its owner.
- The command passed to the SetUID binary was:

```bash
cat /etc/bandit_pass/bandit20
```

## 📌 Key Takeaway

My first attempt failed because `bandit19` did not have permission to directly read the password file:

```bash
cat /etc/bandit_pass/bandit20
```

I then used the provided SetUID binary:

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

The SetUID binary executed the `cat` command with the required privileges and revealed the password for **Level 20**.