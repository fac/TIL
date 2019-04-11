## Finding when code was first introduced.

I often find myself looking at some code and wondering, "when was this first introduced, and by whom?". Up until now my go-to solution has been `git blame`, which shows when the code line(s) were most recently changed, though in many cases this'll highlight a commit where someone made a subtle indentation change, rather than the commit that first introduced the code.

As an example scenario, I want to know when `mysterious_method` was first introduced to our `application_controller`.

After asking for help in our Engineering Slack, I received two solutions, both of which work beautifully to show the history of a code fragment over time.

### `git log` with line numbers

Git's `log` command allows you to pass in the range of line numbers you're interested in for a given file. The command will then return a full list of commits that, at some point in time, updated (or indeed introduced) those line(s) of code. In my early experience `git log` is smart enough to cope with the code block moving around the file (changing line number) as new lines are added or removed.

In today's `master` branch `mysterious_method` is defined between lines 127 and 131, so here's the command we'd run to try and trace the method's origin.

```bash
git log -L 127,131:app/controllers/application_controller.rb
```

### The git pickaxe

In addition to passing explicit line numbers to `git log`, it's also possible to search for mention of a particular string. For example, the command below searches for commits that touch code containing the string `mysterious_method`:

```bash
git log -p -S mysterious_method
```
