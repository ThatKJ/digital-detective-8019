# Mission 5 — Numbers and data

## 1. Task / objective

Convert numbers between decimal, binary and hexadecimal by hand, check every
answer with Python, build a small converter program and test it, and explain how
a computer stores text.

## 2. Work completed

I did all seven conversions on paper first, wrote the steps out below, then
checked each one in Python. After that I wrote `number_converter.py` and ran it
with four different numbers. The last part covers ASCII and UTF-8.

Bits and bytes first, because the rest depends on them: a bit is one position
that holds either 0 or 1, and eight bits together make one byte.

### Task 5.1 — Conversions by hand

**The method I used.** Every number system works the same way. Each digit is
multiplied by the base raised to the power of its position, counting the
rightmost position as 0. For decimal the base is 10, so 472 means
4×10² + 7×10¹ + 2×10⁰. Binary does the same with base 2, and hexadecimal with
base 16. Going the other way, from decimal to binary, I divided by 2 again and
again and kept the remainders.

**1. Decimal 13 to binary**

| Division | Quotient | Remainder |
|---|---|---|
| 13 ÷ 2 | 6 | 1 |
| 6 ÷ 2 | 3 | 0 |
| 3 ÷ 2 | 1 | 1 |
| 1 ÷ 2 | 0 | 1 |

The remainders are read from the bottom up: **1101**.

Check: 1×8 + 1×4 + 0×2 + 1×1 = 8 + 4 + 0 + 1 = 13. Correct.

**2. Decimal 25 to binary**

| Division | Quotient | Remainder |
|---|---|---|
| 25 ÷ 2 | 12 | 1 |
| 12 ÷ 2 | 6 | 0 |
| 6 ÷ 2 | 3 | 0 |
| 3 ÷ 2 | 1 | 1 |
| 1 ÷ 2 | 0 | 1 |

Read from the bottom up: **11001**.

Check: 1×16 + 1×8 + 0×4 + 0×2 + 1×1 = 16 + 8 + 0 + 0 + 1 = 25. Correct.

**3. Binary 1010 to decimal**

Positions from the right: 2³ = 8, 2² = 4, 2¹ = 2, 2⁰ = 1.

1×8 + 0×4 + 1×2 + 0×1 = 8 + 0 + 2 + 0 = **10**

**4. Binary 1101 to decimal**

1×8 + 1×4 + 0×2 + 1×1 = 8 + 4 + 0 + 1 = **13**

**5. Hexadecimal A to decimal**

In hexadecimal, A stands for 10. There is only one digit, so it sits in the
16⁰ position.

A × 16⁰ = 10 × 1 = **10**

**6. Hexadecimal 1F to decimal**

1 is in the 16¹ position and F is in the 16⁰ position. F = 15.

1 × 16 = 16
F × 1 = 15
16 + 15 = **31**

**7. Binary 1111 to hexadecimal**

Hexadecimal digits each hold four bits, so I grouped the binary into one group
of four from the right. It was already one group: 1111.

1×8 + 1×4 + 1×2 + 1×1 = 15, and 15 in hexadecimal is F.

Answer: **F**

### Task 5.2 — Checking with Python

I opened Python from Terminal and used the built-in functions. These are the
real results.

| Question | Expression I tested | Result | Matches my working? |
|---|---|---|---|
| Decimal 13 to binary | `bin(13)` | `'0b1101'` | Yes, 1101 |
| Decimal 25 to binary | `bin(25)` | `'0b11001'` | Yes, 11001 |
| Binary 1010 to decimal | `int('1010', 2)` | `10` | Yes |
| Binary 1101 to decimal | `int('1101', 2)` | `13` | Yes |
| Hexadecimal A to decimal | `int('A', 16)` | `10` | Yes |
| Hexadecimal 1F to decimal | `int('1F', 16)` | `31` | Yes |
| Binary 1111 to hexadecimal | `hex(15)` | `'0xf'` | Yes, F is the same as f |

Two extra checks I ran because they connect the two directions:
`hex(13)` gave `'0xd'` (13 in hex) and `int('0b1111', 2)` gave `15`, which is
the decimal value behind F.

The `0b` in the binary result and the `0x` in the hexadecimal result are labels,
not part of the number. `0b` says "this is binary", `0x` says "this is
hexadecimal". The number itself is what comes after them.

### Task 5.3 — The number converter

`number_converter.py` is short on purpose. It asks for one number, converts it
to an integer, and prints the decimal, binary and hexadecimal forms.

    number = input("Enter a decimal number: ")
    number = int(number)

    print("Decimal:", number)
    print("Binary:", bin(number))
    print("Hexadecimal:", hex(number))

I ran it four times. The input was piped in from Terminal so the output below
looks like the prompt and the answer on the same line.

