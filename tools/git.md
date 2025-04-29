# Git

## Overview
Git is a distributed version control system for tracking changes in source code.

## Basic Commands
```bash
# Initialize
git init
git clone <url>

# Changes
git status
git add .
git commit -m "message"
git push origin main

# Branches
git branch feature
git checkout feature
git checkout -b feature
git merge feature
git branch -d feature

# Remote
git remote add origin <url>
git fetch origin
git pull origin main
git push -u origin main
```

## Workflow
```bash
# Feature branch workflow
git checkout -b feature/new-feature
# make changes
git add .
git commit -m "Add new feature"
git push -u origin feature/new-feature
# Create Pull Request
```

## Useful Commands
```bash
git log --oneline -10
git diff
git stash
git stash pop
git reset --hard HEAD~1
git revert <commit>
git cherry-pick <commit>
git rebase main
```

## Best Practices
1. Write **meaningful commit messages**
2. Use **feature branches**
3. **Pull before push**
4. Keep commits **atomic**

## Resources
- Pro Git Book
