# 🐙 DevOps Core Services: Git & GitHub Reference
![git](https://github.com/shyamdevk/Basics-of-GIT-GitHub/blob/image/git.gif)

This repository provides a **comprehensive and practical guide** to using **Git** and **GitHub** — the two most essential tools for version control and collaborative development in DevOps workflows.

---

## 📘 Table of Contents
- [💾 What is a Version Control System (VCS)?](#-what-is-a-version-control-system-vcs)
- [⚙️ Git Basics](#️-git-basics)
- [🌳 Git Project Areas](#-git-project-areas)
- [🛠️ Basic Git Commands](#️-basic-git-commands)
- [🌿 Branching in Git](#-branching-in-git)
- [🤝 Git Merge](#-git-merge)
- [🔄 Branching Strategies](#-branching-strategies)
- [🧹 Advanced Git Commands](#-advanced-git-commands)
- [☁️ GitHub Overview](#️-github-overview)
- [⚙️ Clone vs Fork](#️-clone-vs-fork)
- [📤 Push, Pull & Fetch](#-push-pull--fetch)
- [🔑 Personal Access Token (PAT)](#-personal-access-token-pat)

---

## 💾 What is a Version Control System (VCS)?

A **Version Control System (VCS)** tracks and records changes to files over time, allowing developers to:
- Roll back to previous versions.
- Collaborate without overwriting each other’s work.
- Track who made what change and when.

### 🧩 Difference Between CVCS and DVCS

| Feature | Centralized VCS (CVCS) | Distributed VCS (DVCS) |
|----------|------------------------|--------------------------|
| Repository Storage | One central server stores the repository. | Every developer has the full repository on their machine. |
| Workflow | Developers check out, edit, then check in. | Developers can commit locally and sync later. |
| Network | Requires a constant connection. | Works offline; faster operations. |
| Safety | Server failure = work stops. | Any developer can restore from a full copy. |
| Examples | Subversion (SVN), CVS | Git, Mercurial |

---

## ⚙️ Git Basics

Git is a **Distributed Version Control System (DVCS)** created by **Linus Torvalds** in 2005.

### 🚀 Why Git?
- **Speed** – optimized for large projects.
- **Data Integrity** – uses cryptographic hashes (SHA-1/SHA-256).
- **Distributed** – every developer has a full copy.
- **Branching & Merging** – efficient and flexible.

---

## 🌳 Git Project Areas

Git organizes your project into four main areas:

1. **Working Directory** – Where your actual files exist.
2. **Staging Area (Index)** – Snapshot of what you plan to commit.
3. **Local Repository** – History of commits stored in `.git/`.
4. **Remote Repository** – Shared copy (e.g., GitHub, GitLab).

---

## 🛠️ Basic Git Commands

| Command | Purpose | Example |
|----------|----------|----------|
| `git init` | Initialize a new Git repository. | `git init` |
| `git status` | Show modified/staged files. | `git status` |
| `git add <file>` | Stage a file for commit. | `git add index.html` |
| `git add .` | Stage all changes. | `git add .` |
| `git commit -m "message"` | Commit staged changes. | `git commit -m "Initial commit"` |
| `git commit -am "message"` | Add & commit tracked files directly. | `git commit -am "Quick update"` |
| `git diff` | Compare working vs staging area. | `git diff` |
| `git diff --staged` | Show staged changes. | `git diff --staged` |

🧠 **Example Workflow:**
```bash
git init
git add .
git commit -m "My first commit"
````

---

## 🌿 Branching in Git
![git](https://github.com/shyamdevk/Basics-of-GIT-GitHub/blob/image/branch.gif)

A **branch** is like a timeline — it allows parallel development without affecting the main code.

### 🔹 Types of Branches

| Branch            | Purpose                          | Example                  |
| ----------------- | -------------------------------- | ------------------------ |
| `main` / `master` | Stable production code.          | `main`                   |
| `feature/*`       | New feature development.         | `feature/login-page`     |
| `bugfix/*`        | Fixing non-critical bugs.        | `bugfix/form-validation` |
| `hotfix/*`        | Urgent production fixes.         | `hotfix/payment-error`   |
| `dev`             | Experimental or unstable branch. | `dev`                    |

### 🧭 Branch Commands

| Command                 | Description                    |
| ----------------------- | ------------------------------ |
| `git branch`            | List all branches.             |
| `git branch <name>`     | Create a new branch.           |
| `git switch -c <name>`  | Create & switch to new branch. |
| `git checkout <name>`   | Switch to another branch.      |
| `git branch -d <name>`  | Delete branch safely.          |
| `git branch -D <name>`  | Force delete branch.           |
| `git branch -m old new` | Rename branch.                 |

---

## 🤝 Git Merge

Merging combines two branches’ histories.

### 🧩 Example:

```bash
git checkout main
git merge feature/login-page
```

> The source branch remains unchanged; only the target (main) is updated.

### ⚔️ Merge Conflict Example

When two branches modify the same line:

```text
<<<<<<< HEAD
Hello from main branch
=======
Hello from feature branch
>>>>>>> feature
```

**To fix:**

1. Edit the file and remove conflict markers.
2. Stage and commit:

   ```bash
   git add hello.txt
   git commit -m "Resolved merge conflict"
   ```

---

## 🔄 Branching Strategies

### 1. **Gitflow**

* `main`: production-ready code
* `develop`: integration branch
* `feature/*`, `release/*`, `hotfix/*` support structured releases.

### 2. **GitHub Flow**

* Single branch `main`.
* Short-lived branches for each feature.
* Continuous deployment with PR review.

### 3. **Trunk-Based Development**

* Everyone commits small, frequent updates to `main`.
* Uses **feature toggles** to control unfinished features.

---

## 🧹 Advanced Git Commands

### 🔁 Git Rebase

Rebase moves commits to a new base branch — makes history linear.

```bash
git checkout feature
git rebase main
```

---

### 📦 Git Stash

Temporarily save uncommitted changes.

| Command           | Purpose                                |
| ----------------- | -------------------------------------- |
| `git stash`       | Save uncommitted changes.              |
| `git stash list`  | Show saved stashes.                    |
| `git stash pop`   | Restore & delete latest stash.         |
| `git stash apply` | Restore latest stash without deleting. |
| `git stash clear` | Remove all stashes.                    |

**Example:**

```bash
git stash
git pull origin main
git stash pop
```

---

### 🔄 Reset vs Revert

| Command      | Purpose                       | Effect              | Safe? |
| ------------ | ----------------------------- | ------------------- | ----- |
| `git reset`  | Undo commits/move HEAD        | Rewrites history    | ❌     |
| `git revert` | Undo by creating a new commit | Keeps history clean | ✅     |

**Example:**

```bash
git reset --hard HEAD~1    # Removes last commit
git revert <commit-id>     # Safely undo one commit
```

---

### 🍒 Git Cherry-pick

Apply a specific commit from another branch:

```bash
git cherry-pick <commit-id>
```

---

## ☁️ GitHub Overview

**GitHub** is a cloud platform for storing Git repositories, enabling collaboration and CI/CD workflows.

### 🔧 Core Features

* **GitHub Actions:** Automate build/test/deploy using YAML workflows.
* **GitHub Packages:** Store artifacts (npm, Docker, etc.).
* **GitHub Projects:** Track tasks with boards and timelines.
* **GitHub Codespaces:** Cloud-based development environment.
* **GitHub Marketplace:** Pre-built automation tools.

---

## ⚙️ Clone vs Fork

| Feature                | Clone                   | Fork                              |
| ---------------------- | ----------------------- | --------------------------------- |
| Definition             | Copy repo locally.      | Copy repo to your GitHub account. |
| Connected to original? | Yes                     | No                                |
| Purpose                | Contribute directly.    | Experiment or propose changes.    |
| Command                | `git clone <repo-link>` | Click **Fork** on GitHub.         |

---

## 📤 Push, Pull & Fetch

<table>
  <tr>
    <td><img src="https://github.com/shyamdevk/Basics-of-GIT-GitHub/blob/image/pull.gif" width="450"></td>
    <td><img src="https://github.com/shyamdevk/Basics-of-GIT-GitHub/blob/image/push.gif" width="450"></td>
  </tr>
</table>


These commands sync changes between your **local** and **remote** repositories.

### 🔼 Git Push

Uploads your local commits to the remote repo.

```bash
git push <remote> <branch>
# Example:
git push origin main
```

### ⬇️ Git Pull

Downloads and merges changes from the remote.

```bash
git pull <remote> <branch>
# Example:
git pull origin main
```

### 👀 Git Fetch

Downloads changes but does **not** merge automatically.

```bash
git fetch origin
git log origin/main
```

### 🧩 Example Workflow

```bash
git clone https://github.com/user/project.git
cd project
git checkout -b feature/new-ui
# make changes
git add .
git commit -m "Added new UI design"
git push origin feature/new-ui
```

---

## 🔑 Personal Access Token (PAT)

A **Personal Access Token (PAT)** is used to authenticate GitHub operations via HTTPS (instead of your password).

### 🔐 Generate a PAT:

1. Go to **GitHub → Settings → Developer Settings → Personal Access Tokens → Tokens (Classic)**
2. Click **Generate new token**
3. Choose scopes like `repo`, `workflow`, `write:packages`
4. Copy and store it securely

**Use it during push/pull authentication**:

```bash
git push https://<username>@github.com/<repo>.git
# When prompted, enter your PAT instead of password
```

---

## 🧠 Summary

| Task             | Command Example        |
| ---------------- | ---------------------- |
| Initialize Repo  | `git init`             |
| Add Files        | `git add .`            |
| Commit Changes   | `git commit -m "msg"`  |
| Create Branch    | `git branch feature1`  |
| Merge Branch     | `git merge feature1`   |
| Push to GitHub   | `git push origin main` |
| Pull from GitHub | `git pull origin main` |
| Stash Changes    | `git stash`            |
| Revert Commit    | `git revert <id>`      |

---

## 🏁 Conclusion

Git and GitHub are the backbone of modern DevOps workflows.
Mastering them enables:

* Seamless collaboration 👥
* Clean version control 🧩
* Automated CI/CD pipelines ⚙️

---

### 💡 Tip

> “Commit often, push regularly, and document everything — good Git habits save hours of debugging.”

---

### 📸 Screenshots & Diagrams

> *(You can manually upload screenshots here — for example: Git branching diagram, GitHub Actions workflow, etc.)*

---

**Author:** *Shyamdev K*
**License:** MIT
**Repository:** [Git & GitHub Reference Guide](https://github.com/your-shyamdevk/Basics-of-GIT-GitHub)

---

```

---

```
