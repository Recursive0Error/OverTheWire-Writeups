# Level 18 → 19

## 🎯 Objective

The password for the next level is stored in a file named:

```text
readme
```

in the home directory.

However, the `.bashrc` file had been modified to immediately log the user out when logging in through SSH.

Therefore, a normal interactive SSH login could not be used.

## 🔎 Understanding the Problem

Normally, I would connect to the Bandit server using SSH:

```bash
ssh -4 bandit18@bandit.labs.overthewire.org -p 2220
```

However, when starting an interactive shell, the shell configuration could cause `.bashrc` to be executed.

Since `.bashrc` had been modified to log the user out, logging in normally would immediately terminate the session.

The challenge was therefore to retrieve the contents of `readme` without starting a normal interactive session.

## 💡 Solution

SSH allows a command to be executed directly on the remote server.

Instead of logging in and then manually running `cat readme`, I included the command directly in the SSH command:

```bash
ssh -4 bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```

This instructed SSH to connect to the server and execute:

```bash
cat readme
```

directly.

## 🔍 Command Breakdown

### `ssh`

```bash
ssh
```

SSH is used to establish a secure connection to a remote machine.

### `-4`

```bash
-4
```

This tells SSH to use IPv4.

### Username and Server

```bash
bandit18@bandit.labs.overthewire.org
```

This specifies:

- Username: `bandit18`
- Server: `bandit.labs.overthewire.org`

### `-p 2220`

```bash
-p 2220
```

This specifies the SSH port.

The Bandit SSH service runs on port:

```text
2220
```

instead of the default SSH port `22`.

### Remote Command

```bash
cat readme
```

This command is executed directly on the remote server.

`cat` reads and displays the contents of the `readme` file.

## 🔑 Password

The command returned the password for **Level 19**:

```text
KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI
```

## 🧠 What I Learned

- `.bashrc` is a shell configuration file that can affect a user's shell session.
- A modified `.bashrc` can interfere with a normal interactive SSH login.
- SSH can execute commands directly on a remote server.
- A remote command can be specified after the SSH connection options.
- Executing a command directly can avoid the need for an interactive shell session.
- `cat` can be executed remotely through SSH to display a file.

---

## 📌 Key Takeaway

Instead of starting an interactive SSH session, I executed the required command directly through SSH:

```bash
ssh -4 bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```

This connected to the server, executed:

```bash
cat readme
```

and returned the password without requiring me to interact with the modified shell configuration.

The password for **Level 19** was:

```text
KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI
```