# Finding files

## Finding a file
* Method 1:
  ```
  locate
  ```
* Method 2:
  ```
  find / -name 'program.c' 2>/dev/null
  find / -name 'program.c' 2>errors.txt
  ```

## Finding multiple files
* Case sensitive match:
  ```
  find . -type f -name '*.pl'
  ```
* Case insensitive match:
  ```
  find . -type f -iname '*.pl'
  ```
* Finding both .h and .cpp files:

    find . -type f -iname '*.h' -o -iname '*.cpp'

## Finding duplicate files

Finding duplicate .m files:
```
find subversion/ -type f -name '*.m' | sort | uniq -d > duplicate_files
```

Finding duplicate files:
```
fdupes -r mydir > ~/duplicate_files.txt
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

Om te kijken of 2 remote directories verschillend zijn:
-------------------------------------------------------

Manier 1:
        Op de remote:
                find . -print | xargs md5sum > file

        Op de locale host in zelfde dir gaan staan en:
                md5sum -c file

Manier 2:

        find . -print | xargs md5sum | ssh $host '(cd $dir; md5sum -c)'

Finding the top 10 largest files names (not directories) in a particular
directory and its subdirectories
------------------------------------------------------------------------
find . -printf '%s %p\n' | sort -nr | head

Finding the smallest file in the current directory and sub directories
----------------------------------------------------------------------
find . -type f -exec ls -s {} \; | sort -n -r | tail -1
find . -type f -exec ls -s {} \; | sort -n  | head -1
