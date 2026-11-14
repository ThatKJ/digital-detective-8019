# Mission 3 — Understand the operating system

## 1. Task / objective

Find out what operating system my Mac is running, which account I am logged in
as, how full the disk is, and what is running in the background. Then look at
paths and file permissions, and explain what an operating system is actually
responsible for.

## 2. Work completed

I ran the commands below and wrote down what each result meant. My account name
appears as `student` everywhere, and no device name, serial number or network
address went into the repository.

### Task 3.1 — Exploring my operating system

| What I looked at | What it tells you | What I actually saw |
|---|---|---|
| System and kernel details | Which OS and version is installed, and what it is built on. | macOS 27.2, build 26B123. It runs on the Darwin 27.2.0 kernel. The boot volume is called Macintosh HD. At the time I checked, the Mac had been up for 6 days, 1 hour and 3 minutes. |
| Who I am logged in as | Which account the Terminal is acting for, and that account's number. | `whoami` and `id -un` both gave my account name, shown as `student` here. `id -u` gave `501`. |
| Disk space | How big the disk is, how much is used, how much is free, and how full that is in percent. | 460 GB total, 294 GB used, 120 GB free, 71 per cent full. |
| What is running | How many processes exist, how busy the CPU is, how memory is being used. | `ps -A` printed 575 lines including the header. `top` showed 568 processes, 2 running and 566 sleeping, with 3975 threads. CPU was 18.71 per cent user, 15.50 per cent system, 65.77 per cent idle. Memory: 15 GB used, 181 MB free. |

Two of these numbers did not agree. `ps` counted 575 and `top` counted 568. That
is not a mistake in either one. Processes start and finish all the time, `top`
takes a moment to settle before it counts, and the two commands ran a few
seconds apart.

### Task 3.2 — Processes

**What a process is.** A process is a program that is actually running. The file
sitting on disk is just a set of instructions. When macOS loads it into memory
and starts working through it, it becomes a process with its own ID, its own
memory and its own state.

**What the PID column means.** PID stands for process identifier. It is the
number the operating system hands to each running process so it can find it
again later. I ran `echo $$` and got `84183`. Then
`ps -p 84183 -o pid,ppid,comm` showed that exact process was `/bin/zsh`, which
is the shell I was typing into. The PPID next to it is the parent process ID, the
process that started this one. For my shell that was `18783`.

**Two processes that were running:**

1. `/sbin/launchd` with PID 1. This is the first thing macOS starts, and
   everything else comes from it or from something it started.
2. `/Applications/Visual Studio Code.app/.../chrome_crashpad_handler` with PID
   51853. A background helper that belongs to VS Code, which was open at the
   time.

That second one made me think. I had closed VS Code windows before and assumed
the app was finished. Clearly it was not.

### Task 3.3 — Paths and permissions

Walking between the repository folder and one of its subfolders changed what
`pwd` printed, exactly as I expected. It went from
`.../digital-detective-8019/mission-02-terminal` down to
`.../mission-02-terminal/terminal-practice`.

**Absolute path.** A full address that starts at the top of the disk. It works
from anywhere. Example from my assignment folder:

    /Users/student/Desktop/SNAI/digital-detective-8019/mission-02-terminal/terminal-practice/notes.txt

**Relative path.** An address that starts from the folder I am standing in.
Same file, written while I am already inside `digital-detective-8019`:

    mission-02-terminal/terminal-practice/notes.txt

Longer but reliable, or shorter but fragile. That is the whole trade-off.

**Permissions on a file I made.** I ran `ls -l` on the notes file:

    -rw-r--r--@ 1 student staff 84 14 Nov 17:47 .../notes.txt

Read it left to right:

- `-` means a normal file, not a folder.
- `rw-` is the owner, which is me. I can read and write it, but not run it.
- `r--` is the group, `staff`. Read only.
- `r--` is everyone else. Read only.

So I can read and change the file, but nothing can execute it. For a text file
that is right. The `@` at the end means macOS is keeping extra metadata on it,
which happens to files made through the Desktop folder.

The folder itself was different: `drwxr-xr-x`. The `d` says directory, and the
owner has `rwx`. On a folder the `x` does not mean "run it", it means "allowed to
go inside it".

