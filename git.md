# Git

## Configuration

To list all variables set in config file, along with their values:

```bash
git config --list
```

### Setting the editor

If you want to set the editor *only* for Git, do either (you don't need both):

* Set `core.editor` in your Git config:

  ```text
  git config --global core.editor "vim"
  ```

* Set the `GIT_EDITOR` environment variable:

  ```bash
   export GIT_EDITOR=vim
   ```

If you want to set the editor for Git *and also other programs*, set the standardized `VISUAL` and `EDITOR` environment variables:

```bash
export VISUAL=vim
export EDITOR="$VISUAL"
```

*NOTE*: Setting both is not necessarily needed, but some programs may not use the more-correct `VISUAL`.  See [`VISUAL` vs `EDITOR`](https://unix.stackexchange.com/questions/4859/visual-vs-editor-what-s-the-difference).

## 2.1 Git Basics - Getting a Git Repository

To initialize a Git repository from an existing directory:

```bash
cd ~/my_project
git init
```

To clone an existing repository:

```bash
git clone https://github.com/libgit2/libgit2
git clone https://github.com/libgit2/libgit2 mylibgit
```

## 2.2 Git Basics - Recording Changes to the Repository

Checking the status of your files:

```bash
git status
```

Getting the status in short-format:

```bash
git status -s
```

Update the index with new content:

```bash
git add README
```

Viewing your staged changes:

```bash
git diff --staged
```

Viewing your unstaged changes:

```bash
git diff
git difftool
```

To see what is available as difftool:

```bash
git difftool --tool-help
```

To see changes between commits with difftool:

```bash
git difftool -d 1b3baae..b2b29ce
```

Committing your changes:

```bash
git commit
git commit -m "Story 182: fix benchmarks for speed"
```

Committing your changes with skipping the staging area:

```bash
git commit -a -m 'Add new benchmarks'
```

Removing files:

```bash
git rm PROJECTS.md
```

Removing files from the staging area:

```bash
git rm --cached README
```

The above command keeps the file in your working tree, but removes it from the staging area.  The file is kept on your hard drive, but you do not have Git tracking it anymore.  This can be useful if you forgot to add something to your `.gitignore` file and accidentally staged it.

Moving files:

```bash
git mv README.md README
```

## 2.3 Git Basics - Viewing the Commit History

Default way of showing the log (showing most recent commit first):

```bash
git log
```

Show the difference introduced in each commit:

```bash
git log -p
git log --patch
```

Limit git log output to most recent two commits:

```bash
git log -2
```

To see some abbreviated stats for each commit:

```bash
git log --stat
```

Change log output format:

```bash
git log --pretty=oneline
git log --pretty=short
git log --pretty=full
git log --pretty=fuller
git log --pretty=reference
git log --pretty=email
git log --pretty=raw
```

To specify your own log output format:

```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

See the `PRETTY FORMATS` section from `git help log` to know what placeholders are possible.

ASCII graph showing branch and merge history:

```bash
git log --pretty=format:"%h %s" --graph
```

Get list of commits from somewhere in the past:

```bash
git log --since=2.weeks
git log --since="2008-01-15"  # shows commits more recent than this date!
git log --since="2 years 1 day 3 minutes ago"
```

Search for specific author:

```bash
git log --author="Bart"
```

Search for text in commit message:

```bash
git log --grep="test"
```

To find commits that added or removed a reference to a specific function:

```bash
git log -S function_name
```

To trace the evolution of a function name with in a certain file:

```bash
git log -L :functionName:./path/to/file.cpp
```

Limit log output to commits that introduced a change to the given files:

```bash
git log -- path/to/file
```

To prevent the display of merge commits, add `--no-merges`.

## 2.6 Git Basics - Tagging

Listing the existing tags:

```bash
git tag
```

Search for tags that match a particular pattern:

```bash
git tag -l "v1.8.5*"
```

To see the tag data along with the commit that was tagged for a certain tag:

```bash
git show v1.4
```

### Annotated tags

*Annotated tags* are stored as full objects in the Git database. They’re checksummed; contain the tagger name, email, and date; have a tagging message; and can be signed and verified with GNU Privacy Guard (GPG).  It is recommended to create annotated tags to have this information.  To create an *annotated* tag:

```bash
git tag -a v1.4 -m "my version 1.4"
```

To tag a certain commit:

```bash
git tag -a v1.2 9fceb02
```

### Leightweight tags

Another way to tag commits is with a *lightweight* tag. This is basically the commit checksum stored in a file — no other information is kept.  To creat a *leightweight* tag:

```bash
git tag v1.4-lw
```

### Sharing tags

The git push command doesn’t transfer tags to remote servers.  You will have to explicitly push tags to a shared server after you have created them.

To push one specific tag:

```bash
git push origin v1.5
```

To transfer all of your tags to the remote server that are not already there:

```bash
git push origin --tags
```

### Deleting tags

To delete a tag on your local repository:

```bash
git tag -d v1.4-lw
```

Deleting a tag from a remote server:

```bash
git push origin :refs/tags/v1.4-lw
```

or

```bash
git push origin --delete <tagname>
```

### Checking out tags

Checking out a tag:

```bash
git checkout v2.0.0
```

The above puts you in *detached head* state!

In “detached HEAD” state, if you make changes and then create a commit, the tag will stay the same, but your new commit won’t belong to any branch and will be unreachable, except by the exact commit hash. Thus, if you need to make changes — say you’re fixing a bug on an older version, for instance — you will generally want to create a branch:

```bash
git checkout -b version2 v2.0.0
```

## 2.7 Git Basics - Git Aliases

You can always create aliases as follows:

```bash
git config --global alias.co checkout
```

## 3.1 Git Branching - Branches in a Nutshell

Create a new branch:

```bash
git branch testing
```

To see where the branch pointers are pointing:

```bash
git log --oneline --decorate
```

To switch to an existing branch:

```branch
git checkout testing
```

To show log for only the branch you checked out:

```bash
git log         (only branch that is checked out)
git log testing (specific branch)
git log --all   (all logs for all branches)
```

```bash
git log --oneline --decorate --graph --all
```

Create branch and immediately switch to it:

```bash
git checkout -b <newbranchname>
```

From git 2.23 on, you can use `git switch` instead of `git checkout`:

```bash
git switch testing-branch
git switch -c new-branch
```

To return to your previously checked out branch:

```bash
git switch -
```

## 3.2 Git Branching - Basic Branching and Merging

To delete a branch:

```bash
git branch -d hotfix
```

Basic Merging

```bash
git checkout master
git merge iss53
```

```bash
git mergetool
```

## 3.3 Git Branching - Branch Management

### Branch Management

List your current branches:

```bash
git branch
```

To see the last commit on each branch:

```bash
git branch -v
```

To see more verbose list and also which branches have no more remotes (gone):

```bash
git branch -vv
```

To see which branches are already merged into the branch you're on:

```bash
git branch --merged
```

To see all the branches that contain work you haven't merged in:

```bash
git branch --no-merged
```

### Changing a branch name

First rename the branch locally:

```bash
git branch --move bad-branch-name corrected-branch-name
```

Then push upstream:

```bash
git push --set-upstream origin corrected-branch-name
```

```bash
git push origin --delete bad-branch-name
```

### Changing the master branch name

## 3.4 Git Branching - Branching Workflows

TODO

## 3.5 Git Branching - Remote Branches

### Remote Branches

To get a full list of remote references explicitly, use

```bash
git ls-remote <remote>
```

or

```bash
git remote show <remote>
```

To synchronize your work with a given remote, you run a

```bash
git fetch <remote>
```

command (e.g. `git fetch origin`). This command looks up which server `origin` is, fetches any data from it that you don’t yet have, and updates your local database, moving for example your `origin/master` pointer to its new, more up-to-date position.

### Pushing

To push your local `serverfix` branch:

```bash
git push origin serverfix
```

which is short for

```bash
git push origin serverfix:serverfix
```

If you want to name it differently on the remote, use

```bash
git push origin serverfix:coolserverfix
```

### Tracking branches

If you want your own `serverfix` branch that you can work on, you can base it off your remote-tracking branch:

```bash
git checkout -b serverfix origin/serverfix
```

or the shorthand (which does the same)

```bash
git checkout --track origin/serferfix
```

or even shorter:

```bash
git checkout serverfix
```

If you want to see what tracking branches you have set up and list out your local branches with more information including what each branch is tracking and if your local branch is ahead, behind or both, use

```bash
git branch -vv
```

Note that the above command does not reach out to the server.

If you want totally up-to-date ahead and behind numbers, you'll need to fetch from all your remotes right before running git branch -vv:

```bash
git fetch --all; git branch -vv
```

TODO:

```bash
git fetch --prune
```

### Pulling

Note that `git fetch` does not merge, it will not modify your working directory at all.  It will get the data for you and let you merge it yourself.

git pull = git fetch followed by git merge (in most cases)

Generally it’s better to simply use the fetch and merge commands explicitly as the magic of git pull can often be confusing.

### Deleting Remote Branches

To delete your serverfix branch from the server:

```bash
git push origin --delete serverfix
```

or the shorthand version

```bash
git push origin :serverfix
```

## 3.6 Git Branching - Rebasing

### The Basic Rebase

```bash
git checkout experiment
git rebase master
```

```bash
git checkout master
git merge experiment
```

### More Interesting Rebases

```bash
git rebase --onto master server client
```

```bash
git checkout master
git merge client
```

To rebase the server branch onto the master branch without having to check it out first:

```bash
git rebase <basebranch> <topicbranch>
```

```bash
git checkout master
git merge server
```

```bash
git branch -d client
git branch -d server
```

### The Perils of Rebasing

Do not rebase commits that exist outside your repository and that people may have based work on.

### Rebase When You Rebase

### Rebase vs. Merge

### Aborting a rebase

To abort a rebase:

```bash
git rebase --abort
```

## 7.3 Git Tools - Stashing and Cleaning

### Stashing your work

To stash modified and staged *tracked* files:

```bash
git stash save (deprecated)
git stash push (better)
```

To push a new stash onto your stack:

```bash
git stash
```

or

```bash
git stash push
```

To see which stashes you’ve stored:

```bash
git stash list
```

To reapply the stash you just stashed (without restaging)

```bash
git stash apply (most recent one)
```

or

```bash
 git stash apply stash@{2}  (older stashes, see git stash list)
```

Not necessary to have a clean working directory and be on the same branch. You can save a stash on one branch, switch to another branch later, and try to reapply the changes. You can also have modified and uncommitted files in your working directory when you apply a stash — Git gives you merge conflicts if anything no longer applies cleanly.

Try to reapply the stash with restaging:

```bash
git stash apply --index
```

Note also that the stashes remain on your stack after git stash apply.  To remove them:

```bash
git stash drop stash@{0}
```

To apply the stash and immediately drop it:

```bash
git stash pop
```

### Creative stashing

Tell Git to not only include all staged content in the stash being created, but simultaneously leave it in the index:

```bash
git stash --keep-index
```

To also include untracked files in the stash being created:

```bash
git stash -u
git stash --include-untracked
```

To additionally include ignored files, use `--all` (or just `-a`):

```bash
git stash -a
git stash --all
```

To not stash everything that is modified but instead prompt you interactively which of the changes you would like to stash and which you would like to keep in your working directory.

```bash
git stash --patch
```

### Creating a branch from a stash

```bash
git stash branch testchanges
```

This is a nice shortcut to recover stashed work easily and work on it in a new branch.

### Cleaning your working directory

Reasons for cleaning your working directory:

* to remove cruft that has been generated by merges or external tools
* to remove build artifacts in order to run a clean build.

To get rid of some work or files in your working directory:

To remove all the untracked files in your working directory (that are not ignored, all ignored files will remain) (= removes any files and also any subdirectories that become empty as a result):

```bash
git clean -f -d
```

The -f means 'force' or “really do this,” and is required if the Git configuration variable clean.requireForce is not explicitly set to false.

To do a dry-run, use `-n`:

```bash
git clean -d -n
```

or

```bash
git clean -d --dry-run
```

To also remove ignored files:

```bash
git clean -n -d -x   (-n is probably not necessary here, is just for dry-run)
```

If you don’t know what the git clean command is going to do, always run it with a -n first to double check before changing the -n to a -f and doing it for real.

To run the clean command in interactive mode:

```bash
git clean -x -i
```

If you happen to be in a working directory under which you’ve copied or cloned other Git repositories (perhaps as submodules), even git clean -fd will refuse to delete those directories. In cases like that, you need to add a second -f option for emphasis.

## 7.11 Git Tools - Submodules

### Starting with Submodules

To add a new submodule:

```bash
git submodule add https://github.com/chaconinc/DbConnector
```

To get a nicer diff output, pass the `--submodule` option to git diff:

```bash
git diff --cached --submodule
```

To commit the added submodule and push:

```bash
git commit -am 'Add DbConnector module'
git push origin master
```

### Cloning a Project with Submodules

#### Method 1

When you clone a project with a submodule in it

```bash
git clone https://github.com/chaconinc/MainProject
```

then by default you get the directories that contain submodules, but none of the files within them yet.

To initialize your local configuration file:

```bash
git submodule init
```

To fetch all the data from the project and check out the appropriate commit listed in your superproject:

```bash
git submodule update
```

The `git submodule init` and `git submodule update` steps can be combined by running

```bash
git submodule update --init
```

To also initialize, fetch and checkout any nested submodules:

```bash
git submodule update --init --recursive
```

#### Method 2

Pass `--recurse-submodules` to the `git clone` command:

```bash
git clone --recurse-submodules https://github.com/chaconinc/MainProject
```

which will automatically initialize and update

### Working on a Project with Submodules

TODO

### Storing your credentials

Globally:

```bash
git config --global credential.helper store
```

or for a specific repository:

```bash
git config credential.helper store
```

TODO: Instead of `store` you can also use `cache`.  what is the difference?

### Differences between branches

To see the diffs between branches

```bash
git diff master..test-branch
```

or using Meld:

```bash
git difftool -d master..test-branch
```

### Undo last (or N last) commit(s)

Not yet pushed:

```bash
git reset --soft HEAD~
```

or

```bash
git reset --soft HEAD~1
```

or if you want for example to undo the last 2 commits:

```bash
git reset --soft HEAD~2
```

After running the command, you'll find the changes as uncommitted local modifications in your working copy.

Already pushed?

```bash
git reset --hard HEAD~1
```

TODO: do we need `git push -f <remote> <branch>` here after this reset?


### Going back to previous commits

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

### Cherry-picking

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

### Git blame

First, do a `git blame` on the file:
```
git blame <filename>
```
Find the commit in which a certain line was introduced.  To see the log message and textual diff for that commit:
```
git show <commit>
```
If you want to see the diff with your difftool:
```
git difftool <commit>~..<commit>
```

To go back in history:
```
git blame <commit>^ -- file.cpp
```

Git GUI also makes it easy to check the history of a line as the versions are clickable:
```
git gui blame <filename>
```

or in `gitk`, rightclick on a file name and select 'Blame parent commit'.
And then, when in git GUI, click on 'Blame Parent Commit'.

References:
* https://stackoverflow.com/questions/5098256/how-can-i-view-prior-commits-with-git-blame
* 

### Merge conflicts

To undo the merge and its conflicts and start over:
```
git merge --abort
```

## Other

### Creating patches

To create a patch:
```
git diff --output foo.patch
```
The above will not include new files.  To include new files, first stage them (using `git add`) and then create the patch with
```
git diff --staged --output foo.patch
```
and later apply as usual.

To prepare patches for e-mail submission (TODO):
```
git format-patch <something>
```

### Applying patches

To apply a patch created with `git diff`:
```
git apply foo.patch
```

## Best practices

* Do not use rebase on commits that you've already pushed/shared on a remote repository.  Instead, use it for cleaning up your local commit history before merging it into a shared team branch.
  See https://git-scm.com/book/en/v2/Git-Branching-Rebasing under 'The Perils of Rebasing'.

References:
* https://opensource.com/article/20/7/git-best-practices
* https://deepsource.io/blog/git-best-practices/
* https://sethrobertson.github.io/GitBestPractices/
* https://commonflow.org/ (section 'Git Best Practices')

## Diff and Merge tools

## Diff tools

## Merge tools

It's most convenient to use a tool that allows you to see all 4 views: base, left, right, and merged result.

### Meld

Meld only allows 3 views. Meld isn't a real merge tool, it's a diff tool since it doesn't shows the base version view.

### KDiff3

### vimdiff

<http://vimcasts.org/episodes/fugitive-vim-resolving-merge-conflicts-with-vimdiff/>

### CLion

See <https://www.jetbrains.com/help/clion/resolve-conflicts.html>

## Monitoring git repos

* [git-dude](https://github.com/sickill/git-dude)
* [git-indicator](https://github.com/itsadok/git-indicator)

Windows only:

* [SourceLog](https://github.com/tomhunter-gh/SourceLog)

## Git clients that work in both Linux and Windows

* [git-gui](https://git-scm.com/docs/git-gui)
* [gitk](https://git-scm.com/docs/gitk)
* [Using Git source control in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview)
* [ungit](https://github.com/FredrikNoren/ungit)
* [gitg](https://wiki.gnome.org/Apps/Gitg/) is the GNOME GUI client to view git repositories
* [Magit](https://magit.vc/) => seems to be an Emacs plugin or so...
* [MeGit](https://github.com/eclipsesource/megit) (based on [EGit](https://eclipse.dev/egit/), which is an Eclipse plugin)

The lists at <https://git-scm.com/downloads/guis> and <https://git.wiki.kernel.org/index.php/InterfacesFrontendsAndTools> also have some promising ones.

## Workflows / Branching stategies

Git Flow (has some issues):

* [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
* [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
* [What is Git Flow](https://www.gitkraken.com/learn/git/git-flow)

GitHub Flow:

* [GitHub Flow - The best way to use Git and GitHub](https://githubflow.github.io/)
* [GitHub flow - Follow GitHub flow to collaborate on projects](https://docs.github.com/en/get-started/quickstart/github-flow)
* [GitHub Flow](https://www.gitkraken.com/learn/git/git-flow#github-flow)

Common-Flow:

* [Common-Flow](https://commonflow.org/)

GitLab Flow:

* [Introduction to GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)

Release Flow:

* [Release Flow: How We Do Branching on the VSTS Team](https://devblogs.microsoft.com/devops/release-flow-how-we-do-branching-on-the-vsts-team/)

General:

* [What is the best Git branch strategy?](https://www.gitkraken.com/learn/git/best-practices/git-branch-strategy)

* [Git Team Workflows Best Practices: Merge or Rebase?](https://www.atlassian.com/git/articles/git-team-workflows-merge-or-rebase)

## TODO

* Check out [git worktree](https://git-scm.com/docs/git-worktree).
