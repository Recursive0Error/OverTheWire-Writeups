# PW Crack 5

- **Event:** Beginner picoMini 2022
- **Author:** LT 'syreal' Jones
- **Category:** General Skills
- **Difficulty:** Medium
- **Challenge:** Crack the password using the supplied password checker, hash, encrypted flag, and password dictionary.

## Problem Statement

The challenge provides a Python password checker and a dictionary containing all possible passwords. The goal is to find the dictionary entry whose hash matches `correct_pw_hash`, then use that password to decrypt the flag.

## Finding the Password

I modified `level5.py` to read each candidate from `dictionary.txt`, remove its newline, hash it, and compare the result with the correct hash:

```python
with open('dictionary.txt', 'r') as f:
    for line in f:
        pw = line.strip()
        if hash_pw(pw) == correct_pw_hash:
            print(f"Found password in dictionary: {pw}")
            break
```

Running the script identified the matching password:

```text
Found password in dictionary: 9581
```

## Solution

I ran the password checker:

```bash
python3 level5.py
```

After the dictionary scan found `9581`, I entered it when prompted:

```text
Please enter correct password for flag: 9581
Welcome back... your flag, user:
picoCTF{h45h_sl1ng1ng_36e992a6}
```

## Flag

```text
picoCTF{h45h_sl1ng1ng_36e992a6}
```

## Takeaways

- A dictionary attack tests a list of likely passwords against a verification condition.
- `strip()` removes the newline from each password read from the file.
- Comparing hashes allows the correct password to be identified without decrypting every candidate.
- Automating the dictionary scan is more practical than testing each entry manually.