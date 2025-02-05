# ls

To list all files with the last modified ones at the bottom:

```text
ls -altr
```

with

`-a`: Write out all directory entries, including those whose names begin with a period ( '.' ).  
`-l`: Write out in long format.  
`-t`: Sort with the primary key being time modified (most recently modified first) and the secondary key being filename in the collating sequence.  
`-r`: Reverse the order of the sort to get reverse collating sequence or oldest first.
