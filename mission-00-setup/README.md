# Mission 0 — Repository and workspace setup

## 1. Task / objective

Set up the repository with the right name, build a folder for each of the nine
missions, write a root README, put it on GitHub as a public repository, and push
the first commit.

The name had to be the assignment name plus the last four digits of my USN, in
lowercase with a hyphen and no spaces. My USN is 2402608019, so the last four
are 8019 and the name is:

`digital-detective-8019`

I used the same name for the folder on my laptop, so the folder and the GitHub
repository match exactly and there is nothing to misread.

## 2. Work completed

1. Checked that Python 3 and Git were already on the Mac.
2. Made the folder `digital-detective-8019` on the Desktop.
3. Ran `git init` inside it so the folder became a Git repository.
4. Made all nine mission folders and one folder called `evidence`.
5. Put an empty `README.md` inside every mission folder, which Step 3 of the
   assignment asks for, and wrote the root README.
6. Wrote this Mission 0 README.
7. Created the public repository `digital-detective-8019` on GitHub and linked
   it to the folder as `origin`.
8. Committed the setup, pushed it, and checked on GitHub that everything was
   there.

Repository URL: https://github.com/ThatKJ/digital-detective-8019

## 3. Commands / tools used

| Command | What it was for |
|---|---|
| `python3 --version` | To confirm Python 3 was installed and note the version. |
| `git --version` | To confirm Git was installed and note the version. |
| `mkdir -p` | To make the main folder and all the mission folders in one command. |
| `cd` | To move into the repository folder before doing anything else. |
| `git init -b main` | To turn the folder into a repository, and to name the first branch `main` instead of the older `master`. |
| `git add .` | To pick the setup files for the commit. |
| `git commit -m "..."` | To save the setup as one commit with a message. |
| `gh repo create` | To make the public repository from the Terminal and link it up in one step. |
| `git remote -v` | To check the folder was connected to GitHub. |
| `git log --oneline` | To check the commit existed locally. |

Versions I saw:

- Python 3.14.7
- git version 2.54.0 (Apple Git-157)
- gh version 2.93.0 (2026-05-27)
- macOS 27.2 on arm64

The output is saved in `evidence/mission-00/tools-check.txt`.

## 4. My understanding

A repository is a folder that Git keeps an eye on. Every commit records what the
files looked like at that moment, so if I break something I can see what changed
and go back. It is not a backup though, because it only knows about the files I
actually add to it.

Git and GitHub are not the same thing. Git is the program running on my laptop
that keeps the history. GitHub is a website holding a copy of that history, so
other people can see it and so it survives my laptop dying.

The folders are split by mission because the assignment is marked mission by
mission. My instructor can open `mission-05-numbers-data` and mark just that
part without scrolling through everything else. It also made one commit per
mission possible, which is what was asked for.

Two things I did not expect. Git tracks files, not folders, so an empty folder
never shows up on GitHub. And that turned out not to matter here, because every
mission folder needs a README anyway. The `evidence` folder had no README
planned, so I saved the first output file into it early to stop it disappearing.

I left my name, USN, account name and email out of the public files. The
assignment allows personal details only if the instructor says so, so I played it
safe. The only personal thing I kept is the USN digits inside the repository
name, and that was required.

## 5. Difficulties faced

- I ran `ls digital-detective-*` before the folder existed and zsh answered
  `no matches found`, which looked like something had gone wrong.
- I was not sure whether to create the GitHub repository first or the local
  folder first. GitHub offers to add a README during setup and the assignment
  warns about ending up with two.
- I did not know empty folders would not be pushed.

## 6. How I resolved them

- I read the message again. `no matches found` just means the wildcard matched
  nothing, so the folder was not there yet. I created it after that.
- I made the local folder and the first commit first, then ran `gh repo create`.
  I did not tick the README box, so there was only ever one README.
- I put an empty README in every mission folder and an output file in `evidence`,
  so every folder had something in it before I pushed.

## 7. Evidence / files

- `README.md` - the root README with the mission index.
- `mission-00-setup/README.md` - this file.
- `evidence/mission-00/tools-check.txt` - the real output of the version
  commands.
- The empty README files in the other eight mission folders, filled in later as
  I reached each one.

## 8. Commit details

Commit message:

    Set up Digital Detective mission structure

Pushed to the `main` branch on GitHub. When I opened the repository page
afterwards, all nine mission folders, the `evidence` folder and the root README
were visible.
