## Opening the original PR from a commit SHA

Sometimes you have the commit you're interested in (thanks `git blame`) but the
commit message just doesn't help that much. What you'd really like is the Pull
Request that introduced the commit. Fortunately, Github has your back.

1. Open the commit in Github. https://github.com/fac/freeagent/commit/:sha
2. Beneath the commit message is a link to the branch the commit is currently
   on (probably `master` in this case) and a little greyed out link to the PR
   it was introduced by, in the form of the PR number in parenthesis e.g. (#13)

