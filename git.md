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

# Monitoring git repos

* [git-dude](https://github.com/sickill/git-dude)
* [git-indicator](https://github.com/itsadok/git-indicator)

Windows only:

* [SourceLog](https://github.com/tomhunter-gh/SourceLog)
