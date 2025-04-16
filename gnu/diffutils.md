# GNU diffutils

## cmp

## diff

### Comparing two directories

```bash
diff -qr dir1 dir2
```

or if you want to exclude the `.git` folder:

```bash
diff -qr --exclude='.git' dir1 dir2
```

This also shows if symlinks in dir1 and dir2 are different.

References:

* [Compare Directories using Diff in Linux](http://linuxcommando.blogspot.com/2008/05/compare-directories-using-diff-in-linux.html)

## diff3

## sdiff
