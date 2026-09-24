# Corrupted File

- **Event:** picoMini by CMU-Africa
- **Author:** Yahaya Meddy
- **Category:** Forensics
- **Difficulty:** Easy
- **Challenge:** Repair the broken image file and recover the hidden flag.

## Problem Statement

The provided file looks damaged or corrupted. The challenge hints that only a few bytes may be wrong, and that repairing the file may reveal the original image containing the hidden flag.

## Initial Inspection

I first checked the file type:

```bash
file file
```

The file was not recognized as a valid image, so I examined the hex dump to see if the file signature was malformed:

```bash
xxd file
```

The dump showed that it was a JPEG/JFIF file, but the header was clearly corrupted. I knew that JPEG files begin with the start-of-image marker:

```text
FF D8
```

That indicated the first bytes were wrong and needed to be restored.

## Breakthrough

I confirmed the problem by checking the expected JPEG header format and identifying that the leading bytes were incorrect. After that, I extracted the hex dump into a text file so I could fix the damaged header cleanly.

## Solution

I saved the hex dump:

```bash
xxd file > dump
```

Then I opened the dump in a text editor and changed the beginning of the file to the correct JPEG header value:

```text
FF D8
```

After fixing the corrupted header, I rebuilt the binary file:

```bash
xxd -r dump dump.jpeg
```

Once the file was reconstructed, the image opened successfully and contained the flag.

## Flag

```text
picoCTF{r3st0r1ng_th3_by73s_b67c1558}
```

## Takeaways

- A broken file signature can make a valid image appear unreadable.
- `file` and `xxd` are useful for identifying malformed binary file headers.
- Fixing a few bytes at the start of a file can restore a complete image.
- File forensics often depends on recognizing the correct structure rather than the visible content alone.
