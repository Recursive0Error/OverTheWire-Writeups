# Mod 26

- **Event:** picoCTF 2021
- **Author:** Pandu
- **Category:** Cryptography
- **Difficulty:** Easy
- **Challenge:** Cryptography can be easy, do you know what ROT13 is?
- **Source file:** [values.txt](https://challenge-files.picoctf.net/c_wily_courier/b5432076063b14f465816ae09a61a2825fa2887265f19b1a28e2a1fe5877d01b/values.txt)

## Problem Statement

The challenge provides a file named `values.txt` containing a string encoded with ROT13:

```text
cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_45559noq}
```

The goal is to decode the string and recover the flag.

## Initial Observation

The challenge explicitly mentions ROT13. ROT13 replaces each letter with the letter 13 positions away in the alphabet. Applying ROT13 a second time returns the original text.

## Solution

I used `cat` to print the contents of `values.txt`, then used the pipe operator to send that output to `tr`:

```bash
cat values.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

The `tr` command translates uppercase and lowercase letters from the first character set into the corresponding letters in the second character set. The two ranges implement ROT13:

- `A-M` becomes `N-Z`
- `N-Z` becomes `A-M`
- `a-m` becomes `n-z`
- `n-z` becomes `a-m`

The command returned the decoded flag.

## Flag

```text
picoCTF{next_time_I'll_try_2_rounds_of_rot13_45559abd}
```

## Takeaways

- ROT13 is a substitution cipher that shifts each letter by 13 positions.
- ROT13 is reversible because applying it twice restores the original text.
- The pipe operator passes one command's output as another command's input.
- `tr` can perform character-by-character translations directly in the terminal.