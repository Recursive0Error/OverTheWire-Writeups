# convertme.py

- **Event:** Beginner picoMini 2022
- **Author:** LT 'syreal' Jones
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Run the Python script and convert the given number from decimal to binary to get the flag.

## Problem Statement

The challenge provides a Python script that asks for the binary representation of a decimal number.

## Approach

I ran the script with Python 3:

```bash
python3 convertme.py
```

The script asked:

```text
If 58 is in decimal base, what is it in binary base?
```

I converted `58` to binary. The result is `111010`.

## Solution

I entered `111010` as the answer. The script confirmed that the answer was correct and printed the flag.

## Flag

```text
picoCTF{4ll_y0ur_b4535_9c3b7d4d}
```

## Takeaways

- Binary is base 2, so decimal values are represented using powers of 2.
- `58` in decimal is `111010` in binary.
- Running the provided script validates the conversion and reveals the flag.