# PW Crack 4

- **Event:** Beginner picoMini 2022
- **Author:** LT 'syreal' Jones
- **Category:** General Skills
- **Difficulty:** Medium
- **Challenge:** Crack the password used by the supplied password checker to obtain the flag.

## Problem Statement

The challenge provides a Python password checker, an encrypted flag, and a hash file. There are 100 possible passwords, but only one produces the correct hash.

## Finding the Password

I opened `level4.py` in a text editor and inspected the password-checking function. It hashes the supplied password and compares the result with `correct_pw_hash`:

```python
def level_4_pw_check(password):
    user_pw = password
    user_pw_hash = hash_pw(user_pw)

    if user_pw_hash == correct_pw_hash:
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
```

The script also provided a list of 100 possible passwords. Instead of entering them manually, I added a loop that tested every candidate:

```python
for i in range(0, 100):
    level_4_pw_check(pos_pw_list[i])
```

## Solution

After adding the loop, I ran the modified checker:

```bash
python3 level4.py
```

The script tested all 100 candidates and printed the flag when it reached the password with the matching hash.

## Flag

```text
picoCTF{fl45h_5pr1ng1ng_cf341ff1}
```

## Takeaways

- A hash comparison can verify a password without revealing the password directly.
- A finite candidate list can be tested automatically with a loop.
- Automating repetitive attempts is more reliable than entering many candidates manually.