# Bandit Level 2

## Objective

Find the password for **Bandit Level 3**.

The password is stored in a file with spaces in its filename:

```text
spaces in this filename
```

## Initial Investigation

After logging into the `bandit2` machine, list the files in the current directory:

```bash
ls
```

Output:

```text
spaces in this filename
```

The filename contains **spaces**.

If we try:

```bash
cat spaces in this filename
```

the shell does not treat it as one filename.

Instead, it interprets each space-separated word as a separate argument:

```text
spaces
in
this
filename
```

So we need to tell the shell that all of these words belong to the same filename.

## Commands Used

One way is to escape each space using `\`:

```bash
cat spaces\ in\ this\ filename
```

Another, simpler method is to put the entire filename inside quotes:

```bash
cat "spaces in this filename"
```

This tells the shell:

> Treat everything inside the quotes as one filename.

## Reasoning

```text
Filename:
spaces in this filename
        ↓
Filename contains spaces
        ↓
Shell normally separates arguments at spaces
        ↓
Put the filename inside quotes
        ↓
"spaces in this filename"
        ↓
cat "spaces in this filename"
        ↓
Password is displayed
```

## Solution

```bash
cat "spaces in this filename"
```

## Concept Learned

### Spaces in Filenames

The shell normally uses spaces to separate different arguments.

For example:

```bash
cat file.txt
```

has one argument:

```text
file.txt
```

But:

```bash
cat my file.txt
```

is interpreted as multiple arguments:

```text
my
file.txt
```

To treat a filename containing spaces as a single argument, use quotes:

```bash
cat "my file.txt"
```

You can also escape spaces with `\`:

```bash
cat my\ file.txt
```

Both methods work.

## Mistake & Lesson

**Mistake:** Treating a filename containing spaces like a normal filename.

**Lesson:** The shell uses spaces to separate arguments. When a filename contains spaces, use quotes or escape the spaces with `\`.
