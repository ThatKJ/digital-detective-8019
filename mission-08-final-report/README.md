# Mission 8 — Final report and submission

## 1. Task / objective

Go through the whole repository and check that everything the assignment asked
for is actually there and working. Fix anything that is missing, write the final
report, update the root README so a first-time visitor understands the project,
and confirm the repository is public and up to date.

## 2. Work completed

I checked the repository against the assignment's final checklist item by item.
The results are in the table below. Each row is something I actually ran or
opened, not something I assumed.

| Check | Result |
|---|---|
| All nine mission folders exist | Pass. `mission-00-setup` to `mission-08-final-report` are all present, plus `evidence`. |
| Every mission has its own README | Pass. Nine folders, nine `README.md` files. |
| Every mission README uses the required format | Pass. All eight required sections are present in every mission README, and none of them is blank. |
| Required tables are complete | Pass. IPOS, hardware/software, computer systems (Mission 1), command reference (Mission 2), OS, processes, permissions and responsibilities (Mission 3), compiler/interpreter (Mission 4), conversions and converter tests (Mission 5), Git operations and glossary (Mission 6), network concepts (Mission 7). |
| Manual conversions show working | Pass. All seven conversions in Mission 5 show the divisions or the position values, plus a check back to the original number. |
| Python programs run | Pass. `hello.py` printed `Hello from Python` and `number_converter.py` ran on 13, 25 and 100 during this review. |
| At least three converter tests recorded | Pass. 13, 25, 100, and 255 as an extra. |
| Git history has a dedicated commit per mission | Pass. Eight commits, one for setup and one for each of Missions 1 to 7, then this final one. |
| Branch activity is visible | Pass. `update-about` exists locally and on GitHub. |
| Pull Request exists | Pass. PR #1 from `update-about` into `main`, still open. |
| Networking exercises documented | Pass. `ping`, `nslookup`, `host` and `dig` output is in Mission 7 and in the evidence folder. |
| Sensitive information removed | Pass. I searched the whole repository for my username, my email address and token-like strings and found nothing. |
| Root README has navigation links | Pass. It has a mission index table linking every mission README. |
| Root README explains how to run the converter | Pass. It now has a short section with the `cd` and `python3` commands and an example of the output. |
| Root README has a short learning summary | Pass. It has a "What I learned" section before the mission overview, written after all nine missions were done. |
| All intended commits are pushed | Pass. `git status` reports the branch is up to date with `origin/main`. |
| Repository is public | Pass. GitHub reports the visibility as PUBLIC. |

### Corrections I made during the review

Three things were wrong when I went through the repository:

1. In the Mission 2 README, I had pasted a real `ls -l` line that still had my
   computer username in the owner column. I replaced it with `[redacted]`.
2. The Mission 3 README used `number_converter.py` as its absolute-path example
   before that file existed. I changed the example to a file that already
   existed at that point.
3. The `__pycache__` folder from running Python was sitting in the repository.
   I deleted it and added a `.gitignore` so it stays out.

### Status of each mission

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

### Git history at the time of this review

    6d06689 Explain networking concepts and website communication
    37e1e7e Complete Git and GitHub collaboration mission
    6db9a82 Build number converter and practise data representation
    85afa85 Compare compilers and interpreters
    3f6e496 Document operating system and file management
    bf8a90f Complete Terminal and file management mission
    66f0d1f Complete computer basics and IPOS mission
    27e6378 Set up Digital Detective mission structure

Plus one commit on `update-about`:

    00fdc9c Add My Learning section to root README

### Submission details

- Repository URL: https://github.com/ThatKJ/digital-detective-8019
- Visibility: public
- Default branch: `main`
- Pull Request: https://github.com/ThatKJ/digital-detective-8019/pull/1 (open, not merged)

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `find . -path ./.git -prune -o -print` | To list every file in the repository and compare it with the required structure. |
| `grep -cE '^## [1-8]\. '` on each README | To count how many of the eight required headings each mission README has. |
| `grep -rniE "..."` | To search the whole repository for my username, my email address and anything that looks like a key or token. |
| `python3 hello.py` | To confirm the Mission 4 program still runs. |
| `python3 number_converter.py` with 13, 25 and 100 | To confirm the Mission 5 program still runs after all the changes. |
| `git log --oneline` | To confirm there is one commit per mission. |
| `git branch -a` | To confirm the `update-about` branch exists locally and on GitHub. |
| `gh pr view 1` | To confirm the Pull Request is still open and what it changes. |
| `gh repo view` | To confirm the repository visibility is public. |

## 4. My understanding

The review was the part that made the assignment feel finished. Building the
folders was easy. Checking that every folder actually contained everything the
rubric asks for was the slow part.

Two things I would do differently next time. First, I would check for private
information in each file before committing it, not in one big sweep at the end,
because the username had already been pushed to GitHub before I caught it.
Second, I would keep one small evidence file per mission from the beginning,
since writing the README later from memory is much less reliable than saving the
output while the terminal is still open.

The Git history also turned out to be useful evidence, not just housekeeping.
Anyone reading the log can see which mission each commit belongs to, and the
branch and Pull Request show the workflow rather than just describing it.

## 5. Difficulties faced

- Replacing the username after it had already been pushed meant the old value
  was still in the commit history, even though the current file is clean.
- I was not sure what "mergeable: UNKNOWN" meant on the Pull Request when I
  re-checked it, because it had said MERGEABLE earlier.
- The `grep` privacy search matched the word "password" and the word "token" in
  ordinary sentences, so it looked like a problem at first.

## 6. How I resolved them

- I fixed the file, committed the correction, and left the history alone rather
  than rewriting it. The assignment says not to alter history, and the username
  appears in old commits only as part of an output block, not as a login.
- I understood it as GitHub recalculating whether the branch can merge cleanly.
  The state that matters for the assignment is OPEN and not merged, and that has
  not changed.
- I read each match in context. "Asks for a password" and "printed ticket or
  token" are normal English, not secrets, so no change was needed.

## 7. Evidence / files

- `mission-08-final-report/README.md` - this file.
- `evidence/mission-08/final-audit.txt` - the real output of the structure,
  heading, privacy and program checks.
- All earlier mission READMEs and their evidence files.

## 8. Commit details

Commit message:

    Complete final report and verify assignment submission

Pushed to `main` on GitHub.
