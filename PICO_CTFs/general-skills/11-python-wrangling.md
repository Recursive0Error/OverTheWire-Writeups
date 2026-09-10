# Python Wrangling

- **Event:** picoCTF 2021
- **Author:** syreal
- **Category:** General Skills
- **Difficulty:** Medium
- **Challenge:** Run `ende.py` with `password.txt` to decrypt `flag.txt.en` and recover the flag.

## Problem Statement

The challenge provides a Python script, a password file, and an encrypted flag file. The script must be run with the correct decrypt option and supplied with the password from `password.txt`.

## Understanding the Script

I first inspected the provided files with `cat`, then checked the script's usage information:

```bash
python3 ende.py -h
```

The help output showed that the decrypt option is `-d`:

```text
Usage: ende.py (-e/-d) [file]
Examples:
  To decrypt a file named 'pole.txt', do: '$ python ende.py -d pole.txt'
```

I then tried to decrypt the encrypted flag directly:

```bash
python3 ende.py -d flag.txt.en
```

The script prompted for a password. Instead of entering it interactively, I supplied the contents of `password.txt` through standard input:

```bash
cat password.txt | python3 ende.py -d flag.txt.en
```

The script decrypted the file and printed the flag.

## Flag

```text
picoCTF{4p0110_1n_7h3_h0us3_9c5f9bcf}
```

## Takeaways

- Use `-h` to inspect a script's command-line options.
- The `-d` option decrypts a file with `ende.py`.
- A file's contents can be supplied to a program through standard input using a pipe.
- `cat password.txt | python3 ende.py -d flag.txt.en` avoids entering the password manually.