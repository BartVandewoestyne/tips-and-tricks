```
user@system$ echo this-is-{1,2,3}
this-is-1 this-is-2 this-is-3
```

```
user@system$ touch a-very-long-name
user@system$ mv a-very-long-name{,-old}
user@system$ ls -al a-very-long-name-old
-rw-r--r-- 1 bvandewoestyne domain users 0 Feb 28 11:46 a-very-long-name-old
```

TODO: pushd and popd
