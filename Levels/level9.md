# Bandit Level 9

## Objective

Find the password for **Bandit Level 10**.

The password is stored in the file:

```text
data.txt
```

It is one of the few **human-readable strings**, preceded by several `=` characters.

## Initial Investigation

After logging into the `bandit9` machine, list the files:

```bash
ls
```

Output:

```text
data.txt
```

The file contains binary data, so simply using:

```bash
cat data.txt
```

produces a lot of unreadable characters.

We need to extract the human-readable strings from the file.

## Commands Used

Use the `strings` command:

```bash
strings data.txt
```

This extracts sequences of printable characters from the file.

There will be many strings in the output, so we can search for the lines containing `=`:

```bash
strings data.txt | grep "="
```

The output will contain several lines.

Among them, one line contains the password.

For example:

```text
======== password_here
```

The text following the `=` characters is the password for **Bandit Level 10**.

## Reasoning

```text
data.txt
   ↓
Contains binary data
   ↓
cat produces unreadable output
   ↓
Use strings to extract readable text
   ↓
Search for "="
   ↓
strings data.txt | grep "="
   ↓
Find the relevant string
   ↓
Password is displayed
```

## Solution

```bash
strings data.txt | grep "="
```

Look through the output for the string containing the password.

## Concept Learned

### The `strings` Command

`strings` extracts printable character sequences from binary or non-text files.

For example:

```bash
strings binary_file
```

may produce:

```text
Hello
Password
Some readable text
```

This is useful when a file contains a mixture of binary data and readable text.

### Combining `strings` and `grep`

We can combine commands using a pipe:

```bash
strings data.txt | grep "="
```

This means:

```text
data.txt
   ↓
strings
   ↓
Readable strings
   ↓
grep "="
   ↓
Lines containing "="
```

This reduces the amount of output we need to inspect manually.

## Mistake & Lesson

**Mistake:** Trying to read a binary file directly with `cat`.

**Lesson:** When a file contains binary data but may contain readable text, `strings` can extract the printable text. `grep` can then help filter the results.
