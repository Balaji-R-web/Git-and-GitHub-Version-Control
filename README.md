# Project 8: Git and GitHub Version Control Project

## 1. Project Overview

This project demonstrates how to use Git for version control and GitHub for hosting source code. It covers repository initialization, staging files, commits, branches, merging, remote repositories, pushing changes, pulling updates, and resolving merge conflicts.

## 2. Objectives

- Understand Git and GitHub fundamentals.
- Initialize a local Git repository.
- Track and commit file changes.
- Create and switch branches.
- Merge branches.
- Connect a local repository to GitHub.
- Push and pull code changes.
- Practice basic merge-conflict resolution.
- Use `.gitignore` to exclude unnecessary files and sensitive information.

## 3. Environment

- Operating system: Amazon Linux 2023 or another Linux distribution
- Tools: Git, Linux terminal, GitHub account
- Repository type: Local Git repository connected to a GitHub remote

> **Note:** Sample outputs are illustrative. Replace `YOUR_GITHUB_USERNAME` with your GitHub username. Never commit passwords, private SSH keys, access tokens, or cloud credentials.

## 4. Step 1: Install Git

Check whether Git is installed:

```bash
git --version
```

Example output:

```text
git version 2.x.x
```

If Git is missing on Amazon Linux:

```bash
sudo dnf install git -y
```

Verify the installation:

```bash
git --version
```

## 5. Step 2: Configure Git

Configure your Git username and email:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Verify the configuration:

```bash
git config --global --list
```

Example output:

```text
user.name=Your Name
user.email=your-email@example.com
```

**Explanation:** Git records the configured name and email in commit metadata. Use an email appropriate for your GitHub account.

## 6. Step 3: Create a Project Directory

Create the project directory and navigate into it:

```bash
mkdir git-github-version-control
cd git-github-version-control
```

Create a sample README:

```bash
cat > README.md <<'EOF'
# Git and GitHub Version Control Project

This repository demonstrates Git version control,
branching, merging, and GitHub integration.
EOF
```

Create a sample script:

```bash
cat > hello.sh <<'EOF'
#!/bin/bash
echo "Hello from my Git project!"
EOF
```

Make the script executable:

```bash
chmod +x hello.sh
```

List the files:

```bash
ls -l
```

Example output:

```text
-rw-r--r-- README.md
-rwxr-xr-x hello.sh
```

## 7. Step 4: Initialize the Git Repository

Initialize Git:

```bash
git init -b main
```

If your installed Git version does not support `-b main`, use:

```bash
git init
git branch -M main
```

Check the repository status:

```bash
git status
```

Example output:

```text
On branch main

No commits yet

Untracked files:
  README.md
  hello.sh
```

**Explanation:** `git init` creates the local repository. Git identifies new files as untracked until they are staged.

## 8. Step 5: Stage and Commit Files

Stage both files:

```bash
git add README.md hello.sh
```

Check the staged changes:

```bash
git status
```

Commit the files:

```bash
git commit -m "Initial commit: add project files"
```

Example output:

```text
[main (root-commit) abc1234] Initial commit: add project files
 2 files changed
 create mode 100644 README.md
 create mode 100755 hello.sh
```

Verify the commit:

```bash
git log --oneline
```

Example output:

```text
abc1234 Initial commit: add project files
```

**Explanation:**
- `git add` stages changes.
- `git commit` saves a snapshot in the local repository.
- `git log` displays commit history.

## 9. Step 6: Modify and Track Changes

Append a new line to the README:

```bash
echo "" >> README.md
echo "## Skills Demonstrated" >> README.md
echo "- Git fundamentals" >> README.md
echo "- Branching and merging" >> README.md
```

View the changes:

```bash
git diff
```

Stage and commit the update:

```bash
git add README.md
git commit -m "Update project documentation"
```

Check the history:

```bash
git log --oneline
```

Example output:

```text
def5678 Update project documentation
abc1234 Initial commit: add project files
```

**Explanation:** `git diff` helps review changes before staging them.

## 10. Step 7: Create and Switch Branches

Create a feature branch:

```bash
git branch feature-update
```

Switch to it:

```bash
git switch feature-update
```

Alternatively, create and switch in one command:

```bash
git switch -c feature-documentation
```

List the branches:

```bash
git branch
```

Example output:

```text
* feature-documentation
  feature-update
  main
```

The asterisk indicates the currently checked-out branch.

## 11. Step 8: Make Changes on a Feature Branch

Add a feature to the sample script:

```bash
cat >> hello.sh <<'EOF'

echo "Version control makes changes easier to track."
EOF
```

Check the difference:

```bash
git diff
```

Stage and commit:

```bash
git add hello.sh
git commit -m "Add version control demonstration"
```

Example output:

```text
[feature-documentation 123abcd] Add version control demonstration
 1 file changed
```

## 12. Step 9: Merge the Feature Branch

Switch back to the main branch:

```bash
git switch main
```

Merge the feature branch:

```bash
git merge feature-documentation
```

Example output:

```text
Updating abc1234..123abcd
Fast-forward
 hello.sh | ...
```

