# Git Guide

Repo: https://github.com/TIMOTHY-glitch-hash/YU-FARMERS

Standard workflow for contributing to this repo. Follow this for every task, every time.

## 0. Get added as a collaborator (one-time, per person)

Before anyone can push, they need write access:

 Each teammate accepts the invite from their email or GitHub notifications

## 1. Clone the repo (one-time, per person)

```bash
git --version
```
If Git isn't installed, install it from git-scm.com first.

```bash
git clone https://github.com/TIMOTHY-glitch-hash/YU-FARMERS.git
cd YU-FARMERS
git status
```
Should say `On branch main, nothing to commit, working tree clean`.

## 2. Before starting any task, sync with main

```bash
git checkout main
git pull origin main
```

## 3. Create a branch for your task

Name it after the feature — lowercase, words separated by hyphens, **no spaces, commas, or special characters** (Windows PowerShell will misinterpret them as shell operators and either hang or fail to create the branch).

```bash
git checkout -b feature/auth-setup
```

Examples matching `CONTRIBUTORS.md`:
- `feature/auth-setup`
- `feature/listing-form`
- `feature/order-request`
- `feature/deployment-docs-demo`

Confirm you're on it:
```bash
git branch
```
The branch with `*` next to it should be your new one, not `main`.

**If a branch gets created wrong (e.g. with a bad name):**
```bash
git checkout main
git branch -D "bad-branch-name"
```

## 4. Work, then stage and commit

```bash
git status
git add .
git commit -m "Add farmer listing creation form"
```
Commit message should describe *what* the change does — not "update" or "fix stuff". Commit often, in small logical chunks.

## 5. Push your branch

```bash
git push -u origin feature/auth-setup
```
(`-u` only needed on the first push of that branch; after that, just `git push`)

If it asks to log in: use a GitHub personal access token, not your account password — GitHub no longer accepts passwords for git operations over HTTPS.

## 6. Open a Pull Request (PR)

1. Use the link Git prints after pushing (e.g. `https://github.com/TIMOTHY-glitch-hash/YU-FARMERS/pull/new/feature/auth-setup`)
2. Confirm base = `main`, compare = your branch
3. Add a title and short description of what you did
4. Under **Reviewers**, pick a teammate
5. Click **Create pull request**

## 7. Review and merge

1. Reviewer opens the **Files changed** tab and reviews line by line
2. Reviewer comments if something needs fixing, or **Review changes** → **Approve**
3. Once approved, go to **Conversation** tab → **Merge pull request** → **Confirm merge**
4. Click **Delete branch** to keep the branch list clean

## 8. Pull before starting the next branch

After any merge — including your own — everyone runs this before creating their next branch:
```bash
git checkout main
git pull origin main
```
This is the step people forget, and it's the #1 cause of merge conflicts.

## If you hit a merge conflict

```bash
git pull origin main
# Git marks conflicting files — open them, resolve the <<<<<<< / ======= / >>>>>>> blocks
git add <resolved-file>
git commit
git push
```

## The full cycle (repeat for every task)

**pull main → branch → work → commit → push → open PR → review → merge → pull main again**

## Ground rules

- Nobody pushes directly to `main` — always through a PR, even for small fixes
- Pull `main` before creating any new branch
- Keep branches short-lived — merge within a day or two, don't let them drift far from `main`
- No spaces or special characters in branch names