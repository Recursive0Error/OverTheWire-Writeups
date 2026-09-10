# Strings It

- **Event:** picoCTF 2019
- **Author:** Sanjay C / Danny Tunitis
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Can you find the flag in the provided file without running it?
- **File:** [strings](https://challenge-files.picoctf.net/c_fickle_tempest/6577d3f1500aebcd300787bd5d96216b30aed379c811f5e83e888f897da4a3d5/strings)

## Problem Statement

The challenge provides a file and asks for the flag without executing it. The goal is to inspect the readable strings embedded in the file.

## Initial Observations

I checked the file type with `file`:

```bash
file strings
```

The output identified it as a Windows executable. Since the challenge says not to run the file, I inspected it statically instead.

## Solution

I printed the readable strings in the executable:

```bash
strings strings
```

The output was large, so I filtered it for lines containing `pico`:

```bash
strings strings | grep "pico"
```

This revealed the flag.

## Flag

```text
picoCTF{5tRIng5_1T_d6306c19}
```

## Takeaways

- `file` can identify a file's type without executing it.
- `strings` extracts readable text from binary files.
- Piping the output to `grep` makes it easier to find a known flag prefix.
- Static inspection is useful when a challenge specifically says not to run a file.