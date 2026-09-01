# Level 8 → 9

## Objective
The password for the next level is stored in the file `data.txt` and appears exactly once.

## Steps
1. Inspect the directory.
2. Sort the lines.
3. Use `uniq -u` to find the unique entry.

```bash
ls
sort data.txt | uniq -u
```

Sorting makes identical lines adjacent, which allows `uniq -u` to detect lines that appear only once.

## Password
```text
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

## What I Learned
- `sort` orders text lines alphabetically.
- `uniq` can report duplicate or unique lines.
- `uniq -u` shows only entries that occur exactly once.
- Chaining commands with pipes is a core Linux skill.
- Sorting before deduplication is important for correct results.
