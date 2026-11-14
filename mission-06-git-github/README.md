# Mission 6 — Git and GitHub

## 1. Task / objective

Practise the Git workflow: check status, stage, commit, read the history. Then
make a branch called `update-about`, add a "My Learning" section to the root
README, push the branch, open a Pull Request into `main`, and look at what
changed.

## 2. Work completed

### Task 6.1 — The basic Git workflow

I started from a clean repository, ran the four operations one at a time, and
checked the output after each one.

| Operation | What it does, in my words |
|---|---|
| Check status | Shows which branch I am on and which files have changed, split into staged and not staged. Before I started it said `nothing to commit, working tree clean`. |
| Stage changes | Picks exactly which changed files go into the next commit. I staged one file, `README.md`, and it moved from "Changes not staged" to "Changes to be committed". |
| Create a commit | Saves the staged changes into the history with a message and an ID. The output was `[update-about 00fdc9c] Add My Learning section to root README` and `1 file changed, 12 insertions(+)`. |
| View history | Lists commits newest first, with a short ID and the message. My new commit `00fdc9c` sat above the Mission 5 commit `6db9a82`. |

**Staging versus committing.** Staging marks a file as "include this in the next
commit". The file on disk has already changed by then, but nothing is in the
history yet. Committing takes that staged snapshot and writes it in with a
message, so the change gets an ID I can point at later. Staging is choosing,
committing is recording. That is also why `git status` keeps two lists.

### Task 6.2 — Making and using a branch

I made the branch with `git switch -c update-about`. `git branch` then showed
both branches, with an asterisk on `update-about`.

On that branch I added a section at the end of the root README:

    ## My Learning

    Three things I did not know before this assignment:

    1. Git does not track empty folders. A folder only appears on GitHub once there
       is a file inside it, which is why every mission folder has a README.
    2. Python compiles my code to bytecode before it runs it, so calling Python
       "purely interpreted" is not really accurate.
    3. `>` replaces everything in a file while `>>` adds to the end. One missing
       character is enough to lose text with no warning and no undo.

Then I checked status, staged the file and committed:

    git status
    git add README.md
    git commit -m "Add My Learning section to root README"
    git push -u origin update-about

`git diff --stat` before staging said `1 file changed, 12 insertions(+)`, which
was what I expected.

### Task 6.3 — The Pull Request

Once the branch was on GitHub, I opened a Pull Request from `update-about` into
`main`. I used the GitHub CLI, which makes the same Pull Request the website would
make.

The description I wrote:

> This PR adds a short "My Learning" section to the end of the root README.
>
> It lists three things I learned during the assignment: Git does not track empty
> folders, Python compiles to bytecode before it runs, and ">" replaces a file's
> contents while ">>" appends.
>
> No other files are changed.

Where it stands:

| Item | Value |
|---|---|
| PR number | 1 |
| Link | https://github.com/ThatKJ/digital-detective-8019/pull/1 |
| From | `update-about` |
| Into | `main` |
| State | OPEN |
| Mergeable | MERGEABLE |
| Files changed | 1, `README.md` |
| Merged? | No |

I did not merge it. The assignment says to merge only if the instructor asks, and
mine did not, so the PR stays open where the branch and the review can be seen.

**What a branch is.** A separate line of work. It starts from wherever I am and
then moves on its own, so commits on it do not touch `main` until they are
merged.

**What a Pull Request is.** A request to put a branch's changes into another
branch, with the diff shown so someone can look before accepting. It is not a
Git command, it is a GitHub feature built on top of branches.

**Why bother, when several people share a project.** If five people committed
straight to `main`, half-finished work would mix with finished work and mistakes
would be painful to unpick. With branches, each person works on their own copy of
the history, and the Pull Request becomes the place where the change is
discussed, checked, and then merged or dropped in one go. `main` stays usable the
whole time.

### Task 6.4 — Git command glossary

