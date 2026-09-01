# Level 22 → 23

## 🎯 Objective

A program is running automatically at regular intervals using **cron**, the time-based job scheduler.

The challenge instructed me to look in:

```text
/etc/cron.d/
```

and find out what command is being executed.

The goal was to understand the script and retrieve the password for **Level 23**.

## 🔎 Finding the Cron Job

I first checked the contents of my home directory:

```bash
ls
```

There were no files of interest, so I moved to the cron configuration directory:

```bash
cd /etc/cron.d/
```

I then listed the files:

```bash
ls
```

Among the files, I found:

```text
cronjob_bandit23
```

I read its contents:

```bash
cat cronjob_bandit23
```

The output was:

```text
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```

## 🔍 Understanding the Cron Job

The important line was:

```text
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
```

The five `*` characters mean that the command runs every minute:

```text
* * * * *
│ │ │ │ │
│ │ │ │ └── Day of week
│ │ │ └──── Month
│ │ └────── Day of month
│ └──────── Hour
└────────── Minute
```

The username:

```text
bandit23
```

means that the script is executed as the **bandit23** user.

The script being executed is:

```text
/usr/bin/cronjob_bandit23.sh
```

## 📄 Reading the Script

I initially tried:

```bash
cat cronjob_bandit23.sh
```

but this returned:

```text
cat: cronjob_bandit23.sh: No such file or directory
```

This was because I was currently inside:

```text
/etc/cron.d/
```

while the script was actually located in:

```text
/usr/bin/
```

I therefore used the full path:

```bash
cat /usr/bin/cronjob_bandit23.sh
```

The script contained:

```bash
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

## 🔍 Understanding the Script

### Line 1

```bash
#!/bin/bash
```

This is the **shebang** and tells the system to execute the script using Bash.

### Line 2

```bash
myname=$(whoami)
```

`whoami` prints the username of the user currently running the script.

The output is stored in the variable:

```text
myname
```

This is important because the cron job runs the script as:

```text
bandit23
```

Therefore, when cron executes the script:

```bash
myname=bandit23
```

### Line 3

```bash
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
```

This line generates the name of the temporary file.

First:

```bash
echo I am user $myname
```

When the script runs as `bandit23`, this becomes:

```bash
echo I am user bandit23
```

The output is then piped into:

```bash
md5sum
```

which generates an MD5 hash.

Finally:

```bash
cut -d ' ' -f 1
```

extracts only the hash and removes the additional information printed by `md5sum`.

For `bandit23`, the resulting filename is:

```text
7dfc5d0348e965fba8b56a01c1508c98
```

Therefore:

```text
mytarget=7dfc5d0348e965fba8b56a01c1508c98
```

### Line 4

```bash
echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
```

This prints a debug message showing which password file is being copied and where it is being copied.

### Line 5

```bash
cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

This reads the password file corresponding to the current user and redirects its contents into the temporary file.

Since cron executes the script as `bandit23`, the command effectively becomes:

```bash
cat /etc/bandit_pass/bandit23 > /tmp/7dfc5d0348e965fba8b56a01c1508c98
```

Therefore, the password for `bandit23` will be stored in:

```text
/tmp/7dfc5d0348e965fba8b56a01c1508c98
```

## 🧪 Manually Executing the Script

The challenge suggested executing the script to see its debug information.

I ran:

```bash
/usr/bin/cronjob_bandit23.sh
```

I got:

```text
Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/8169b67bd894ddbb4412f91573b38db3
```

I then read the generated file:

```bash
cat /tmp/8169b67bd894ddbb4412f91573b38db3
```

This returned:

```text
RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz
```

However, this was **not the new password**.

### Why?

I had manually executed the script while logged in as:

```text
bandit22
```

Therefore:

```bash
whoami
```

returned:

```text
bandit22
```

So the script copied:

```text
/etc/bandit_pass/bandit22
```

instead of:

```text
/etc/bandit_pass/bandit23
```

The actual cron job runs the script as:

```text
bandit23
```

so I needed to calculate the target filename using `bandit23`.

## 🔐 Finding the Correct Temporary File

The script uses:

```bash
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
```

Since the cron job runs the script as `bandit23`, I calculated the filename manually:

```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
```

This returned:

```text
8ca319486bfbbc3663ea0fbe81326349
```

Therefore, the password should be stored in:

```text
/tmp/8ca319486bfbbc3663ea0fbe81326349
```

I read the file using:

```bash
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

This returned:

```text
gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw
```

## 🔑 Password

```text
gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw
```

## 🧠 What I Learned

The important part of this level was understanding that the script behaves differently depending on which user executes it.

When I manually ran:

```bash
/usr/bin/cronjob_bandit23.sh
```

I was logged in as `bandit22`, so:

```bash
whoami
```

returned:

```text
bandit22
```

and the script copied the `bandit22` password.

However, the cron configuration specifies:

```text
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh
```

so cron executes the script as `bandit23`.

This means:

```bash
myname=$(whoami)
```

becomes:

```text
myname=bandit23
```

and the script ultimately performs the equivalent of:

```bash
cat /etc/bandit_pass/bandit23 > /tmp/8ca319486bfbbc3663ea0fbe81326349
```

I could then read the password with:

```bash
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

which gave:

```text
gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw
```