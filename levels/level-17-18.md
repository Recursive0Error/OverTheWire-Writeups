# Level 17 → 18

## 🎯 Objective

There are two files in the home directory:

```text
passwords.old
passwords.new
```

The password for the next level is stored in `passwords.new` and is the only line that has changed between `passwords.old` and `passwords.new`.

Therefore, I needed to compare the two files and identify the changed line.

## 🔎 Enumeration

I first listed the files in the home directory:

```bash
ls
```

This showed the following files:

```text
passwords.old
passwords.new
```

Since both files contained mostly identical lines, manually reading and comparing every line would be inefficient.

## 💡 Solution

I used the `diff` command to compare the two files:

```bash
diff passwords.new passwords.old
```

The `diff` command compares two files and displays the differences between them.

The output was:

```text
42c42
< OQxXZjELndr90zuhOTDYBEomI0SZITXI
---
> qOg5pVOjPx9x9VccyYBADiT4xxyoUB8D
```

## 🔍 Understanding the Output

The first line:

```text
42c42
```

indicates that line `42` in one file differs from line `42` in the other file.

Since I used:

```bash
diff passwords.new passwords.old
```

the first file is:

```text
passwords.new
```

and the second file is:

```text
passwords.old
```

The symbols in the output mean:

```text
<  Line from the first file
>  Line from the second file
```

Therefore:

```text
< OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

is the line from:

```text
passwords.new
```

And:

```text
> qOg5pVOjPx9x9VccyYBADiT4xxyoUB8D
```

is the line from:

```text
passwords.old
```

Since the challenge stated that the password is stored in `passwords.new`, the password for **Level 18** was:

```text
OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

## 🔑 Password

```text
OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

## 🧪 Additional Command

I also ran:

```bash
diff passwords.new passwords.old | cat
```

This produced the same output.

This happens because the pipe sends the output of `diff` to `cat`, and `cat` simply displays that output.

Therefore, in this case:

```bash
diff passwords.new passwords.old
```

and:

```bash
diff passwords.new passwords.old | cat
```

produce the same visible result.

Using `| cat` is unnecessary here because `diff` already prints its output directly to the terminal.

## 🧠 What I Learned

- `diff` is used to compare the contents of two files.
- The order of the files in the `diff` command is important.
- `<` represents a line from the first file.
- `>` represents a line from the second file.
- `42c42` indicates that line 42 was changed.
- Piping the output of `diff` to `cat` does not change the output in this situation.
- Comparing files with command-line tools is much faster than manually checking every line.

---

## 📌 Key Takeaway

The order of files in the `diff` command matters.

I used:

```bash
diff passwords.new passwords.old
```

Because `passwords.new` was the first file, the line beginning with `<` belonged to `passwords.new`.

The password was:

```text
OQxXZjELndr90zuhOTDYBEomI0SZITXI
```