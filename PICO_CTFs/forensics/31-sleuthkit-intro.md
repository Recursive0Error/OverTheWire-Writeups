# Sleuthkit Intro

- **Event:** picoCTF 2022
- **Author:** LT 'syreal' Jones
- **Category:** Forensics
- **Difficulty:** Medium
- **Challenge:** Use `mmls` to find the size of the Linux partition in a disk image.

## Problem Statement

The challenge provides a compressed disk image named `disk.img.gz`. The goal is to extract the image, inspect its partition table with `mmls`, and submit the Linux partition size to the remote checker service.

## Extracting the Disk Image

I downloaded the image and extracted it:

```bash
gzip -d disk.img.gz
```

## Inspecting the Partition Table

I ran `mmls` on the extracted disk image:

```bash
mmls disk.img
```

The output showed the Linux partition:

```text
Start        End          Length       Description
0000002048   0000204799   0000202752   Linux (0x83)
```

The Linux partition size is `202752` sectors.

## Checking the Answer

I connected to the checker service and submitted the partition length:

```bash
nc saturn.picoctf.net 61321
```

```text
What is the size of the Linux partition in the given disk image?
Length in sectors: 0000202752
0000202752
Great work!
```

## Flag

```text
picoCTF{mm15_f7w!}
```

## Takeaways

- `mmls` displays partition tables and volume layouts in disk images.
- The partition size is given by the `Length` column, measured in sectors.
- For this image, the Linux partition occupies `202752` sectors.
