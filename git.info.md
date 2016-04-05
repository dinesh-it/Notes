## Git and Github useful commands ##

### Working on a personal forked repo ###
[Click here for full documentation of what is fork and how to fork a repo from github](https://help.github.com/articles/fork-a-repo/)
* `git clone git@github.com:<your-github-id>/Project.git` - clone your forked Project personal repo
* `cd Project/` - get into your repository
* `git fetch origin` - fetch all the details/indexes (branches and commits) from **remote origin**
* `git branch` - check all the available branches and check current working branch (working branch will have \*\<branch name\>).
* `git checkout origin/master` - change your current working branch to master.
* `git pull origin master` - update your local branch to with your fork repo in the remote(origin)
* `git add file_path` - add this file to commit
* `git rm file_path` - delete file from git
* `git commit` - commit your changes (It is allways good to **have your repo uptodate(pull the code) before you do a commit** else you will be getting a merge commit).
* `git push origin master` - push your commits to remote repo.

### Changing the last commit ### 
* **Don't use this if you pushed the code to remote repo (specifically public repo) - because you have to do -f push which will change the history of others commit also if any.**
* Do all the changes same as you do for a normal commit (`add` , `rm`) and do commit with --amend flag
* `git commit --amend` this will overwrite your last commit, don't worry your previous changes will also be there. 
* If you just want to change the commit message, enter this command which will prompt you for commit message with last commit message pre filled.
* Ref: [Changing the last commit](http://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#Changing-the-Last-Commit)

### What is git stash? ###
* It is simply a backup for your local modified files since last commit of the current branch.
* `git stash save` - save/backup modified files
* `git stash list` - list all the saved stash
* `git stash pop` - apply saved/backed up files to the current branch

### Sync/Update your fork(personal repo) with the upstream(remote repo) ###
* `git remote -v` - to list out all the remote repos(remote url's and it alias name) you added.
* `git remote add upstream git@github.com:remote/Project.git` - add upstream as a remote which points to main repository of your project
* `git remote -v` - see all remotes
* `git fetch upstream` - fetch all the details(branches and commits) from remote "upstream"
* `git stash save` - Save your local changes if any
* `git pull --rebase upstream master` - update your local repo with upstream repo ( --rebase is used to avoid merge commit )
* `git satsh pop` - if you did stash save before
* `git push origin <branch_name>` - update your fork with the local changes
* Ref: [Sync a fork with upstream](https://help.github.com/articles/syncing-a-fork/)

### Merge/Squash branches
* To merge all the changes from branch1 to current branch
* `git merge --squash <branch1>` this commmand will get all the changes from your branch1 to your current branch and will not commit it. You can see the modified files using `git status`. 
* Now proceed to commit as usual and dont forget to delete the branch1, else your changes will still be there and create problem when you do merge (squash) for next fix.
* Other way to squash commits is using rebase - you can read about this at [Squash several git commits into single commit using rebase -i](http://makandracards.com/makandra/527-squash-several-git-commits-into-a-single-commit)
* Ref: [git merge doc](https://www.kernel.org/pub/software/scm/git/docs/git-merge.html)

### Update/sync a branch with other branch changes ###
```bash
git checkout <fix1_branch>
git rebase <sync_from_branch>(can be master)
``````
or
`git rebase <sync_from_branch> <fix1_branch>`
this will update your branch and apply all the changes of current branch on top of it.
* **rebase will update the git log also, whereas squash will just merge the changes**

### Reset your fork to upstream ###
* You messed up your fork and wanted to reset your fork to upstream as if you forked freshly.
* `git reset --hard upstream/master` - your all local changes will be **WIPED OUT** (master is a branch name you want to reset to from upstream)
* Now update your fork forcely - `git push origin <branch> -f`

### Creating and applying patch ###
* #### Creating patch files ####
    * Patch of an **entire branch** `git format-patch master --stdout > fix_branch.patch` - your current branch should be \<fix_branch\>.
    * Above command will create a new file fix_branch.patch with all changes from the current branch (fix_branch) against master branch.
    * Create patch for a **single commit** `git format-patch -1 commitssh --stdout > commit_name.patch`

* #### Applying patch ####
    * Check what are all the changes in the patch using `git apply --stat fix_branch.patch`
    * Check whether you have any issues appying this patch by `git apply --check fix_branch.patch`
    * Now apply the patch using `git apply < fix_branch.patch` - you can see the applied changes in `git status`
    * When you apply patches created from someone else you can use `git am --signoff < fix_branch.patch` - so that signed off message will be appended to your commit.
    - Alternatively you can use patch command `patch -p1 < path/file.patch` Ref:[Patch apply](https://www.drupal.org/patch/apply)
* Ref: [Create and apply a patch with git](https://ariejan.net/2009/10/26/how-to-create-and-apply-a-patch-with-git/)

### Good to read ###
* [25 Tips for intermediate git users](https://www.andyjeffries.co.uk/25-tips-for-intermediate-git-users/)
* [Git branch doc](http://git-scm.com/book/en/v1/Git-Branching-What-a-Branch-Is) or [Git branch tutorial](https://www.atlassian.com/git/tutorials/using-branches/git-branch)
* [Effective pull requests and other good practices for teams using github](http://codeinthehole.com/writing/pull-requests-and-other-good-practices-for-teams-using-github/)
* [Fixup earlier commit](http://stackoverflow.com/questions/204461/git-squash-fixup-earlier-commit)
* [Merge vs Rebase](https://www.atlassian.com/git/tutorials/merging-vs-rebasing/)
