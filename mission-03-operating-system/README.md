# Mission 3 — Understand the operating system

## 1. Task / objective

Find out what operating system my Mac is running, which account is active, how
much storage is left, and what is running in the background. Then look at paths
and file permissions, and explain what an operating system is actually
responsible for.

## 2. Work completed

I ran the Terminal commands listed below and wrote down what each result meant.
My username has been replaced with `[redacted]` everywhere, and I did not copy
any device name, serial number or network address into the repository.

### Task 3.1 — Exploring my operating system

| Information explored | What it tells you | My observation (privacy-safe) |
|---|---|---|
| Operating system / system details | Which OS and version is installed, and which kernel it runs on. | macOS 27.2, build 26B123. The kernel is Darwin 27.2.0. The boot volume is named Macintosh HD and the Mac had been running for 6 days and 1 hour at the time I checked. |
| Current account identity | Which user account the Terminal is acting as, and that account's numeric ID. | `whoami` and `id -un` both returned my username, which I have replaced with `[redacted]`. `id -u` returned 501. |
| Available and used storage | Total size of the disk, how much is used, how much is free, and the percentage full. | The data volume is 460 GB in total, 294 GB used, 120 GB available, 71 per cent full. |
| System activity snapshot | How many processes exist, how busy the CPU is, and how memory is being used. | `ps -A` listed 575 lines including the header. `top` showed 568 processes, 2 running and 566 sleeping, with 3975 threads. CPU was 18.71 per cent user, 15.50 per cent system and 65.77 per cent idle. Memory: 15 GB used, 181 MB unused. |

Two things worth writing down from this: `ps` and `top` did not agree on the
number of processes (575 against 568). That is because the list changes between
the two commands, and `top` had already been running for a moment when it
counted. Neither number is wrong.

`df -h /` showed only 13 GB used, while `/System/Volumes/Data` showed 294 GB
used. On macOS these are two volumes that share the same free space: one holds
the protected system files, the other holds my files and apps. Reading only the
first one would have made the disk look almost empty.

### Task 3.2 — Processes

**What is a process?** A process is a program that is currently running. The
file on disk is just instructions. Once macOS loads it into memory and starts
executing it, it becomes a process with its own process ID, its own memory and
its own state.

**What does the PID column represent?** PID means process identifier. It is the
unique number the operating system gives to each running process so that it can
track it. When I ran `echo $$`, the shell printed `84183`, and
`ps -p 84183 -o pid,ppid,comm` showed that exact process as `/bin/zsh`. The PPID
column next to it is the parent process ID, which is the process that started
this one.

**Two examples of processes that may be running:**

1. `/sbin/launchd` with PID 1. This is the first process macOS starts, and every
   other process is started either by it or by something it started.
2. `/Applications/Visual Studio Code.app/.../chrome_crashpad_handler` with
   PID 51853. That is a background helper that belongs to VS Code, which was
   open at the time.

A background process like the VS Code helper explains something I had not
thought about before: closing an app's window does not always end every process
that belongs to it.

### Task 3.3 — Paths and permissions

Moving between the repository folder and one of its subfolders changed the
output of `pwd` exactly as expected: from
`.../digital-detective-8019/mission-02-terminal` down into
`.../mission-02-terminal/terminal-practice`.

**Absolute path.** A full address that starts from the top of the disk and
works every time, no matter where I currently am. Example from my assignment
folder:

    /Users/[redacted]/Desktop/SNAI/digital-detective-8019/mission-02-terminal/terminal-practice/notes.txt

**Relative path.** An address that starts from the folder I am standing in.
Example, while I am already inside `digital-detective-8019`:

    mission-02-terminal/terminal-practice/notes.txt

The same file, two ways of writing it. The absolute path is longer but it does
not depend on where I start. The relative path is shorter but wrong if I run it
from a different folder.

**Permissions on a file in my practice area.** I checked the file
`mission-02-terminal/terminal-practice/notes.txt`:

    -rw-r--r--@ 1 [redacted] staff 84 14 Nov 17:47 .../notes.txt

Reading the first block from left to right:

- `-` means it is a normal file, not a folder.
- `rw-` is the owner, me. I can read it and write to it, but not execute it.
- `r--` is the group, `staff`. Read only.
- `r--` is everyone else. Read only.

So the owner can read and write the file but cannot execute it. That makes sense
for a text file. The `@` at the end means macOS is storing extra metadata on the
file, which on this laptop comes from files created through the Desktop folder.

For comparison, the practice folder itself was `drwxr-xr-x`: the `d` means
directory, and the owner has `rwx`, so I can enter the folder as well as list
and change things inside it. On a folder, the `x` permission means "allowed to
go into it", not "allowed to run it".

