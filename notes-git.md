# Git Notes ![Git badge](https://img.shields.io/badge/GIT-E44C30?style=for-the-badge&logo=git&logoColor=white)

This document contains essential Git workflows and troubleshooting steps for managing data analysis and coding repositories.

## How-tos

### How to Clone a Remote Repository on GitHub to Your Local Machine

Steps:
1. Go to GitHub and open the target remote repository.
2. Click the `[Code]` button and select the `[HTTPS]` tab.
3. Copy the HTTPS URL.
4. Open your Command-Line Interface (CLI) / Terminal.
5. Use `cd <directory-path>` to navigate to the folder where you want to store the repository[^1].
6. Run `git clone <HTTPS-URL>` and press `[ENTER]`[^2].

[^1]: A folder with the same name and structure as the remote repository will be created inside your current directory.
[^2]: You do not need to run `git init` before `git clone` because the cloned repository already contains a configured `.git` folder.

### How to Create and Push a New Local Repository to GitHub

Steps:
1. Create a new repository on GitHub (without initializing files if pushing an existing local folder).
2. Open your CLI and navigate to your project directory using `cd`.
3. Type `git init` to initialize Git tracking.
4. Type `git add .` to stage all files in the current folder[^3].
5. Type `git commit -m "Initial commit"` to save a snapshot of the staged changes.
6. Type `git branch -M main` to ensure the default branch is named `main`[^4].
7. Type `git remote add origin <HTTPS-URL>` to link your local repo to the GitHub remote.
8. Type `git push -u origin main` to push your commits to GitHub[^5].

[^3]: Always make sure you have a `.gitignore` file before running `git add .` so you don't accidentally upload large virtual environments (`venv/`) or sensitive `.env` keys.
[^4]: Renaming the branch to `main` ensures consistency with GitHub's default branch naming.
[^5]: The `-u` flag (`--set-upstream`) links your local `main` branch to the remote `origin/main` branch for future `git pull` and `git push` commands.

## Common Errors & Fixes

### Error: `failed to push some refs to 'https://github.com/....git'`

<ins>Cause</ins>: The remote repository on GitHub contains commits (such as an online edit to `README.md`) that you do not have locally.
<br />
<ins>Fix</ins>: Pull and integrate the remote changes first before pushing:
```bash
git pull origin main