Verify the script:

```bash
cat hello.sh
```

Verify the history:

```bash
git log --oneline --graph --all
```

**Explanation:** Merging integrates changes from a feature branch into the current branch. The exact output depends on the repository history.

## 13. Step 10: Create a GitHub Repository

1. Sign in to GitHub.
2. Create a new repository named `git-github-version-control`.
3. Choose public or private according to your preference.
4. For this lab, create an empty repository without initializing another README, license, or `.gitignore`.

Copy the repository's HTTPS URL. It will resemble:

```text
https://github.com/YOUR_GITHUB_USERNAME/git-github-version-control.git
```

Connect your local repository:

```bash
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/git-github-version-control.git
```

Check the remote:

```bash
git remote -v
```

Example output:

```text
origin  https://github.com/YOUR_GITHUB_USERNAME/git-github-version-control.git (fetch)
origin  https://github.com/YOUR_GITHUB_USERNAME/git-github-version-control.git (push)
```

## 14. Step 11: Push Code to GitHub

Push the main branch:

```bash
git push -u origin main
```

GitHub may prompt you to authenticate. For HTTPS, use an approved authentication method, such as Git Credential Manager or a personal access token when required. Do not place tokens directly in commands or commit them to files.

Example output:

```text
To https://github.com/YOUR_GITHUB_USERNAME/git-github-version-control.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

Verify the files on your GitHub repository page.

## 15. Step 12: Push a Feature Branch

Push the feature branch:

```bash
git push -u origin feature-documentation
```

Open GitHub and check the **Branches** page. You can create a pull request to propose merging the feature branch into `main`.

**Explanation:** Pushing uploads local commits to the remote repository. A pull request supports code review before merging changes.

## 16. Step 13: Pull Remote Changes

Fetch and integrate remote changes:

```bash
git pull --ff-only origin main
```

**Explanation:** This command updates the current branch from the remote when Git can perform a fast-forward. If it fails because the branches have diverged, inspect the repository history before deciding whether to merge or rebase.

Check the status:

```bash
git status
```

Example output:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

## 17. Step 14: Create a `.gitignore` File

Create a `.gitignore` file:

```bash
cat > .gitignore <<'EOF'
*.log
.env
.venv/
__pycache__/
*.pem
*.key
EOF
```

Stage and commit it:

```bash
git add .gitignore
git commit -m "Add Git ignore rules"
```

Push the change:

```bash
git push origin main
```

**Explanation:** `.gitignore` tells Git which untracked files to ignore. It does not automatically remove files that are already tracked. Never rely on `.gitignore` alone to protect secrets.

## 18. Step 15: Practice Merge-Conflict Resolution (Optional)

A merge conflict occurs when Git cannot automatically reconcile competing changes.

For a safe practice lab, create a separate test branch and edit the same line differently in two branches. Commit both changes, then merge one branch into the other.

If Git reports a conflict, inspect the affected file:

```bash
git status
```

Conflict markers may look like this:

```text
<<<<<<< HEAD
This is the change on the current branch.
=======
This is the change on the other branch.
>>>>>>> other-branch
```

Edit the file to keep the correct final content and remove all conflict markers.

Stage the resolved file:

```bash
git add README.md
```

Complete the merge if Git has paused for conflict resolution:

```bash
git commit
```

Verify the result:

```bash
git status
git log --oneline --graph --all
```

**Explanation:** Always review the resolved file before committing. Do not blindly accept one side if both contain important changes.

## 19. Step 16: Useful Git Commands

| Command | Purpose |
|---|---|
| `git status` | Check repository status |
| `git add .` | Stage changes in the current directory and below |
| `git commit -m "message"` | Commit staged changes |
| `git log --oneline` | View commit history |
| `git diff` | View unstaged changes |
| `git branch` | List branches |
| `git switch main` | Switch branches |
| `git merge branch-name` | Merge a branch into the current branch |
| `git remote -v` | View remote repositories |
| `git fetch origin` | Download remote references |
| `git pull` | Fetch and integrate remote changes |
| `git push` | Upload local commits |
| `git clone URL` | Copy a remote repository locally |
| `git restore filename` | Discard unstaged changes to a file |
| `git rm --cached filename` | Stop tracking a file while retaining it locally |

**Caution:** `git restore filename` can discard your uncommitted edits. Review `git status` and `git diff` first.

## 20. Project Outcome

After completing this project, I can:

- Create and manage Git repositories.
- Stage, commit, and inspect changes.
- Work with branches and merge feature changes.
- Connect a local repository to GitHub.
- Push and pull changes.
- Understand basic pull-request workflows.
- Resolve simple merge conflicts.
- Apply `.gitignore` and credential-handling best practices.

## 21. Tools and Technologies

- Linux
- Git
- GitHub
- Bash
- HTTPS-based Git authentication

## 22. Conclusion

This project provides practical experience with Git and GitHub workflows used in software development, cloud engineering, and DevOps. Version control helps track changes, collaborate with others, review code, and maintain a reliable project history.
