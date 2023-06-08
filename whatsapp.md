To download all images from a chat group in WhatsApp web:
# Load the chat/group
# Go to media and load all the files
# Select any one photo from the media section (this is important)
# Press (Ctrl+Shift+i) or F12 and go to the console tab
# Paste the given script in console:

Eerst alles downloaden door in image viewer te gaan:
```
function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

for (var start=1; start < 100; start++) {
    document.querySelectorAll('[data-testid="chevron-left"]').forEach(s => s.click()); await sleep(100);
}
```

  document.querySelectorAll('[data-testid="media-download"]').forEach(s => s.click())
  document.querySelectorAll('[data-testid="checkbox-round-passive"]').forEach(s => s.click())
```
Note : the css selector [data-testid="checkbox-round-passive"] may change time to time so you will have to inspect the element and figure out the correct selector if this one doesn’t work

now all the files will be selected automatically (it may hang your browser for a while if images are too many)

now click on the download icon and you will get the zip.

See also https://youtu.be/Bkhn34_xfAA and 
https://www.quora.com/How-can-I-export-all-images-from-a-specific-group-in-WhatsApp-for-Android/answer/Aamir-Khan-501
