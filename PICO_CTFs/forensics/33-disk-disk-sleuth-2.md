# Disk, disk, sleuth! II

- **Event:** picoCTF 2021
- **Author:** syreal
- **Category:** Forensics
- **Difficulty:** Medium
- **Challenge:** Locate and extract `down-at-the-bottom.txt` from a disk image using Sleuth Kit.

## Problem Statement

The challenge provides a compressed disk image named `dds2-alpine.flag.img.gz`. The only known detail is that the file containing the flag is named `down-at-the-bottom.txt`.

## Extracting the Disk Image

I extracted the compressed image:

```bash
gzip -d dds2-alpine.flag.img.gz
```

This produced the disk image `dds2-alpine.flag.img`.

## Inspecting the Partition Table

I used `mmls` to inspect the partition table:

```bash
mmls dds2-alpine.flag.img
```

The Linux partition starts at sector `2048`. Sleuth Kit commands must use this value as the partition offset.

## Finding the File

I recursively listed the partition and searched for the known filename:

```bash
fls -r -p -o 2048 dds2-alpine.flag.img | grep down-at-the-bottom.txt
```

The file was found at inode `18291`:

```text
r/r 18291:      root/down-at-the-bottom.txt
```

## Extracting the File

I used `icat` with the partition offset and inode number to recover the file contents:

```bash
icat -o 2048 dds2-alpine.flag.img 18291
```

The output contained the flag, displayed as ASCII art.

## Flag

```text
picoCTF{f0r3ns1c4t0r_n0v1c3_4bd721f2}
```

## Takeaways

- `mmls` identifies partition boundaries and the sector offset needed by Sleuth Kit tools.
- `fls -r -p` recursively lists filesystem entries with their paths.
- `icat` extracts file contents from an inode inside a disk image.