# Level 1 → 2

## Objective
Find the password for the next level.

## Steps
1. Inspect the current directory.
2. Notice that the password file is named `-`.
3. Access it explicitly from the current directory.

```bash
ls
cat ./-
```

A normal `cat -` would be interpreted as standard input instead of a file, so the path had to be written explicitly.

## Password
```text
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

## What I Learned
- `-` can have special meaning in Linux commands.
- `./` explicitly targets a file in the current directory.
- Filenames can be intentionally tricky and require careful handling.
- Some command-line tools treat certain characters specially.
