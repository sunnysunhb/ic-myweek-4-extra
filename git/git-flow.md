# Git, Git-Flow, and Pull Requests: A Beginner's Guide

## Git Basics

### What is Git?
Git is a distributed version control system that tracks changes to your code, allowing multiple people to work together on the same project.

### Key Concepts
- **Repository (Repo)**: A project's folder containing all files and their history
- **Commit**: A snapshot of your files at a specific point in time
- **Branch**: An independent line of development

### Essential Commands

```bash
# Initialize a new repository
git init

# Check status of your files
git status

# Add files to staging area
git add filename    # Add specific file
git add .           # Add all files

# Commit changes
git commit -m "Your message describing the changes"

# View commit history
git log

# Create a new branch
git branch branch-name

# Switch to a branch
git checkout branch-name
# OR (newer syntax)
git switch branch-name

# Create and switch to a new branch
git checkout -b new-branch-name
# OR (newer syntax)
git switch -c new-branch-name

# Push changes to remote repository
git push origin branch-name

# Pull changes from remote repository
git pull origin branch-name
```

## Git-Flow Workflow

Git-Flow is a branching model designed to organize development work.

### Main Branches
- **main** (or master): Contains production-ready code
- **develop**: Integration branch for features

### Supporting Branches
- **feature/**: For developing new features
- **release/**: For preparing a new release
- **hotfix/**: For fixing critical bugs in production

### Workflow Example

```bash
# Create a feature branch from develop
git checkout develop
git pull
git checkout -b feature/new-feature

# Work, commit changes
git add .
git commit -m "Add new feature"

# Push feature branch to remote
git push origin feature/new-feature

# When feature is complete, merge back to develop (via Pull Request)
```

## Pull Requests

Pull Requests (PRs) are a way to propose changes, discuss them, and merge them into another branch.

### PR Process

1. **Create a branch** for your feature/fix
2. **Make changes** and commit them
3. **Push** your branch to the remote repository
4. **Create a Pull Request** in GitHub/GitLab/etc.
5. **Review** and discuss the changes
6. **Merge** the PR when approved

### PR Best Practices

- Give your PR a clear, descriptive title
- Describe what changes you made and why
- Keep PRs focused on a single task
- Request reviews from relevant team members
- Address all comments and feedback
- Make sure CI/tests pass before merging

## Practical Example: Feature Development with Git-Flow

```bash
# 1. Start from develop branch
git checkout develop
git pull

# 2. Create a feature branch
git checkout -b feature/login-page

# 3. Make changes, commit frequently
git add login.html
git commit -m "Create login form structure"
git add login.css
git commit -m "Add styling to login page"

# 4. Push your branch to remote
git push origin feature/login-page

# 5. Create Pull Request (through web interface)

# 6. After PR is approved and merged, clean up
git checkout develop
git pull
git branch -d feature/login-page
```

## Common Scenarios

### Dealing with Merge Conflicts

```bash
# When you encounter conflicts during merge or pull
git status  # See which files have conflicts
# Edit the files to resolve conflicts
git add .   # Mark as resolved
git commit  # Complete the merge
```

### Updating Your Branch with Latest Changes

```bash
# Get latest changes from develop while on your feature branch
git checkout feature/your-feature
git fetch origin
git merge origin/develop
# OR
git rebase origin/develop
```

### Undoing Changes

```bash
# Discard changes in working directory
git restore file.txt
# OR (older syntax)
git checkout -- file.txt

# Unstage files
git restore --staged file.txt
# OR (older syntax)
git reset HEAD file.txt

# Undo the last commit (keeping changes)
git reset --soft HEAD~1
```

## Visual Tools

If you prefer visual interfaces over command line:
- GitHub Desktop
- GitKraken
- SourceTree
- VS Code Git integration
