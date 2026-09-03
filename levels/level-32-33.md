# Level 32 → 33

## 🎯 Objective

The goal was to escape the restricted shell for `bandit32` and retrieve the password for the next level.

## 🔐 Logging In

I connected to Level 32 using the password from the previous challenge:

```bash
ssh bandit32@bandit.labs.overthewire.org -p 2220
```

## 🧪 Identifying the Shell Behavior

After logging in, the shell displayed an unusual prompt. Commands typed in lowercase were automatically converted to uppercase before execution.

For example, entering:

```bash
ls
```

resulted in an error similar to:

```text
sh: 1: LS: not found
```

This showed that the shell was applying an uppercase filter to the entered commands.

## 🚪 Escaping the Restricted Shell

In a Unix shell, `$0` expands to the name of the current shell or script. Entering it at the restricted prompt bypassed the command transformation and started a normal `/bin/sh` session:

```bash
$0
```

The prompt changed to a simple `$`, indicating that the unrestricted shell was active.

## 🔑 Retrieving the Password

From the unrestricted shell, I read the password file for Level 33:

```bash
cat /etc/bandit_pass/bandit33
```

This returned:

```text
u4P2CyPOwPGLe94RdD9Uo2FxFwvnFswM
```

## 🔑 Password

```text
u4P2CyPOwPGLe94RdD9Uo2FxFwvnFswM
```

## 🧠 What I Learned

* Restricted shells may transform or filter commands before executing them.
* `$0` refers to the current shell or script name in Unix shell environments.
* Expanding `$0` can be used to start a fresh shell when the wrapper does not filter variable expansion.
* Once the unrestricted shell was available, the next password file could be read normally.

## 📌 Key Takeaway

The important steps were:

```text
Log in as bandit32
        ↓
Observe that commands are converted to uppercase
        ↓
Enter $0 to start a normal shell
        ↓
Read /etc/bandit_pass/bandit33
        ↓
Retrieve the next password
```

The main commands were:

```bash
ssh bandit32@bandit.labs.overthewire.org -p 2220
$0
cat /etc/bandit_pass/bandit33
```

This revealed the password for **Level 33**:

```text
u4P2CyPOwPGLe94RdD9Uo2FxFwvnFswM
```
