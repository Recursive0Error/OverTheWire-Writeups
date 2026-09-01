# Level 21 → 22

## 🎯 Objective

A program is running automatically at regular intervals using **cron**, the time-based job scheduler.

The challenge instructed me to look inside:

```text
/etc/cron.d/
```

and find the configuration that determines which command is being executed.

## 🔎 Finding the Cron Job

I first listed the contents of `/etc/cron.d/`:

```bash
ls /etc/cron.d/
```

This displayed:

```text
behemoth4_cleanup
clean_tmp
cronjob_bandit22
cronjob_bandit23
cronjob_bandit24
e2scrub_all
leviathan5_cleanup
manpage3_resetpw_job
otw-tmp-dir
```

The relevant file for this level was:

```text
cronjob_bandit22
```

I then changed into the directory:

```bash
cd /etc/cron.d/
```

## 📄 Examining the Cron Configuration

I read the cron configuration using:

```bash
cat cronjob_bandit22
```

It contained:

```text
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

The important entry was:

```text
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

### 🔍 Understanding the Cron Entry

The five fields:

```text
* * * * *
```

represent:

```text
minute hour day-of-month month day-of-week
```

Using `*` in all five positions means the command runs **every minute**.

The next field:

```text
bandit22
```

specifies the user that the cron job runs as.

Therefore, the script is executed every minute as the `bandit22` user.

The command being executed is:

```text
/usr/bin/cronjob_bandit22.sh
```

The following:

```text
&> /dev/null
```

redirects both standard output and standard error to `/dev/null`, so the cron job does not display output.

## 🔍 Examining the Script

I then read the script:

```bash
cat /usr/bin/cronjob_bandit22.sh
```

The script contained:

```bash
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

### Line 1: `#!/bin/bash`

```bash
#!/bin/bash
```

This is called a **shebang**.

It tells the operating system that the script should be executed using the Bash interpreter located at:

```text
/bin/bash
```

### Line 2: `chmod 644`

```bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

`chmod` is used to change file permissions.

The permission:

```text
644
```

means:

```text
Owner  → read + write
Group  → read
Others → read
```

Since the file is made readable by others, the `bandit21` user can read it.

### Line 3: Password Redirection

```bash
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

This command reads the password file:

```text
/etc/bandit_pass/bandit22
```

The cron job is running as `bandit22`, so the script has permission to read that file.

The `>` symbol is the **output redirection operator**.

Instead of displaying the password on the terminal, it redirects the output into:

```text
/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

The overall process is therefore:

```text
Cron
  │
  │ Every minute
  ▼
cronjob_bandit22.sh
  │
  │ Runs as bandit22
  ▼
Reads /etc/bandit_pass/bandit22
  │
  ▼
Writes password to /tmp/...
  │
  ▼
chmod 644 makes the file readable
  │
  ▼
I can read the file
```

## 🔑 Retrieving the Password

Since the cron job runs every minute, it created the temporary file and placed the password inside it.

I read the file using:

```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

This returned:

```text
RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz
```

## 🔑 Password

```text
RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz
```

## 🧠 What I Learned

- **Cron** is used to schedule commands and scripts to run automatically.
- Cron configuration files can be found in `/etc/cron.d/`.
- The five `*` fields in a cron expression represent minute, hour, day of month, month, and day of week.
- `* * * * *` means the command runs every minute.
- The username after the cron schedule specifies which user executes the command.
- `chmod 644` makes a file readable by the owner, group, and other users while only the owner can write to it.
- `>` redirects command output into a file.
- `/dev/null` can be used to discard command output.
- A scheduled task running with higher privileges can create files that another user may be able to read.

---

## 📌 Key Takeaway

The main idea of this level was to follow the chain:

```text
/etc/cron.d/cronjob_bandit22
        ↓
/usr/bin/cronjob_bandit22.sh
        ↓
Runs every minute as bandit22
        ↓
Reads /etc/bandit_pass/bandit22
        ↓
Writes password to /tmp/...
        ↓
chmod 644
        ↓
Password becomes readable
```

The important commands I used were:

```bash
ls /etc/cron.d/
```

```bash
cat /etc/cron.d/cronjob_bandit22
```

```bash
cat /usr/bin/cronjob_bandit22.sh
```

and finally:

```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

which gave me the password for **Level 22**:

```text
RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz
```