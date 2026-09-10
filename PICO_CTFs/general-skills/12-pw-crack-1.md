# PW Crack 1

- **Event:** Beginner picoMini 2022
- **Author:** LT 'syreal' Jones
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Crack the password used by the supplied password checker to obtain the flag.

## Problem Statement

The challenge provides a Python password checker and an encrypted flag file. The goal is to inspect the checker, determine the correct password, and run the program with that password.

## Finding the Password

I inspected the Python program with `cat`:

```bash
cat level1.py
```

The source code compared the entered password with a hard-coded value:

```python
if user_pw == "691d":
```

Therefore, the password was:

```text
691d
```

## Solution

I ran the password checker:

```bash
python3 level1.py
```

When prompted, I entered `691d`. The program accepted the password and printed the flag.

## Flag

```text
picoCTF{545h_r1ng1ng_56891419}
```

## Takeaways

- Inspecting a small password-checking script can reveal hard-coded credentials.
- `cat` can display the source code of a text-based program.
- After finding the expected value, run the checker and provide it at the prompt.