# GNU tail

To output the last 2 bytes of a binary file:
```text
tail -c 2 file.bin
```
To see the bytes in the order as they are stored in the file:
```text
tail -c 2 file.bin | xxd -g 1
```
