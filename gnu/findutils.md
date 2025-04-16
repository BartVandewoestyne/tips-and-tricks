# GNU findutils

## GNU find

### Pure GNU find

* Case insensitive search:

  ```text
  find . -type f -iname '*.pl'
  ```

* Excluding directories:

  ```text
  find . -not -iwholename '*.svn*'
  ```

### GNU find in combination with other tools

Finding the top 10 largest files (not directories) in a particular directory and its subdirectories:

```text
find . -type f -printf '%s %p\n' | sort -nr | head -n 10
```

Excluding certain directories when finding large files:

```text
find . -type d -name '.vs' -prune -o -type d -name '.svn' -prune -o -type f -printf '%s %p\n' | sort -nr | head
```

## GNU xargs
