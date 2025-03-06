```
user@system$ echo this-is-{1,2,3}
this-is-1 this-is-2 this-is-3
```

```
user@system$ touch a-very-long-name
user@system$ mv a-very-long-name{,-old}
user@system$ ls -al a-very-long-name-old
-rw-r--r-- 1 bvandewoestyne domain users 0 Feb 28 11:46 a-very-long-name-old
```

TODO: pushd and popd

# Debugging

set -e
makes the script exit immediately if any command returns a non-zero exit status (i.e., if a command fails). This helps catch errors early and prevents the script from continuing execution in an unexpected state.

set -x
Add set -x at the beginning of your script to print each command before executing it:

Trap errors and dispy useful info:
trap 'echo "Error at line $LINENO"' ERR

To clean up before exiting:
trap 'cleanup_function' EXIT

Run your script line by line in an interactive shell:
sh -i script.sh

Use shellcheck to analyze your script for common mistakes:
shellcheck myscript.sh
