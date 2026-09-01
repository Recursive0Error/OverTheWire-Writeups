# Level 4 → 5

## Objective
Find the password for the next level. The password is stored in one of the files inside the `inhere` directory.

## Steps
1. Change into the `inhere` directory.
2. List the files.
3. Use `file` to determine which file contains readable text.
4. Read the correct file.

```bash
cd inhere
ls
file -- *
cat ./'-file07'
```

The files all started with `-`, so `--` was needed to treat them as filenames rather than options. One of them contained ASCII text, which was the correct password file.

## Password
```text
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

## What I Learned
- `file` identifies the type of data stored in a file.
- `--` prevents command options from being parsed as file names.
- Some files may contain binary data instead of plain text.
- Filtering by file type is a fast way to narrow a search.
