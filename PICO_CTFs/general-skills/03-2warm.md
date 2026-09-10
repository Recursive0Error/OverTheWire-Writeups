# 2Warm

- **Event:** picoCTF 2019
- **Author:** Sanjay C / Danny Tunitis
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Can you convert the number 42 (base 10) to binary (base 2)?

## Problem Statement

The challenge asks for the binary representation of the decimal number `42`.

## Approach

I looked up the decimal-to-binary conversion and found that `42` in base 10 is `101010` in base 2.

This can be verified using binary place values:

```text
101010 = (1 x 32) + (0 x 16) + (1 x 8) + (0 x 4) + (1 x 2) + (0 x 1)
       = 32 + 8 + 2
       = 42
```

## Flag

```text
picoCTF{101010}
```

## Takeaways

- Binary is base 2, so each position represents a power of 2.
- The binary digits needed to represent 42 are in the `32`, `8`, and `2` positions.
- Therefore, `42` in decimal is `101010` in binary.