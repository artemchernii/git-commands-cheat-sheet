# **_Git commands ultimate cheat sheet_**

### <i>Very basic and rare commands are not included in this list (like configs and so on)</i>

##### <i>In case you didn't find any commands you were looking - just find them in google :) </i>

<hr>

## **_Useful commands:_**

- add + commit msg:
  git commit -am "commit message"
- check if there some changes in branch
  git fetch
- check diff of files
  git diff filename
- creating a Branch from Another Branch
  git checkout -b feature4 develop
  git checkout -b 'new branch name' 'starting point (parent branch)'
- download Branch from Remote Repository
  git pull origin <branch name> (git pull origin feature/addnavbar)
  git branch
  git checkout <branch name> (git checkout feature/addnavbar)
  git branch
- merging Branches in a Local Repository
  git checkout main (or master or any another branch)
  git merge jeff/feature1 (name of the branch you want to merge with)
- merging Branches to Remote Repository (in case you want to keep branch on remote repo)

## **_Git push:_**

- git push --set-upstream origin <branch name>
- what is merge with --squash ? It's basically when we merge with branch but add only one commit msg and ignore all commits in that branch.
- git merge --squash feature/addnavbar
- git commit -m "feat: my only one commit msg"
- what is rebase? rebase is used to update ONLY feature branch with master(main). Squash multiple commits. reverting rebase would be very difficult
- git checkout feature/addnavbar
- git rebase master
- merge with squash? in this case we merge to master the feature banch changes and combine all feature branch's commits in one we need
- git merge --squash feature/addnavbar
- git commit -m "My only one commit msg"
- what is stash? we want to keep our changes in feature/fix branch without actually commiting it.
- git stash --- command to stash all changes (STAGED ONE) | to include unstaged add -u
- git stash push -m "describe this changes" --- stash changes with message
- git stash apply 1(1 is index) --- apply first stash changes without deleting
- git stash pop 1 --- apply stash changes to the branch
- git stash list --- shows list of stash items
- git stash drop 2 --- delete stash item with index 2
- git stash clear --- clear list of stash items
- git stash show --- show differences or add -p to show all diffs

- how to revert last(you pick) commit from history?
  git reset --soft HEAD~1 --- this basically revert one last commit? --soft flag not deleting all modified files in that commit. --hard will discard all changes made in commit. --mixed will remove files from git index but keep in directory

- git log --oneline --- check commit history
- git revert HEAD --- a bit different method. In this case we add another commit where we saying that prev commit is reverted.
- what is interactive rebase? it's where we can combine two specific commits into one or rename prevs commits.
  git rebase -i HEAD~3 --- we are targeting third 3 commit and are going to change it. Then in popup we should use special action word to make changes to specific commit
- what is cherry-pick? it basically allows you to select individual commits to be integrated. In case you commited in wrong branch and want that commit in another one.
- git cherry-pick "hash of commit" --- pick specific commit to your branch
- git reset --hard HEAD~1 --- in another branch where this commit should not be we delete it
- git reset --hard origin/main --- gonna delete all local commits changes and pull all changes from remote branch main
- git reset --- unstage all files but doesnt overwrite it
- git reset "filename" --- unstage one file
- git reset --hard --- unstage and overwriteall files (basically go back hard)
- what is reflog? reflog basically show of logs deleted and not
  git reflog --- shows all commits
  git branch "our branch" "hash of commit" --- here we can bring back our deleted commit
- what if we need to search specific commits where someone changed specific files? Basically we can find by author or by file
  git log -- "FILENAME"
  git log --author="NAME"

- amend? when you want to change commit msg of last commit
  git commit --amend -m "new msg"

## **_Good logs:_**

- git log --oneline --graph --decorate
- git log --oneline --stat --- show nice logs with files that have been modified

- git log --pretty=format:"%h%x09%an%x09%ad%x09%s" --- the best logs with author and date

## **_GIT BRANCHE NAMING_**

<hr>

- REGULAR BRANCHES:
  - master --- master stable branch
  - dev --- development branch
  - qa --- contains all the code for testing
- TEMPORARY BRANCHES:
  - Bug fix
  - Hot fix
  - Feature branch
  - WIP

EXAMPLE: wip-8712-add-testing-module
bug-logo-alignment-issue

## **_GIT ADDITIONAL USEFUL COMMANDS_**

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

### We do:

- git log --oneline
- git checkout GOODCOMMITHASH
- git checkout -b "new branch with good commit where its last one"

## **_GIT CLEAN_**

<hr>
### To remove untracked files use git clean:

- git clean -n --- will show which files are going be removed
- git clean -f --- actually remove delete these files

## **_GIT REWRITE HISTORY_**

- changing the last commit with --amend It lets you combine staged changes with the previous commit instead of creating an entirely new commit. It can also be used to simply edit the previous commit message without changing its snapshot.

- git commit --amend -m "an updated commit message" --- basically just rewrite commit message for the last commit

### <b>Example:</b>

#### Edit hello.py and main.py

- git add hello.py
- git commit

#### Realize you forgot to add the changes from main.py

- git add main.py
- git commit --amend --no-edit

- git commit --amend lets you take the most recent commit and add new staged changes to it

## **_REBASE:_**

    Rebase itself has 2 main modes: "manual" and "interactive" mode.

## **_REFLOG:_**

    git diff main@{0} main@{1.day.ago} - diff the current main branch against main 1 day ago
