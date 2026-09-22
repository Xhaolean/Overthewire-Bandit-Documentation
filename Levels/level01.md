# Bandit Level 1

## Objective

Find the password for **Bandit Level 2**.

The password is stored in a file named:

```text
-
```

## Initial Investigation

After logging into the `bandit1` machine, list the files in the current directory:

```bash
ls
```

Output:

```text
-
```

The filename is simply `-`.

This is unusual because `-` is commonly interpreted by Linux commands as an option or special input.

## Commands Used

First try:

```bash
cat -
```

This does not read the file as expected because `cat` interprets `-` specially.

So explicitly specify that the file is in the current directory:

```bash
cat ./-
```

## Reasoning

```text
File name: -
       ↓
"-" has a special meaning in Linux commands
       ↓
Use ./ to specify a file path
       ↓
./- means "the file named - in the current directory"
       ↓
cat ./-
       ↓
Password is displayed
```

## Solution

```bash
cat ./-
```

## Concept Learned

### Relative Path

`./` means **the current directory**.

Therefore:

```text
./-
```

means:

> The file named `-` inside the current directory.

## Mistake & Lesson

**Mistake:** Treating `-` like a normal filename.

**Lesson:** When a filename conflicts with command syntax, using an explicit path such as `./filename` can remove the ambiguity.
