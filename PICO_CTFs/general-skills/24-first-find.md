# First Find

- **Author:** LT 'syreal' Jones
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Unzip the archive and find the file named `uber-secret.txt`.

## Problem Statement

The challenge provides a ZIP archive containing a directory tree with many files. The goal is to locate the file named `uber-secret.txt` and read its contents.

## Extracting the Archive

I extracted the archive with:

```bash
unzip files.zip
```

This created a directory named `files` containing several nested folders.

## Finding the File

I entered the extracted directory and searched recursively for the target filename:

```bash
cd files
find -name "uber-secret.txt"
```

The search found the file at:

```text
./adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
```

I read the file with:

```bash
cat ./adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
```

## Flag

```text
picoCTF{f1nd_15_f457_ab443fd1}
```

## Takeaways

- `unzip` extracts the contents of a ZIP archive.
- `find -name` searches recursively for a file by name.
- Hidden directories are included in the search results, even when they are not shown by a normal `ls` command.