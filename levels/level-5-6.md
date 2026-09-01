# Level 5 → 6

## Objective
The password for the next level is stored in a file under the `inhere` directory. The file is human-readable, exactly 1033 bytes in size, and not executable.

## Steps
1. Change into the `inhere` directory.
2. Use `find` to locate files with the expected size and type.
3. Read the matching file.

```bash
cd inhere
find . -type f -size 1033c
cat ./maybehere07/.file2
```

The challenge gave specific file properties, so a targeted `find` search was much faster than checking each directory manually.

## Password
```text
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```

## What I Learned
- `find` can search recursively.
- `-type f` restricts results to regular files.
- `-size 1033c` matches files that are exactly 1033 bytes.
- Using challenge clues is an efficient way to reduce search space.
- Hidden files and nested directories are common in Bandit challenges.
