# Mission 5 — Numbers and data

## 1. Task / objective

Convert numbers between decimal, binary and hexadecimal by hand, check every
answer with Python, build a small converter program and test it, and explain how
a computer stores text.

## 2. Work completed

I did the seven conversions on paper first, wrote the steps out below, then
checked each one in Python. After that I wrote `number_converter.py` and ran it
with four different numbers. The last part is ASCII and UTF-8.

Bits and bytes first, because everything else leans on them. A bit is one
position holding either 0 or 1. Eight bits together make one byte.

### Task 5.1 — Conversions by hand

**The method.** Every number system works the same way. Each digit is multiplied
by the base raised to the power of its position, counting the rightmost position
as 0. Decimal 472 means 4×10² + 7×10¹ + 2×10⁰. Binary does the same with base 2
and hexadecimal with base 16. Going the other way, from decimal to binary, I
divided by 2 over and over and kept the remainders.

**1. Decimal 13 to binary**

| Division | Quotient | Remainder |
|---|---|---|
| 13 ÷ 2 | 6 | 1 |
| 6 ÷ 2 | 3 | 0 |
| 3 ÷ 2 | 1 | 1 |
| 1 ÷ 2 | 0 | 1 |

Read the remainders from the bottom up: **1101**.

Check: 1×8 + 1×4 + 0×2 + 1×1 = 8 + 4 + 0 + 1 = 13. That matches.

**2. Decimal 25 to binary**

| Division | Quotient | Remainder |
|---|---|---|
| 25 ÷ 2 | 12 | 1 |
| 12 ÷ 2 | 6 | 0 |
| 6 ÷ 2 | 3 | 0 |
| 3 ÷ 2 | 1 | 1 |
| 1 ÷ 2 | 0 | 1 |

Bottom up: **11001**.

Check: 1×16 + 1×8 + 0×4 + 0×2 + 1×1 = 16 + 8 + 0 + 0 + 1 = 25. Correct.

**3. Binary 1010 to decimal**

Positions from the right: 2³ = 8, 2² = 4, 2¹ = 2, 2⁰ = 1.

1×8 + 0×4 + 1×2 + 0×1 = 8 + 0 + 2 + 0 = **10**

**4. Binary 1101 to decimal**

1×8 + 1×4 + 0×2 + 1×1 = 8 + 4 + 0 + 1 = **13**

**5. Hexadecimal A to decimal**

In hexadecimal, A stands for 10. It is a single digit, so it sits in the 16⁰
position.

A × 16⁰ = 10 × 1 = **10**

**6. Hexadecimal 1F to decimal**

1 is in the 16¹ position, F is in the 16⁰ position, and F means 15.

1 × 16 = 16
F × 1 = 15
16 + 15 = **31**

**7. Binary 1111 to hexadecimal**

A hexadecimal digit holds exactly four bits, so I grouped from the right in
fours. It was already one group: 1111.

1×8 + 1×4 + 1×2 + 1×1 = 15, and 15 in hexadecimal is F.

Answer: **F**

### Task 5.2 — Checking with Python

I opened Python in the Terminal and used the built-in functions. These are the
real results, not what I expected them to be.

| Question | What I typed | Result | Did it match my working? |
|---|---|---|---|
| Decimal 13 to binary | `bin(13)` | `'0b1101'` | Yes, 1101 |
| Decimal 25 to binary | `bin(25)` | `'0b11001'` | Yes, 11001 |
| Binary 1010 to decimal | `int('1010', 2)` | `10` | Yes |
| Binary 1101 to decimal | `int('1101', 2)` | `13` | Yes |
| Hexadecimal A to decimal | `int('A', 16)` | `10` | Yes |
| Hexadecimal 1F to decimal | `int('1F', 16)` | `31` | Yes |
| Binary 1111 to hexadecimal | `hex(15)` | `'0xf'` | Yes, F and f are the same digit |

Two extra checks, because they join the two directions. `hex(13)` gave `'0xd'`,
which is 13 in hex. `int('0b1111', 2)` gave `15`, which is the decimal value
behind F.

The `0b` on the binary result and the `0x` on the hexadecimal result are labels,
not part of the number. `0b` says "binary" and `0x` says "hexadecimal". The
number is what comes after them.

### Task 5.3 — The number converter

`number_converter.py` is short on purpose. It asks for one number, turns it into
an integer, and prints the decimal, binary and hexadecimal forms.

    number = input("Enter a decimal number: ")
    number = int(number)

    print("Decimal:", number)
    print("Binary:", bin(number))
    print("Hexadecimal:", hex(number))

I ran it four times, piping the input in from the Terminal, so the prompt and the
answer end up on the same line.

