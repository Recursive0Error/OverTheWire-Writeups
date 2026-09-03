# Level 33 — Final Level

## 🎯 Objective

The previous level provided the password for `bandit33`. After logging in, the task was to inspect the final account and determine whether another challenge remained.

## 🔐 Logging In

I connected to the final Bandit account using port `2220`:

```bash
ssh bandit33@bandit.labs.overthewire.org -p 2220
```

## 📂 Inspecting the Home Directory

I listed the files in the home directory:

```bash
ls
```

The only file present was:

```text
README.txt
```

I read it with:

```bash
cat README.txt
```

The file congratulated me for completing the last level and explained that there were currently no more levels in the game. It also mentioned that OverTheWire may add new levels in the future and suggested trying the other available wargames.

## ✅ Completion

There is no password for a Level 34 because Level 33 is currently the final Bandit level. The game was successfully completed.

## 🧠 What I Learned

* The final level can be confirmed by inspecting the account's home directory.
* A `README.txt` file can provide completion information even when no challenge remains.
* Not every login leads to another password or level.

## 📌 Key Takeaway

The final steps were:

```text
Log in as bandit33
        ↓
List the home directory
        ↓
Find README.txt
        ↓
Read the completion message
        ↓
Confirm that the Bandit game is complete
```

The main commands were:

```bash
ssh bandit33@bandit.labs.overthewire.org -p 2220
ls
cat README.txt
```

This completed the OverTheWire Bandit wargame through **Level 33**.
