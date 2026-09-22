# Bandit Level 10

## Objective

Find the password for **Bandit Level 11**.

The password is stored in the file:

```text
data.txt
```

The entire file is encoded in **Base64**.

## Initial Investigation

After logging into the `bandit10` machine, list the files:

```bash
ls
```

Output:

```text
data.txt
```

Read the file:

```bash
cat data.txt
```

The output looks something like:

```text
VGhlIHBhc3N3b3JkIGlzIH...
```

This does not look like normal text.

The objective tells us that the data is encoded using **Base64**.

## Commands Used

We can decode Base64 using the `base64` command.

Use:

```bash
base64 -d data.txt
```

The `-d` option means:

```text
-d → decode
```

The decoded output is the password for **Bandit Level 11**.

We can also use:

```bash
cat data.txt | base64 -d
```

Both commands produce the decoded password.

## Reasoning

```text
data.txt
   ↓
Contains Base64 encoded data
   ↓
Use the base64 command
   ↓
base64 -d data.txt
   ↓
Decode the Base64 data
   ↓
Password is displayed
```

## Solution

```bash
base64 -d data.txt
```

## Concept Learned

### Base64 Encoding

Base64 is a way of representing binary data using a set of printable characters.

For example:

```text
Hello
```

can be Base64 encoded as:

```text
SGVsbG8=
```

Decoding it:

```bash
echo "SGVsbG8=" | base64 -d
```

produces:

```text
Hello
```

### The `base64` Command

To encode data:

```bash
base64 file.txt
```

To decode Base64:

```bash
base64 -d file.txt
```

The important option in this level is:

```text
-d → decode
```

## Mistake & Lesson

**Mistake:** Treating the Base64 text as a password directly.

**Lesson:** Base64 is an encoding, not encryption. If you know data is Base64 encoded, it can be decoded using tools such as `base64 -d`.
