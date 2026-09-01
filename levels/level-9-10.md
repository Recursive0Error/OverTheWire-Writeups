# Level 9 → 10

## Objective
The password for the next level is stored in the file `data.txt` in a human-readable string that is preceded by several `=` characters.

## Steps
1. View the file to confirm it is not plain text.
2. Extract readable strings.
3. Filter for the lines containing `===`.

```bash
cat data.txt
strings data.txt | grep "==="
```

`strings` extracts readable text from binary or noisy files, and the challenge hint narrowed the result to the correct line.

## Password
```text
B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

## What I Learned
- `cat` is not always useful on binary-like files.
- `strings` extracts printable sequences from data.
- `grep` can filter output for a specific pattern.
- Binary data often contains embedded readable fragments.
- Combining commands with pipes is a common and effective workflow.
