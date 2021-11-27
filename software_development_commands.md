# hexdump
```
hexdump -v -c file.bin
hexdump -v -d Model.msh
hexdump -v -e '1/4 "%d\n"' -n 4 Model.msh
hexdump -v -e '1/8 "%10.5f\n"' -s 20 Model.msh
hexdump -v -e '1/8 "%_ad%10.5f\n"' -s 20 Model.msh
```
Show header of 12 bytes (3 four byte integers):
```
hexdump -v -e '"[" 3/4 "%u " "]\n"' -n  12 reso2~dad.mat
```
Show data following this header (4 byte floats following each other):
```
hexdump -v -e '"[" 1/4 "%f " "]\n"' -s  12 reso2~dad.mat
```
A good hexeditor for Linux is ghex2.  For windows, you can use wxhexeditor.

# Java

Find out class file version:
```
$ javap -verbose HelloServlet | grep major
```

# CVS

Perform a first, clean checkout:
```
cvs -q -d :ext:bartv@radon.cs.kuleuven.be:/export/home2/cvs co qmcpack
```

When you do a `cvs update` you can have:
* M - Modified - this file had been modified on YOUR local machine and needed to
                be uploaded to server.  Bij een commit zullen alle files
                waar een M bij stond getoond worden in de commit lijst.
* P - Patched - minor changes from the server had been patched to your files
* U - Updated - your file is overwritten by the latest version due to major
               changes
* C - Conflict - Er is een conflict en je moet het eerst oplossen

# Profiling
* Using gprof:
** compile with the compileer met -pg optie
* voer sourcecode uit, je bekomt een gmon.out
* gprof binary gmon.out

# Creating a patch
Assume original source code at folder dir1 and latest source code at folder
dir2.  And there can be multiple subdirectories:
```
diff -crB dir1 dir2 > Tb02.patch

  -c context
  -r recursive (multiple levels dir)
  -B is to ignore Blank Lines.
```
Testing the patch:
```
patch --dry-run -p1 -i Tb02.patch
```
Applying the patch:
```
patch -p1 -i Tb02.patch
```
To create a patch from CVS:
```
cvs diff -uN > patch.txt
```
Or if you added files:
```
cvs add newfile
cvs diff -uNa > patch.txt
```