# Mission 4 — How programs run

## 1. Task / objective

Write a one-line Python program that prints `Hello from Python`, run it with
Python 3 from the Terminal, then compare how a compiler and an interpreter deal
with a program.

## 2. Work completed

I made `hello.py` inside this folder. It is one line:

    print("Hello from Python")

I ran `python3 hello.py` and the Terminal printed `Hello from Python`. The exit
status was 0, which means it finished with no error.

I did not want to just repeat what a website says about compilers, so I ran a
few extra checks:

- `python3 -m py_compile hello.py` created `__pycache__/hello.cpython-314.pyc`,
  which is 155 bytes of bytecode. Python translated my file before running it.
  That alone means "Python is interpreted" is not the full story.
- I wrote the same program in C in a temporary folder outside the repository and
  compiled it with `cc hello.c -o hello`. The result was a 33432-byte file called
  `hello`, with permissions starting `-rwxr-xr-x`, and `file hello` said
  `Mach-O 64-bit executable arm64`. I ran `./hello` and it printed
  `Hello from C`, with no separate interpreting step anywhere.

I deleted the temporary C folder after copying the output into the evidence file.
Nothing compiled was left inside the repository, and `__pycache__` is ignored by
Git.

### Task 4.2 — Compiler versus interpreter

| Point | Compiler | Interpreter |
|---|---|---|
| When translation happens | First, once, before the program runs. Running it is a separate step later. | While the program runs, usually one statement at a time. |
| Typical output | A new file the computer can run directly. My C build produced a 33432-byte `hello` executable. | No runnable file. The program just prints its output, and nothing usable is left behind apart from possible cache files. |
| One example | C, compiled with `cc` or `gcc`. I used Apple clang 21.0.0. | Python, run with `python3`. |
| One advantage | Translation happens once, so the finished program never pays for it again, which usually makes it faster. Mistakes are also caught before the program ever runs. | A small change can be tested straight away with no build step, and when something breaks the error points at the exact line. |

In a few sentences: a compiler reads the whole source file and produces a
separate program, and only then do I run that program. An interpreter reads the
source and carries out the instructions as it goes, so it needs the source file
every time. The difference is easy to see in the folder. My C folder had a
33432-byte executable next to an 83-byte source file. Python left only a
155-byte `.pyc` cache and still needed `hello.py` to run. Most real languages
mix the two, and Python is the proof, because it compiles to bytecode first and
then runs that bytecode.

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `cat hello.py` | To show the program before running it. |
| `python3 --version` | To confirm the version, which was 3.14.7. |
| `python3 hello.py` | To run the program with Python 3. |
| `echo $?` | To check the exit status after the run. |
| `python3 -m py_compile hello.py` | To make Python produce its bytecode file, so I could see that compiling really happens. |
| `cc hello.c -o hello` | To compile a small C program for comparison. |
| `file hello` | To confirm the C output was a real executable. |
| VS Code | To write `hello.py`. |

## 4. My understanding

The file is not the thing that runs. It is text that has to be turned into
something the CPU can carry out. That translation is the whole difference
between a compiler and an interpreter. A compiler does the translation and saves
the result. An interpreter does it while the program runs.

What surprised me is that Python still compiles. The `.pyc` file is the
translated version, and Python reuses it until the source changes. So "Python is
interpreted" is a shortcut, not the truth. It compiles to bytecode, and the
Python virtual machine runs that bytecode.

The practical side matters too. In C I had to compile before I could run
anything, and a mistake stopped me at compile time. In Python I just run the
file and find out what breaks as it happens. That is why Python feels quicker
for small scripts, and probably why big programs are often written in compiled
languages.

## 5. Difficulties faced

- The table asked for "typical output" and I was not sure whether that meant
  what the compiler prints or what the program prints.
- I expected Python to leave no extra files behind, then found a `__pycache__`
  folder after one run.
- My first plan was to write the C comparison inside the mission folder, which
  would have left a compiled executable sitting in the repository.

## 6. How I resolved them

- I read it as the output of the translating tool, not the program, and wrote
  both into the table. The compiler gives you an executable. The interpreter
  gives you nothing you can run on its own.
- I looked inside `__pycache__` and found `hello.cpython-314.pyc`. That is
  compiled bytecode, so Python does compile, just not into a standalone program.
- I moved the C test to a temporary folder and saved only the text output. I also
  added a `.gitignore` with `__pycache__/` and `*.pyc` so build files cannot be
  committed by accident.

## 7. Evidence / files

- `mission-04-programs/hello.py` - the one-line Python program.
- `mission-04-programs/README.md` - this file with the comparison.
- `evidence/mission-04/program-run.txt` - the real output of both runs, with my
  account name shown as `student`.
- `.gitignore` - keeps Python cache files out of the repository.

## 8. Commit details

Commit message:

    Compare compilers and interpreters

Pushed to `main` on GitHub.