| Test number | Binary output | Hexadecimal output |
|---|---|---|
| 13 | `0b1101` | `0xd` |
| 25 | `0b11001` | `0x19` |
| 100 | `0b1100100` | `0x64` |
| 255 (extra test) | `0b11111111` | `0xff` |

What each function does:

- `input("Enter a decimal number: ")` shows the message and waits for me to
  type something. It always gives back text, even if I type digits.
- `int(number)` turns that text into a whole number so Python can do arithmetic
  with it. Without this step, `input()` would hand me the characters `"1"` and
  `"3"`, not the number 13.
- `bin(number)` gives the binary version as text, with `0b` in front.
- `hex(number)` gives the hexadecimal version as text, with `0x` in front.

The program has no error handling, so typing a word instead of a number stops it
with a `ValueError`. That is fine for this task, but it is the first thing I
would add if I kept building on it.

### Task 5.4 — How text is stored

ASCII covers a basic set of characters and gives each one a number. I checked
the two the task asked for with `ord()`:

- Uppercase **A** is decimal **65** (`ord('A')` returned `65`)
- Lowercase **a** is decimal **97** (`ord('a')` returned `97`)

Going the other way, `chr(65)` returned `'A'` and `chr(97)` returned `'a'`.
That is the whole idea of an encoding: the computer stores the number, and the
encoding says which character that number means.

**Why an encoding standard is needed.** A computer can only store bytes, so
every letter has to be turned into a number before it can be saved, and turned
back afterwards. Without a standard, the number 65 could mean A on one machine
and something else on another, so text would not survive being moved between
computers.

**One character that is not in basic ASCII.** The Indian rupee sign ₹. ASCII
only goes up to 127, so ₹ has no ASCII code at all. It has the Unicode value
U+20B9, and `hex(0x20B9)` confirmed the number. In UTF-8 it is stored as three
bytes: `'₹'.encode('utf-8')` returned `b'\xe2\x82\xb9'`.

ASCII and UTF-8 fit together, which I checked: `'A'.encode('utf-8')` returned
`b'A'`, a single byte worth 65. So the first 128 characters of UTF-8 are the
same as ASCII, and anything outside that needs more bytes. That is why a text
file full of English is small, and a file with emoji or rupee signs is bigger
than the letter count suggests.

## 3. Commands / tools used

| Command or function | Purpose |
|---|---|
| `python3` | To run the checks and the converter. |
| `bin()` | Decimal to binary, as text with a `0b` prefix. |
| `int(value, base)` | Text in a given base to a decimal integer. |
| `hex()` | Decimal to hexadecimal, as text with a `0x` prefix. |
| `ord()` | Character to its numeric code. |
| `chr()` | Numeric code back to a character. |
| `.encode('utf-8')` | Text to the actual bytes used to store it. |
| `print()` | To display the results. |
| VS Code | To write `number_converter.py`. |

## 4. My understanding

All number systems are the same rule with a different base. Once I saw 472 as
4×100 + 7×10 + 2×1, binary and hexadecimal stopped looking like a separate
topic. The only thing that changes is what each position is worth.

Going from decimal to binary is the only direction that needs the division
method, and the answer only comes out right if the remainders are read from the
bottom up. Going from binary to decimal is simpler because I just add the
position values of the 1s.

Hexadecimal is not harder, it is just more compact. Four binary digits fit
exactly into one hexadecimal digit, which is why 1111 becomes F. That is the
real reason programmers use it: one hex digit replaces four bits, so long binary
numbers become short enough to read.

For text, the number is the character. Every encoding standard is a published
agreement about which number means which character, and the file is just bytes.

## 5. Difficulties faced

- Reading the remainders from bottom to top was the part I had to be careful
  with. Written in the order they are produced, the answers come out wrong.
- The `0b` and `0x` in the Python results looked like part of the number.
- In `int('1010', 2)` I did not understand what the second part was for.
- I expected the rupee sign to take one byte like a letter does.

## 6. How I resolved them

- I checked every answer back by adding the position values. If the sum matched
  the original decimal number, the order was right, so I did not have to trust
  my memory of the rule.
- I read the prefixes as labels and wrote the number separately, so `0b1101` is
  binary 1101.
- The `2` in `int('1010', 2)` is the base. It tells Python how to read the text.
  The same text read with base 16 would give a different number.
- I looked at `.encode('utf-8')`. ₹ became `b'\xe2\x82\xb9'`, three bytes,
  because it is outside the first 128 characters. ASCII has no code for it at
  all.

## 7. Evidence / files

- `mission-05-numbers-data/README.md` - this file, with all seven conversions and
  the tests.
- `mission-05-numbers-data/number_converter.py` - the working converter.
- `evidence/mission-05/python-verification.txt` - the real Python output for
  every expression.
- `evidence/mission-05/converter-tests.txt` - the real output of the four runs.

## 8. Commit details

Commit message:

    Build number converter and practise data representation

Pushed to `main` on GitHub.
