# POSIX find

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
