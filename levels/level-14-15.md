# Level 14 → 15

## 🎯 Objective

The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

## 🔎 Understanding the Challenge

The challenge requires me to send the current level's password to a service running locally on port `30000`.

The term `localhost` refers to the current machine itself. It is commonly associated with the IP address:

```text
127.0.0.1
```

The number `30000` is the network port where the service is listening.

Therefore, I needed to establish a connection to:

```text
localhost:30000
```

and send the current password.

## 💡 Solution

I used the `telnet` command:

```bash
telnet localhost 30000
```

The command connected to the service running on port `30000`:

```text
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
```

I then entered the password from the previous level:

```text
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

The server responded:

```text
Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

The returned value was the password for **Level 15**.

The connection was then closed by the server:

```text
Connection closed by foreign host.
```

## 🔑 Password

```text
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

## 🧠 What I Learned

- `localhost` refers to the current machine.
- `127.0.0.1` is the loopback IP address commonly used for localhost.
- A **port** identifies a specific network service running on a machine.
- `30000` was the port where the required service was listening.
- `telnet` is a command-line protocol/tool that can establish a basic TCP connection to a specified host and port.
- Telnet does not provide encryption, so it should not be used for transmitting sensitive information over untrusted networks.
- Network services can accept input and return responses through TCP connections.
- The server's response confirmed whether the submitted password was correct.

---

## 📌 Key Takeaway

This level introduced basic interaction with a network service running on the local machine.

I connected to port `30000` using:

```bash
telnet localhost 30000
```

I then submitted the current password:

```text
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

The server responded with:

```text
Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

The returned string was the password for the next level.