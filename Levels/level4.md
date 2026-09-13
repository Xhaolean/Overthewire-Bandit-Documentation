# Bandit Level 4

## Objective

Find the password for **Bandit Level 5**.

The password is stored in the **only human-readable file** in the `inhere` directory.

## Initial Investigation

After logging into the `bandit4` machine, list the files in the current directory:

```bash
ls
```

Output:

```text
inhere
```

Enter the directory:

```bash
cd inhere
```

Now list the files:

```bash
ls
```

Output:

```text
-file00
-file01
-file02
-file03
-file04
-file05
-file06
-file07
-file08
-file09
```

There are multiple files, so we need to determine which one contains readable text.

## Commands Used

First, check the type of each file:

```bash
file ./*
```

The output will identify different files as things such as:

```text
./-file00: data
./-file01: data
./-file02: ASCII text
...
```

We are looking for the file identified as **ASCII text**, because this indicates that it contains human-readable text.

For example:

```text
./-file07: ASCII text
```

Now read that file:

```bash
cat ./-file07
```

The password is displayed.

## Reasoning

```text
Current directory
       ↓
inhere
       ↓
cd inhere
       ↓
Multiple files
       ↓
Need to find the human-readable file
       ↓
file ./*
       ↓
Find the file identified as ASCII text
       ↓
cat ./filename
       ↓
Password is displayed
```

## Solution

```bash
cd inhere
file ./*
cat ./-file07
```

> The exact filename containing the password can be confirmed from the output of `file ./*`.

## Concept Learned

### The `file` Command

The `file` command determines the type of a file.

For example:

```bash
file example.txt
```

might output:

```text
example.txt: ASCII text
```

While another file might show:

```text
example.bin: data
```

This is useful when you have many files and need to determine which ones contain readable text.

### The `./` Path

The files in this level begin with `-`:

```text
-file00
-file01
```

Using:

```bash
cat ./-file07
```

makes it clear that `-file07` is a filename in the current directory rather than a command-line option.

## Mistake & Lesson

**Mistake:** Trying to open every file manually without first checking what type they are.

**Lesson:** When a directory contains many unknown files, the `file` command can quickly identify which files contain human-readable text.
