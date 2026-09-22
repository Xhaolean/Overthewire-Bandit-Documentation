# Bandit Level 11

## Objective

Find the password for **Bandit Level 12**.

The password is stored in the file:

```text id="p6b9c7"
data.txt
```

All lowercase and uppercase letters in the password have been **rotated by 13 positions**.

This is called **ROT13**.

## Initial Investigation

After logging into the `bandit11` machine, list the files:

```bash id="wq0y5d"
ls
```

Output:

```text id="qj1m2e"
data.txt
```

Read the file:

```bash id="l1j2ke"
cat data.txt
```

The output looks like random text:

```text id="rj7s8k"
gur cnffjbeq vf ...
```

The characters are not encrypted. They have been transformed using **ROT13**.

## Commands Used

We can decode ROT13 using the `tr` command.

Use:

```bash id="c2m8zn"
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

The `tr` command replaces characters according to the two character sets.

The mapping works like this:

```text id="w4r6tq"
A → N
B → O
C → P
...
M → Z

N → A
O → B
P → C
...
Z → M
```

The same transformation works in reverse, which is why applying ROT13 to ROT13 text reveals the original text.

## Reasoning

```text id="a8k3yf"
data.txt
   ↓
Text has been transformed using ROT13
   ↓
Need to rotate letters by 13 positions
   ↓
Use tr
   ↓
A-Z → N-ZA-M
a-z → n-za-m
   ↓
Original text is displayed
   ↓
Password is found
```

## Solution

```bash id="v8z1pq"
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

## Concept Learned

### ROT13

ROT13 means **Rotate by 13 places**.

For example:

```text id="h2q4vy"
A → N
B → O
C → P
```

And:

```text id="n7f3kx"
N → A
O → B
P → C
```

Because the alphabet contains 26 letters, rotating by 13 twice returns to the original letter.

For example:

```text id="q5r8wm"
A → N → A
```

### The `tr` Command

`tr` is used to translate or replace characters.

Basic example:

```bash id="z9x2pl"
echo "abc" | tr 'a-z' 'A-Z'
```

Output:

```text id="f4m7qd"
ABC
```

In this level:

```bash id="u6k3sr"
tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

performs the ROT13 transformation.

## Mistake & Lesson

**Mistake:** Assuming the text was encrypted and trying to use an encryption tool.

**Lesson:** ROT13 is a simple character substitution technique, not secure encryption. The `tr` command can be used to perform the required character transformation directly.
