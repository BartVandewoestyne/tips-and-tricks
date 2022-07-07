# Configuration
## Setting the editor
If you want to set the editor *only* for Git, do either (you don't need both):

* Set `core.editor` in your Git config: `git config --global core.editor "vim"`
* Set the `GIT_EDITOR` environment variable: `export GIT_EDITOR=vim`

If you want to set the editor for Git *and also other programs*, set the standardized `VISUAL` and `EDITOR` environment variables:

```
export VISUAL=vim
export EDITOR="$VISUAL"
```
_NOTE_: Setting both is not necessarily needed, but some programs may not use the more-correct `VISUAL`.  See [`VISUAL` vs `EDITOR`](https://unix.stackexchange.com/questions/4859/visual-vs-editor-what-s-the-difference).