# Flag in Flame

- **Event:** picoMini by CMU-Africa
- **Author:** Prince Niyonshuti N.
- **Category:** Forensics
- **Difficulty:** Easy
- **Challenge:** Investigate the suspicious encoded log file and uncover the hidden message.

## Problem Statement

The challenge gives a very large log file that appears to contain an encoded blob instead of normal log output. The file likely hides data inside a larger structure, and the goal is to decode it and find the concealed flag.

## Initial Inspection

I started by printing the file to see what kind of data it contained:

```bash
cat logs.txt
```

The output looked like a large block of base64 text, so I tried decoding it:

```bash
base64 -d logs.txt > logs.bin
```

Once the data was decoded, I checked the file type:

```bash
file logs.bin
```

The result showed that the decoded file was actually a PNG image:

```text
logs.bin: PNG image data, 1200 x 800, 8-bit grayscale, non-interlaced
```

## Breakthrough

At this point, the file looked like a normal image instead of an encoded log, so I renamed it to match the file type:

```bash
mv logs.bin logs.png
```

Opening the image revealed a small hidden text string at the bottom of the image. It looked like hexadecimal data rather than readable English, which strongly suggested the final step was to decode it.

## Solution

I converted the hexadecimal string that appeared at the bottom of the image into readable text. The idea is to take the hex payload and decode it as ASCII:

```bash
python - <<'PY'
import binascii
hex_text = "<hex string visible at the bottom of the image>"
print(binascii.unhexlify(hex_text).decode())
PY
```

The decoded text revealed the flag:

```text
picoCTF{forensics_analysis_is_amazing_ac1e3584}
```

## Flag

```text
picoCTF{forensics_analysis_is_amazing_ac1e3584}
```

## Takeaways

- A large encoded blob can hide a valid file inside it.
- `base64 -d` followed by `file` is a strong first-pass approach for suspicious text files.
- Sometimes the real clue is not in the obvious content but in a hidden payload inside an image.
- Looking carefully for embedded text or encoded strings in the image itself can reveal the final flag.