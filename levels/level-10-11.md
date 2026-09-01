# Level 10 → 11

## Objective
The password for the next level is stored in the file `data.txt`, which contains Base64 encoded data.

## Steps
1. Check the directory contents.
2. Decode the Base64 text.
3. Read the result to get the password.

```bash
ls
base64 -d data.txt
```

The file contained Base64-encoded data rather than plaintext, so decoding it revealed the password directly.

## Password
```text
pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

## What I Learned
- Base64 is an encoding format, not encryption.
- `base64 -d` decodes Base64 content.
- Encoded files can still be identified by their content and challenge context.
- `-d` is the standard decode flag for the `base64` utility.
