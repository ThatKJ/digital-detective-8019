# Mission 1 — Know your computer

## 1. Task / objective

Explain how a computer takes input, processes it, gives output and stores the
result. Do this for one real activity I do on my laptop. Then list hardware and
software I actually use, and describe three computer-based systems I see in
daily life that are not a laptop or a phone.

The four stages are called IPOS: Input, Processing, Output, Storage.

## 2. Work completed

I completed the three tables for Tasks 1.1, 1.2 and 1.3, plus a short
explanation under each one.

Before writing the tables I ran `system_profiler` so the hardware details were
my real laptop's and not guessed. My laptop is a MacBook Pro (Mac17,2) with an
Apple M5 chip, 10 CPU cores and 16 GB of memory. The SSD shows about 460 GB
total space with roughly 120 GB free.

### Task 1.1 — One activity traced through IPOS

The activity I chose is writing a document in VS Code and saving it. This is
exactly what I did while writing this README, so I could watch each stage
happen.

| Stage | What happens in my example | Hardware / component |
|---|---|---|
| Input | I press keys to type letters. The trackpad is used when I click to move the cursor or select text. | Keyboard and trackpad |
| Processing | The M5 chip runs VS Code, decides which character was pressed, and updates the document. The text I have typed but not saved sits in RAM. | CPU (Apple M5) and RAM |
| Output | The letters appear on the screen as I type. The cursor moves and the line numbers change. | Built-in display |
| Storage | When I press Command+S, the file is written to the SSD so it is still there after I close the editor or shut down. | 460 GB SSD |

Extra step for this activity: the file is saved inside the Git repository, so
`git add` and `git commit` record a second copy of the change in the `.git`
folder.

How the activity moves through the stages: my fingers create input, the
processor turns that input into changes in the document while it is open in
memory, the screen shows me the result immediately, and saving copies the
finished file onto the disk. Input and output happen constantly while I type,
but storage only happens when I save.

### Task 1.2 — Hardware and software I use

| Item / software name | Hardware or software? | Software type | Purpose |
|---|---|---|---|
| MacBook keyboard | Hardware | Not applicable | Types text and runs shortcuts like Command+S |
| Trackpad | Hardware | Not applicable | Moves the pointer and clicks |
| Built-in display | Hardware | Not applicable | Shows the screen output |
| Apple M5 chip | Hardware | Not applicable | Runs the instructions of every program |
| SSD | Hardware | Not applicable | Keeps files when the laptop is switched off |
| macOS 27.2 | Software | Operating system software | Manages the hardware, files, memory and running apps |
| VS Code | Software | Application software | Writing and editing code and text files |
| Safari | Software | Application software | Browsing websites |
| Homebrew | Software | Utility software | Installs and updates other software from Terminal |
| Activity Monitor | Software | Utility software | Shows running processes and memory or CPU usage |

The difference I understood: the operating system is the layer between me and
the hardware. Applications are the programs I open to do a task. Utility
software does not do my work for me, it looks after the computer itself.

### Task 1.3 — Computer systems around me

| System | Main purpose | One input | One output |
|---|---|---|---|
| ATM | Lets a bank customer withdraw cash and check the balance without going to a counter | ATM card and the PIN typed on the keypad | Cash from the slot and a printed receipt |
| Smart TV | Plays streaming apps, cable channels and screen mirroring | Remote control buttons or a voice command | Picture on the screen and sound from the speakers |
| Metro ticket machine | Sells tickets or tokens at a station | Touchscreen selection and the payment (card or cash) | Printed ticket or token and the amount shown on screen |

How I would explain these in class: an ATM is a small computer with a card
reader, a keypad, a screen, a cash dispenser and a printer. The card and PIN are
input, the bank's computer checks the PIN during processing, and cash plus a
receipt are output. A smart TV is a computer built around a large display, so
its main output is the picture and sound. A metro ticket machine is input and
output almost only: it takes my choice through the touchscreen and gives me a
printed ticket.

## 3. Commands / tools used

| Command or tool | Purpose |
|---|---|
| `system_profiler SPHardwareDataType` | Shows the model, chip, number of cores and memory of my Mac, so the hardware table is accurate. |
| `df -h /` | Shows total and free disk space. |
| VS Code | Used to write the tables and the explanations. |

The real output, with the serial number, hardware UUID and UDID removed, is in
`evidence/mission-01/hardware-summary.txt`.

## 4. My understanding

A computer is not doing four separate jobs one after another. It is doing them
in a loop. Every key press is a tiny input, then processing, then output, and
the loop starts again before my finger is off the key.

Memory and storage are not the same thing, and this was the part I had to think
about. RAM holds the document while I am working on it, and it is fast but it is
emptied when the app closes. The SSD keeps the file after everything is switched
off, and it is slower than RAM. That is why an unsaved document can be lost in a
power cut even though the laptop has plenty of free disk space.

Input and output devices are not fixed either. A touchscreen is both. On my
laptop the display is output only, but the trackpad is input only.

Why this matters: once I could see the four stages, a lot of ordinary problems
made sense. A laptop that is slow but has 120 GB free is short of memory, not
storage. A file that disappears after a restart was never stored.

## 5. Difficulties faced

- I was not sure whether saving belongs to "output" or "storage". At first I
  wrote the file save as output.
- I could not remember the difference between the M5 chip and RAM until I looked
  at what each one does while a program is running.
- For a while I mixed up operating system software and utility software,
  because both seem to "manage" the computer.

## 6. How I resolved them

- I settled it by asking what I can actually see. The visible file appearing on
  screen is output. Writing the bytes to the SSD is storage. Saving does both,
  so I listed it under storage and mentioned the screen update in output.
- I compared them directly: the chip carries out instructions, RAM holds the
  data those instructions are working on right now. One is the worker, the other
  is the desk.
- I used the definitions given in the assignment. The operating system manages
  the whole machine and is needed for anything to run. A utility is an extra
  program that maintains the machine, like Homebrew or Activity Monitor. macOS
  would still start without Homebrew, so Homebrew is a utility.

## 7. Evidence / files

- `mission-01-computer-basics/README.md` - this file with all three tables.
- `evidence/mission-01/hardware-summary.txt` - real hardware and disk output,
  with serial number, hardware UUID and UDID removed.

## 8. Commit details

Commit message:

    Complete computer basics and IPOS mission

Pushed to `main` on GitHub.
