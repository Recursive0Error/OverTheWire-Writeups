# Level 2 → 3

## Objective
Find the password for the next level.

## Steps
1. Inspect the directory contents.
2. Identify the file whose name contains spaces.
3. Read it using quotes so the shell treats it as one filename.

```bash
ls
cat "--file with spaces--"
```

The shell normally splits arguments on spaces, so quoting the filename was necessary.

## Password
```text
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

## What I Learned
- Filenames with spaces must be quoted.
- The shell parses arguments before passing them to commands.
- Quoting prevents spaces from being treated as argument separators.
- Special characters in filenames can break naive commands if not handled correctly.
