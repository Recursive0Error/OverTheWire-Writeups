# Bases

- **Event:** picoCTF 2019
- **Author:** Sanjay C / Danny T
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** What does `bDNhcm5fdGgzX3IwcDM1` mean? I think it has something to do with bases.
- **Optional tool:** [CyberChef](https://gchq.github.io/CyberChef)

## Problem Statement

The challenge provides the encoded string `bDNhcm5fdGgzX3IwcDM1` and hints that it has something to do with bases.

## Initial Observation

The string uses characters commonly found in Base64, and its length is compatible with Base64 encoding. The challenge also links to CyberChef, which can decode Base64 in a browser.

## Solution

I used the `base64` command-line tool to decode the string:

```bash
echo "bDNhcm5fdGgzX3IwcDM1" | base64 -d
```

The command returned:

```text
l3arn_th3_r0p35
```

The decoded text is the flag content, so I wrapped it in the standard picoCTF flag format.

## Flag

```text
picoCTF{l3arn_th3_r0p35}
```

## Takeaways

- Base64 is an encoding scheme, not encryption.
- The `base64 -d` option decodes Base64 input.
- CyberChef can perform the same operation with its `From Base64` recipe.