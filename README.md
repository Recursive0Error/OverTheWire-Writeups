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

