# PW Crack 2

- **Event:** Beginner picoMini 2022
- **Author:** LT 'syreal' Jones
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Crack the password used by the supplied password checker to obtain the flag.

## Problem Statement

The challenge provides a Python password checker. The correct password is built from hexadecimal character codes in the source code, so the goal is to decode those values and run the checker.

## Finding the Password

I inspected the Python program with `cat`:

```bash
cat level2.py
```

The password comparison used this expression:

```python
if user_pw == chr(0x34) + chr(0x65) + chr(0x63) + chr(0x39):
```

I converted each hexadecimal value to its corresponding character:

```text
0x34 = 4
0x65 = e
0x63 = c
0x39 = 9
```

Joining the characters produced the password:

```text
4ec9
```

## Solution

I ran the password checker:

```bash
python3 level2.py
```

When prompted, I entered `4ec9`. The program accepted the password and printed the flag.

## Flag

```text
picoCTF{tr45h_51ng1ng_9701e681}
```

## Takeaways

- `chr()` converts an integer character code into a character in Python.
- Hexadecimal values can be decoded to reveal a password hidden in source code.
- Reading the password-checking logic is often enough to solve simple password challenges.