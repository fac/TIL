# Pry tricks

### Using the `whereami` command

If you've inserted a pry for debugging, and then gone off spelunking, it can be easy to forget how you got there. Pry's `whereami` to the rescue!

```
[1] pry(#<Copilot>)> whereami

From: app/models/copilot.rb:117 Copilot#company_is_valid_type:

    115: def company_is_valid_type
    116:   require 'pry'; binding.pry
 => 117:   unless eligibility.valid_company_type?
    118:     errors.add(:company, "must be in #{Pricing.valid_company_types.join(", ")}")
    119:   end
    120: end
```

### Using the `cd` command

Using the `cd` command, you can navigate between objects to change the context of your Pry session. As an example (also using `show-method`):

```
[1] pry(main)> company = Company.first
[2] pry(main)> cd company.subscription
[3] pry(#<FAPDSubscription>):1> show-method read_only?

From: app/models/subscription.rb:319:
Owner: Subscription
Visibility: public
Signature: read_only?()
Number of lines: 3

def read_only?
  READ_ONLY == access_level || access_blocked_by_account_manager?
end
```

### Using the `edit` command

If you've configured your shell environment with an `$EDITOR` value (e.g. setting it to `vim` or `code --wait`), from within a Pry REPL session you can use `edit` to compose a command in your editor. When you exit the temporary file that your editor opens, Pry will evaluate it.

One nice additional thing the `edit` command does is make it really easy to patch existing method definitions:

```
[1] pry(main)> edit --patch Salesforce#deliverable?

# Vim opens, and lets us edit:
def deliverable?
  # settings.deliverable?
  true
end

[2] pry(main)> Salesforce.new.deliverable?
=> true # nice!
```

For full detail of all the functionality that's on offer, you can run `edit --help`:

```
[1] pry(main)> edit --help
Usage: edit [--no-reload|--reload|--patch] [--line LINE] [--temp|--ex|FILE[:LINE]|OBJECT|--in N]

Open a text editor. When no FILE is given, edits the pry input buffer.
When a method/module/command is given, the code is opened in an editor.
Ensure `Pry.config.editor` or `pry_instance.config.editor` is set to your editor of choice.

edit sample.rb                edit -p MyClass#my_method
edit sample.rb --line 105     edit MyClass
edit MyClass#my_method        edit --ex
edit --method                 edit --ex -p

https://github.com/pry/pry/wiki/Editor-integration#wiki-Edit_command

    -e, --ex             Open the file that raised the most recent exception (_ex_.file)
    -i, --in             Open a temporary file containing the Nth input expression. N may be a range
    -t, --temp           Open an empty temporary file
    -l, --line           Jump to this line in the opened file
    -n, --no-reload      Don't automatically reload the edited file
    -c, --current        Open the current __FILE__ and at __LINE__ (as returned by `whereami`)
    -r, --reload         Reload the edited code immediately (default for ruby files)
    -p, --patch          Instead of editing the object's file, try to edit in a tempfile and apply as a monkey patch
    -m, --method         Explicitly edit the _current_ method (when inside a method context).
    -h, --help           Show this message.
```

### Using the `help` command

Pry can do all sorts of other clever things; at any time, you can run `help` to get a list of commands, or `help <COMMAND>` (or even `<COMMAND> --help`) to get documentation and examples for a specific command:

```
[8] pry(main)> help show-doc
Usage:   show-doc [OPTIONS] [METH]
Aliases: ?

Show the documentation for a method or class. Tries instance methods first and
then methods by default.

show-doc hi_method # docs for hi_method
show-doc Pry       # for Pry class
show-doc Pry -a    # for all definitions of Pry class (all monkey patches)

    -s, --super             Select the 'super' method. Can be repeated to traverse the ancestors
    -l, --line-numbers      Show line numbers
    -b, --base-one          Show line numbers but start numbering at 1 (useful for `amend-line` and `play` commands)
    -a, --all               Show all definitions and monkeypatches of the module/class
    -h, --help              Show this message.
```

### Command reference

```
Help
  help               Show a list of commands or information about a specific command.

Context
  cd                 Move into a new context (object or scope).
  find-method        Recursively search for a method within a class/module or the current namespace.
  ls                 Show the list of vars and methods in the current scope.
  pry-backtrace      Show the backtrace for the pry session.
  raise-up           Raise an exception out of the current pry instance.
  reset              Reset the repl to a clean state.
  watch              Watch the value of an expression and print a notification whenever it changes.
  whereami           Show code surrounding the current context.
  wtf?               Show the backtrace of the most recent exception.

Editing
  !                  Clear the input buffer.
  amend-line         Amend a line of input in multi-line mode.
  edit               Invoke the default editor on a file.
  hist               Show and replay readline history.
  play               Playback a string variable, method, line, or file as input.
  show-input         Show the contents of the input buffer for the current multi-line expression.

Introspection
  ri                 View ri documentation.
  show-doc           Show the documentation for a method or class.
  show-source        Show the source for a method or class.
  stat               View method information and set _file_ and _dir_ locals.

Commands
  import-set         Import a pry command set.

Aliases
  !!!                Alias for `exit-program`
  !!@                Alias for `exit-all`
  $                  Alias for `show-source`
  /whereami[!?]+/    Alias for `whereami`
  ?                  Alias for `show-doc`
  @                  Alias for `whereami`
  file-mode          Alias for `shell-mode`
  find-routes        Alias for `find-route`
  history            Alias for `hist`
  quit               Alias for `exit`
  quit-program       Alias for `exit-program`
  reload-method      Alias for `reload-code`
  show-method        Alias for `show-source`

Byebug
  backtrace          Display the current stack.
  break              Set or edit a breakpoint.
  continue           Continue program execution and end the pry session.
  down               Move current frame down.
  finish             Execute until current stack frame returns.
  frame              Move to specified frame #.
  next               Execute the next line within the current stack frame.
  step               Step execution into the next line or method.
  up                 Move current frame up.

Input and output
  .<shell command>   All text following a '.' is forwarded to the shell.
  cat                Show code from a file, pry's input buffer, or the last exception.
  change-inspector   Change the current inspector proc.
  change-prompt      Change the current prompt.
  clear-screen       Clear the contents of the screen/window pry is running in.
  fix-indent         Correct the indentation for contents of the input buffer
  list-inspectors    List the inspector procs available for use.
  save-file          Export to a file using content from the repl.
  shell-mode         Toggle shell mode. bring in pwd prompt and file completion.

Misc
  pry-version        Show pry version.
  reload-code        Reload the source file that contains the specified code object.
  toggle-color       Toggle syntax highlighting.

Navigating pry
  !pry               Start a pry session on current self.
  disable-pry        Stops all future calls to pry and exits the current session.
  exit               Pop the previous binding.
  exit-program       End the current program.
  jump-to            Jump to a binding further up the stack.
  nesting            Show nesting information.
  switch-to          Start a new subsession on a binding in the current stack.

Rails
  find-route         See which urls match a given controller.
  recognize-path     See which route matches a url.
  show-middleware    Show all middleware (that rails knows about).
  show-model         Show the given model.
  show-models        Show all models.
  show-routes        Show all routes in match order.
```
