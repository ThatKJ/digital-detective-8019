# Mission 6 — Git and GitHub

## 1. Task / objective

Practise the Git workflow: check status, stage, commit and read the history.
Then create a branch called `update-about`, add a "My Learning" section to the
root README, push the branch, open a Pull Request into `main`, and inspect the
changed files.

## 2. Work completed

### Task 6.1 — The basic Git workflow

I started with a clean repository, ran the four operations one at a time, and
checked the output after each one.

| Git operation | What it does in my own words |
|---|---|
| Check repository status | Shows which branch I am on and which files have changed, split into changes that are staged and changes that are not. Before I started it said `nothing to commit, working tree clean`. |
| Stage selected changes | Chooses exactly which changed files go into the next commit. I staged one file, `README.md`, and `git status` then showed it under "Changes to be committed" instead of "Changes not staged for commit". |
| Create a commit | Saves the staged changes in the history with a message and a commit ID. The output was `[update-about 00fdc9c] Add My Learning section to root README` and `1 file changed, 12 insertions(+)`. |
| View commit history | Lists the commits from newest to oldest with a short ID and the message. My newest commit was at the top, `00fdc9c`, above the Mission 5 commit `6db9a82`. |

**Staging versus committing.** Staging marks a file as "include this in the next
commit". The file on disk has already changed at that point, but nothing is in
the history yet. Committing takes the staged snapshot and writes it permanently
into the repository with a message, so the change gets a commit ID I can point
at later. Staging is choosing, committing is recording. This is also why
`git status` has two separate lists.

### Task 6.2 — Creating and using a branch

I created the branch with `git switch -c update-about`. `git branch` then showed
both branches with an asterisk next to `update-about`, which is the one I was on.

On that branch I added a section at the end of the root README:

    ## My Learning

    Three things I did not know before this assignment:

    1. Git does not track empty folders. A folder only appears on GitHub once there
       is a file inside it, which is why every mission folder has a README.
    2. Python compiles my code to bytecode before it runs it, so calling Python
       "purely interpreted" is not really accurate.
    3. `>` replaces everything in a file while `>>` adds to the end. One missing
       character is enough to lose text with no warning and no undo.

Then I checked status, staged `README.md`, and committed:

    git status
    git add README.md
    git commit -m "Add My Learning section to root README"
    git push -u origin update-about

`git diff --stat` before staging showed `1 file changed, 12 insertions(+)`, which
matched what I expected.

### Task 6.3 — The Pull Request

After the branch was pushed, I opened a Pull Request from `update-about` into
`main`. I used the GitHub CLI, which creates the same Pull Request as the website
would.

The PR description I wrote:

> This PR adds a short "My Learning" section to the end of the root README.
>
> It lists three things I learned during the assignment: Git does not track empty
> folders, Python compiles to bytecode before it runs, and ">" replaces a file's
> contents while ">>" appends.
>
> No other files are changed.

Status at the time of writing:

| Item | Value |
|---|---|
| PR number | 1 |
| Link | https://github.com/ThatKJ/digital-detective-8019/pull/1 |
| From branch | `update-about` |
| Into branch | `main` |
| State | OPEN |
| Mergeable | MERGEABLE |
| Files changed | 1, `README.md` |
| Merged? | No |

I did not merge it. The assignment says to merge only if the instructor asks for
the merge, and my instructor did not ask, so the PR is left open so the branch
and the review can be seen.

**What a branch is.** A branch is a separate line of work. It starts as a copy
of the current state and then moves on its own, so commits made on it do not
change `main` until they are merged.

**What a Pull Request is.** A Pull Request is a request to put a branch's
changes into another branch, with the diff shown so someone can review it before
it is accepted. It is not a Git command; it is a GitHub feature built around
branches.

**Why they are useful when people work on the same project.** If five people
committed straight to `main`, unfinished work would mix with finished work and
mistakes would be hard to undo. With branches, each person works on their own
copy of the history, and the Pull Request becomes the place where the change is
discussed, reviewed and then merged (or rejected) in one step. The `main` branch
stays in a working state.

### Task 6.4 — Git command glossary

