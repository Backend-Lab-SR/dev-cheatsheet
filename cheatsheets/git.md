# Git Cheatsheet

## Basic Commands

```bash
# Initialize repository
git init

# Clone repository
git clone <url>
git clone <url> <directory-name>

# Check status
git status
git status -s  # Short format

# Add files
git add <file>
git add .  # Add all files
git add -A  # Add all changes including deletions
git add -u  # Add only modified files

# Commit changes
git commit -m "commit message"
git commit -am "commit message"  # Add and commit

# View commit history
git log
git log --oneline
git log --graph --oneline --all
git log -p  # With diffs
git log --stat  # With stats

```

## Branching

```bash
# List branches
git branch
git branch -a  # All branches including remote
git branch -r  # Remote branches only

# Create branch
git branch <branch-name>
git checkout -b <branch-name>  # Create and switch
git switch -c <branch-name>  # Modern way

# Switch branch
git checkout <branch-name>
git switch <branch-name>  # Modern way

# Delete branch
git branch -d <branch-name>  # Safe delete
git branch -D <branch-name>  # WARNING: Force delete

# Rename branch
git branch -m <old-name> <new-name>
git branch -m <new-name>  # Rename current branch

```

## Remote Operations

```bash
# List remotes
git remote -v

# Add remote
git remote add <name> <url>

# Remove remote
git remote remove <name>

# Fetch from remote
git fetch
git fetch <remote>
git fetch --all

# Pull changes
git pull
git pull <remote> <branch>
git pull --rebase  # Pull with rebase

# Push changes
git push
git push <remote> <branch>
git push -u <remote> <branch>  # Set upstream
git push --all  # Push all branches
git push --tags  # Push tags

# Show remote branches
git branch -r

```

## Stashing

```bash
# Stash changes
git stash
git stash save "message"
git stash push -m "message"

# List stashes
git stash list

# Apply stash
git stash apply
git stash apply stash@{0}

# Pop stash (apply and remove)
git stash pop

# Drop stash
git stash drop stash@{0}

# Clear all stashes
git stash clear

# Stash including untracked files
git stash -u
```

## Undoing Changes

```bash
# Discard changes in working directory
git checkout -- <file>
git restore <file>  # Modern way

# Unstage file
git reset HEAD <file>
git restore --staged <file>  # Modern way

# Amend last commit
git commit --amend
git commit --amend -m "new message"

# Reset to previous commit
git reset --soft HEAD~1  # Keep changes staged
git reset --mixed HEAD~1  # Keep changes unstaged
# WARNING: Destructive command
# git reset --hard HEAD~1  # Discard changes

# Revert commit
git revert <commit-hash>
git revert HEAD  # Revert last commit

```

## Diff and Comparison

```bash
# Show changes
git diff
git diff <file>
git diff --staged  # Staged changes
git diff HEAD  # All changes

# Compare branches
git diff <branch1> <branch2>
git diff <branch1>..<branch2>

# Compare with remote
git diff origin/main

# Show file at specific commit
git show <commit-hash>:<file>
```

## Tagging

```bash
# List tags
git tag
git tag -l "v1.*"

# Create tag
git tag <tag-name>
git tag -a <tag-name> -m "message"  # Annotated tag

# Push tags
git push origin <tag-name>
git push --tags  # Push all tags

# Delete tag
git tag -d <tag-name>
git push origin --delete <tag-name>

```

## Advanced Commands

```bash
# Interactive rebase
git rebase -i HEAD~3
git rebase -i <commit-hash>

# Cherry-pick commit
git cherry-pick <commit-hash>

# Show commit details
git show <commit-hash>

# Find commit by message
git log --grep="search term"

# Find commit by content
git log -S "search term"

# Find file history
git log --follow <file>

# Blame (who changed what)
git blame <file>
```

## Configuration

```bash
# Set user name
git config --global user.name "Your Name"

# Set user email
git config --global user.email "your.email@example.com"

# List configuration
git config --list
git config --global --list

# Set editor
git config --global core.editor "vim"

# Set default branch name
git config --global init.defaultBranch main

# Set pull strategy
git config --global pull.rebase false

```

## Submodules

```bash
# Add submodule
git submodule add <url> <path>

# Initialize submodules
git submodule init
git submodule update
git submodule update --init --recursive

# Clone with submodules
git clone --recursive <url>

# Update submodules
git submodule update --remote

```

## Useful Aliases

```bash
# Add to ~/.gitconfig
[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    unstage = reset HEAD --
    last = log -1 HEAD
    visual = !gitk
    lg = log --oneline --decorate --graph --all
```
