# Subversion

## Find out from what branch a branch was originally copied of

1. Identify the branch URL of the branch you are currently on:

   ```text
   svn info | grep ^URL
   ```

1. Still on that branch, examine the log for the branch creation:

   ```text
   svn log --stop-on-copy -v
   ```

   The `-v` flag will also print the affected paths so that you can see what is copied from where.  For example:

   ```text
   r54174 | tvrd | 2024-04-25 16:52:57 +0200 (Do, 25 Apr 2024) | 2 lines
   Changed paths:
      A /trunk/terminal/buildtools/modembuild/branches/dialog_to_intuition_migration (from /trunk/terminal/buildtools/modembuild/dialog_trunk:54173)

   Create feature branch for Dialog-to-Intuition migration feature.
   ```

## Merging

To see what will be merged, for example by a sync-merge from trunk:

```text
svn merge --dry-run ^/trunk .
```

## Using Meld as a merge tool

1. Configure `meld` as the merge tool by editing `~/.subversion/config`:

   ```text
   [helpers]
   merge-tool-cmd = meld
   ```

1. Perform the merge

   ```text
   svn merge htttp://path/to/branch
   ```

1. Identify conflicted files:

   ```text
   svn status
   ```

1. Resolve conflicts with `meld`:

   ```text
   meld conflicted_file.txt.rOLD conflicted_file.txt.rNEW conflicted_file.txt
   ```

1. Mark the conflict as resolved:

   ```text
   svn resolve --accept working conflicted_file.txt
   ```

## Creating and applying a patch

### Using `/usr/bin/patch`

```text
svn diff > mypatchfile.patch
...
patch -p0 < mypatchfile.patch
```

This will apply your changes well if there are not added/deleted files through `svn add` or `svn delete`.

To apply your changes if there are no added/deleted files through `svn add` or `svn delete`:

```text
patch -p0 < mypatchfile.patch
```

### Using `svn diff` and `svn patch`

```text
svn diff > mypatchfile.patch
...
svn patch mypatchfile.patch
```

This tracks added and deleted files too.

Note that neither tracks `svn move`s and `svn rename`s.

References:

* [How to make and apply SVN patch?](https://stackoverflow.com/questions/10333712/how-to-make-and-apply-svn-patch)

## Reverting changes

To revert a single file:

```text
svn revert foo.c
```

To revert a whole directory of files:

```text
svn revert --recursive .
```

## Sparse checkouts and updates

When checking out, you can use the `--depth ARG` option with `ARG` equal to any of `empty`, `files`, `immediates` or `infinity`.

When updating, you can use `--depth` with `empty`, `files`, `immediatese` or `infinity` and you can use `--set-depth` with `exclude`, `empty`, `files`, `immediatese` or `infinity`.

## Monitoring SVN repositories

* [Subversion repository monitor](https://ghost.tweakblogs.net/blog/3073/subversion-repository-monitor.html)

## SVN clients

### RabbitVCS

Pros:

* Latest release is from February 12, 2020.
* Interface is inspired by TortoiseSVN.

Cons:

* Only Linux

### Integrated Subversion source control for VSCode

<https://marketplace.visualstudio.com/items?itemName=johnstoncode.svn-scm>

Cons:

* Requires VSCode

### SubTile

* <https://en.wikipedia.org/wiki/SubTile>

### RapidSVN

Cons:

* Latest release is form June 28, 2012...

### QSvn

<https://en.wikipedia.org/wiki/QSvn>

Cons:

* Development stopped in 2010.

### eSVN

Cons:

* Latest release is from 2007...