| Operation | Command | What it means in my own words |
|---|---|---|
| Initialise a repository | `git init -b main` | Turns an ordinary folder into a Git repository and names the first branch `main`. |
| Check status | `git status` | Shows the current branch and which files are staged, changed or untracked. |
| Stage changes | `git add README.md` | Picks the files that will go into the next commit. |
| Commit changes | `git commit -m "message"` | Records the staged files in the history as one snapshot. |
| View history | `git log --oneline` | Lists past commits, newest first, one line each. |
| Create or list branches | `git branch`, `git switch -c update-about` | Lists branches, or creates a new one and switches to it. |
| Switch branches | `git switch main` | Changes the working files to match that branch. |
| Publish changes | `git push origin main` | Sends my local commits to GitHub. |
| Retrieve remote changes | `git pull` | Brings commits from GitHub into my local branch. |

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `git status` | To see what had changed before staging. |
| `git diff --stat` | To see how many lines changed in which file. |
| `git add README.md` | To stage one specific file. |
| `git commit -m "..."` | To record the change. |
| `git log --oneline -4` | To confirm the new commit was at the top of the history. |
| `git switch -c update-about` | To create and move to the new branch. |
| `git branch`, `git branch -vv` | To list branches and see which commit each one points to. |
| `git push -u origin update-about` | To publish the branch and set it to track the remote one. |
| `git switch main`, `git pull` | To go back to `main` and check for remote changes. |
| `gh pr create` | To open the Pull Request with a title and description. |
| `gh pr view 1 --json ...` | To read the PR state, branches and changed files. |
| `gh pr diff 1 --name-only` | To confirm only `README.md` was part of the PR. |

## 4. My understanding

The thing that made Git click was that a commit is a snapshot, not a diff. The
diff is just how GitHub displays the difference between two snapshots.

Staging felt unnecessary until I understood it. Without a staging area, every
commit would contain every file I had touched, including half-finished work. By
staging only `README.md`, I could commit the README change and leave everything
else alone.

A branch is much cheaper than I expected. It is not a copy of all the files, it
is a pointer to a commit that moves forward as I commit. Switching branches
changes the files on disk, which is why `git status` has to be clean enough to
switch safely.

`git pull` showed `Already up to date.` because nothing new had been pushed to
`main` from anywhere else. If a teammate had pushed, `pull` would have brought
those commits down. If both sides had changed the same lines, I would have had a
merge conflict to resolve.

## 5. Difficulties faced

- I was not sure whether to stage with `git add .` or `git add README.md`. The
  first adds everything, including files I might not want in that commit.
- Creating the PR failed when I first thought about doing it before pushing the
  branch. A PR needs the branch to exist on GitHub first.
- `gh pr diff 1 --stat` returned `unknown flag: --stat`, because that flag
  belongs to `git diff` and not to `gh pr diff`.
- I expected switching back to `main` to keep the "My Learning" section visible,
  but it disappears, because that text only exists on `update-about` until the
  PR is merged.

## 6. How I resolved them

- I staged the exact file by name. `git status` then showed the file under
  "Changes to be committed", which confirmed only that one file was going in.
- I pushed with `git push -u origin update-about` first, and only then created
  the PR. The push output itself suggested the pull request link.
- I read the error message, saw that `--stat` was not accepted, and used
  `gh pr diff 1 --name-only` instead, which gave the file list I actually wanted.
- I checked `git branch -vv` and saw that `main` pointed at `6db9a82` while
  `update-about` pointed at `00fdc9c`. That confirmed the change is only on the
  branch, which is exactly how it is supposed to work until the merge happens.

## 7. Evidence / files

- `mission-06-git-github/README.md` - this file.
- `evidence/mission-06/git-workflow.txt` - real output of the status, staging,
  commit, push and branch commands.
- `evidence/mission-06/pull-request.txt` - real output of the PR creation and
  inspection.
- The branch `update-about` and PR #1 on GitHub.

## 8. Commit details

Commit message for this mission:

    Complete Git and GitHub collaboration mission

The branch commit itself used the message:

    Add My Learning section to root README

Both were pushed. The mission commit is on `main`, and the branch commit is on
`update-about` and included in PR #1.
