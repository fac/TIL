## Force Push... with lease

We all `git push --force` at least once in our life.
At least once, we regretted it straight away.

Fortunately, git has the solution: `--force-with-lease`.

### What's the difference?

With `git push --force-with-lease`, git will check that the remote branch had not been updated since the last time you fetched it.

### Further Reading

- [Atlassian](https://developer.atlassian.com/blog/2015/04/force-with-lease/)
- [Git-SCM](https://git-scm.com/docs/git-push)
