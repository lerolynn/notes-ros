# Git

### Initialize Git Repository

---
`git init` - Creates new git repository (creates `.git` folder)

`git clone /path/to/repository` - Checkout repository.
This creates a local copy of a repository hosted on a server.

### Add and Commit

---

`git commit -a -m "Commit Message"` - Commit and add to __HEAD__

---

`git add <filename>` - Add specific folder of file to git staging area.

`git commit -m "Commit message"` - Commit files to __HEAD__.



### Push Changes

---
`git push` -  Push changes to server

---

`git push origin master` - Push changes to specific branch. (to origin master branch)

`git remote add origin <server>` - Connect repository to remote server if repository has not been cloned before.

### Configure Users

---

`git config --global user.name lerolynn` - Configures author username for commits to name specified.

---
`git config --global user.email lerolynn@gmail.com` - Configures author email for commits to email specified.

`git config --list` - Lists local configuration settings (eg. user.name, user.email)


### Branching

---

`git checkout master` - Switch back to master branch.

---
`git checkout -b new_branch_name` - Create a new branch and switch to it. (Branch only created locally unless pushed)
`git push origin <branch>` -  Push branch to remote repository.
`git branch -d unwanted_branch` - Delete branch.

### Update and Merge
---
`git pull` - Update local repository to newest commit. (Normally done before making any changes to local repository)

---
`git merge <branch_to_be_merged>` - merge branch to active (current) branch.

If there are conflicts while merging:

`git diff <source_branch> <target_branch>` - view differences in files.

Merge conflicts by manually editing files.

`git add <filename>` - Mark files as merged after changing files.

### Tagging
---
Tags are created for software releases.

`git tag 1.0.0 qwerty1234` - create tag 1.0.0 for commit id `qwerty1234`

### Log
---
`git log` - Check repository history.

---
`git log --author=lero` - See commits of certain author.

### Replace Local Changes
---
`git checkout -- <filename>` - Replaces changes in working tree with last content from __HEAD__. Changes added to index and new files are kept.

To drop all local changes and commits:

`git fetch origin` - Fetch latest history from server.

`git reset --hard origin/master` - Reset to local master branch.




## Source
https://rogerdudler.github.io/git-guide/
