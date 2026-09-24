# Riddle Registry

- **Event:** picoMini by CMU-Africa
- **Author:** Prince Niyonshuti N.
- **Category:** Forensics
- **Difficulty:** Easy
- **Challenge:** Find the hidden flag in the metadata of a suspicious PDF.

## Problem Statement

The challenge provides a PDF named `confidential.pdf`. Although the document appears to contain mostly garbled nonsense, the flag is hidden in its metadata.

## Inspecting the Metadata

I used ExifTool to inspect the PDF metadata:

```bash
exiftool confidential.pdf
```

The author metadata contained a suspicious string. It looked like Base64 rather than a normal author name, so I treated it as encoded data.

## Decoding the Metadata

I decoded the value with `base64`:

```bash
echo 'BASE64_VALUE' | base64 -d
```

The decoded output was the flag.

## Flag

```text
picoCTF{puzzl3d_m3tadata_f0und!_c999e2a4}
```

## Takeaways

- PDF metadata can contain useful hidden information even when the document contents look meaningless.
- `exiftool` is useful for inspecting metadata in PDFs and other file formats.
- A metadata value that resembles Base64 can be decoded with `base64 -d`.