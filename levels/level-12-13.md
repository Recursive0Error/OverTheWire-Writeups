# Level 12 → 13

## Objective
The password for the next level is stored in a hexdump file that has been repeatedly compressed.

## Steps
1. Create a temporary working directory.
2. Reverse the hexdump into a binary file.
3. Identify the file type.
4. Rename and decompress the file repeatedly until the final password is visible.

```bash
mktemp -d
cp data.txt /tmp/<temporary-directory>/
cd /tmp/<temporary-directory>
xxd -r data.txt data.bin
file data.bin
mv data.bin data.gz
gzip -d data.gz
file data
```

This challenge required repeated decompression and file-type detection until reaching the final readable text.

## Password
```text
qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```

## What I Learned
- `xxd -r` reverses a hexdump back into a binary file.
- `file` reveals the format of the data.
- Multiple layers of compression can be handled by repeating the same workflow.
- Temporary directories help keep the working copy isolated from the original file.
- Systematic decompression beats guessing the file format.