| Permission | Meaning | Example |
|---|---|---|
| r - Read | Allows a file's contents to be read. | Opening a text file, or `cat notes.txt`. |
| w - Write | Allows a file to be changed. | Editing the file, or `echo "text" >> notes.txt`. |
| x - Execute | Allows a file to be run. On a folder, it allows access or traversal into it. | Running a Python script, or `cd` into a folder. |

I did not change any permissions on any file, inside or outside the repository.

### Task 3.4 — What the operating system is responsible for

| OS responsibility | My explanation | Example |
|---|---|---|
| Process management | Decides which running program gets the CPU and for how long, starts processes and stops them when they finish. | `top` showed 2 processes running and 566 sleeping. The CPU can only run a few at a time, so macOS keeps switching between them. |
| Memory management | Hands out RAM to programs and takes it back when they close, and uses the disk as extra memory when RAM runs out. | `top` showed 15 GB used and only 181 MB unused, with 4450 MB in the compressor. That is macOS squeezing memory instead of letting the Mac slow to a stop. |
| Device management | Talks to the hardware through drivers so programs do not have to know how each device works. | The keyboard, trackpad, display and SSD all work without VS Code knowing anything about them. |
| File management | Keeps the folder structure, tracks where each file is stored, and enforces who may read or write it. | `pwd`, `ls` and `mkdir` are all requests to the file system. A permission change on a file is enforced here. |
| User interface / shell | Gives me a way to give instructions: a graphical interface with windows and icons, or a shell like zsh where I type commands. | Finder is the graphical side. The Terminal window running zsh is the command-line side. Both are talking to the same operating system. |
| Security and permissions | Makes sure a normal user cannot damage system files or read another user's data, and asks for a password for anything that needs more power. | The system volume is separate from my data volume and is protected. `[redacted]` owns my files but not the system files, and `sudo` is needed for those. I did not use `sudo` for this assignment. |

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `sw_vers` | Shows the macOS product name, version and build. |
| `uname -sr` | Shows the kernel name and release (Darwin 27.2.0). |
| `system_profiler SPSoftwareDataType` | Shows a longer software summary including boot volume and uptime. |
| `whoami`, `id -u`, `id -un` | Shows which account I am using and its numeric ID. |
| `df -h` | Shows total, used and free disk space in a readable form. |
| `ps -A`, `ps -A -o pid,ppid,comm` | Lists running processes, optionally with chosen columns. |
| `echo $$` | Prints the PID of the current shell. |
| `ps -p <pid> -o pid,ppid,comm` | Shows details for one specific process. |
| `top -l 1 -n 5 -o cpu` | Takes one snapshot of system activity, sorted by CPU use. |
| `ls -l`, `ls -ld` | Shows permissions for a file, or for a folder itself. |
| `stat -f "..."` | Prints the permission string, owner and size of a file. |

## 4. My understanding

The operating system is the layer that stands between the programs and the
hardware. My Python program does not know what kind of SSD is installed. It asks
the operating system to write a file, and macOS handles the rest. That is the
main idea I took from this mission.

Processes and memory are connected. Every process needs memory, and every
process has a PID so the OS can find it again. When I looked at `top` and saw
15 GB used out of 16 GB with only 181 MB unused, my laptop looked almost out of
memory, yet it was still working normally. The compressor figure explains why:
macOS compresses memory instead of failing.

Permissions made more sense once I read the string as three groups of three
instead of one long word. Owner, group, everyone. Each group gets read, write
and execute in that fixed order.

Paths are the same address written two ways. That is why the same command can
work in one Terminal window and fail in another: the relative path is being
resolved from a different place.

## 5. Difficulties faced

- `df -h /` and `df -h /System/Volumes/Data` gave completely different "used"
  numbers for a disk that is supposed to be one disk.
- I did not know why `ps -A` showed 575 lines and `top` showed 568 processes.
- I confused PID with PPID for a while when reading `ps -p`.
- I had to be careful with the outputs, because `whoami` and `ps` print my
  username by default.

## 6. How I resolved them

- I read the "Mounted on" column and realised `/` and
  `/System/Volumes/Data` are two different volumes that share the same free
  space. The system volume only holds macOS itself, so it looks nearly empty.
- I accepted that the two numbers were taken at different moments. `top` counts
  again after it starts, and processes open and close constantly.
- I looked at the two columns side by side. PID is the process itself, PPID is
  the process that started it. For my shell, PID was 84183 and PPID was 18783.
- I saved the real output to a file first, replaced my username with
  `[redacted]`, and only then wrote the notes. I also left out the computer name
  and the serial number, which `system_profiler` shows by default.

## 7. Evidence / files

- `mission-03-operating-system/README.md` - this file.
- `evidence/mission-03/system-observations.txt` - the real command output with
  the username replaced by `[redacted]` and no device name or serial number.

## 8. Commit details

Commit message:

    Document operating system and file management

Pushed to `main` on GitHub.
