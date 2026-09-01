# Level 3 → 4

## Objective
Find the password for the next level stored in a hidden file inside the `inhere` directory.

## Steps
1. Change into the `inhere` directory.
2. List all files, including hidden ones.
3. Open the hidden file containing the password.

```bash
cd inhere
ls -a
cat ./."...Hiding-From-You"
```

Linux hidden files begin with a dot, which is why `ls -a` was necessary.

## Password
```text
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

## What I Learned
- `cd` changes directories.
- Hidden files begin with `.`.
- `ls -a` shows hidden files.
- Quoting helps when filenames contain special characters.
- Checking all file types and naming patterns can reveal hidden data.
