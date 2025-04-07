Got it! Here's a filtered list of the most important and commonly used Git commands — ideal for daily development and interviews:


---

1. Setup

git config --global user.name "Your Name"
git config --global user.email "your@email.com"


---

2. Initialize & Clone

git init                          # Initialize a Git repo
git clone <repo-url>             # Clone a repo from GitHub


---

3. Basic Workflow

git status                       # Check current changes
git add <file>                   # Stage a file
git add .                        # Stage all files
git commit -m "message"          # Commit with message


---

4. Branching

git branch                       # List branches
git branch <branch-name>         # Create branch
git checkout <branch-name>       # Switch branch
git checkout -b <branch-name>    # Create + switch branch


---

5. Merging & Pulling

git merge <branch>               # Merge into current branch
git pull origin <branch>         # Pull latest from remote


---

6. Pushing

git push origin <branch>         # Push branch to remote
git push -u origin <branch>      # First time push with upstream


---

7. Undo Changes

git reset <file>                 # Unstage file
git checkout -- <file>           # Discard local changes
git reset --hard                 # Reset everything to last commit


---

8. Logs & History

git log                          # View commit history
git log --oneline                # Compact log


---

9. Stashing

git stash                        # Save uncommitted changes
git stash apply                  # Re-apply stash


---

Would you like me to convert this into a cheat sheet PDF or add a few interview-specific commands too?

