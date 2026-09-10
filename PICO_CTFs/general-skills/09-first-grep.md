# First Grep

- **Event:** picoCTF 2019
- **Author:** Alex Fulton / Danny Tunitis
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Find the flag in the provided file without manually searching through the entire output.
- **File:** [file](https://challenge-files.picoctf.net/c_fickle_tempest/92807684f3e52665caaf90d69e1e661f990b8731b2f8005e18631be23ff991bb/file)

## Problem Statement

The challenge provides a file containing a large amount of text. Manually looking through it would be tedious, so the goal is to use a command-line search tool to locate the flag.

## Solution

I used `strings` to extract readable text and piped the output to `grep`. The `-o` option prints only the matching text, while the extended regular expression matches a complete `picoCTF` flag:

```bash
strings file | grep -o -E "picoCTF\{[^}]+\}"
```

The command returned the flag directly:

```text
picoCTF{grep_is_good_to_find_things_eb80073D}
```

## Flag

```text
picoCTF{grep_is_good_to_find_things_eb80073D}
```

## Takeaways

- `strings` extracts readable text from a file.
- `grep` searches command output for a pattern.
- `grep -o` prints only the matching portion instead of the entire line.
- The pattern `picoCTF\{[^}]+\}` matches a flag beginning with `picoCTF{` and ending at the next `}`.