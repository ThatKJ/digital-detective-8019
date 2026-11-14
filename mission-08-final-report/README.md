# Mission 8 — Final report and submission

## 1. Task / objective

Go through the whole repository and check that everything the assignment asked
for is actually there and still works. Fix whatever is missing, write the final
report, tidy the root README so a first-time visitor can follow it, and confirm
the repository is public and up to date.

## 2. Work completed

I went down the assignment's final checklist one item at a time. Every row below
is something I actually ran or opened, not something I assumed was fine.

| Check | Result |
|---|---|
| All nine mission folders exist | Pass. `mission-00-setup` to `mission-08-final-report`, plus `evidence`. |
| Every mission has its own README | Pass. Nine folders, nine `README.md` files. |
| Every README uses the required format | Pass. All eight required sections are present in every mission README, and none is blank. |
| Required tables are complete | Pass. IPOS, hardware and software, computer systems in Mission 1; the command reference in Mission 2; OS, processes, permissions and responsibilities in Mission 3; compiler against interpreter in Mission 4; conversions and converter tests in Mission 5; Git operations and the glossary in Mission 6; network concepts in Mission 7. |
| The manual conversions show working | Pass. All seven in Mission 5 show the divisions or position values, plus a check back to the original number. |
| The Python programs run | Pass. `hello.py` printed `Hello from Python` and `number_converter.py` ran on 13, 25 and 100 during this review. |
| At least three converter tests are recorded | Pass. 13, 25 and 100, with 255 as an extra. |
| There is a dedicated commit per mission | Pass. One for setup, one for each mission, and the closing commits for the report itself. |
| The branch work is visible | Pass. `update-about` exists locally and on GitHub. |
| A Pull Request exists | Pass. PR #1 from `update-about` into `main`, still open. |
| The networking work is documented | Pass. `ping`, `nslookup`, `host` and `dig` output in Mission 7 and in the evidence folder. |
| Sensitive information is removed | Pass. I searched the whole repository for my account name, my email and anything that looks like a key, and found nothing. |
| The root README links to each mission | Pass. It has an index table linking all nine. |
| The root README explains how to run the converter | Pass. A short section with the `cd` and `python3` commands and an example of the output. |
| The root README has a short learning summary | Pass. A "What I learned" section before the mission overview, written after all nine missions. |
| All the intended commits are pushed | Pass. `git status` reports the branch is level with `origin/main`. |
| The repository is public | Pass. GitHub reports the visibility as PUBLIC. |

### Mistakes I found and fixed

Three things were wrong when I went back through the repository:

1. In the Mission 2 README I had pasted a real `ls -l` line that still had my
   account name in the owner column. I replaced it.
2. The Mission 3 README used `number_converter.py` as its absolute path example
   before that file existed. I changed the example to a file that did exist at
   that point.
3. The `__pycache__` folder from running Python was sitting in the repository. I
   deleted it and added a `.gitignore` so it stays out.

### Where each mission stands

| Mission | State |
|---|---|
| 0 — Repository and workspace setup | Complete, committed, pushed |
| 1 — Computer fundamentals and IPOS | Complete, committed, pushed |
| 2 — Terminal and file management | Complete, committed, pushed |
| 3 — Operating system and permissions | Complete, committed, pushed |
| 4 — How programs run | Complete, committed, pushed |
| 5 — Numbers and data | Complete, committed, pushed |
| 6 — Git and GitHub | Complete, committed, pushed, PR #1 open |
| 7 — Computer networks | Complete, committed, pushed |
| 8 — Final review | This file, committed and pushed last |

### Git history when I ran the audit

    6d06689 Explain networking concepts and website communication
    37e1e7e Complete Git and GitHub collaboration mission
    6db9a82 Build number converter and practise data representation
    85afa85 Compare compilers and interpreters
    3f6e496 Document operating system and file management
    bf8a90f Complete Terminal and file management mission
    66f0d1f Complete computer basics and IPOS mission
    27e6378 Set up Digital Detective mission structure

And one commit on the branch:

    00fdc9c Add My Learning section to root README

Two commits came after the audit itself, because the audit found work to do: the
final report commit, and one adding the learning summary to the root README. This
README was rewritten in plain language after that.

### Submission details

- Repository URL: https://github.com/ThatKJ/digital-detective-8019
- Visibility: public
- Default branch: `main`
- Pull Request: https://github.com/ThatKJ/digital-detective-8019/pull/1 (open, not merged)

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `find . -path ./.git -prune -o -print` | To list every file and compare it with the required structure. |
| `grep -cE '^## [1-8]\. '` on each README | To count how many of the eight required headings each one has. |
| `grep -rniE "..."` | To search the repository for my account name, my email and anything key-shaped. |
| `python3 hello.py` | To confirm the Mission 4 program still runs. |
| `python3 number_converter.py` with 13, 25 and 100 | To confirm the Mission 5 program still runs after all the changes. |
| `git log --oneline` | To confirm there is one commit per mission. |
| `git branch -a` | To confirm `update-about` exists locally and on GitHub. |
| `gh pr view 1` | To confirm the PR is still open and what it changes. |
| `gh repo view` | To confirm the repository is public. |

## 4. My understanding

The review was the part that made this feel finished. Making the folders was
easy. Checking that every folder really contained what the rubric asks for was
the slow bit.

Two things I would do differently next time. First, I would check for private
information in each file before committing it, not in one sweep at the end,
because my account name was already pushed to GitHub by the time I spotted it.
Second, I would save one small evidence file per mission as I went, because
writing a README from memory a week later is far less reliable than copying the
Terminal while it is still open.

The Git history turned out to be useful evidence too, not just housekeeping.
Anyone reading the log can see which commit belongs to which mission, and the
branch and Pull Request show the workflow instead of only describing it.

## 5. Difficulties faced

- Fixing the account name after it was already pushed meant the old value was
  still in the earlier commits, even though the current files are clean.
- When I re-checked the Pull Request it said `mergeable: UNKNOWN`, where it had
  said MERGEABLE before, and I did not know what had changed.
- The privacy search matched the ordinary words "password" and "token" in normal
  sentences, so it looked like a problem at first.
- Several sections were too long and too technical for me to defend if I were
  asked about them, so I rewrote them in shorter, plainer sentences.

## 6. How I resolved them

- I fixed the file, committed the correction and left the history alone instead
  of rewriting it. The assignment says not to alter history, and the old value
  only appears inside a pasted output block, not as a login.
- I read `UNKNOWN` as GitHub still working out whether the branch merges cleanly.
  What matters for the assignment is that it is OPEN and not merged, and that has
  not changed.
- I read every match in context. "Asks for a password" and "printed ticket or
  token" are ordinary English, not secrets, so nothing needed changing.
- I went through the READMEs again and cut the long sentences, removed the parts I
  could not explain out loud, and kept every measured number exactly as it was.

## 7. Evidence / files

- `mission-08-final-report/README.md` - this file.
- `evidence/mission-08/final-audit.txt` - the real output of the structure,
  heading, privacy and program checks.
- All the earlier mission READMEs and their evidence files.

## 8. Commit details

Commit message:

    Complete final report and verify assignment submission

Pushed to `main` on GitHub, with the correction commits after it.
