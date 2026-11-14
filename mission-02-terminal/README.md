# Mission 2 — Become comfortable with the Terminal

## 1. Task / objective

Use the Terminal instead of Finder to look around the folder, create files,
change them, copy them, move them and read them. Then understand what flags do,
how a pipe works, and what a package manager is for.

All the practice happened inside `mission-02-terminal/terminal-practice`, so
nothing outside the assignment repository was touched.

## 2. Work completed

- Opened Terminal inside the repository and used `pwd` to confirm the location.
- Created the `terminal-practice` folder and moved into it.
- Created `notes.txt` with `touch`, then wrote one line into it, then added a
  second line without losing the first.
- Made a copy with `cp` and renamed the copy with `mv`.
- Wrote a separate `demo.txt` to compare `>` with `>>` on a file that already
  had text in it.
- Moved between folders using both a relative path (`cd ..`) and an absolute
  path (`cd ~/Desktop/...`).
- Compared `ls`, `ls -l`, `ls -a`, `ls -lh` and `ls -lah` in the same folder at
  the same moment.
- Sent a detailed listing into `head` with a pipe.
- Checked that Homebrew was already installed, noted its version, and counted
  the packages it manages.

The full transcript is saved in `evidence/mission-02/terminal-session.txt` with
my username replaced by `[redacted]`.

### Task 2.1 — Basic Terminal operations

| Operation / command name | What it does | What I observed |
|---|---|---|
| Current-directory display: `pwd` | Prints the full path of the folder I am standing in. | It printed `/Users/[redacted]/Desktop/SNAI/digital-detective-8019/mission-02-terminal/terminal-practice`, which is the whole path from the top of the disk. |
| Directory listing: `ls` | Lists the files and folders in the current location. | In an empty folder it printed nothing at all. After `touch` it printed `notes.txt`. |
| Detailed listing: `ls -l` | Lists the same items in columns with permissions, owner, size, date and name. | First line was `total 0` in the empty folder, then `-rw-r--r--@ 1 [redacted] staff 0 14 Nov 17:47 notes.txt`. The `0` is the size in bytes. |
| Change directory: `cd ..` | Moves up one folder. | `pwd` changed from `.../mission-02-terminal/terminal-practice` to `.../mission-02-terminal`. |
| Create directory: `mkdir terminal-practice` | Creates a new folder. | It created the folder with no message. Running `ls` in the parent folder showed it. |
| Create empty file: `touch notes.txt` | Creates an empty file, or updates the date on an existing file. | It appeared in `ls -l` with size `0`. |
| Copy file: `cp notes.txt notes-copy.txt` | Makes a second file with the same contents. | After the copy, `ls -l` showed two files with the same size, 84 bytes each. |
| Move / rename file: `mv notes-copy.txt backup-day1.txt` | Moves a file to another place, or renames it if only the name changes. | `notes-copy.txt` was gone and `backup-day1.txt` was there instead, with the same 84 bytes. No new file was created. |
| Display file contents: `cat notes.txt` | Prints the whole file into the Terminal. | It printed both lines in the order I added them. |

### Task 2.2 — File changes done safely

I created `notes.txt`, added `Line one: this is my first line of text.`, then
added `Line two: added without removing line one.` with `>>`. `cat` showed both
lines. Then I copied it to `notes-copy.txt` and renamed the copy to
`backup-day1.txt`.

Answers to the four questions:

**Replacing a file's contents versus adding to the end.** A single `>` sends
output to the file and throws away whatever was there before. A double `>>`
adds to the end and keeps the old text. I tested this on `demo.txt`. The first
write gave `first version of this file`. The second write with `>` left only
`second version, written with a single >`, so the first line was gone. The third
write with `>>` kept the second line and added the new one under it.

**Copying versus moving.** `cp` leaves the original where it is and makes a
second file, so there are two files afterwards and both take up space. `mv`
takes the file away from the old name and puts it under the new one, so there is
still only one file. `mv` does not need to copy anything, which also means it is
much faster when the file is large.

**What the current-directory display gives me.** `pwd` tells me exactly where I
am, as a full path. This matters because most commands work on "the folder I am
in right now", so a wrong location means the command runs somewhere I did not
intend. When `cat notes.txt` worked but `ls` in the parent folder did not show
`notes.txt`, `pwd` was how I understood why.

**Why a directory listing is useful.** It shows what is actually there instead
of what I remember being there. I used it after every change to confirm the
result: after `touch` to check the file was created, after `cp` to see two files,
and after `mv` to see the old name disappear.

### Task 2.3 — Flags and pipes

All five listings below were run in the same folder at the same moment, so the
only thing that changes is the flag.

