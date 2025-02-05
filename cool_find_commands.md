# Finding files

## Finding duplicate files

Finding duplicate .m files:
```
find subversion/ -type f -name '*.m' | sort | uniq -d > duplicate_files
```

Finding duplicate files:
```
fdupes -r mydir > ~/duplicate_files.txt
```

## Finding large or small files

Finding the top 10 largest files (not directories) in a particular directory and its subdirectories
```
find . -printf '%s %p\n' | sort -nr | head
```

Finding the smallest file in the current directory and sub directories
```
find . -type f -exec ls -s {} \; | sort -n -r | tail -1
find . -type f -exec ls -s {} \; | sort -n  | head -1
```

Excluding certain directories when finding large files:
```
find . -type d -name '.vs' -prune -o -type d -name '.svn' -prune -o -type f -printf '%s %p\n' | sort -nr | head
```

## Excluding certain directories

Excluding one directory:
* Method 1 (untested):
  ```
  find . -path ./jpeg -prune  -o -print
  ```
* Method 2:
  ```
  find . -not -iwholename '*.svn*'
  ```
* Method 3:
  ```
  find . ! -path "./tmp/*" ! -path "./scripts/*"
  ```
* Method 4:
  ```
  find . -type d -name 'ThirdParty' -prune -o -type f -name '*.pro' -print
  ```

# Finding text in files

```
find . -type f -name '*.pl' | xargs grep text
```

To run a <command> on files with spaces:
```
find . -print0 | xargs -0 <command>
```

# Replacing text in files

Replacing a string in a lot of files, including subdirs:
```
find . -type f -name '*.f95' -exec perl -pi -e 's/foo/bar/g' {} \;
```

To see if two remote directories are different:
* Method 1: on the remote host, do:
  ```
  find . -print | xargs md5sum > file
  ```
  and then on the local host, go into the same directory and do:
  ```
  md5sum -c file
  ```
* Method 2:
  ```
  find . -print | xargs md5sum | ssh $host '(cd $dir; md5sum -c)'
  ```
