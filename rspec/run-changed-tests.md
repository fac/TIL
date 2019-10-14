# How to run only tests that have been changed

When you've made changes to some specs that you've been working on, you might only want to run tests that you've fiddled with 
rather than the whole test suite. Using this snippet allows you to run just the changed specs, regardless of whether they've
been staged for commit yet:

```console
$ git status --porcelain | cut -c "4-" | grep "^spec" | paste -s -d " " - | xargs bundle exec rspec
```

To ensure just Ruby specs are run through RSpec, use this command:

```console
$ git status --porcelain | cut -c "4-" | grep "^spec/.+\.rb$" | paste -s -d " " - | xargs bundle exec rspec
```

This one-liner can also be adapted to run Rubocop over changed files as well. Here's an example command:

```console
$ git status --porcelain | cut -c "4-" | grep "rb$" | paste -s -d " " - | xargs bundle exec rubocop
```

In this case, we've changed the grep command to search for lines ending in `rb`, rather than those that begin with `spec` and
passed it to `bundle exec rubocop`.

## Breakdown

For those interested in what this whole snippet does piece-by-piece, I thought I'd explain each command:

### `git status --porcelain`

The `--porcelain` flag for `git-status` produces a stripped back status output that's easier to parse for scripts.

Here's an example output when running on my dirty worktree:

```console
$ git status --porcelain
 M app/jobs/email_marketing/marketing_consent_prospect_update_job.rb # <- Modified, but unstaged
M  config/environments/development.rb # <- Modified & staged
M  config/environments/integration.rb
M  config/environments/production.rb
M  config/environments/sandbox.rb
M  config/environments/staging.rb
M  config/environments/test.rb
 M lib/email_marketing/end_users_client.rb
 M spec/controllers/signup_controller_spec.rb
 M spec/features/signup_spec.rb
 M spec/jobs/email_marketing/marketing_consent_prospect_update_job_spec.rb
 M spec/lib/email_marketing/end_users_client_spec.rb
 M spec/requests/signup_conversion_tracking_spec.rb
?? vim-ruby.log # <- new file, unknown to git
```

The lines beginning with `M` at the beginning of the line are files that I've changed and staged for commit. The lines with
an `M` but a leading indentation are changed, but not yet staged for commit. The lines beginning with `??` are files unknown
to `git`.

### `cut -c "4-"`

This `cut`s out everything before the 4th character, leaving the rest of the line.

In terms of the above command, it leaves us with:

```console
$ git status --porcelain | cut -c "4-"
app/jobs/email_marketing/marketing_consent_prospect_update_job.rb
config/environments/development.rb
config/environments/integration.rb
config/environments/production.rb
config/environments/sandbox.rb
config/environments/staging.rb
config/environments/test.rb
lib/email_marketing/end_users_client.rb
spec/controllers/signup_controller_spec.rb
spec/features/signup_spec.rb
spec/jobs/email_marketing/marketing_consent_prospect_update_job_spec.rb
spec/lib/email_marketing/end_users_client_spec.rb
spec/requests/signup_conversion_tracking_spec.rb
vim-ruby.log
```

### `grep "^spec"`

`grep` is a tool for searching through text and matching it against a regular expression. For people who know a bit of regular
expressions (regex for short), you might recognise the caret character, `^`, in `^spec`. The caret (`^`) specifies the
beginning of the line, so this regex will only select lines that begin with `spec`.

Here's what our output is now:

```console
$ git status --porcelain | cut -c "4-" | grep "^spec"
spec/controllers/signup_controller_spec.rb
spec/features/signup_spec.rb
spec/jobs/email_marketing/marketing_consent_prospect_update_job_spec.rb
spec/lib/email_marketing/end_users_client_spec.rb
spec/requests/signup_conversion_tracking_spec.rb
```

### `paste -s -d " " -`

This command simply joins all the lines from the previous output into a new list delimited by spaces.

```console
$ git status --porcelain | cut -c "4-" | grep "^spec" | paste -s -d " " -
spec/controllers/signup_controller_spec.rb spec/features/signup_spec.rb spec/jobs/email_marketing/marketing_consent_prospect_update_job_spec.rb spec/lib/email_marketing/end_users_client_spec.rb spec/requests/signup_conversion_tracking_spec.rb
```

### `xargs bundle exec rspec`

`xargs` is a tool for processing arguments to be passed into another command. In this case, taking the specific spec files and
passing them to `rspec` to become 
`bundle exec rspec spec/controllers/signup_controller_spec.rb spec/features/signup_spec.rb ...`

```console
$ git status --porcelain | cut -c "4-" | grep "^spec" | paste -s -d " " - | xargs bundle exec rspec
<some spec output here>
```