| Permission | What it allows | Example |
|---|---|---|
| r — read | Reading a file's contents. | Opening a text file, or running `cat notes.txt`. |
| w — write | Changing a file. | Editing it, or `echo "text" >> notes.txt`. |
| x — execute | Running a file. On a folder, going into it. | Running a Python script, or `cd` into a folder. |

I did not change permissions on anything, inside the repository or outside it.

### Task 3.4 — What the operating system is responsible for

| Responsibility | My explanation | Example from this Mac |
|---|---|---|
| Process management | Decides which running program gets the CPU and for how long, starts them and stops them. | `top` showed 2 processes running and 566 sleeping. The CPU cannot run them all at once, so macOS keeps swapping between them. |
| Memory management | Hands RAM out to programs, takes it back when they close, and uses the disk as overflow when RAM runs low. | `top` showed 15 GB used and only 181 MB free, with 4450 MB sitting in the compressor. macOS was squeezing memory rather than letting the Mac grind to a halt. |
| Device management | Talks to the hardware through drivers, so programs do not need to know how each device works. | The keyboard, trackpad, screen and SSD all work without VS Code knowing anything about them. |
| File management | Keeps the folder structure, tracks where each file lives, and enforces who may read or write it. | `pwd`, `ls` and `mkdir` are all requests to the file system. So is a permission check. |
| User interface and shell | Gives me a way to give instructions, either with windows and icons or by typing. | Finder is the graphical side. The Terminal running zsh is the typed side. Both talk to the same operating system. |
| Security and permissions | Stops a normal user from damaging system files or reading someone else's data, and asks for a password when more power is needed. | The system volume is kept separate from my data volume. `student` owns my files but not the system ones, and `sudo` is needed for those. I did not use `sudo` in this assignment. |

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `uname -sr` | Shows the kernel name and release. |
| `whoami`, `id -u`, `id -un` | Shows which account I am using and its number. |
| `echo $$` | Prints the PID of the shell I am typing in. |
| `top -l 1 -n 5 -o cpu` | Takes one snapshot of system activity, sorted by CPU use. |
| `ls -l`, `ls -ld` | Shows permissions on a file, or on a folder itself. |

## 4. My understanding

The operating system is the thing standing between my programs and the
hardware. My Python program does not know what kind of SSD is in this laptop. It
asks macOS to write a file and macOS deals with the rest. That is the main idea
I came away with.

Processes and memory are tied together. Every process needs memory, and every
process has a PID so the system can find it again. When `top` said 15 GB used
out of 16 GB with almost nothing free, I expected the Mac to be crawling. It was
fine. The compressor number is the reason.

Permissions only made sense once I read the string as three groups of three
instead of one long word. Owner, group, everyone. Each group gets read, write and
execute, always in that order.

Paths are one address written two ways, which explains a lot of confusing
errors. The same command can work in one Terminal window and fail in another
because the relative path is being resolved from a different place.

## 5. Difficulties faced

- `ps -A` gave 575 lines and `top` gave 568, for the same computer at nearly the
  same time.
- I kept mixing up PID and PPID when reading the `ps` output.
- I thought `x` on a folder meant something could be executed from it.
- I had to be careful with the output, because `whoami` and `ps` print my account
  name without being asked.

## 6. How I resolved them

- I decided the two numbers were taken at different moments and that processes
  open and close constantly. Neither tool was wrong.
- I put the two columns side by side. PID is the process itself, PPID is the one
  that started it. Mine were 84183 and 18783.
- Reading `drwxr-xr-x` on a folder and then successfully `cd`-ing into it showed
  me what `x` means there. It is permission to pass through.
- I saved the real output to a file first, replaced my account name with
  `student`, and wrote the notes afterwards. I also left out the computer name
  and the serial number, which the system tools print by default.

## 7. Evidence / files

- `mission-03-operating-system/README.md` - this file.
- `evidence/mission-03/system-observations.txt` - the real command output, with
  my account name shown as `student`, and no device name or serial number.

## 8. Commit details

Commit message:

    Document operating system and file management

Pushed to `main` on GitHub.
