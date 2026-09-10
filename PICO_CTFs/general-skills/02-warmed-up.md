# Warmed Up

- **Event:** picoCTF 2019
- **Author:** Sanjay C / Danny Tunitis
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** What is `0x3D` (base 16) in decimal (base 10)?

## Problem Statement

The challenge asks for the decimal value of the hexadecimal number `0x3D`.

## Approach

I looked up the hexadecimal value and found that `0x3D` is equal to `61` in decimal.

The conversion can also be worked out using the hexadecimal place values:

```text
0x3D = (3 x 16^1) + (D x 16^0)
     = (3 x 16) + (13 x 1)
     = 48 + 13
     = 61
```

In hexadecimal, `D` represents the decimal value `13`.

## Flag

```text
picoCTF{61}
```

## Takeaways

- Hexadecimal is base 16, so each digit represents a power of 16.
- The hexadecimal digits `A` through `F` represent decimal values `10` through `15`.
- `0x3D` converts to decimal as `(3 x 16) + 13 = 61`.