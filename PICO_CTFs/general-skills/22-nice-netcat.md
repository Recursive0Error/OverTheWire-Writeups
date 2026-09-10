# Nice netcat...

- **Event:** picoCTF 2021
- **Author:** syreal
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Connect to the provided program with netcat and decode its output to get the flag.

## Problem Statement

The challenge provides a network service that prints a sequence of decimal numbers. Each number represents an ASCII character.

## Approach

I connected to the service with netcat:

```bash
nc wily-courier.picoctf.net 55524
```

The service returned decimal ASCII codes, beginning with:

```text
112 105 99 111 67 84 70 123 ... 125 10
```

I converted each decimal value to its ASCII character and joined the characters in order. For example, `112` is `p`, `105` is `i`, and `99` is `c`.

## Solution

After decoding the complete sequence, the resulting text was:

```text
picoCTF{g00d_k1tty!_n1c3_k1tty!_e9c85}
```

## Flag

```text
picoCTF{g00d_k1tty!_n1c3_k1tty!_e9c85}
```

## Takeaways

- Netcat can connect to simple TCP services from the command line.
- Decimal ASCII codes can be converted directly into text.
- Decoding the values in order reveals the flag.