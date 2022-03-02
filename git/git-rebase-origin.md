# Git Rebase Origin
or: You can rebase origin!!!

Today, I accepted a suggested commit on github, then forgot to pull that commit to my local branch.

Then, as written in the script from the "wouldn't it be dumb if..." play about this exact scenario, I committed a change locally.

And when I went to push, git pointed out my dumb, but very human error.

After about 20 seconds of panic, and thinking of ways I know to fix this, I thought "I wonder if..." and the answer was yes, the internet confirmed.

`git rebase origin/[branch-name]`

Worked a treat.

I felt a little smart seconds after feeling incredibly dumb.
