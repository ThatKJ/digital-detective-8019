# Mission 2 — Become comfortable with the Terminal

## 1. Task / objective

Do in the Terminal what I normally do in Finder. Look around a folder, make
files, change them, copy them, move them and read them back. Then work out what
flags do, how a pipe works, and what a package manager is for.

I did all of it inside `mission-02-terminal/terminal-practice`, so nothing
outside the assignment folder got touched.

## 2. Work completed

- Opened Terminal in the repository and ran `pwd` to check where I was.
- Made the `terminal-practice` folder and went into it.
- Made `notes.txt` with `touch`, wrote one line into it, then added a second
  line without losing the first one.
- Copied it with `cp` and renamed the copy with `mv`.
- Made a separate `demo.txt` so I could see `>` and `>>` side by side on a file
  that already had text in it.
- Went up one level with `cd ..` and came back down with a full absolute path,
  so I could feel the difference.
- Compared `ls`, `ls -l` and `ls -a` on the same folder.
- Pushed a listing into `head` with a pipe.
- Checked that Homebrew was already installed, noted the version, and counted
  what it manages.

The real session output is in `evidence/mission-02/terminal-session.txt`. My
account name shows up as `student` in that file.

### Task 2.1 — Basic Terminal operations

| Command | What it does | What I saw |
|---|---|---|
| `pwd` | Prints the full path of the folder I am standing in. | It printed `/Users/student/Desktop/SNAI/digital-detective-8019/mission-02-terminal/terminal-practice`. That is the whole path from the top of the disk right down to the folder. |
| `ls` | Lists what is in the current folder. | Empty folder, so it printed nothing at all. After `touch` it printed `notes.txt`. |
| `ls -l` | Lists the same items but in columns, with permissions, owner, group, size, date and name. | In the empty folder the first line was `total 0`. After `touch`: `-rw-r--r--@ 1 student staff 0 14 Nov 17:47 notes.txt`. The `0` is the size in bytes. |
| `cd ..` | Moves me up one folder. | `pwd` changed from `.../mission-02-terminal/terminal-practice` to `.../mission-02-terminal`. |
| `mkdir terminal-practice` | Makes a new folder. | It made the folder and said nothing. `ls` in the parent folder showed it. |
| `touch notes.txt` | Makes an empty file, or updates the date on one that exists. | It showed up in `ls -l` with size `0`. |
| `cp notes.txt notes-copy.txt` | Makes a second file with the same contents. | After the copy, `ls -l` showed two files and both were 84 bytes. |
| `mv notes-copy.txt backup-day1.txt` | Moves a file somewhere else, or renames it if the folder stays the same. | `notes-copy.txt` was gone and `backup-day1.txt` was there instead, still 84 bytes. No new file appeared. |
| `cat notes.txt` | Prints the whole file into the Terminal. | It printed both lines, in the order I added them. |

### Task 2.2 — File changes done safely

I made `notes.txt`, wrote `Line one: this is my first line of text.` into it,
then added `Line two: added without removing line one.` with `>>`. `cat` showed
both lines. Then I copied it and renamed the copy to `backup-day1.txt`.

**Replacing contents versus adding to the end.** One `>` sends output into the
file and throws away whatever was there. Two, `>>`, adds to the end and keeps
the old text. I tested this on `demo.txt`. First write gave me
`first version of this file`. Second write with `>` left only
`second version, written with a single >`, so the first line was gone. Third
write with `>>` kept that line and put the new one under it.

**Copying versus moving.** `cp` leaves the original alone and makes a second
file, so afterwards there are two files and both take up space. `mv` takes the
file off the old name and puts it on the new one, so there is still only one.
Because `mv` does not duplicate anything, it is also much quicker on a big file.

**What `pwd` is actually for.** It tells me exactly where I am, as a full path.
Most commands work on "the folder I am in right now", so if I am in the wrong
place the command quietly does the wrong thing. That is how I worked out why
`cat notes.txt` worked but `ls` in the parent folder did not show the file.

**Why listing a folder is useful.** It shows what is really there, not what I
remember putting there. I ran it after every change: after `touch` to check the
file existed, after `cp` to see two files, after `mv` to see the old name gone.

### Task 2.3 — Flags and pipes

I ran three listings in the same folder, one after another, so the only thing
that changes is the flag.

