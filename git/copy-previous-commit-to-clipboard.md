## Copying your previous git commit to clipboard

Ever find yourself committing a change that’s almost *exactly* the same as your previous commit to a git repo, but different enough to warrant its own commit?  

The following code snippet copies your last commit message to clipboard, so you can paste it a second time, tweak slightly, and commit :heart:

```ruby
git log -1 --pretty=%B | pbcopy
```

Source: https://coderwall.com/p/kdhlcg/copy-last-git-commit-message-to-clipboard-in-osx
