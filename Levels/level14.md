# Bandit Level 14

## Objective

Find the password for **Bandit Level 15**.

The password for the current level is stored in:

```text
/etc/bandit_pass/bandit14
```

We need to send this password to **port 30000 on localhost**.

## Initial Investigation

After logging into the `bandit14` machine, read the password file:

```bash
cat /etc/bandit_pass/bandit14
```

This gives us the password that needs to be sent to the local service.

The objective tells us that the service is listening on:

```text
localhost:30000
```

## Commands Used

We can use `nc` (Netcat) to connect to the service:

```bash
nc localhost 30000
```

Then paste the password and press **Enter**.

If the password is correct, the service will return the password for **Bandit Level 15**.

A faster method is to send the password directly:

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

This works by:

```text
cat
 ↓
Reads the password
 ↓
Pipe |
 ↓
nc
 ↓
Sends the password to localhost:30000
 ↓
Server responds with Level 15 password
```

## Reasoning

```text
Current user: bandit14
        ↓
Read /etc/bandit_pass/bandit14
        ↓
Password obtained
        ↓
Service is listening on localhost:30000
        ↓
Use Netcat to connect
        ↓
Send the password
        ↓
Server verifies it
        ↓
Bandit Level 15 password is displayed
```

## Solution

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

## Concept Learned

### Netcat (`nc`)

Netcat is a networking utility that can create connections to TCP or UDP ports.

Basic syntax:

```bash
nc host port
```

For example:

```bash
nc localhost 30000
```

means:

> Connect to port `30000` on the local machine.

### Pipes

A pipe `|` sends the output of one command to another command.

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

The output from `cat` becomes the input for `nc`.

### Localhost

`localhost` refers to the current machine.

It normally resolves to the loopback address:

```text
127.0.0.1
```

So:

```text
localhost:30000
```

means:

> Port 30000 on the current machine.

## Mistake & Lesson

**Mistake:** Simply reading the password file and assuming that was enough.

**Lesson:** When a challenge provides a network service and a specific port, use a networking tool such as `nc` to send the required data to that service.
