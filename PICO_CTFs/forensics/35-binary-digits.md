# Binary Digits

- **Event:** picoCTF 2026
- **Author:** Yahaya Meddy
- **Category:** Forensics
- **Difficulty:** Easy
- **Challenge:** Recover meaningful data from a file containing only binary digits.

## Problem Statement

The challenge provides a file named `digits.bin` containing a long sequence of `1`s and `0`s. The goal is to determine whether the binary digits encode another file or useful information.

## Initial Inspection

I checked the file type and inspected its beginning:

```bash
file digits.bin
head -c 100 digits.bin
```

The bits began with:

```text
11111111 11011000 11111111 11100000
```

Grouping the digits into 8-bit bytes and converting them to hexadecimal produced:

```text
FF D8 FF E0
```

These bytes are the standard magic header for a JPEG image, so the binary digits likely represent an encoded JPEG file.

## Recovering the Image

I converted every group of eight bits into one byte and wrote the result to `recovered.jpg`:

```bash
python3 - << 'PY'
bits = open("digits.bin", "r").read().strip()
data = bytes(
    int(bits[i:i + 8], 2)
    for i in range(0, len(bits), 8)
    if len(bits[i:i + 8]) == 8
)
open("recovered.jpg", "wb").write(data)
print("wrote", len(data), "bytes")
PY
```

I opened the recovered image:

```bash
xdg-open recovered.jpg
```

The image contained the flag.

## Flag

```text
picoCTF{h1dd3n_1n_th3_b1n4ry_cc2099d3}
```

## Takeaways

- Binary digits can encode a file when grouped into 8-bit bytes.
- File magic bytes can reveal the format of data with an unclear extension.
- `FF D8 FF E0` identifies the beginning of a JPEG image.