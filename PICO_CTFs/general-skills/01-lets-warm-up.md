# Lets Warm Up

- **Event:** picoCTF 2019
- **Author:** Sanjay C / Danny Tunitis
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** If I told you a word started with `0x70` in hexadecimal, what would it start with in ASCII?

## Problem Statement

The challenge asks for the ASCII character represented by the hexadecimal value `0x70`.

## Approach

I converted `0x70` from hexadecimal to decimal:

```text
0x70 = (7 x 16) + 0
     = 112
```

The ASCII character for decimal `112` is the lowercase letter `p`.

## Flag

```text
picoCTF{p}
```

## Takeaways

- Hexadecimal values can represent ASCII characters.
- `0x70` is decimal `112`, which maps to the ASCII character `p`.