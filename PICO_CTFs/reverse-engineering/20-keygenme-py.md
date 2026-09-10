# keygenme-py

- **Event:** picoCTF 2021
- **Author:** syreal
- **Category:** Reverse Engineering
- **Difficulty:** Medium
- **Status:** Unsolved
- **Challenge:** Analyze the supplied Python key generator and obtain the license key for the full version.

## Problem Statement

The challenge provides the source code for a trial version of a key-generation program. The goal is to reverse engineer the license-key validation logic and produce a valid key.

Source file: [keygenme-trial.py](https://challenge-files.picoctf.net/c_wily_courier/2dfa4596b25ece8987532bd9d7221bd5b098b4485b285ad93f84d1c2fd1e5604/keygenme-trial.py)

## What I Tried

I reviewed the challenge source code, but I was not able to determine the license key or complete the challenge.

## Current Status

This challenge is intentionally recorded as unsolved. I plan to return to it later and analyze the key-validation logic to recover the correct license key and flag.

## Flag

Not solved yet.

## Next Step

When revisiting this challenge, inspect how the program validates each part of the license key and work backward from those constraints to construct a valid key.
