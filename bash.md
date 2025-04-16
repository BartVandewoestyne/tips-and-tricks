# bash

## Brace Expansion

```bash
bash$ echo this-is-{1,2,3}
this-is-1 this-is-2 this-is-3
```

```bash
bash$ touch a-very-long-name
bash$ mv a-very-long-name{,-old}
bash$ ls -al a-very-long-name-old
-rw-r--r-- 1 bvandewoestyne domain users 0 Feb 28 11:46 a-very-long-name-old
```

References:

* [Brace Expansion](https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html)

## pushd and popd

TODO

## Debugging

### Exit immediately

Make the script exit immediately if any command returns a non-zero exit status (i.e., if a command fails):

```bash
set -e
```

This helps catch errors early and prevents the script from continuing execution in an unexpected state.

### Print each command

To print each command before executing it, add

```bash
set -x
```

at the beginning of your script.

### Trapping errors

To trap errors and dispy useful info:

```bash
trap 'echo "Error at line $LINENO"' ERR
```

### Cleaning up before exiting

To clean up before exiting:

```bash
trap 'cleanup_function' EXIT
```

### Running script line by line in interactive shell

Run your script line by line in an interactive shell:

```bash
sh -i script.sh
```

### Check for common mistakes

Use shellcheck to analyze your script for common mistakes:

```bash
shellcheck myscript.sh
```
