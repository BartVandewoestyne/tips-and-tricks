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

# Monitoring git repos

* [git-dude](https://github.com/sickill/git-dude)
* [git-indicator](https://github.com/itsadok/git-indicator)

Windows only:

* [SourceLog](https://github.com/tomhunter-gh/SourceLog)
