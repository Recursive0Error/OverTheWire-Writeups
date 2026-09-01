# Bandit Level 26 → Level 27

## 🎯 Objective

The goal of this level is to retrieve the password for **bandit27**.

After completing the previous level, I already had access to a normal Bash shell as:

```text
bandit26
```

From this shell, I needed to examine the files in the current directory and look for something that could be used to execute commands with higher privileges.

## 🔎 Listing the Files

I used:

```bash
ls -la
```

This displayed the files in the current directory along with their permissions.

Among the files, I found:

```text
bandit27-do
```

The important thing about this file was its **Set User ID (Setuid)** permission.

## 🔐 Understanding Setuid

Setuid is a special Linux permission that allows an executable file to run with the permissions of its **owner**, rather than the permissions of the user executing it.

In this case, the executable:

```text
bandit27-do
```

is owned by:

```text
bandit27
```

Therefore, when I execute:

```bash
./bandit27-do
```

the command runs with the permissions of **bandit27**.

This is important because I am currently logged in as:

```text
bandit26
```

Normally, `bandit26` cannot read:

```text
/etc/bandit_pass/bandit27
```

However, the Setuid executable allows me to execute a command with `bandit27`'s permissions.

The basic idea is:

```text
bandit26
    │
    │ Executes
    ▼
./bandit27-do
    │
    │ Setuid
    ▼
Runs with bandit27 permissions
```

## 🔍 Using `bandit27-do`

The executable allows me to provide a command that should be executed.

I used:

```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

Here:

```text
./bandit27-do
```

executes the Setuid program.

The remaining part:

```text
cat /etc/bandit_pass/bandit27
```

is the command passed to the program.

The `cat` command attempts to read:

```text
/etc/bandit_pass/bandit27
```

Because `bandit27-do` runs with the permissions of `bandit27`, the command has sufficient privileges to read the password file.

## 🔑 Retrieving the Password

I ran:

```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

The command returned:

```text
STJLJBRRphMxKB392CT4iOr5CbzPU9ER
```

## 🔑 Password

```text
STJLJBRRphMxKB392CT4iOr5CbzPU9ER
```

## 🧠 What I Learned

* `ls -la` displays files along with their permissions and ownership.
* Linux has special permissions in addition to the normal read, write, and execute permissions.
* **Setuid** allows an executable to run with the permissions of its owner.
* The owner of a Setuid executable can therefore be important when analyzing its behavior.
* `./filename` is used to execute a file located in the current directory.
* Arguments can be passed to an executable after its filename.
* `cat` can be used to display the contents of a file.
* Setuid executables can sometimes provide access to resources that the current user cannot normally access.
* Understanding Linux file permissions is an important skill when working with Linux systems and cybersecurity challenges.

---

## 📌 Key Takeaway

The main idea of this level was to recognize the **Setuid** permission on the `bandit27-do` executable and use it to execute a command with `bandit27`'s permissions.

The complete process was:

```text
Bash shell as bandit26
        ↓
ls -la
        ↓
Find bandit27-do
        ↓
Notice Setuid permission
        ↓
Execute ./bandit27-do
        ↓
Command runs with bandit27 permissions
        ↓
cat /etc/bandit_pass/bandit27
        ↓
Password for Level 27
```

The important command I used was:

```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

which gave me the password for **Level 27**:

```text
STJLJBRRphMxKB392CT4iOr5CbzPU9ER
```