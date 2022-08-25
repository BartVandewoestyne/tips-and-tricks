* To see the full Make build output, you have two options:
 1. When you run make, add `VERBOSE=1`:

     ```
     cmake .
     make VERBOSE=1
     ```
 2. Add `-DCMAKE_VERBOSE_MAKEFILE:BOOL=ON` to the cmake command for permanent verbose command output from the generated Makefiles:

     ```
cmake -DCMAKE_VERBOSE_MAKEFILE:BOOL=ON .
make
```
