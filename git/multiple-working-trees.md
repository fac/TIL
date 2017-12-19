# Multiple working trees

The "working tree" is the name given to all the files in a project that are checked out and written to disk when you either clone a repository, or when you checkout a branch.

In other words, it's your source code.

Every repository has one main working tree, but with the `git worktree` command you can add more.

Each new working tree lives in a separate folder on disk, and each one points to a different branch (or commit).

Having multiple trees can be useful for exploring the historical state of a project, or for browsing the code on two different branches.

Add a working tree like this:

    $ git worktree add <path> [branch]

For example, if you were working on a topic branch on the `my-app` project and wanted to see what things looked like on `master`, you might do:

    $ git worktree add ../my-app2 master

All the local branches and commits in your main working tree are available to be checked out in the linked working tree.

    $ cd ../my-app2
    $ git checkout <sha>

See the `git-worktree(1)` man page for more details (there are `list`, `lock`, and `prune` sub commands to learn about).
