# Mission 1 — Know your computer

## 1. Task / objective

Explain how a computer takes input, processes it, gives output and stores the
result, using one real activity I do on my laptop. Then list the hardware and
software I actually use, and describe three computer-based systems I see in
daily life that are not a laptop or a phone.

The four stages have a name. IPOS stands for Input, Processing, Output and
Storage.

## 2. Work completed

I filled in the three tables for Tasks 1.1, 1.2 and 1.3 and wrote a short
explanation under each one.

Before writing any of it I ran `system_profiler`, so the hardware details were
from my own laptop instead of from a website. It is a MacBook Pro (Mac17,2) with
an Apple M5 chip, 10 CPU cores and 16 GB of memory. The disk shows about 460 GB
in total with around 120 GB free.

### Task 1.1 — One activity through IPOS

I picked typing a document in VS Code and saving it, because that is exactly
what I was doing while writing this file, so I could watch each stage happen.

| Stage | What happens in my example | Which part does it |
|---|---|---|
| Input | I press keys to type letters. I use the trackpad to move the cursor and select text. | Keyboard and trackpad |
| Processing | The M5 chip runs VS Code, works out which key I pressed, and updates the document. The text I have typed but not saved is sitting in RAM. | CPU (Apple M5) and RAM |
| Output | The letters appear on screen as I type. The cursor moves and the line numbers change. | Built-in display |
| Storage | When I press Command+S, the file is written to the SSD, so it is still there after I close the editor or shut the laptop down. | 460 GB SSD |

There is one extra step in this activity. The file lives inside a Git
repository, so `git add` and `git commit` record a second copy of the change
inside the `.git` folder.

How the activity moves through the stages: my fingers make the input, the
processor turns that into changes in the open document, the screen shows me the
result straight away, and saving copies the finished file onto the disk. Input
and output happen non-stop while I type. Storage only happens when I save.

### Task 1.2 — Hardware and software I use

| Item or software | Hardware or software? | Type of software | Purpose |
|---|---|---|---|
| MacBook keyboard | Hardware | Not applicable | Types text and runs shortcuts like Command+S |
| Trackpad | Hardware | Not applicable | Moves the pointer and clicks |
| Built-in display | Hardware | Not applicable | Shows what the computer is doing |
| Apple M5 chip | Hardware | Not applicable | Carries out the instructions of every program |
| SSD | Hardware | Not applicable | Keeps files when the laptop is off |
| macOS 27.2 | Software | Operating system | Manages the hardware, files, memory and running apps |
| VS Code | Software | Application | Writing and editing code and text files |
| Safari | Software | Application | Browsing websites |
| Homebrew | Software | Utility | Installs and updates other software from the Terminal |
| Activity Monitor | Software | Utility | Shows what is running and how much memory or CPU it uses |

How I tell them apart: the operating system is the layer between me and the
hardware. Applications are the programs I open to get something done. Utilities
are not doing my work for me, they look after the computer itself.

### Task 1.3 — Computer systems around me

| System | Main purpose | One input | One output |
|---|---|---|---|
| ATM | Lets a bank customer take out cash or check a balance without queueing at a counter | The card and the PIN typed on the keypad | Cash from the slot and a printed receipt |
| Smart TV | Plays streaming apps and cable channels, and mirrors a phone screen | Remote control buttons or a voice command | Picture on the screen and sound from the speakers |
| Metro ticket machine | Sells a ticket or token at a station | Touching a choice on the screen and paying by card or cash | A printed ticket or token, and the amount shown on screen |

How I would say this out loud: an ATM is a small computer with a card reader, a
keypad, a screen, a cash dispenser and a printer. The card and PIN go in, the
bank's computer checks the PIN while processing, and cash plus a receipt come
out. A smart TV is really a computer built around a big screen, so its main
output is picture and sound. A metro ticket machine is mostly input and output
and not much else.

## 3. Commands / tools used

| Command or tool | Purpose |
|---|---|
| `system_profiler SPHardwareDataType` | Shows the model, chip, number of cores and memory, so the hardware table is real. |
| `df -h /` | Shows total and free disk space. |
| VS Code | Used to write the tables and explanations. |

The output, with the serial number, hardware UUID and UDID taken out, is in
`evidence/mission-01/hardware-summary.txt`.

## 4. My understanding

A computer is not doing four separate jobs one after another. It is doing them in
a loop. Every key press is a small input, then processing, then output, and the
loop starts again before my finger is off the key.

Memory and storage are the pair I had to think about. RAM holds the document
while I am working on it. It is fast, and it is emptied when the app closes. The
SSD keeps the file after everything is switched off, and it is slower. That is
why an unsaved document can vanish in a power cut even though the laptop has
plenty of free disk space.

Input and output devices are not fixed either. A touchscreen is both at once. On
my laptop the screen is output only and the trackpad is input only.

Once I could see the four stages, some everyday problems made sense. A laptop
that is slow but has 120 GB free is short of memory, not storage. A file that
disappears after a restart was never stored in the first place.

## 5. Difficulties faced

- I was not sure whether saving belongs under output or storage. At first I put
  the file save as output.
- I could not keep the M5 chip and RAM apart until I looked at what each one
  actually does while a program runs.
- I mixed up operating system software with utility software, because both seem
  to "manage" the computer.

## 6. How I resolved them

- I asked myself what I can see happen. The file appearing on the screen is
  output. The bytes going onto the SSD is storage. Saving does both, so I listed
  it under storage and mentioned the screen update under output.
- I compared them as a worker and a desk. The chip carries out the instructions,
  RAM holds the data those instructions are working on.
- I used the definitions from the assignment. The operating system runs the
  whole machine and nothing works without it. A utility is an extra program that
  maintains the machine, like Homebrew. macOS would start fine without Homebrew,
  so Homebrew is a utility.

## 7. Evidence / files

- `mission-01-computer-basics/README.md` - this file, with all three tables.
- `evidence/mission-01/hardware-summary.txt` - the real hardware and disk
  output, with the serial number, hardware UUID and UDID removed.

## 8. Commit details

Commit message:

    Complete computer basics and IPOS mission

Pushed to `main` on GitHub.
