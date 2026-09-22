# Bandit Level 13

## Objective

Find the password for **Bandit Level 14**.

This level is different from the previous ones.

There is no password file to read directly.

Instead, the password for Level 14 can be obtained by logging into the `bandit14` account using an **SSH private key**.

The private key is stored in the current directory:

```text
sshkey.private
```

## Initial Investigation

After logging into the `bandit13` machine, list the files:

```bash
ls
```

Output:

```text
sshkey.private
```

This is an SSH private key.

We can use this key to authenticate as the `bandit14` user.

## Commands Used

First, check the permissions of the private key:

```bash
ls -l sshkey.private
```

SSH private keys should not be readable by other users.

Set the permissions so that only the owner can read the file:

```bash
chmod 600 sshkey.private
```

Now use the private key to connect to `bandit14`:

```bash
ssh -i sshkey.private bandit14@localhost
```

Let's break this command down:

```text
ssh
```

Start an SSH connection.

```text
-i sshkey.private
```

Use `sshkey.private` as the identity/private key.

```text
bandit14@localhost
```

Connect to the `bandit14` user on the same machine.

After connecting, verify the current user:

```bash
whoami
```

Output:

```text
bandit14
```

The password for the next level is stored in:

```text
/etc/bandit_pass/bandit14
```

Read it:

```bash
cat /etc/bandit_pass/bandit14
```

The password is displayed.

## Reasoning

```text
Current user: bandit13
        ↓
Find sshkey.private
        ↓
Private SSH key is available
        ↓
Set secure permissions
        ↓
chmod 600 sshkey.private
        ↓
Use the key to SSH as bandit14
        ↓
ssh -i sshkey.private bandit14@localhost
        ↓
Logged in as bandit14
        ↓
cat /etc/bandit_pass/bandit14
        ↓
Password is displayed
```

## Solution

```bash
chmod 600 sshkey.private
ssh -i sshkey.private bandit14@localhost
```

Then:

```bash
cat /etc/bandit_pass/bandit14
```

## Concept Learned

### SSH Private Keys

SSH can authenticate users using a **private key** instead of a password.

A private key is usually kept secret and is paired with a public key.

The basic SSH command is:

```bash
ssh user@host
```

When using a specific private key:

```bash
ssh -i private_key user@host
```

In this level:

```bash
ssh -i sshkey.private bandit14@localhost
```

means:

> Connect to `localhost` as `bandit14` using `sshkey.private` for authentication.

### File Permissions

The command:

```bash
chmod 600 sshkey.private
```

sets the permissions to:

```text
6 → owner: read + write
0 → group: no permissions
0 → others: no permissions
```

So only the owner can read or modify the private key.

## Mistake & Lesson

**Mistake:** Treating the SSH private key like a normal text file containing the password.

**Lesson:** SSH private keys are authentication credentials. They can be used with `ssh -i` to authenticate without directly providing a password.
