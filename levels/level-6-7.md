# Level 6 → 7

## Objective
The password for the next level is stored somewhere on the server and matches the following conditions:
- owned by user `bandit7`
- owned by group `bandit6`
- exactly 33 bytes in size

## Steps
1. Search from the current directory and then expand the search to the whole filesystem.
2. Suppress permission errors.
3. Read the matching file.

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

Because the file could be anywhere, the search had to start from `/` instead of the current directory. Redirecting `stderr` to `/dev/null` made the output readable.

## Password
```text
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

## What I Learned
- `find` can apply multiple constraints simultaneously.
- `/` represents the root of the filesystem.
- `-user` and `-group` can narrow the search by ownership.
- `2>/dev/null` suppresses permission errors from noisy directories.
- Specific filtering criteria are often the quickest path to the answer.
