# Bandit Level 6

## Objective

Find the password for **Bandit Level 7**.

The password is stored **somewhere on the server** and has these properties:

* Owned by user `bandit7`
* Owned by group `bandit6`
* Exactly **33 bytes** in size

## Initial Investigation

After logging into the `bandit6` machine, we are in the home directory:

```bash
pwd
```

Output:

```text
/home/bandit6
```

Unlike the previous level, the password is **not necessarily inside the current directory**.

The objective says it is somewhere on the server, so we need to search from the root directory `/`.

## Commands Used

Use the `find` command:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

Let's break this command down:

```text
find /
```

Search from the root directory.

```text
-user bandit7
```

Find files owned by the user `bandit7`.

```text
-group bandit6
```

Find files owned by the group `bandit6`.

```text
-size 33c
```

Find files that are exactly **33 bytes**.

The `c` means bytes.

```text
2>/dev/null
```

Hide permission-denied error messages.
you can more about it [here](https://github.com/Xhaolean/Overthewire-Bandit-Documentation/blob/main/dev_null.md)

The search should return the path of the required file.

For example:

```text
/var/lib/dpkg/info/... 
```

The important part is the file path returned by `find`.

Now read that file:

```bash
cat /path/to/file
```

The password is displayed.

## Reasoning

```text
Password is somewhere on the server
       ↓
Start searching from /
       ↓
Need a file owned by bandit7
       ↓
Group must be bandit6
       ↓
File size must be 33 bytes
       ↓
Use find with all conditions
       ↓
find / -user bandit7 -group bandit6 -size 33c
       ↓
Hide permission errors with 2>/dev/null
       ↓
Required file is found
       ↓
cat filename
       ↓
Password is displayed
```

## Solution

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

Then read the file returned by the command:

```bash
cat /path/to/file
```

## Concept Learned

### Searching the Entire Filesystem

The `/` directory is the root of the Linux filesystem.

Using:

```bash
find /
```

means:

> Search from the root directory and therefore potentially search the entire filesystem.

### File Ownership

Linux files have an owner and a group.

For example:

```text
owner: bandit7
group: bandit6
```

The `find` command can search based on these properties:

```bash
find / -user bandit7
```

Find files owned by `bandit7`.

```bash
find / -group bandit6
```

Find files belonging to group `bandit6`.

These conditions can be combined:

```bash
find / -user bandit7 -group bandit6
```

### Redirecting Errors

When searching the entire filesystem, you may encounter many permission errors.

```bash
2>/dev/null
```

means:

```text
2    → standard error (stderr)
>    → redirect
/dev/null → discard the output
```

So:

```bash
find / ... 2>/dev/null
```

keeps the useful results while hiding permission-denied messages.
More Detailed information [here](https://github.com/Xhaolean/Overthewire-Bandit-Documentation/blob/main/dev_null.md) 

## Mistake & Lesson

**Mistake:** Searching only inside `/home/bandit6`.

**Lesson:** When the objective says a file is located somewhere on the server, search from `/` and use the file's known properties to narrow down the results.