| Command | What changed |
|---|---|
| `ls` | Just the names: `backup-day1.txt`, `demo.txt`, `notes.txt`. |
| `ls -l` | The same three names, but in columns with permissions, owner, group, size, date and time. |
| `ls -a` | Two extra entries appeared, `.` and `..`. Those are the current folder and the parent folder. They are always there, they are just hidden by default. |

One thing caught me out. The `total 24` line on top of `ls -l` is not the number
of files, and it is not the total size in bytes either. It is how much disk space
those files use, counted in 512-byte blocks. Three files of 84, 66 and 84 bytes
came to 24 blocks, because each file takes up a whole block even when it is
smaller than one.

For the pipe I ran:

    ls -l | head -4

`ls -l` on the left made the detailed listing. The `|` took that output and
handed it to `head -4` instead of printing all of it. `head -4` kept the first
four lines, which was the `total` line plus the first three files. So each side
has one job. The left side produces, the right side decides what to keep, and
nothing is written to a file.

### Task 2.4 — Package managers

Homebrew was already installed at `/opt/homebrew/bin/brew`, version 7.0.10. It
manages 186 formulae and 13 casks on this Mac.

The point of a package manager is that it installs software and also remembers
what it installed, so updating everything is one command instead of going back
to each website. It also picks the right build for my machine, which is why I
never had to think about the Apple Silicon version of anything. I did not
install or remove anything for this mission.

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `pwd` | To see the exact folder I was in. |
| `ls`, `ls -l`, `ls -a` | To list files, with different amounts of detail. |
| `cd`, `cd ..`, `cd ~/...` | To change folder with a relative or an absolute path. |
| `mkdir terminal-practice` | To make the practice folder. |
| `touch notes.txt` | To make an empty file. |
| `echo "..." > file` | To write text into a file and replace what was there. |
| `echo "..." >> file` | To add text to the end of a file. |
| `cat notes.txt` | To read the file back. |
| `cp` | To make a copy. |
| `mv` | To rename or move a file. |
| `head -4` | To show only the first few lines of output. |
| `which brew`, `brew --version`, `brew list --formula`, `brew list --cask` | To look at the package manager without changing anything. |

## 4. My understanding

The Terminal is not a different computer. It is a different way of asking for
the same work. Finder shows me a picture of the files and I click on them. The
Terminal takes one line of text, does that one thing, and prints the result or
prints nothing at all.

The part that clicked was that a command, a flag and a target are three separate
pieces. `ls` is the command, `-l` changes how it behaves, and the folder is what
it works on. Once I saw that, long commands stopped looking like one big word.

Paths made sense from the `cd` test. `cd ..` only means "up one level from
wherever I am", so it lands somewhere different depending on where I start.
`cd ~/Desktop/SNAI/...` means the same folder no matter where I start. That is
also why a script full of relative paths can behave differently on someone
else's machine.

`>` and `>>` are the most dangerous things I practised. One wrong character and
text is gone, with no warning and no undo. Copying a file before editing it
costs nothing and I did it here for that reason.

## 5. Difficulties faced

- I wrote into `demo.txt` with `>` a second time and lost the first line. I did
  it on purpose to see what happens, but it showed me how easy the mistake is.
- `ls -a` showed `.` and `..` and I did not know what they were.
- I went looking for a rename command and could not find one. `mv` sounded like
  it only moved files between folders.
- I could not work out what `total 24` meant.
- I was not sure whether `touch` would wipe a file that already had text in it.

## 6. How I resolved them

- I ran `cat` after every write, so I could see for myself what `>` and `>>`
  actually did instead of guessing.
- I read `.` as "here" and `..` as "one level up". That fits how `cd ..` behaves,
  which is how I convinced myself.
- I tried `mv notes-copy.txt backup-day1.txt` and watched the old name disappear.
  A rename is just a move that stays in the same folder.
- I added up the three file sizes and the number did not match the `total` line,
  so I looked it up and found macOS counts disk blocks.
- I ran `touch` on the file that already had two lines and read it back with
  `cat`. Both lines were still there, so `touch` only changes the date.

## 7. Evidence / files

- `mission-02-terminal/README.md` - this file.
- `mission-02-terminal/terminal-practice/notes.txt` - the two-line file I made.
- `mission-02-terminal/terminal-practice/backup-day1.txt` - the copy I renamed.
- `mission-02-terminal/terminal-practice/demo.txt` - the file I used to test
  `>` against `>>`.
- `evidence/mission-02/terminal-session.txt` - the real session output, with my
  account name shown as `student`.

## 8. Commit details

Commit message:

    Complete Terminal and file management mission

Pushed to `main` on GitHub.
