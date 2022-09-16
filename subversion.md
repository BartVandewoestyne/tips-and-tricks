# Creating and applying a patch

Creating a patch:

```
svn diff > mypatchfile.patch
```

To apply your changes if there are no added/deleted files through `svn add` or `svn delete`:

```
patch -p0 < mypatchfile.patch
```

To track added and deleted files too:

```
svn patch mypatchfile.patch
```

Note that neither tracks `svn move`s and `svn rename`s.

# Monitoring SVN repositories
* [Subversion repository monitor](https://ghost.tweakblogs.net/blog/3073/subversion-repository-monitor.html)
