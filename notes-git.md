# Git Notes ![Git badge](https://img.shields.io/badge/GIT-E44C30?style=for-the-badge&logo=git&logoColor=white)

> Git is a time machine for your project. Learn five commands and you'll never lose work again; learn ten more and you'll never fear a merge.

These workflows apply to every data analysis and coding repo I touch.

## 🗺️ Contents

1. [The Mental Model](#-the-mental-model)
2. [How-tos](#-how-tos)
3. [Everyday Commands](#-everyday-commands)
4. [Branching](#-branching)
5. [Undo & Rescue](#-undo--rescue)
6. [Tracking Remote Branches](#-extra-tracking-a-remote-branch)
7. [Errors & Fixes](#-errors--fixes)

## 🧠 The Mental Model

```
Working Directory  --git add-->  Staging Area  --git commit-->  Local Repo  --git push-->  GitHub
   (your edits)                  (ready to save)                (history)                   (remote)
```

Edit files, stage what you want, commit a snapshot, push it to GitHub. Every command below is one of those moves.

## 📖 How-tos

### 📥 Get a Remote Repository onto Your Machine

1. Go to GitHub and open the target repository.
2. Click **[Code]** and select the **[HTTPS]** tab.
3. Copy the HTTPS URL.
4. Open a CLI and `cd` into the folder where the repo should live[^1].
5. Run:
   ```bash
   git clone <HTTPS-URL>
   ```
   No `git init` needed[^2].

[^1]: A folder with the same name and structure as the remote repo appears in the directory where you run `git clone`.
[^2]: The cloned repo already has a `.git` folder inside it.

### 🆕 Create a New Repository (Remote → Local)

1. On GitHub: **Profile → Repositories → [New]**.
2. Name it, choose **[Public]** or **[Private]**, click **[Create repository]**[^3].
3. In your CLI:
   ```bash
   cd path/to/where/you/want/it        # [^4]
   mkdir my-new-repo
   cd my-new-repo
   git init                             # start tracking
   git add .                            # stage everything [^5]
   git commit -m "Initial commit"       # snapshot [^6]
   git branch -M main                   # rename branch to main [^7]
   git remote add origin <HTTPS-URL>    # link to GitHub [^8]
   git push -u origin main              # first push [^9]
   ```

[^3]: You can also tick `README.md`, `.gitignore` and `LICENSE` on the create page.
[^4]: Your file manager works too.
[^5]: Stages the current project state for the next commit.
[^6]: Records a snapshot you can return to later.
[^7]: A remote repo with no files has no branch yet. Once files exist, the default is `main`; this keeps your local branch name in sync.
[^8]: `origin` is the nickname for your remote URL.
[^9]: `-u` is short for `--set-upstream`. It links your local branch to the remote one so later you can just type `git push`.

### ✏️ Rename a Remote Repository and Fix the Local Copy

1. On GitHub open the repo → **[Settings]**.
2. Under **Repository name**, type the new name and click **[Rename]**.
3. Copy the new repo URL.
4. Locally, run:
   ```bash
   git remote set-url origin <new-URL>
   git remote -v                 # verify
   ```
   (`git remote show origin` gives more detail.)

## ⚡ Everyday Commands

```bash
git status                  # what changed? (run this constantly)
git diff                    # see unstaged changes
git add <file>              # stage one file
git add .                   # stage everything
git commit -m "message"     # save a snapshot
git log --oneline --graph   # compact history
git pull                    # fetch + merge from remote
git push                    # send commits to remote
```

**Good commit messages** say *what and why*: `Add null-value cleanup for orders data`, not `update`.

### 🙈 `.gitignore`: things Git should never see

Create a `.gitignore` file in the repo root:

```gitignore
venv/
env/
__pycache__/
.ipynb_checkpoints/
.env
*.log
```

Virtual environments, secrets and checkpoints don't belong on GitHub. (More in [notes-virtual-env.md](notes-virtual-env.md).)

## 🌿 Branching

Branches let you experiment without breaking `main`.

```bash
git branch                     # list branches
git switch -c feature/eda      # create and switch
git switch main                # go back
git merge feature/eda          # merge into current branch
git branch -d feature/eda      # delete after merging
```

## 🛟 Undo & Rescue

| Situation | Command |
|:----------|:--------|
| Discard changes to a file (careful, it's gone) | `git restore <file>` |
| Unstage a file | `git restore --staged <file>` |
| Fix the last commit message | `git commit --amend -m "new message"` |
| Undo a commit safely (keeps history) | `git revert <commit-hash>` |
| Undo last commit, keep changes staged | `git reset --soft HEAD~1` |
| Park unfinished work temporarily | `git stash` then `git stash pop` |

> ⚠️ `git reset --hard` deletes uncommitted work permanently. Use it only when you mean it.

## 🔗 Extra: Tracking a Remote Branch

**Case 01: you're on `main` and have added `origin`**

- Full: `git branch --set-upstream-to=origin/main main`
- Short: `git branch -u origin/main main`

**Case 02: you're on another branch and have added `origin`**

- Full: `git branch --set-upstream-to=origin/main`
- Short: `git branch -u origin/main`

## 🚨 Errors & Fixes

### `failed to push some refs to 'https://github.com/....git'`

**Cause:** the remote has commits you don't have locally.
**Fix:** bring them in first, then push again.

```bash
git pull origin main
```

### `refusing to merge unrelated histories`

**Cause:** the two repos grew up separately and share no common history (classic when GitHub created a README and you also ran `git init` locally).
**Fix:**

```bash
git pull origin main --allow-unrelated-histories
```
