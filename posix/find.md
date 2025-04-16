# POSIX find

## Finding files

* Finding a file on your filesystem in a case-sensitive manner:

  ```text
  find / -type f -name 'filename.txt'
  ```

  Note that searching `/` requires root privileges, so you may need `sudo`.

* Finding multiple files:

  ```text
  find . -type f -name '*.pl'
  ```

* List all `.h` and `.cpp` files in the current directory and subdirectories:

  ```text
  find . -type f \( -name '*.h' -o -name '*.cpp' \)
  ```

## Excluding directories

* Method 1 (untested):

  ```text
  find . -path ./jpeg -prune  -o -print
  ```

* Method 2:

  ```text
  find . ! -path "./tmp/*" ! -path "./scripts/*"
  ```

* Method 3:

  ```text
  find . -type d -name 'ThirdParty' -prune -o -type f -name '*.pro' -print
  ```

## Doing things with the found files

* Run a certain command on files that might contain spaces:

  ```text
  find . -exec <command> {} +
  ```

  Examples:

  * Search for a string in files:

    ```text
    find . -type f -name '*.pl' -exec grep foobar {} +
    ```

  * Replace a string in a lot of files, including subdirs:

    ```text
    find . -type f -name '*.f95' -exec perl -pi -e 's/foo/bar/g' {} \;
    ```

## Powerful combining with other tools

* Find the smallest file in the current directory and sub directories:

  ```text
  find . -type f -exec ls -s {} \; | sort -n -r | tail -1
  ```

  or

  ```text
  find . -type f -exec ls -s {} \; | sort -n  | head -1
  ```

* Finding .m files with the same name:

  ```text
  find dir/ -type f -name '*.m' | sort | uniq -d > filename_duplicates.txt
  ```
