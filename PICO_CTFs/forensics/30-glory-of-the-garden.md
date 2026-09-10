# Glory of the Garden

- **Event:** picoCTF 2019
- **Author:** jedavis/Danny
- **Category:** Forensics
- **Difficulty:** Easy
- **Challenge:** Find the hidden flag in `garden.jpg`.

## Problem Statement

The challenge provides an image named `garden.jpg` and says that the file contains more than it seems. The flag may be hidden in the file's contents rather than visible in the image.

## Initial Inspection

I first checked the image metadata with ExifTool:

```bash
exiftool garden.jpg
```

The metadata did not contain anything useful, so I inspected the printable strings embedded in the file and searched for the usual picoCTF flag prefix:

```bash
strings garden.jpg | grep "pico"
```

The command revealed the flag directly:

```text
Here is a flag: picoCTF{more_than_m33ts_the_3y339140129}
```

## Flag

```text
picoCTF{more_than_m33ts_the_3y339140129}
```

## Takeaways

- Useful information can be appended to or embedded in binary files without changing their normal appearance.
- `strings` extracts readable text from binary files.
- Searching for `pico` is a quick way to locate a picoCTF flag in file output.