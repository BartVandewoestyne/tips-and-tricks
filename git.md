# Configuration
## Setting the editor
If you want to set the editor *only* for Git, do either (you don't need both):

* Set `core.editor` in your Git config: `git config --global core.editor "vim"`
* Set the `GIT_EDITOR` environment variable: `export GIT_EDITOR=vim`

If you want to set the editor for Git *and also other programs*, set the standardized `VISUAL` and `EDITOR` environment variables:

```
export VISUAL=vim
export EDITOR="$VISUAL"
```
_NOTE_: Setting both is not necessarily needed, but some programs may not use the more-correct `VISUAL`.  See [`VISUAL` vs `EDITOR`](https://unix.stackexchange.com/questions/4859/visual-vs-editor-what-s-the-difference).

# 2.1 Git Basics - Getting a Git Repository

Initializing a Repository in an Existing Directory:

```
$ cd ~/my_project
$ git init
```

Cloning an Existing Repository:

```
$ git clone https://github.com/libgit2/libgit2
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

# 2.2 Git Basics - Recording Changes to the Repository

Checking the Status of Your Files:

```
$ git status
```

Short status:

```
$ git status -s
```

Tracking New Files:

```
$ git add README
```

Viewing Your Staged Changes:

```
$ git diff --staged
```

Viewing Your Unstaged Changes:

```
$ git diff
$ git difftool
```

To see what is available as difftool:

```
git difftool --tool-help
```

Committing your changes:

```
$ git commit
$ $ git commit -m "Story 182: fix benchmarks for speed"
```

Committing your changes with skipping the staging area:

```
$ git commit -a -m 'Add new benchmarks'
```

Removing files:

```
$ git rm PROJECTS.md
```

Removing files from the staging area:  
Keeps the file in your working tree, but removes it from the staging area.
Keeps file on hard drive, but do not have Git tracking it anymore.
Useful if you forgot to add something to your `.gitignore` file and accidentally staged it.

```
$ git rm --cached README
```

Moving files:

```
 git mv README.md README
```

# 2.3 Git Basics - Viewing the Commit History

Default (showing most recent commit first)

```
$ git log
```

Show the difference introduced in each commit:

```
$ git log -p
$ git log --patch
```

Limit git log output to most recent two commits:

```
$ git log -2
```

To see some abbreviated stats for each commit:

```
$ git log --stat
```

Change log output format:

```
$ git log --pretty=oneline
$ git log --pretty=short
$ git log --pretty=full
$ git log --pretty=fuller
... and so on ...
```

To specify your own log output format:

```
$ git log --pretty=format:"%h - %an, %ar : %s"
```

ASCII graph showing branch and merge history:

```
$ git log --pretty=format:"%h %s" --graph
```

Get list of commits from the last two weeks:

```
$ git log --since=2.weeks
$ git log --since="2008-01-15" (TODO: check this!)
$ git log --since="2 years 1 day 3 minutes ago"
```

Search for specific author:

```
$ git log --author="Bart"
```

Search for text in commit message:

```
$ git log --grep="test"
```

To find commits that added or removed a reference to a specific function:

```
$ git log -S function_name
```

Limit log output to commits that introduced a change to the given files:

```
$ git log -- path/to/file
```

To prevent the display of merge commits, add `--no-merges`.

# 2.6 Git Basics - Tagging

Listing the existing tags:

```
$ git tag
$ $ git tag -l "v1.8.5*"
```

Creating an *annotated* tag:

```
$ git tag -a v1.4 -m "my version 1.4"
```

To see the tag data along with the commit that was tagged for a certain tag:

```
$ git show v1.4
```

Creating a *leightweight* tag:

```
$ git tag v1.4-lw
```

To tag a certain commit:

```
$ git tag -a v1.2 9fceb02
```

The git push command doesn’t transfer tags to remote servers.  You will have to explicitly push tags to a shared server after you have created them.

```
$ git push origin v1.5
$ git push origin --tags
```

To delete a tag on your local repository:

```
$ git tag -d v1.4-lw
```

Deleting a tag from a remote server:

```
$ git push origin :refs/tags/v1.4-lw
or
$ git push origin --delete <tagname>
```

Checking out a tag:

```
$ git checkout v2.0.0
```

The above puts you in *detached head* state!

In “detached HEAD” state, if you make changes and then create a commit, the tag will stay the same, but your new commit won’t belong to any branch and will be unreachable, except by the exact commit hash. Thus, if you need to make changes — say you’re fixing a bug on an older version, for instance — you will generally want to create a branch:

```
$ git checkout -b version2 v2.0.0
```

# 2.7 Git Basics - Git Aliases


You can always create aliases as follows:

```
$ git config --global alias.co checkout
```

# 3.1 Git Branching - Branches in a Nutshell

Create a new branch:

```
$ git branch testing
```

To see where the branch pointers are pointing:

```
$ git log --oneline --decorate
```

To switch to an existing branch:

```
$ git checkout testing
```

To show log for only the branch you checked out:

```
git log         (only branch that is checked out)
git log testing (specific branch)
git log --all   (all logs for all branches)
```

```
git log --oneline --decorate --graph --all
```

Create branch and immediately switch to it:

```
git checkout -b <newbranchname>
```

From git 2.23 on, you can use `git switch` instead of `git checkout`:

```
git switch testing-branch
git switch -c new-branch
```

To return to your previously checked out branch:

```
git switch -
```

# 3.2 Git Branching - Basic Branching and Merging

```
$ git checkout master
$ git merge hotfix
```

To delete a branch:

```
$ git branch -d hotfix
```

Basic Merging

```
$ git checkout master
$ git merge iss53
```

```
$ git mergetool
```

# 3.3 Git Branching - Branch Management

## Branch Management

List your current branches:

```
$ git branch
```

To see the last commit on each branch:

```
$ git branch -v
```

To see which branches are already merged into the branch you're on:

```
git branch --merged
```

To see all the branches that contain work you haven't merged in:

```
$ git branch --no-merged
```

## Changing a branch name

First rename the branch locally:

```
$ git branch --move bad-branch-name corrected-branch-name
```

Then push upstream:

```
$ git push --set-upstream origin corrected-branch-name
```

```
$ git push origin --delete bad-branch-name
```

## Changing the master branch name

# 3.4 Git Branching - Branching Workflows

TODO

# 3.5 Git Branching - Remote Branches

## Remote Branches

To get a full list of remote references explicitly, use

```
git ls-remote <remote>
```

or

```
git remote show <remote>
```

To synchronize your work with a given remote, you run a

```
git fetch <remote>
```

command (e.g. `git fetch origin`). This command looks up which server `origin` is, fetches any data from it that you don’t yet have, and updates your local database, moving for example your `origin/master` pointer to its new, more up-to-date position.

## Pushing

To push your local `serverfix` branch:

```
git push origin serverfix
```

which is short for

```
git push origin serverfix:serverfix
```

If you want to name it differently on the remote, use

```
git push origin serverfix:coolserverfix
```

## Tracking branches

If you want your own `serverfix` branch that you can work on, you can base it off your remote-tracking branch:

```
git checkout -b serverfix origin/serverfix
```
or the shorthand (which does the same)

```
git checkout --track origin/serferfix
```
or even shorter:

```
git checkout serverfix
```

If you want to see what tracking branches you have set up and list out your local branches with more information including what each branch is tracking and if your local branch is ahead, behind or both, use

```
git branch -vv
```

Note that the above command does not reach out to the server.

If you want totally up-to-date ahead and behind numbers, you'll need to fetch from all your remotes right before running git branch -vv:

```
$ git fetch --all; git branch -vv
```

## Pulling

Note that `git fetch` does not merge, it will not modify your working directory at all.  It will get the data for you and let you merge it yourself.

git pull = git fetch followed by git merge (in most cases)

Generally it’s better to simply use the fetch and merge commands explicitly as the magic of git pull can often be confusing.

## Deleting Remote Branches

To delete your serverfix branch from the server:

```
$ git push origin --delete serverfix
```

or the shorthand version

```
$ git push origin :serverfix
```

## Tracking Branches

# 7.3 Git Tools - Stashing and Cleaning

## Stashing your work

To stash modified and staged *tracked* files:

```
git stash save (deprecated)
git stash push (better)
```

To push a new stash onto your stack:

```
$ git stash
or
$ git stash push
```

To see which stashes you’ve stored:

```
$ git stash list
```

To reapply the stash you just stashed (without restaging)

```
$ git stash apply (most recent one)
or 
$ git stash apply stash@{2}  (older stashes, see git stash list)
```

Not necessary to have a clean working directory and be on the same branch. You can save a stash on one branch, switch to another branch later, and try to reapply the changes. You can also have modified and uncommitted files in your working directory when you apply a stash — Git gives you merge conflicts if anything no longer applies cleanly.

Try to reapply the stash with restaging:

```
$ git stash apply --index
```

Note also that the stashes remain on your stack after git stash apply.  To remove them:

```
$ git stash drop stash@{0}
```

To apply the stash and immediately drop it:

```
$ git stash pop
```

## Creative stashing

Tell Git to not only include all staged content in the stash being created, but simultaneously leave it in the index:

```
$ git stash --keep-index
```

To also include untracked files in the stash being created:

```
$ git stash -u
$ git stash -include-untracked
```

To additionally include ignored files, use --all (or just -a):

```
$ git stash -a
$ git stash --all
```

To not stash everything that is modified but instead prompt you interactively which of the changes you would like to stash and which you would like to keep in your working directory.
```
$ git stash --patch
```

## Creating a branch from a stash


```
$ git stash branch testchanges
```
This is a nice shortcut to recover stashed work easily and work on it in a new branch.

## Cleaning your working directory

Reasons for cleaning your working directory:

* to remove cruft that has been generated by merges or external tools
* to remove build artifacts in order to run a clean build.

To get rid of some work or files in your working directory:

To remove all the untracked files in your working directory (that are not ignored, all ignored files will remain) (= removes any files and also any subdirectories that become empty as a result):

```
git clean -f -d
```

The -f means 'force' or “really do this,” and is required if the Git configuration variable clean.requireForce is not explicitly set to false.

To do a dry-run, use `-n`:

```
$ git clean -d -n
or
$ git clean -d --dry-run
```

To also remove ignored files:

```
$ git clean -n -d -x   (-n is probably not necessary here, is just for dry-run)
```

If you don’t know what the git clean command is going to do, always run it with a -n first to double check before changing the -n to a -f and doing it for real.

To run the clean command in interactive mode:

```
$ git clean -x -i
```

If you happen to be in a working directory under which you’ve copied or cloned other Git repositories (perhaps as submodules), even git clean -fd will refuse to delete those directories. In cases like that, you need to add a second -f option for emphasis.

## Storing your credentials

Globally:
```
git config --global credential.helper store
```
or for a specific repository:
```
git config credential.helper store
```

TODO: Instead of `store` you can also use `cache`.  what is the difference?

## Differences between branches 

To see the diffs between branches

```
git diff master..test-branch
```

or using Meld:

```
git difftool -d master..test-branch
```

## Undo last commit

Not yet pushed:
```
git reset --soft HEAD~1
```

After running the command, you'll find the changes as uncommitted local modifications in your working copy.

```
git reset --hard HEAD~1
```


## Going back to previous commits

One that is already pushed:

Option 1:

```
git checkout be9055b .
git add -A
git commit -m "Revert commit: be9055b"
git push

```

Option 2:

```
git revert <oldest_commit_hash>..<latest_commit_hash>
```

## Cherry-picking

To only pick one commit from another branch (and immediately create a commit):

```
git cherry-pick a6817d7
```

To pick multiple commits:

```
git cherry-pick a6817d7 sdfasdf
```

To cherry-pick without immediately committing:

```
git cherry-pick a6817d7 -n
```

# Monitoring git repos

* [git-dude](https://github.com/sickill/git-dude)
* [git-indicator](https://github.com/itsadok/git-indicator)

Windows only:

* [SourceLog](https://github.com/tomhunter-gh/SourceLog)
