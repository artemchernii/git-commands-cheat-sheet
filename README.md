# 🥷 **_Git commands ultimate cheat sheet_** 🥷

### <i>Very basic and rare commands are not included in this list (like configs and so on)</i>

##### <i>In case you didn't find any commands you were looking - use google </i>😅😅😅

<hr>

## **_Useful commands:_**

```
$ git commit -am "commit message"
- add + commit command
$ git fetch
- check if there some changes in branch
$ git diff filename
- check diff of files
$ git checkout -b feature4[new branch] develop[origin branch]
- creating a Branch from Another Origin Branch
$ git checkout -b 'new branch name' 'starting point (parent branch)'

$ git pull origin <branch name> (git pull origin feature/addnavbar)
- download Branch from Remote Repository
$ git branch
- see all local branches
$ git checkout <branch name> (git checkout feature/addnavbar)
- switch to feature(or any other) branch

Merging Branches in a Local Repository:
$ git checkout main (or master or any another branch)
$ git merge jeff/feature1 (name of the branch you want to merge with)

$ git push --delete origin branch_name_here
- delete remote branch

$ git branch -d feature/login
- delete local branch
```

## **_Git push:_**

```
$ git push --set-upstream origin <branch name>
```

### What is merge with --squash ? It's basically when we merge with branch but add only one commit msg and ignore all new local commits in that branch

<hr>

```
$ git merge --squash feature/addnavbar
$ git commit -m "feat: my only one commit msg"
```

### What is rebase? Rebase is used to update ONLY feature branch with master(main). Squash multiple commits. !Reverting rebase would be very difficult!

<hr>

```
$ git checkout feature/addnavbar
$ git rebase master
```

### Merge with squash? In this case we merge to master the feature banch changes and combine all feature branch's commits in one we need

<hr>

```
$ git merge --squash feature/addnavbar
$ git commit -m "My only one commit msg"
```

### What is stash? We want to keep our changes in feature/fix branch without actually commiting it.

<hr>

```
$ git stash
- command to stash all changes (STAGED ONE) |
$ git stash -u
- to include unstaged
$ git stash push -m "describe this changes"
- stash changes with message
$ git stash apply 1(1 is index)
-apply first stash changes without deleting
$ git stash pop 1
-apply stash changes to the branch
$ git stash list
-shows list of stash items
$ git stash drop 2
-delete stash item with index 2
$ git stash clear
-clear list of stash items
$ git stash show
-show differences or add -p to show all diffs
```

### How to revert last(you pick) commit from history?

<hr>

#### Reseting:

```
$ git reset --soft HEAD~1
- this basically revert one last commit?
flags:
-soft flag not deleting all modified files in that commit
-hard will discard all changes made in commit
-mixed will remove files from git index but keep in directory
$ git reset --hard HEAD~1
- basically delete/remove last(or more) commit
$ git reset --hard origin/main
- gonna delete all local commits changes and pull all changes from remote branch main
$ git reset
- unstage all files but doesnt overwrite it
$ git reset "filename"
- unstage one file
$ git reset --hard
- unstage and overwrite all files (basically go back hard)
```

#### Reverting:

```
$ git revert HEAD
- a bit different method. In this case we add another commit where we saying that prev commit is reverted.
```

#### Amending:

Changing the last commit with --amend It lets you combine staged changes with the previous commit instead of creating an entirely new commit. It can also be used to simply edit the previous commit message without changing its snapshot.

```
$ git commit --amend -m "an updated commit message"
- basically just rewrite commit message for the last commit
```

## **_REBASE:_**

### Rebase itself has 2 main modes: "manual" and "interactive" mode.

#### Manual rebase:

```
$ git rebase <base>
- git rebase in standard mode will automatically take the commits in your current working branch and apply them to the head of the passed branch.
```

#### What is interactive rebase? it's where we can combine two specific commits into one or rename prevs commits.

```
$ git rebase -i HEAD~3
- we are targeting third 3 commit and are going to change it. Then in popup we should use special action word to make changes to specific commit

Interactive mode:
git rebase -i master
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
```

## **_REFLOG:_**

### What is reflog? Reflogs track when Git refs were updated in the local repository. Reflog basically show all local activities.

```
$ git reflog
- shows all commits
$ git branch "our branch" "hash of commit"
- here we can bring back our deleted commit
$ git diff main@{0} main@{1.day.ago}
- diff the current main branch against main 1 day ago
```

## **_USEFUL LOGS:_**

```
$ git log --oneline
- check commit history
$ git log --oneline --graph --decorate
$ git log --oneline --stat --- show nice logs with files that have been modified
```

### What if we need to search specific commits where someone changed specific files? Basically we can find by author or by file

```
$ git log -- "FILENAME"
$ git log --author="NAME"
$ git log --pretty=format:"%h%x09%an%x09%ad%x09%s"
- the best logs with author and date
```

### Realize you forgot to add the changes from main.py

```
$ git add main.py
$ git commit --amend --no-edit
$ git commit --amend
lets you take the most recent commit and add new staged changes to it
```

## **_GIT CLEAN:_**

### To remove untracked files use git clean:

```
$ git clean -n
- will show which files are going be removed
$ git clean -f
- actually remove delete these files
```

## **_OTHER USEFUL COMMANDS RELATED TO REWRITING HISTORY:_**

### What is cherry-pick? it basically allows you to select individual commits to be integrated. In case you commited in wrong branch and want that commit in another one.

```
$ git cherry-pick "hash of commit"
- pick specific commit to your branch
```

## **_GIT BRANCHE NAMING:_**

<hr>

### REGULAR BRANCHES:

- master --- master stable branch
- dev --- development branch
- qa --- contains all the code for testing

### TEMPORARY BRANCHES:

- Bug fix
- Hot fix
- Feature branch
- WIP

### EXAMPLE:

- wip-8712-add-testing-module
- bug-logo-alignment-issue

## **_GIT ADDITIONAL USEFUL COMMANDS:_**

<hr>

- git clone -branch new_feature git://remoterepository.git ---- clone specific branch of repo

- git diff main new_branch ./diff_test.txt --- To compare a specific file across branches, pass in the path of the file as the third argument to git diff

- git stash branch add-stylesheet stash@{1} --- basically create a new branch from stash 1

- git tag -a v1.0 "commit" -m "My msg" --- creating tag for specific commit
- git tag --- list of tags | by tag you can push it to origin

- git blame README.md --- show who was chaneging this README file and when and basically first line of the content.

## **_CHECKOUT STARTEGY TO UNDO SOMETHING_**

<hr>

### In case we have 3 commits:

1-bad
2-good
3-good

### What we do:

```
$ git log --oneline
$ git checkout GOODCOMMITHASH
$ git checkout -b "new branch with good commit where its last one"
```

## **_PULL REQUEST:_**
