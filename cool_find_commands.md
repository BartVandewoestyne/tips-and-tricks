# Finding files

## Finding duplicate files

Finding duplicate files based on content:
```
fdupes -r mydir > ~/file_duplicates.txt
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
