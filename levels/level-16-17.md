# Level 16 → 17

## 🎯 Objective

The credentials for the next level can be retrieved by submitting the password of the current level to a service running on **localhost**.

The service is listening on a port in the range:

```text
31000 - 32000
```

The challenge required me to:

1. Find which ports have a server listening on them.
2. Identify which of those services use SSL/TLS.
3. Submit the current password to the SSL/TLS services.
4. Find the server that provides the credentials for the next level.

Some of the other servers simply echo back whatever data is sent to them.

## 🔎 Scanning for Open Ports

I used Nmap to scan the specified range of ports:

```bash
nmap -sV -p 31000-32000 localhost
```

### Command Breakdown

```bash
nmap
```

Nmap is a network scanning tool that can be used to discover hosts, open ports, and services.

```bash
-sV
```

This enables **service version detection**. Nmap attempts to determine what service is running on each open port.

```bash
-p 31000-32000
```

This tells Nmap to scan all ports from `31000` to `32000`.

```bash
localhost
```

This scans the current machine.

## 📊 Scan Results

The scan returned the following open ports:

```text
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```

Most of the services were identified as regular `echo` services.

However, two ports were identified as using SSL/TLS:

```text
31518/tcp
31790/tcp
```

Therefore, these were the two ports I needed to investigate further.

---

## 🔐 Testing Port 31518

I first submitted the current password to port `31518` using `openssl s_client`:

```bash
echo "kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V" | openssl s_client -connect localhost:31518 -ign_eof
```

The command works as follows:

```text
echo
  ↓
Current password
  ↓
Pipe operator |
  ↓
openssl s_client
  ↓
Encrypted TLS connection
  ↓
localhost:31518
```

However, this service simply returned the same string that I sent.

This indicated that the service was an **SSL/TLS echo service** and was not the service that provided the next credentials.

---

## 🔐 Testing Port 31790

I then tested the second SSL/TLS port:

```bash
echo "kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V" | openssl s_client -connect localhost:31790 -ign_eof
```

This time, the service responded with an **OpenSSH private key** instead of simply echoing the password.

The private key is used as the credential for the next level.

---

## 🔑 Next-Level Credential

The service running on:

```text
localhost:31790
```

returned an OpenSSH private key.

Unlike previous levels, the next credential was not a normal password. Instead, I received a private SSH key that can be used to authenticate as the next Bandit user.

The private key can be saved to a file and used with SSH in the following way:

```bash
ssh -i <private_key_file> bandit17@bandit.labs.overthewire.org -p 2220
```

The private key file must have restrictive permissions before SSH will accept it.

For example:

```bash
chmod 600 <private_key_file>
```

Then it can be used for authentication.

## 🧠 What I Learned

- `nmap` can be used to scan for open ports.
- `-p` specifies the port or port range to scan.
- `-sV` enables service and version detection.
- Multiple services can be running on different ports on the same machine.
- `echo` services simply send back the data they receive.
- `ssl/echo` indicates an echo service protected by SSL/TLS.
- `openssl s_client` can be used to test services that require SSL/TLS.
- Not every SSL/TLS service provides the desired result, so individual services may need to be tested.
- SSH private keys can be used instead of passwords for authentication.

---

## 📌 Key Takeaway

The main strategy for this level was to first narrow down the possible services instead of manually testing all 1001 ports.

I scanned the port range using:

```bash
nmap -sV -p 31000-32000 localhost
```

This revealed two SSL/TLS services:

```text
31518
31790
```

The first SSL/TLS service on port `31518` simply echoed my password back.

I then tested port `31790`:

```bash
echo "kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V" | openssl s_client -connect localhost:31790 -ign_eof
```

This service returned an **OpenSSH private key**, which could then be used as the credential to access **Level 17**.