# Level 7 → 8

## Objective
The password for the next level is stored in the file `data.txt` next to the word `millionth`.

## Steps
1. Check the current directory.
2. Search for the keyword `millionth` in the file.
3. Read the matching line.

```bash
ls
grep "millionth" data.txt
```

This challenge was a direct text search problem: once the keyword was known, the password was on the matching line.

## Password
```text
VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

## What I Learned
- `grep` searches for specific text patterns inside a file.
- A known keyword can make a large file easy to analyze.
- Searching for relevant text is often faster than reading the whole file.
- Pipes and filters are useful when processing text data.
