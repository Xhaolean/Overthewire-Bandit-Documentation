# Bandit Level 7

## Objective

Find the password for **Bandit Level 8**.

The password is stored in the file:

```text
data.txt
```

It is located in the home directory.

The password is next to the word:

```text
millionth
```

## Initial Investigation

After logging into the `bandit7` machine, list the files:

```bash
ls
```

Output:

```text
data.txt
```

The file contains a large amount of data.

We could use:

```bash
cat data.txt
```

but this would display everything in the terminal.

Instead, we can search the file for the specific word `millionth`.

## Commands Used

Use `grep`:

```bash
grep "millionth" data.txt
```

The command searches `data.txt` for lines containing:

```text
millionth
```

The output will look similar to:

```text
millionth    [password]
```

The text after `millionth` is the password for **Bandit Level 8**.

## Reasoning

```text
data.txt
   ↓
Contains a large amount of data
   ↓
Password is next to "millionth"
   ↓
Search for "millionth"
   ↓
grep "millionth" data.txt
   ↓
Matching line is displayed
   ↓
Read the password
```

## Solution

```bash
grep "millionth" data.txt
```

## Concept Learned

### The `grep` Command

`grep` is used to search for text inside files.

For example:

```bash
grep "hello" file.txt
```

This searches `file.txt` for lines containing:

```text
hello
```

In this level:

```bash
grep "millionth" data.txt
```

means:

> Search `data.txt` for the word `millionth`.

### Why `grep` Instead of `cat`?

`cat` displays the contents of the entire file:

```bash
cat data.txt
```

If the file is very large, this can produce a huge amount of output.

`grep` allows us to search directly for the information we need:

```bash
grep "millionth" data.txt
```

## Mistake & Lesson

**Mistake:** Reading a large file manually with `cat`.

**Lesson:** When you know a specific word or pattern you're looking for, use `grep` to search the file directly.
