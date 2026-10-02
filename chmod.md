# `chmod` — Linux File Permissions

`chmod` stands for **Change Mode**. It is a Linux command used to **change the permissions of files and directories**.

Permissions control who can:

- **Read** a file
- **Write** to a file
- **Execute** a file

Basic syntax:

```bash
chmod [permissions] [file]
```

---

## Linux Permissions

You can view permissions using:

```bash
ls -l
```

Example:

```text
-rwxr-xr-- 1 user user 1234 file.txt
```

The first part represents the permissions:

```text
-rwxr-xr--
 │ │  │  │
 │ │  │  └── Others
 │ │  └───── Group
 │ └──────── Owner
 └────────── File type
```

The three main permissions are:

| Permission | Symbol | Meaning |
|---|---|---|
| Read | `r` | Read the file |
| Write | `w` | Modify the file |
| Execute | `x` | Run the file |

---

## Using Symbolic Permissions

You can add or remove permissions using:

```bash
chmod +x file
```

This gives the file **execute permission**.

Remove execute permission:

```bash
chmod -x file
```

Give the owner write permission:

```bash
chmod u+w file
```

Remove write permission from others:

```bash
chmod o-w file
```

Here:

| Symbol | Meaning |
|---|---|
| `u` | User/Owner |
| `g` | Group |
| `o` | Others |
| `a` | Everyone |

---

## Using Numeric Permissions

`chmod` can also use numbers.

| Number | Permission |
|---|---|
| `4` | Read (`r`) |
| `2` | Write (`w`) |
| `1` | Execute (`x`) |
| `0` | No permission |

You add the values together:

```text
r = 4
w = 2
x = 1
```

For example:

```text
7 = 4 + 2 + 1 = rwx
6 = 4 + 2     = rw-
5 = 4 + 1     = r-x
4 = 4         = r--
```

---

## Example: `chmod 755`

```bash
chmod 755 script.sh
```

This gives:

```text
Owner  → rwx
Group  → r-x
Others → r-x
```

So the permission becomes:

```text
rwxr-xr-x
```

Another common example:

```bash
chmod 644 file.txt
```

This gives:

```text
Owner  → rw-
Group  → r--
Others → r--
```

Result:

```text
rw-r--r--
```

---

## Why `chmod` Matters in Bandit

In Linux challenges, you may encounter files that cannot be executed because they do not have the required permission.

For example:

```bash
./script.sh
```

might return:

```text
Permission denied
```

You can check the permissions:

```bash
ls -l script.sh
```

and, if appropriate, add execute permission:

```bash
chmod +x script.sh
```

Then:

```bash
./script.sh
```

can be executed.

> **Remember:** `chmod` changes who can **read, write, or execute** a file. Always check the existing permissions before changing them.
