# Static ain't always noise

- **Event:** picoCTF 2021
- **Author:** syreal
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Inspect the data in a binary using the provided bash script to find the flag.

## Problem Statement

The challenge provides a binary named `static` and a script named `ltdis.sh`. The goal is to analyze the binary and locate the flag hidden among its strings.

## Running the Binary

Initially, the binary did not have execute permission:

```bash
./static
```

This returned `permission denied`, so I made it executable:

```bash
chmod +x static
./static
```

The binary printed:

```text
Oh hai! Wait what? A flag? Yes, it's around here somewhere!
```

## Analyzing the Binary

The analysis script also needed execute permission, so I enabled it:

```bash
chmod +x ltdis.sh
```

Running the script without an input file showed that it expects a program-file argument. I then analyzed `static`:

```bash
./ltdis.sh static
```

This generated `static.ltdis.x86_64.txt` and `static.ltdis.strings.txt`. I searched the extracted strings for the flag prefix:

```bash
cat static.ltdis.strings.txt | grep "pico"
```

The search found the flag at offset `3020`.

## Flag

```text
picoCTF{d15a5m_t34s3r_20335e41}
```

## Takeaways

- `chmod +x` grants a file execute permission.
- The provided script can disassemble a binary and extract printable strings.
- Searching extracted strings with `grep` is useful when a flag is embedded in a binary.