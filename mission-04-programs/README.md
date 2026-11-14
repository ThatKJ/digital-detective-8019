# Mission 4 — How programs run

## 1. Task / objective

Write a one-line Python program that prints "Hello from Python", run it with
Python 3 from Terminal, then compare how a compiler and an interpreter handle a
program.

## 2. Work completed

I created `hello.py` inside this mission folder. It contains one line:

    print("Hello from Python")

I ran it with `python3 hello.py` and the Terminal printed `Hello from Python`.
The exit status was 0, which means the program finished without an error.

I also wanted to see the difference for myself instead of only reading about it,
so I ran a few extra checks:

- I ran `python3 -m py_compile hello.py`, which created
  `__pycache__/hello.cpython-314.pyc`. That is 155 bytes of bytecode. Python
  translated my source file before running it, which is why I would not call
  Python "pure interpretation".
- I wrote the same program in C in a temporary folder outside the repository and
  compiled it with `cc hello.c -o hello`. The result was a 33432-byte file
  called `hello` that starts with `-rwxr-xr-x`, and `file hello` said
  `Mach-O 64-bit executable arm64`. I could run it with `./hello` and it printed
  `Hello from C` even though there is no separate "interpret this" step.

The temporary C folder was deleted after I copied the output into the evidence
file. Nothing compiled was left inside the repository, and `__pycache__` is
ignored by Git.

### Task 4.2 — Compiler versus interpreter

| Point | Compiler | Interpreter |
|---|---|---|
| When translation / execution happens | Translation happens first, once, before the program is run. The program is executed afterwards as a separate step. | Translation and execution happen together while the program runs, usually one statement at a time. |
| Typical output | A new file that the computer can run directly. My C program produced a 33432-byte `hello` executable. | No new runnable file. The program prints its own output, like `Hello from Python`, and nothing is left over apart from possible cache files. |
| One example | C, compiled with `cc` or `gcc` (I used Apple clang 21.0.0). | Python, run with `python3`. |
| One advantage | The translation is done once, so the finished program does not pay that cost again every time it runs, which usually makes it faster. Errors are also reported before the program ever runs. | A small change can be tested immediately with no build step, and when something is wrong the error points at the exact line that failed. |

In three or four sentences: a compiler reads the whole source file and turns it
into a separate program, and only then do I run that program. An interpreter
reads the source and carries out the instructions as it goes, so the source file
is still needed every time. The difference shows in the output: my C folder had
a 33432-byte executable next to an 83-byte source file, while Python only had a
155-byte cached `.pyc` and still needed `hello.py` to run. Most real languages
mix both, and Python is the proof, because it compiles to bytecode first and
then runs that bytecode.

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `cat hello.py` | To show the program before running it. |
| `python3 --version` | To confirm the Python version, 3.14.7. |
| `python3 hello.py` | To run the program with Python 3. |
| `echo $?` | To check the exit status after the run. |
| `python3 -m py_compile hello.py` | To force Python to produce its bytecode file, so I could see that compilation really happens. |
| `cc hello.c -o hello` | To compile a small C program for comparison. |
| `file hello` | To confirm the C output was a real executable. |
| VS Code | To write `hello.py`. |

## 4. My understanding

The program file is not what runs. The file is text that has to be turned into
something the CPU can carry out. That translation is the whole difference
between a compiler and an interpreter: a compiler does the translation and
saves the result, while an interpreter does it while running.

What surprised me was that Python still compiles. The `.pyc` file is the
translated version, and Python reuses it if the source has not changed. So
"Python is interpreted" is really shorthand. It compiles to bytecode, and a
program called the Python virtual machine runs that bytecode.

The practical side matters too. With C I had to compile before running, and if
the code was wrong I got errors at compile time. With Python I just run the file
and find out what breaks as it runs. That is why Python feels quicker for small
scripts, and why big programs are often written in compiled languages.

## 5. Difficulties faced

- The comparison table asked for "typical output", and I was not sure whether
  that meant the output of the compiler or the output of the program.
- I expected Python to leave no extra files, and then found a `__pycache__`
  folder after running it.
- My first idea was to write the C comparison inside the mission folder, which
  would have left an executable file in the repository.

## 6. How I resolved them

- I read it as the output of the translating tool, not of the program, and put
  both in the table: the compiler gives an executable file, the interpreter
  gives nothing you can run on its own.
- I looked inside `__pycache__` and saw `hello.cpython-314.pyc`. That is the
  compiled bytecode, so Python does compile, just not to a standalone program.
- I did the C test in a temporary folder instead and saved only the text output.
  I also added a `.gitignore` with `__pycache__/` and `*.pyc` so build files do
  not get committed by accident.

## 7. Evidence / files

- `mission-04-programs/hello.py` - the one-line Python program.
- `mission-04-programs/README.md` - this file with the comparison.
- `evidence/mission-04/program-run.txt` - real output of both runs, with the
  username replaced by `[redacted]`.
- `.gitignore` - keeps Python cache files out of the repository.

## 8. Commit details

Commit message:

    Compare compilers and interpreters

Pushed to `main` on GitHub.
