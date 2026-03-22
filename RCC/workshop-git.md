# Git Workshop

Hosted by the Roadrunner Connect Club

## What is Git?

Git is a Version Control System

| Think of it as a "save history" for your code.

1. Tracks every change made to your files over time
2. Lets you revert to any previous state if something breaks
3. Enables collaboration — multiple people can work on the same project
4. Branches keep experiments isolated from stable code

## Installing and Configuring Git

**macOS** (via Homebrew):

```shell
brew install git
```

**Linux** (Debian/Ubuntu):

```shell
sudo apt install git
```

**Windows**: Download the installer from [git-scm.com](https://git-scm.com)

Then configure your identity — Git attaches these to every commit you make:

```shell
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Verify your config was saved:

```shell
git config --list
```

## The Building Blocks of Git

**Repository:**
A folder tracked by Git. Contains all your files and their full history.

**Commit:**
A snapshot of your changes. Like pressing save with a message describing what changed and why.

**Branch:**
An independent line of development. `main` is the default branch. You can create branches to work on features without affecting stable code.

**Merge:**
Combine changes from one branch into another. Typically used to bring a feature branch back into `main`.

**Remote:**
A copy of your repository hosted online (i.e., GitHub, GitLab, Azure DevOps). Lets you share your work and collaborate with others.

**HEAD:**
A pointer to your current position in the commit history. Usually points to the tip of your current branch.

## Your First Repository

```shell
# Create a new project folder and initialize Git
mkdir hello-git
cd hello-git
git init

# Create a file and stage it
echo "Hello, World!" > README.md
git add README.md

# Save your first snapshot
git commit -m "initial commit"
```

### Useful Commands

`git status`

Check the status of your current changes — shows which files are staged, unstaged, or untracked.

| Color   | State                  | Description                                                                |
| ------- | ---------------------- | -------------------------------------------------------------------------- |
| Red     | Untracked / Unmodified | Files Git doesn't know about yet, or files with changes that aren't staged |
| Green   | Staged                 | Files you've run `git add` on. They're ready to be committed.              |
| Nothing | Clean                  | Your working directory matches the last commit.                            |

---

`git add [file]`

Tells Git to stage a file, making it ready to be committed.

- Stage a single file: `git add README.md`
- Stage everything: `git add .`

Using `git restore --staged [file]` unstages a file without discarding your changes.

---

`git commit -m "[message]"`

Saves a snapshot of your staged changes with a descriptive message.

```shell
git commit -m "add login page"
```

---

`git branch`

List all branches in your repo. The branch you're currently on is marked with `*`.

- Create a new branch: `git branch feature/login`
- Delete a branch: `git branch -d feature/login`

---

`git checkout [branch]`

Switch to a different branch. Your working directory updates to reflect that branch's state.

- Create and switch in one step: `git checkout -b feature/login`

> **Note:** `git switch` is the modern alternative to `git checkout` for switching branches.

---

`git merge [branch]`

Merge the specified branch into your current branch.

```shell
git checkout main
git merge feature/login
```

---

## Git Conflicts

A conflict occurs when two branches have changes to the same part of the same file and Git can't automatically decide which to keep.

**When does it happen?**
When you run `git merge` and Git finds overlapping edits.

**What it looks like:**

```
<<<<<<< HEAD
This is my version of the line.
=======
This is the other branch's version.
>>>>>>> feature/login
```

**How to resolve it:**

1. Open the conflicting file
2. Decide which version to keep (or combine them manually)
3. Delete the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
4. Stage the resolved file: `git add [file]`
5. Complete the merge: `git commit`

**Tips:**

- Use `git status` to see which files have conflicts
- VS Code and most IDEs have built-in conflict resolution tools
- When in doubt, communicate with your collaborator before resolving

---

### Git Stash

Sometimes, you need to switch to another branch or task, but you have uncommitted changes that you’re not ready to commit yet. Instead of committing or discarding these changes, you can stash them.

```shell
# Save your uncommitted changes to the stash
git stash

# View the list of stashed changes
git stash list

# Apply the last stashed changes to your working directory
git stash apply

# Apply and remove the stash in one step 
git stash pop
```

> **Tip**: Use `git stash save "description"` to label your stashes for clarity.

---

### .gitignore

A `.gitignore` file specifies which files or directories Git should ignore. This is useful for excluding temporary files, build outputs, or sensitive data.

Create a `.gitignore` file in the root of your repository and add the patterns for files you want to ignore:

```shell
# Ignore log files and node_modules
*.log
node_modules/

# Ignore system files
.DS_Store
Thumbs.db
```

> Good practice: Use a `.gitignore` template for your language or project type from [gitignore.io](https://www.toptal.com/developers/gitignore).