## Using the --patch option with git-add

If you ever find youself in a situation when you're about to commit but there are some changes you'd rather leave for a later commit, you can use --patch or -p to pick and choose the diffs or "hunks" that you want to stage:

`git add -p`

It will cycle through each hunk and ask if you want to stage it or not (along with some other options, too):
```
Stage this hunk [y,n,q,a,d,e,?]?
```

[https://git-scm.com/docs/git-add](https://git-scm.com/docs/git-add)