| Operation | Command | What it means |
|---|---|---|
| Initialise a repository | `git init -b main` | Turns an ordinary folder into a Git repository and names the first branch `main`. |
| Check status | `git status` | Shows the branch and which files are staged, changed or untracked. |
| Stage changes | `git add README.md` | Picks the files going into the next commit. |
| Commit changes | `git commit -m "message"` | Records the staged files as one snapshot. |
| View history | `git log --oneline` | Lists past commits, newest first, one line each. |
| Create or list branches | `git branch`, `git switch -c update-about` | Lists branches, or makes a new one and moves to it. |
| Switch branches | `git switch main` | Changes the files on disk to match that branch. |
| Publish changes | `git push origin main` | Sends my commits to GitHub. |
| Retrieve remote changes | `git pull` | Brings commits from GitHub into my branch. |

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `git status` | To see what changed before staging. |
| `git diff --stat` | To see how many lines changed, in which file. |
| `git add README.md` | To stage one specific file. |
| `git commit -m "..."` | To record the change. |
| `git log --oneline -4` | To confirm the new commit was at the top. |
| `git switch -c update-about` | To make the branch and move onto it. |
| `git branch`, `git branch -vv` | To list branches and see which commit each points at. |
| `git push -u origin update-about` | To publish the branch and link it to the remote one. |
| `git switch main`, `git pull` | To go back to `main` and check for remote changes. |
| `gh pr create` | To open the Pull Request with a title and description. |
| `gh pr view 1 --json ...` | To read the PR state, branches and changed files. |
| `gh pr diff 1 --name-only` | To confirm only `README.md` was in the PR. |

## 4. My understanding

What made Git click was that a commit is a snapshot, not a diff. The diff is just
how GitHub shows the difference between two snapshots.

Staging looked like an unnecessary extra step until I thought about it. Without a
staging area, every commit would carry every file I had touched, including
half-finished work. Staging only `README.md` meant I could commit that change and
leave everything else alone.

A branch is much cheaper than I expected. It is not a copy of all the files, it
is a pointer to a commit that moves forward as I add commits. Switching branches
changes the files on disk, which is why the working tree has to be in a sensible
state before I switch.

`git pull` said `Already up to date.` because nothing new had reached `main` from
anywhere else. If a teammate had pushed, `pull` would have brought those commits
down. If both of us had changed the same lines, I would have had a merge conflict
to sort out.

## 5. Difficulties faced

- I was torn between `git add .` and `git add README.md`. The first grabs
  everything, including files I might not want in that commit.
- I first thought about creating the PR before pushing the branch, and it would
  not have worked. The branch has to exist on GitHub first.
- `gh pr diff 1 --stat` came back with `unknown flag: --stat`, because that flag
  belongs to `git diff` and not to the `gh` version.
- I expected the "My Learning" section to stay visible after switching back to
  `main`. It does not, because that text only exists on `update-about`.

## 6. How I resolved them

- I staged the file by name. `git status` then showed exactly one file under
  "Changes to be committed", which is what I wanted to confirm.
- I pushed with `git push -u origin update-about` first. The push output even
  offered me the pull request link, so I created it after that.
- I read the error, saw `--stat` was not accepted, and used
  `gh pr diff 1 --name-only` instead, which gave the file list I was after.
- I ran `git branch -vv` and saw `main` pointing at `6db9a82` and `update-about`
  pointing at `00fdc9c`. That proved the change was only on the branch, which is
  exactly how it is meant to work before a merge.

## 7. Evidence / files

- `mission-06-git-github/README.md` - this file.
- `evidence/mission-06/git-workflow.txt` - the real output of status, staging,
  commit, push and the branch commands.
- `evidence/mission-06/pull-request.txt` - the real output of creating and
  inspecting the PR.
- The branch `update-about` and PR #1 on GitHub.

## 8. Commit details

Commit message for this mission:

    Complete Git and GitHub collaboration mission

The branch commit used its own message:

    Add My Learning section to root README

Both were pushed. The mission commit is on `main`, and the branch commit is on
`update-about` inside PR #1.
