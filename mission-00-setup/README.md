# Mission 0 — Repository and workspace setup

## 1. Task / objective

Create the repository with the correct name, build the folder structure for all
nine missions, write a root README, publish the repository on GitHub as a
public repo, and push the first commit.

The repository name had to be the assignment name plus the last four digits of
my USN, in lowercase and with a hyphen. My USN is 2402608019, so the last four
digits are 8019 and the name is:

`digital-detective-8019`

I used the same name for the local folder so that the folder name and the
GitHub repository name match exactly.

## 2. Work completed

1. Checked that Python 3 and Git were already installed on my Mac.
2. Created the local folder `digital-detective-8019` on my Desktop.
3. Ran `git init` inside it so the folder became a Git repository.
4. Created all nine mission folders and an `evidence` folder.
5. Created an empty `README.md` inside every mission folder, as the assignment
   asks in Step 3, and filled in the root README.
6. Wrote the Mission 0 README, which is this file.
7. Created the public GitHub repository `digital-detective-8019` and connected
   it to the local folder as `origin`.
8. Committed the setup and pushed it, then checked on GitHub that the folders
   and files were there.

Repository URL: https://github.com/ThatKJ/digital-detective-8019

## 3. Commands / tools used

| Command | What it was for |
|---|---|
| `python3 --version` | To confirm Python 3 was installed and note the version. |
| `git --version` | To confirm Git was installed and note the version. |
| `mkdir -p` | To create the main folder and the mission folders in one go. |
| `cd` | To move into the repository folder before running other commands. |
| `git init -b main` | To turn the folder into a repository, and to name the first branch `main` instead of the older default `master`. |
| `git add .` | To select the setup files for the commit. |
| `git commit -m "..."` | To save the setup as one commit with a message. |
| `gh repo create` | To create the public repository on GitHub from Terminal and link it to the folder. |
| `git remote -v` | To confirm the local folder was connected to the GitHub repository. |
| `git log --oneline` | To confirm the commit existed locally. |

Versions I saw:

- Python 3.14.7
- git version 2.54.0 (Apple Git-157)
- gh version 2.93.0 (2026-05-27)
- macOS 27.2 on arm64

The full output is saved in `evidence/mission-00/tools-check.txt`.

## 4. My understanding

A repository is a folder that Git keeps track of. Git records what the files
looked like at every commit, so if I break something I can see what changed and
go back to an older version. It is not the same thing as a backup, because it
only stores the files I actually add to it.

Git and GitHub are two different things. Git is the program that runs on my
laptop and stores the history. GitHub is a website that keeps a copy of that
history online so other people can see it and so I do not lose it if my laptop
breaks.

The folders are arranged by mission because the assignment is marked mission by
mission. When my instructor opens the repository, they can go straight to
`mission-05-numbers-data` and mark only that part. It also helped me keep one
commit per mission, which is what the assignment asks for.

I also learned that Git tracks files, not empty folders. An empty folder simply
does not appear on GitHub. Since every mission folder needed a README anyway,
that solved the problem, but I had to create a file inside `evidence` too or the
folder would have been missing online.

I kept my name, USN, computer username and email out of the public files. The
assignment says to include personal details only if the instructor allows it, so
I left them out and only used the USN digits inside the repository name, which
the assignment requires.

## 5. Difficulties faced

- I first ran `ls digital-detective-*` in the wrong folder to see if the folder
  already existed. zsh answered `no matches found` and stopped, which looked
  like an error but only meant the pattern matched nothing yet.
- I was not sure whether creating the GitHub repository first or the local
  folder first was correct, because GitHub usually offers to add a README
  during setup and the assignment warns against having two.
- I did not know that empty folders are not pushed to GitHub.

## 6. How I resolved them

- I read the zsh message properly. `no matches found` is zsh telling me the
  wildcard matched no file, so the folder did not exist yet. I created it after
  that.
- I created the local folder and the first commit first, and only then created
  the GitHub repository with `gh repo create`. I did not tick the README option
  on GitHub, so there was only one README in the project.
- I put an empty `README.md` in every mission folder and saved the first output
  file inside `evidence`, so every folder had at least one file in it.

## 7. Evidence / files

- `README.md` - the root README with the mission index.
- `mission-00-setup/README.md` - this file.
- `evidence/mission-00/tools-check.txt` - the real output of the version
  commands.
- The empty README files in the other eight mission folders, which were filled
  in later when I reached those missions.

## 8. Commit details

Commit message:

    Set up Digital Detective mission structure

The commit was pushed to the `main` branch on GitHub. I checked the repository
page afterwards and the nine mission folders, the `evidence` folder and the
root README were all visible.
