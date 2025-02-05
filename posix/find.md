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
