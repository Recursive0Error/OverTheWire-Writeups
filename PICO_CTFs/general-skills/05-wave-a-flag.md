# Wave a flag

- **Event:** picoCTF 2021
- **Author:** syreal
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information...
- **Program:** [warm](https://challenge-files.picoctf.net/c_wily_courier/70013ed41d4cfe2bb48628471dac6fc12238b5dbe164301ae3b4e35277b1e80b/warm)

## Problem Statement

The challenge provides a program named `warm`. The prompt suggests using a help flag to discover what the program can do.

## Initial Attempt

I first tried to execute the program directly:

```bash
./warm
```

The terminal returned a permission-denied error because the file did not have execute permission.

## Solution

I used `chmod +x` to add execute permission to the program:

```bash
chmod +x warm
```

I then ran the program:

```bash
./warm
```

It printed:

```text
Hello user! Pass me a -h to learn what I can do!
```

The message indicated that the program accepts the `-h` help flag. I ran:

```bash
./warm -h
```

The program returned the flag directly:

```text
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}
```

## Flag

```text
picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}
```

## Takeaways

- A permission-denied error can mean that a file is not marked as executable.
- `chmod +x filename` adds execute permission to a file.
- Many command-line tools and binaries provide information through flags such as `-h` or `--help`.