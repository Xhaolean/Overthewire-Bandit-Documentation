# `/dev/null` — Linux Black Hole

`/dev/null` is a **special file in Linux and Unix-like systems** that discards anything written to it.

It is commonly called a **"black hole"** because data sent to it disappears and is not stored.

```text
Command
   │
   ▼
/dev/null
   │
   ▼
Discarded
```

## Why Use `/dev/null`?

Commands often produce output that we don't need to see.

For example, instead of displaying unnecessary output:

```bash
command
```

we can discard it:

```bash
command > /dev/null
```

This is useful for keeping the terminal clean, especially when running scripts or searching through the filesystem.

---

## Standard Output and Errors

Linux uses **file descriptors** for input and output:

| File Descriptor | Name     | Purpose        |
| --------------- | -------- | -------------- |
| `0`             | `stdin`  | Input          |
| `1`             | `stdout` | Normal output  |
| `2`             | `stderr` | Error messages |

### Discard Normal Output

```bash
command > /dev/null
```

`>` redirects `stdout` (FD `1`) to `/dev/null`.

### Discard Errors

```bash
command 2> /dev/null
```

`2>` redirects `stderr` (FD `2`) to `/dev/null`.

### Discard Everything

```bash
command > /dev/null 2>&1
```

This redirects both `stdout` and `stderr` to `/dev/null`.

---

## Example

When searching the entire filesystem:

```bash
find / -name "password.txt" 2> /dev/null
```

`find` may generate many **Permission denied** errors.

The useful results are still displayed, while the errors are sent to `/dev/null` and discarded.

```text
Useful results  → Terminal
Errors          → /dev/null → Discarded
```

## Important

`/dev/null` **does not stop a command from running** and does not make it successful.

It only discards the output that is redirected to it.

> **Remember:** `/dev/null` = *send it here if you don't want to see or store it.*
