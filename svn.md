# Reverting changes

To revert a single file:
```
svn revert foo.c
```

To revert a whole directory of files:
```
svn revert --recursive .
```

# Creating patches

Using `/usr/bin/patch`:

```
svn diff > $TMPDIR/mypatchfile.patch
...
patch -p0 < $TMPDIR/mypatchfile.patch
```

This will apply your changes well if there are not added/deleted files through `svn add` or `svn delete`.

Using `svn patch`:

```
svn diff > $TMPDIR/mypatchfile.patch
...
svn patch $TMPDIR/mypatchfile.patch
```

This tracks added and deleted files too.

# SVN clients

## RabbitVCS

Pros:

* Latest release is from February 12, 2020.
* Interface is inspired by TortoiseSVN.

Cons:

* Only Linux

## Integrated Subversion source control for VSCode

https://marketplace.visualstudio.com/items?itemName=johnstoncode.svn-scm

Cons:

* Requires VSCode

## SubTile

* https://en.wikipedia.org/wiki/SubTile

## RapidSVN

Cons:

* Latest release is form June 28, 2012...

## QSvn

https://en.wikipedia.org/wiki/QSvn

Cons:

* Development stopped in 2010.

## eSVN

Cons:

* Latest release is from 2007...
