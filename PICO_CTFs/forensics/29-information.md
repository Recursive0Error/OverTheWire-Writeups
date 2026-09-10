# Information

- **Event:** picoCTF 2021
- **Author:** susie
- **Category:** Forensics
- **Difficulty:** Easy
- **Challenge:** Inspect an image's metadata to find the hidden flag.

## Problem Statement

The challenge provides an image named `cat.jpg`. The prompt says that files can be changed in a secret way, suggesting that the flag may be hidden in the file's metadata rather than visible in the image.

## Initial Inspection

I first checked the file type:

```bash
file cat.jpg
```

The file was correctly identified as a JPEG, so I inspected its metadata with ExifTool:

```bash
exiftool cat.jpg
```

Most fields looked normal, but the `License` field contained this Base64 string:

```text
cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
```

## Decoding the Metadata

My first attempt passed the encoded text directly to `base64 -d`, which made the command treat it as a filename. The encoded value needs to be sent through standard input instead:

```bash
echo "cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9" | base64 -d
```

The decoded output was:

```text
picoCTF{the_m3tadata_1s_modified}
```

## Flag

```text
picoCTF{the_m3tadata_1s_modified}
```

## Takeaways

- File metadata can contain hidden or altered challenge information.
- `exiftool` is useful for inspecting image metadata.
- Base64 decoding tools commonly read from standard input or require an input filename; piping text with `echo` avoids that ambiguity.