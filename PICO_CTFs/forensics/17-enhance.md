# Enhance!

- **Event:** picoCTF 2022
- **Author:** LT 'syreal' Jones
- **Category:** Forensics
- **Difficulty:** Medium
- **Challenge:** Download an SVG image and find the hidden flag.

## Problem Statement

The challenge provides an SVG image named `drawing.flag.svg`. The goal is to inspect the image file and recover the flag hidden in its contents.

## Initial Inspection

I displayed the SVG file as text:

```bash
cat drawing.flag.svg
```

The file contained many `<tspan>` elements. Each element held a small piece of text, and the text was styled with an extremely small font size and white fill, making it effectively invisible when viewing the image normally.

## Finding the Flag

I inspected the text inside the `<tspan>` elements and concatenated the characters in order. The hidden text decoded to:

```text
picoCTF{3nh4nc3d_24374675}
```

## Flag

```text
picoCTF{3nh4nc3d_24374675}
```

## Takeaways

- Image files can contain useful information in their underlying markup or metadata.
- SVG files are text-based XML documents and can be inspected with standard command-line tools.
- Tiny or white SVG text may be invisible in an image viewer while still being present in the file.
