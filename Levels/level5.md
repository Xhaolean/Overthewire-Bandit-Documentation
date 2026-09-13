# Bandit Level 5

## Objective

Find the password for **Bandit Level 6**.

The password is stored in a file somewhere inside the `inhere` directory.

The file has these properties:

* Human-readable
* Exactly **1033 bytes** in size
* Not executable

## Initial Investigation

After logging into the `bandit5` machine, list the files:

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

Now list its contents:

```bash
ls
```

You will see multiple directories.

We need to search through them and find the file matching the required properties.

## Commands Used

The `find` command can search for files based on different properties.

Use:

```bash
find . -type f -size 1033c ! -executable
```

Let's break this command down:

```text
find .
```

Search starting from the current directory.

```text
-type f
```

Search only for regular files.

```text
-size 1033c
```

Find files that are exactly **1033 bytes**.

The `c` means bytes.

```text
! -executable
```

Exclude executable files.

The command should return the path of the required file.

For example:

```text
./maybehere07/.file2
```

Now read the file:

```bash
cat ./maybehere07/.file2
```

The password is displayed.

## Reasoning

```text
Current directory
       ↓
inhere
       ↓
Many directories and files
       ↓
Need to find one specific file
       ↓
Human-readable
Exactly 1033 bytes
Not executable
       ↓
Use find with conditions
       ↓
find . -type f -size 1033c ! -executable
       ↓
Required file is found
       ↓
cat filename
       ↓
Password is displayed
```

## Solution

```bash
cd inhere
find . -type f -size 1033c ! -executable
```

Then use the path returned by `find`:

```bash
cat ./path/to/file
```

## Concept Learned

### The `find` Command

`find` is used to search for files and directories based on conditions.

Basic example:

```bash
find .
```

Searches the current directory and everything inside it.

You can add conditions:

```bash
find . -type f
```

Find regular files.

```bash
find . -size 1033c
```

Find files that are 1033 bytes.

```bash
find . -executable
```

Find executable files.

Multiple conditions can be combined:

```bash
find . -type f -size 1033c ! -executable
```

This is useful when there are many files and manually checking each one would be inefficient.

## Mistake & Lesson

**Mistake:** Trying to manually open every file to find the password.

**Lesson:** When you know specific properties of a file, use `find` to search for those properties instead of checking files one by one.
