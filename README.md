Here’s a clean list of Git commands mentioned in your handwritten notes, organized by sections:


---

Initializing a Repo

git init  # Initialize a Git repository in the root directory


---

Staging Files

git add file1.js  # Stage a single file
git add file1.js file2.js  # Stage multiple files
git add *.js  # Stage files matching a pattern
git add .  # Stage entire directory (all content)


---

Viewing the Status

git status  # Full status
git status -s  # Short status


---

Configuring Git

git config --global user.name "My name"
git config --global user.email "someone@email.com"
git config --list  # List current configuration


---

Push Command

git push origin main  # Push local repo content to remote repo


---

Init Command (Full Flow)

git init
git remote add origin <link>
git remote -v  # Verify remote link
git branch  # Check branch
git branch -M main  # Rename branch to main
git push origin main


---

Directory Navigation

cd ..  # Go out of the folder
mkdir LocalRepo  # Make a new folder


---

Branch Operations

git branch  # Check branches
git branch -M main  # Rename current branch to main
git checkout <branch_name>  # Navigate to existing branch
git checkout -b <branch_name>  # Create and switch to new branch
git branch -d <branch_name>  # Delete a branch


---

Setting Upstream (Push Shortcut)

git push -u origin main  # Set upstream so you can later just use 'git push'


---

Let me know if you want these in a downloadable format (PDF/Markdown).


