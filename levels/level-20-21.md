# Level 20 → 21

## 🎯 Objective

There is a **SetUID binary** in the home directory that connects to `localhost` on a port specified as a command-line argument.

The binary then:

1. Connects to the specified port on `localhost`.
2. Reads a line of text from the connection.
3. Compares it with the password from the previous level (`bandit20`).
4. If the password is correct, it sends the password for the next level (`bandit21`) back through the connection.

## 🔎 Understanding the Challenge

The SetUID binary provided in the home directory was:

```text
suconnect
```

I needed to provide a port number to it:

```bash
./suconnect <port>
```

Since `suconnect` connects to the specified port, I needed to create a service that was listening on that port and would send the current password to it.

## 🌐 Creating a TCP Listener

I used **Netcat (`nc`)** to create a simple TCP listener:

```bash
echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -l -p 12345 &
```

### 🔍 Command Breakdown

#### `echo`

```bash
echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA"
```

`echo` outputs the password from the previous level.

#### Pipe `|`

```bash
|
```

The pipe sends the output of `echo` to the input of `nc`.

Therefore, the previous level's password is passed to Netcat.

#### `nc`

```bash
nc
```

`nc` stands for **Netcat**, a command-line networking utility that can establish TCP connections and listen for incoming connections.

#### `-l`

```bash
-l
```

The `-l` option puts Netcat into **listen mode**.

This makes Netcat wait for an incoming connection.

#### `-p 12345`

```bash
-p 12345
```

This tells Netcat to listen on port `12345`.

I chose `12345` as the port for the connection.

#### `&`

```bash
&
```

The `&` runs the command in the background.

This allowed me to use the same terminal to execute `suconnect` while the Netcat listener continued running.

## 🔗 Connecting With `suconnect`

After starting the listener, I executed:

```bash
./suconnect 12345
```

This caused `suconnect` to connect to:

```text
localhost:12345
```

The connection worked as follows:

```text
             suconnect
                 │
                 │ Connects to
                 ▼
          localhost:12345
                 │
                 ▼
          Netcat Listener
                 │
                 │ Sends password
                 ▼
      4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

## 📤 Program Output

The `suconnect` program first showed the password it received:

```text
Read: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

It then confirmed that the password matched:

```text
Password matches, sending next password
```

Finally, it returned the password for the next level:

```text
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```

The shell also showed that the background Netcat process had finished:

```text
[1]+  Done
```

This happened because the Netcat listener exited after completing the connection.

## 🔑 Password

```text
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```

## 🧠 What I Learned

- `nc` (Netcat) can be used to create a TCP listener.
- `-l` puts Netcat into listening mode.
- `-p` specifies the port.
- `&` runs a command in the background.
- The pipe operator `|` sends the output of one command to another command.
- A client needs a server/listener to connect to.
- `suconnect` acts as the client in this challenge.
- Netcat acts as the server/listener.
- The client connected to the listener using the specified port.
- The SetUID binary checked whether the received password matched the current level's password.

## 📌 Key Takeaway

The important part of this level was understanding that **`suconnect` connects to the port rather than listening on it**.

Therefore, I first created a listener using:

```bash
echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -l -p 12345 &
```

Then I connected to it using:

```bash
./suconnect 12345
```

The program confirmed:

```text
Read: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
Password matches, sending next password
```

and returned:

```text
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```

Therefore, the password for **Level 21** was:

```text
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```