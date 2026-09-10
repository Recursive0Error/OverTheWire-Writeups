# PW Crack 3

- **Event:** Beginner picoMini 2022
- **Author:** LT 'syreal' Jones
- **Category:** General Skills
- **Difficulty:** Medium
- **Challenge:** Crack the password used by the supplied password checker to obtain the flag.

## Problem Statement

The challenge provides a Python password checker, an encrypted flag, and a hash file. The checker contains seven possible passwords, one of which is correct.

## Finding the Password Candidates

I inspected the Python program with `cat`:

```bash
cat level3.py
```

The source code contained a list of seven potential passwords. I manually entered each candidate into the password checker until one was accepted.

## Solution

I ran the checker:

```bash
python3 level3.py
```

The correct password was:

```text
865e
```

After entering it at the prompt, the program accepted the password and printed the flag.

## Flag

```text
picoCTF{m45h_fl1ng1ng_2b072a90}
```

## Takeaways

- Inspecting the source code can reveal a finite list of possible passwords.
- When there are only a few candidates, manually testing each one is practical.
- The correct password is confirmed when the checker prints its success message and flag.