# Bandit Level 8

## Objective

Find the password for **Bandit Level 9**.

The password is stored in the file:

```text
data.txt
```

The password is the **only line that occurs exactly once**.

## Initial Investigation

After logging into the `bandit8` machine, list the files:

```bash
ls
```

Output:

```text
data.txt
```

The file contains many lines, so manually checking them would be difficult.

We need to find the line that appears only once.

## Commands Used

First, sort the contents of the file:

```bash
sort data.txt
```

`sort` arranges the lines alphabetically.

However, we need to find the line that occurs only once.

We can combine `sort` with `uniq`:

```bash
sort data.txt | uniq -u
```

The `|` symbol is called a **pipe**.

It sends the output of one command into another command.

The command works like this:

```text
data.txt
   ↓
sort
   ↓
Sorted lines
   ↓
uniq -u
   ↓
Line appearing only once
```

The output is the password for **Bandit Level 9**.

## Reasoning

```text
data.txt
   ↓
Many lines
   ↓
Password occurs only once
   ↓
Sort the lines
   ↓
Group identical lines together
   ↓
Use uniq -u
   ↓
Unique line is displayed
   ↓
Password found
```

## Solution

```bash
sort data.txt | uniq -u
```

## Concept Learned

### The `sort` Command

`sort` arranges lines of text in order.

Example:

```text
banana
apple
orange
```

Running:

```bash
sort file.txt
```

produces:

```text
apple
banana
orange
```

### The `uniq` Command

`uniq` is used to detect or remove repeated **adjacent** lines.

For example:

```text
apple
apple
banana
banana
orange
```

Running:

```bash
uniq file.txt
```

produces:

```text
apple
banana
orange
```

The `-u` option means:

> Show only lines that occur exactly once.

```bash
uniq -u
```

### The Pipe `|`

The pipe sends the output of one command directly into another command.

For example:

```bash
sort data.txt | uniq -u
```

means:

```text
sort data.txt
       ↓
   output
       ↓
uniq -u
       ↓
unique line
```

This allows multiple Linux commands to be combined into a single command.

## Mistake & Lesson

**Mistake:** Using `uniq -u data.txt` directly.

**Lesson:** `uniq` only detects repeated lines when they are next to each other. Sorting the file first groups identical lines together, allowing `uniq -u` to correctly find the line that appears only once.