| Test number | Binary | Hexadecimal |
|---|---|---|
| 13 | `0b1101` | `0xd` |
| 25 | `0b11001` | `0x19` |
| 100 | `0b1100100` | `0x64` |
| 255 (extra test) | `0b11111111` | `0xff` |

What each piece does:

- `input("...")` shows the message and waits for me to type. It always hands
  back text, even when I type digits.
- `int(number)` turns that text into a whole number, so Python can do maths with
  it. Without this step I would have the characters `"1"` and `"3"`, not 13.
- `bin(number)` gives the binary version as text, with `0b` in front.
- `hex(number)` gives the hexadecimal version as text, with `0x` in front.

There is no error handling, so typing a word instead of a number stops the
program with a `ValueError`. For this task that is fine, but it is the first thing
I would add if I kept working on it.

### Task 5.4 — How text is stored

ASCII covers a basic set of characters and gives each one a number. I checked the
two the task asked for with `ord()`:

- Capital **A** is **65**. `ord('A')` returned `65`.
- Small **a** is **97**. `ord('a')` returned `97`.

The other direction worked too. `chr(65)` gave `'A'` and `chr(97)` gave `'a'`.
That is the whole idea of an encoding. The computer stores the number, and the
encoding says which character that number means.

**Why a standard is needed.** A computer can only store bytes, so every letter
has to become a number before it can be saved, and be turned back afterwards.
Without a shared standard, 65 could mean A on one machine and something else on
another, and text would break the moment it moved between computers.

**A character that is not in basic ASCII.** The Indian rupee sign ₹. ASCII stops
at 127, so ₹ has no ASCII code at all. Its Unicode value is U+20B9, and
`hex(0x20B9)` confirmed that number. In UTF-8 it takes three bytes:
`'₹'.encode('utf-8')` returned `b'\xe2\x82\xb9'`.

ASCII sits inside UTF-8, which I checked: `'A'.encode('utf-8')` returned `b'A'`,
one byte worth 65. So the first 128 characters of UTF-8 are the same as ASCII,
and anything beyond that needs more bytes. That is why a plain English text file
is small and a file full of emoji or rupee signs is bigger than the character
count suggests.

## 3. Commands / tools used

| Command or function | Purpose |
|---|---|
| `python3` | To run the checks and the converter. |
| `bin()` | Decimal to binary, as text with a `0b` prefix. |
| `int(value, base)` | Text in a given base to a decimal integer. |
| `hex()` | Decimal to hexadecimal, as text with a `0x` prefix. |
| `ord()` | A character to its number. |
| `chr()` | A number back to a character. |
| `.encode('utf-8')` | Text to the actual bytes used to store it. |
| `print()` | To show the results. |
| VS Code | To write `number_converter.py`. |

## 4. My understanding

All number systems are one rule with a different base. Once I saw 472 as
4×100 + 7×10 + 2×1, binary and hexadecimal stopped feeling like a separate
topic. The only thing that changes is what each position is worth.

Decimal to binary is the only direction that needs the division method, and it
only comes out right if the remainders are read from the bottom up. Binary to
decimal is easier, because I just add up the position values where there is a 1.

Hexadecimal is not harder, it is just shorter. Four binary digits fit exactly
into one hex digit, which is why 1111 becomes F. That is the real reason
programmers use it. One character replaces four bits, so a long binary number
becomes short enough to read at a glance.

For text, the number is the character. A file is only bytes, and every encoding
is a published agreement about which number means which character.

## 5. Difficulties faced

- Reading the remainders bottom to top was the part I had to slow down for.
  Written in the order they come out, the answer is wrong.
- The `0b` and `0x` in the Python results looked like part of the number to me.
- In `int('1010', 2)` I did not understand what the `2` was doing.
- I assumed the rupee sign would take one byte, the same as a letter.

## 6. How I resolved them

- I checked every answer back by adding the position values. If the total matched
  the original decimal number, the order was right, so I did not have to trust my
  memory of the rule.
- I read the prefixes as labels and wrote the number by itself, so `0b1101` is
  binary 1101.
- The `2` is the base. It tells Python how to read the text. The same text read
  with base 16 would give a completely different number.
- I looked at the encoded bytes. ₹ became `b'\xe2\x82\xb9'`, three bytes, because
  it sits outside the first 128 characters. ASCII has no code for it at all.

## 7. Evidence / files

- `mission-05-numbers-data/README.md` - this file, with the seven conversions and
  all the tests.
- `mission-05-numbers-data/number_converter.py` - the working converter.
- `evidence/mission-05/python-verification.txt` - the real Python output for
  every expression.
- `evidence/mission-05/converter-tests.txt` - the real output of the four runs.

## 8. Commit details

Commit message:

    Build number converter and practise data representation

Pushed to `main` on GitHub.
