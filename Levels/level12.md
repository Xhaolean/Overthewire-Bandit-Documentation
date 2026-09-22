# Bandit Level 12

## Objective

Find the password for **Bandit Level 13**.

The password is stored in:

```text
data.txt
```

The file is a **hexdump** of a file that has been compressed multiple times.

We need to:

1. Convert the hexdump back into binary data.
2. Identify the compression format.
3. Decompress it.
4. Repeat until we reach the actual password.

## Initial Investigation

After logging into the `bandit12` machine, list the files:

```bash
ls
```

Output:

```text
data.txt
```

View the file:

```bash
cat data.txt
```

The contents look like hexadecimal values:

```text
00000000: 1f8b 0808 ...
00000010: ...
```

This is not the actual compressed file. It is a **hexdump**.

## Commands Used

First, create a temporary working directory:

```bash
mkdir /tmp/bandit12
```

Copy the file into it:

```bash
cp data.txt /tmp/bandit12/
```

Move into the directory:

```bash
cd /tmp/bandit12
```

Now convert the hexdump back into binary data:

```bash
xxd -r data.txt data
```

The `-r` option means **reverse** the hexdump.

Now check what type of file we have:

```bash
file data
```

It will tell us which compression format is currently being used.

For example, it may say:

```text
data: gzip compressed data
```

Rename the file with the appropriate extension:

```bash
mv data data.gz
```

Then decompress it:

```bash
gzip -d data.gz
```

Check the resulting file again:

```bash
file data
```

It may now be another compression format such as:

```text
bzip2 compressed data
```

Rename it:

```bash
mv data data.bz2
```

Then decompress:

```bash
bzip2 -d data.bz2
```

Continue checking the file:

```bash
file data
```

and use the appropriate decompression command until the file finally becomes normal text.

## Reasoning

```text
data.txt
   ↓
Hexdump
   ↓
xxd -r
   ↓
Binary compressed file
   ↓
file
   ↓
Identify compression format
   ↓
Decompress
   ↓
file again
   ↓
Another compression layer
   ↓
Repeat
   ↓
Normal text file
   ↓
Password is displayed
```

## Useful Commands

### Convert Hexdump Back to Binary

```bash
xxd -r data.txt data
```

### Identify File Type

```bash
file data
```

### Gzip

```bash
mv data data.gz
gzip -d data.gz
```

### Bzip2

```bash
mv data data.bz2
bzip2 -d data.bz2
```

### Tar

If `file` reports a tar archive:

```bash
mv data data.tar
tar -xf data.tar
```

After extracting, check the resulting file again:

```bash
file *
```

## Solution

The important idea is to repeatedly use:

```bash
file data
```

then apply the correct decompression/extraction command.

The general process is:

```bash
xxd -r data.txt data
file data
```

Then repeatedly:

```bash
file data
```

followed by the appropriate decompression command.

Eventually, the final file will contain the password.

## Concept Learned

### Hexdump

A hexdump represents binary data using hexadecimal numbers.

For example:

```text
1f 8b 08 00 ...
```

does not mean the file is text containing those characters. It is a representation of the underlying bytes.

`xxd` can create a hexdump:

```bash
xxd file
```

And `xxd -r` can reverse it:

```bash
xxd -r hexdump.txt file
```

### The `file` Command

The `file` command identifies what type of data a file contains:

```bash
file data
```

This is particularly useful when the filename does not have an extension.

### Multiple Compression Layers

A file can be compressed multiple times.

For example:

```text
gzip
  ↓
bzip2
  ↓
tar
  ↓
gzip
  ↓
password
```

Therefore, after every decompression step, use:

```bash
file data
```

to determine what to do next.

## Mistake & Lesson

**Mistake:** Trying to guess the compression format from the filename.

**Lesson:** File extensions are not always reliable. Use the `file` command to identify the actual format, then decompress or extract it accordingly.

Also, use a temporary directory such as `/tmp/bandit12` instead of modifying the original `data.txt`.
