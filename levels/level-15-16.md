# Level 15 → 16

## 🎯 Objective

The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost using SSL/TLS encryption**.

Unlike the previous level, a normal unencrypted connection using Telnet is not sufficient because the service requires an encrypted TLS connection.

## 🔎 Understanding the Challenge

The previous level required connecting to a service using:

```text
localhost:30000
```

However, this level requires connecting to:

```text
localhost:30001
```

using **SSL/TLS encryption**.

TLS encrypts the communication between the client and the server.

To create this encrypted connection, I used the OpenSSL command-line tool.

## 💡 Solution

I used the following command:

```bash
echo "pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7" | openssl s_client -connect localhost:30001 -ign_eof
```

This command performs several operations.

### 1. `echo`

```bash
echo "pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7"
```

The `echo` command prints the password from the current level.

The password is:

```text
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

### 2. Pipe Operator `|`

```bash
|
```

The pipe operator sends the output of the command on the left as input to the command on the right.

In this case, it sends the password produced by `echo` directly to `openssl s_client`.

The flow is:

```text
echo
  ↓
Current Level Password
  ↓
Pipe |
  ↓
openssl s_client
  ↓
Encrypted TLS Connection
  ↓
Server
```

### 3. `openssl s_client`

```bash
openssl s_client
```

`openssl` is a command-line tool for working with cryptographic protocols and certificates.

The `s_client` command acts as an SSL/TLS client and allows me to establish an encrypted connection to a server.

### 4. `-connect localhost:30001`

```bash
-connect localhost:30001
```

This specifies the server and port to connect to.

- `localhost` refers to the current machine.
- `30001` is the port where the TLS-enabled service is running.

### 5. `-ign_eof`

```bash
-ign_eof
```

Normally, when `echo` finishes sending the password, the pipe reaches **EOF (End Of File)**.

The `-ign_eof` option tells `openssl s_client` to ignore the immediate EOF from standard input and keep the connection open long enough to receive the server's response.

This is useful because the server may send its response after the password has been transmitted.

## 🔐 TLS Connection

The command successfully established an encrypted TLS connection:

```text
Connecting to 127.0.0.1
CONNECTED
```

OpenSSL then displayed information about the server's TLS certificate and connection.

One message shown was:

```text
verify error:num=18:self-signed certificate
```

This occurred because the server uses a **self-signed certificate**.

A self-signed certificate is not signed by a publicly trusted Certificate Authority, so OpenSSL cannot verify it in the normal way.

For this Bandit challenge, the important part was successfully establishing the encrypted connection to the local service.

The connection used:

```text
TLSv1.3
```

## 🔑 Submitting the Password

The current level's password was automatically sent through the encrypted TLS connection:

```text
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

The server responded:

```text
Correct!
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

Therefore, the password for **Level 16** was:

```text
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

## 🔑 Password

```text
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

## 🧠 What I Learned

- SSL/TLS is used to encrypt communication between a client and a server.
- `openssl s_client` can be used to establish an SSL/TLS connection from the command line.
- `-connect` specifies the host and port of the server.
- The pipe operator `|` sends the output of one command as input to another command.
- `echo` can be used to automatically provide input to another command.
- `-ign_eof` prevents `openssl s_client` from immediately closing the connection when standard input reaches EOF.
- A self-signed certificate is not signed by a publicly trusted Certificate Authority.
- TLS certificates are used as part of establishing secure connections.

---

## 📌 Key Takeaway

This level was similar to the previous networking challenge, but instead of using an unencrypted Telnet connection, the service required SSL/TLS encryption.

The command I used was:

```bash
echo "pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7" | openssl s_client -connect localhost:30001 -ign_eof
```

The password was sent through an encrypted TLS connection, and the server responded with:

```text
Correct!
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

This introduced me to using OpenSSL and interacting with services that require encrypted network communication.