| Command | What changed |
|---|---|
| `ls` | Just the names: `backup-day1.txt`, `demo.txt`, `notes.txt`. |
| `ls -l` | Same three names, but in columns with permissions, owner, group, size, date and time. |
| `ls -a` | Added two extra entries, `.` and `..`. These are the current folder and the parent folder. They are always there but hidden by default. |
| `ls -lh` | Same as `-l`, but the size column became `84B` and `66B` instead of `84` and `66`. The `h` means human readable. It makes no visible difference at this size because the files are only bytes, but on a big file it would show `2.1M` instead of a long number. |
| `ls -lah` | Combined all three. The `.` and `..` lines appeared and were shown as `160B` and `128B`, and every line started with `d` or `-` to show folder or file. |

One thing I did not expect: the `total 24` line at the top of `ls -l` is not
the number of files and it is not the total size in bytes. It is the amount of
disk space the listed files are using, counted in 512-byte blocks by macOS.
Three files of 84, 66 and 84 bytes came to 24 blocks because each file takes a
whole block.

For the pipe I ran:

    ls -l | head -4

The `ls -l` on the left produced the detailed listing. The pipe symbol `|`
took that output and passed it into `head -4` instead of printing it on screen.
The `head -4` on the right kept only the first four lines: the `total 24` line
and the first three files. So each side has one job. The left side makes the
output and the right side decides what to do with it. Nothing is written to a
file, the output just goes into the next command.

### Task 2.4 — Package managers

Homebrew was already installed at `/opt/homebrew/bin/brew`, version 7.0.10. It
manages 186 formulae and 13 casks on this Mac.

Package managers are useful because they install software and also keep track of
what was installed, so updating everything is one command instead of visiting
each website again. They also check that the version I am installing matches the
system, which is why I did not have to worry about the Apple Silicon build of a
tool. I did not install or remove anything for this mission.

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `pwd` | To see the exact folder I was in. |
| `ls`, `ls -l`, `ls -a`, `ls -lh`, `ls -lah` | To list files, with different levels of detail. |
| `cd`, `cd ..`, `cd ~/...` | To change folder using a relative or an absolute path. |
| `mkdir terminal-practice` | To create the practice folder. |
| `touch notes.txt` | To create an empty file. |
| `echo "..." > file` | To write text into a file, replacing what was there. |
| `echo "..." >> file` | To add text to the end of a file. |
| `cat notes.txt` | To read the file back. |
| `cp` | To make a copy. |
| `mv` | To rename or move a file. |
| `head -4` | To show only the first lines of output. |
| `which brew`, `brew --version`, `brew list --formula`, `brew list --cask` | To check the package manager without changing anything. |

## 4. My understanding

The Terminal is not a different computer, it is a different way of asking for
the same work. Finder shows me a picture of the files and I click them. The
Terminal takes one line of text, does exactly that one thing, and prints the
result or nothing at all.

The part that clicked for me was that a command, a flag and a target are three
separate pieces: `ls` is the command, `-l` changes how it behaves, and the
folder or file is what it works on.

Relative and absolute paths finally made sense from the `cd` test. `cd ..` only
means "up one level from wherever I am", so it gives a different result
depending on the starting point. `cd ~/Desktop/SNAI/...` means the same folder
no matter where I start. That is also why a script with relative paths behaves
differently depending on the folder it is run from.

`>` and `>>` are the most dangerous thing I practised, because a single wrong
character silently destroys text with no warning and no undo in the Terminal.
`cp` before editing is a cheap way to avoid losing work, which is why I made a
backup file in this mission.

## 5. Difficulties faced

- I wrote to `demo.txt` with `>` a second time and lost the first line. I did
  it on purpose to see the difference, but it showed how easy the mistake is.
- `ls -a` showed `.` and `..` and I did not know what they were at first.
- I expected one command called "rename" and could not find one. `mv` looked
  like it only moved files into folders.
- I did not know what `total 24` meant in the `ls -l` output.
- I was not sure whether `touch` on a file that already had text would erase it.

## 6. How I resolved them

- I ran `cat` after each write so I could see exactly what `>` and `>>` did.
  After the overwrite test only one line was left, which proved `>` replaces.
- I read `.` and `..` as "here" and "one level up". `ls -lah` showed both of
  them starting with `d`, which confirmed they are folders.
- I tried `mv notes-copy.txt backup-day1.txt` and saw that the old name vanished.
  A rename is just a move to the same folder with a different name.
- I worked out the `total` line by adding the three file sizes and noticing the
  number did not match, then checking that macOS counts disk blocks. It is not
  the number of files.
- I ran `touch notes.txt` on the file that had two lines and then `cat` again.
  Both lines were still there, so `touch` only changes the date on an existing
  file.

## 7. Evidence / files

- `mission-02-terminal/README.md` - this file.
- `mission-02-terminal/terminal-practice/notes.txt` - the two-line file I made.
- `mission-02-terminal/terminal-practice/backup-day1.txt` - the copy I renamed.
- `mission-02-terminal/terminal-practice/demo.txt` - the overwrite versus append
  test file.
- `evidence/mission-02/terminal-session.txt` - the real session output, with the
  username replaced by `[redacted]`.

## 8. Commit details

Commit message:

    Complete Terminal and file management mission

Pushed to `main` on GitHub.
