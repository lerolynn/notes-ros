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
you stash some work, leave it there for a while, and continue on the branch from which you stashed the work, you may have a problem reapplying the work. If the apply tries to modify a file that you’ve since modified, you’ll get a merge conflict and will have to try to r
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

 `git pull origin master` - To make sure branch is up to date. `git fetch` then `git merge` to update local repository with remote repository.

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

### Stash

---
`git stash` - Stash uncommited changes in local repository. (If don't want to commit yet.)

---

`git stash apply` / `git stash pop` - Reapply stashed changes.

`git stash drop` - Drop stashed changes.

`git stash show -p` - See changes between stashed and un-stashed work in most recent stash.

### Pull Requests

1. Copy or fork the remote repository on GitHub and clone the copy of the repository. `git clone <url>`

2, Create a new branch to work on changes. `git checkout -b <newbranch>`
3. Make changes locally and push changes to remote copy of the repository. `git push -u origin <newbranch>`
4. Make a pull request. On the original GitHub repository, press  `Compare and pull request` button.




## Source
https://rogerdudler.github.io/git-guide/

http://archaeogeek.github.io/foss4gukdontbeafraid/fixes/pullrequest.html
