## Finding when code was first introduced.

I often find myself looking at some code and wondering, "when was this first introduced, and by whom?". Up until now my go-to solution has been `git blame`, which shows when the code line(s) were *most recently* changed, though in many cases this'll highlight a commit where someone made a subtle indentation change, rather than the commit that first introduced the code.

In my scenario, I wanted to know when the `validate_sender_email` was first introduced to our `password_reset_controller`.

After [asking for help in #git](https://freeagent.slack.com/archives/C427X7VD2/p1554809453000700) I received two solutions, both of which work beautifully to show the history of a code fragment over time.

### `git log` with line numbers

Git's `log` command allows you to pass in the range of line numbers you're interested in for a given file. The command will then return a full list of commits that, at some point in time, updated (or indeed introduced) those line(s) of code. In my early experience `git log` is smart enough to cope with the code block moving around the file (changing line number) as new lines are added or removed.

In [today's master](https://github.com/fac/freeagent/blob/5a41fc92e6678b0efb2096649874f0f212b9fb5b/app/controllers/sessions/password_reset_controller.rb#L127-L131) the `validate_sender_email` method is defined between lines 127 and 131, so here's the command we'd run to try and trace the method's origin.

```bash
git log -L 127,131:app/controllers/sessions/password_reset_controller.rb
```

### The git pickaxe

In addition to passing explicit line numbers to `git log`, it's also possible to search for mention of a particular string. For example, the command below searches for commits that mention `validate_sender_email`:

```bash
git log -p -S validate_sender_email
```
