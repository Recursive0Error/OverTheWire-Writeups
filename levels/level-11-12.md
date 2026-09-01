# Level 11 → 12

## Objective
The password for the next level is stored in `data.txt`, where all letters have been rotated by 13 positions using ROT13.

## Steps
1. Read the file.
2. Apply a ROT13 transformation with `tr`.
3. Retrieve the password from the decoded output.

```bash
cat data.txt
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

ROT13 is symmetric, so applying the same transformation again decodes the text back to readable content.

## Password
```text
GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

## What I Learned
- ROT13 shifts letters by 13 positions.
- `tr` can translate characters according to a mapping table.
- `A-Za-z` and `N-ZA-Mn-za-m` is the standard ROT13 pattern.
- Pipes let one command pass its output to another for clean transformations.
