# Finding files

## Finding duplicate files

Finding .m files with the same name:
```
find subversion/ -type f -name '*.m' | sort | uniq -d > filename_duplicates.txt
```

Finding duplicate files based on content:
```
fdupes -r mydir > ~/file_duplicates.txt
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

# Replacing text in files


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
