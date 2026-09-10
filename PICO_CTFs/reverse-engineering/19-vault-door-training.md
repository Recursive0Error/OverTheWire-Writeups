# vault-door-training

- **Event:** picoCTF 2019
- **Author:** Mark E. Haase
- **Category:** Reverse Engineering
- **Difficulty:** Easy
- **Challenge:** Read the training vault's Java source code and determine the password.

## Problem Statement

The challenge provides the source code for a training vault, `VaultDoorTraining.java`. The goal is to inspect the password-checking logic and enter the correct password to open the vault.

## Inspecting the Source Code

I displayed the Java source file:

```bash
cat VaultDoorTraining.java
```

The `main` method removes the outer `picoCTF{` prefix and the final `}` before passing the remaining text to `checkPassword`:

```java
String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
if (vaultDoor.checkPassword(input)) {
```

The password is directly visible in the `checkPassword` method:

```java
public boolean checkPassword(String password) {
    return password.equals("w4rm1ng_Up_w1tH_jAv4_000uMfhzBuS");
}
```

## Forming the Flag

The hard-coded string is the content inside the flag braces. I wrapped it with the required `picoCTF{}` format:

```text
picoCTF{w4rm1ng_Up_w1tH_jAv4_000uMfhzBuS}
```

## Flag

```text
picoCTF{w4rm1ng_Up_w1tH_jAv4_000uMfhzBuS}
```

## Takeaways

- Source code can reveal secrets when passwords are hard-coded directly in a program.
- Understanding how input is transformed helps identify the expected flag format.
- Reverse engineering often begins with tracing comparisons and validation logic.
