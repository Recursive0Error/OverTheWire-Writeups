# Level 13 → 14

## Objective
The password for the next level is stored in `/etc/bandit_pass/bandit14` and can only be read by the `bandit14` user. This level provides a private SSH key to authenticate as `bandit14`.

## Steps
1. Inspect the home directory.
2. Fix the file permissions on the private key.
3. Connect to the next user via SSH.
4. Read the password file.

```bash
ls
chmod 600 temp_key
ssh -4 -i temp_key bandit14@bandit.labs.overthewire.org -p 2220
cat /etc/bandit_pass/bandit14
```

The SSH private key initially had overly broad permissions, so the server rejected it until the file was restricted to the owner only.

## Password
```text
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

## What I Learned
- SSH can authenticate using a private key.
- `chmod 600` restricts file access to the owner.
- SSH refuses keys with permissions that are too open.
- Private keys must be protected carefully.
- Error messages often explain exactly what needs to be fixed.
