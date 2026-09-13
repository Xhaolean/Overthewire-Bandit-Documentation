# Bandit Level 3

## Objective

Find the password for **Bandit Level 4**.

The password is stored in a **hidden file** inside the `inhere` directory.

## Initial Investigation

After logging into the `bandit3` machine, list the files in the current directory:

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

No files are displayed.

This does **not** necessarily mean the directory is empty.

Linux files whose names begin with `.` are considered **hidden files**, and normal `ls` does not show them.

## Commands Used

Use:

```bash
ls -la
```

Output will show something similar to:

```text
.  ..  .hidden
```

The file we are interested in is:

```text
.hidden
```

Now read it:

```bash
cat .hidden
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
ls
       ↓
Nothing visible
       ↓
Could contain hidden files
       ↓
ls -la
       ↓
.hidden appears
       ↓
cat .hidden
       ↓
Password is displayed
```

## Solution

```bash
cd inhere
ls -la
cat .hidden
```

## Concept Learned

### Hidden Files

In Linux, filenames beginning with `.` are normally hidden from regular `ls` output.

For example:

```text
file.txt
.hidden
```

Running:

```bash
ls
```

may only show:

```text
file.txt
```

To show hidden files, use:

```bash
ls -a
```

The `-a` option means:

> Show all files, including hidden files.

`-l` displays the files in a detailed/long format:

```bash
ls -la
```

So:

```text
-a → show hidden files
-l → long/detailed listing
```

## Mistake & Lesson

**Mistake:** Assuming that `ls` showing nothing means the directory contains no files.

**Lesson:** Hidden files are not displayed by normal `ls`. Use `ls -a` or `ls -la` when you need to inspect hidden files.
