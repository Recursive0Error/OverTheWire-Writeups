# Big Zip

- **Event:** picoCTF 2022
- **Author:** LT 'syreal' Jones
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Unzip the supplied archive and find the flag.

## Problem Statement

The challenge provides an archive named `big-zip-files.zip`. The goal is to extract its contents and locate the flag among the many nested folders and files.

## Extracting the Archive

I extracted the archive with:

```bash
unzip big-zip-files.zip
```

The archive created a directory tree containing many nested folders and text files.

## Finding the Flag

Instead of opening each file manually, I searched recursively for the `pico` prefix:

```bash
grep -r "pico" .
```

The search found the flag in a deeply nested text file:

```text
./folder_pmbymkjcya/folder_cawigcwvgv/folder_ltdayfmktr/folder_fnpfclfyee/whzxrpivpqld.txt:information on the record will last a billion years. Genes and brains and books encode picoCTF{gr3p_15_m4g1c_ef8790dc}
```

## Flag

```text
picoCTF{gr3p_15_m4g1c_ef8790dc}
```

## Takeaways

- `unzip` extracts files from a ZIP archive while preserving its directory structure.
- Recursive search is useful for locating text across many nested files.
- `grep -r` can quickly find a known flag prefix such as `pico`.
