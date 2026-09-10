# Disk, disk, sleuth!

- **Event:** picoCTF 2021
- **Author:** syreal
- **Category:** Forensics
- **Difficulty:** Medium
- **Challenge:** Use `srch_strings` and terminal tools to find a hidden flag in a disk image.

## Problem Statement

The challenge provides a compressed disk image named `dds1-alpine.flag.img.gz`. The goal is to extract the image and search its strings for the flag.

## Extracting the Disk Image

I extracted the compressed disk image:

```bash
gzip -d dds1-alpine.flag.img.gz
```

This produced the disk image `dds1-alpine.flag.img`.

## Searching the Disk Image

I used Sleuth Kit's `srch_strings` utility and filtered the output for strings containing `pico`:

```bash
srch_strings dds1-alpine.flag.img | grep "pico"
```

The output included a few unrelated kernel symbols, but also revealed the flag:

```text
SAY picoCTF{f0r3ns1c4t0r_n30phyt3_5e56e786}
```

## Flag

```text
picoCTF{f0r3ns1c4t0r_n30phyt3_5e56e786}
```

## Takeaways

- `srch_strings` extracts printable strings from disk images and other binary data.
- Piping the output through `grep` quickly narrows the results to likely flag text.
- Disk images may contain both useful embedded text and unrelated strings from the underlying filesystem or software.
