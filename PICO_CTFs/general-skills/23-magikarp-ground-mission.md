# Magikarp Ground Mission

- **Event:** picoCTF 2021
- **Author:** syreal
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Use SSH, directory navigation, and file-reading commands to collect three parts of the flag.

## Problem Statement

The challenge provides a container accessible over SSH. The goal is to move between directories, follow the instructions in text files, and read the three flag fragments.

## Connecting to the Container

I connected to the challenge container with SSH over IPv4:

```bash
ssh -4 ctf-player@wily-courier.picoctf.net -p 64551
```

## Finding the Flag Fragments

After connecting, I listed the files in the starting directory and read the first fragment:

```bash
ls
cat 1of3.flag.txt
```

This produced:

```text
picoCTF{xxsh_
```

The instructions said to go to the root directory, so I ran:

```bash
cd /
ls
cat 2of3.flag.txt
```

The second fragment was:

```text
0ut_0f_//4t3r_
```

The final instructions said to go home, represented by `~`. I ran:

```bash
cd ~
ls
cat 3of3.flag.txt
```

The final fragment was:

```text
0b24fc4f}
```

## Flag

Joining the three fragments in order gives:

```text
picoCTF{xxsh_0ut_0f_//4t3r_0b24fc4f}
```

## Takeaways

- `ssh` connects to a remote shell.
- `cd /` moves to the root directory, while `cd ~` moves to the current user's home directory.
- `ls` lists directory contents and `cat` prints file contents.
- Flag fragments can be collected from different directories and joined in order.