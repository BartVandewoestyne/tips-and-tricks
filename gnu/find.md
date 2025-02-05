# GNU find

## Pure GNU find

* Case insensitive search:

  ```text
  find . -type f -iname '*.pl'
  ```

## GNU find in combination with other tools

Finding the top 10 largest files (not directories) in a particular directory and its subdirectories:

```text
find . -type f -printf '%s %p\n' | sort -nr | head -n 10
```
