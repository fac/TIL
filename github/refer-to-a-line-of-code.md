## Refer to a line of code

When viewing a file on GitHub, we can generate a link to a particular line by clicking the relevant line number.
Doing so highlights the line in yellow and adds, for example, `#L45` to the github.com file URL, if we're wanting to highlight line 45, say:

```
https://github.com/fac/freeagent/blob/master/app/models/invoice.rb#L45
```

It should be noted that this is not future-proof.

To generate a link to a particular line with reference to the current moment in git history, follow the steps above and, once the line is highlighted, press `y`. This will add the current SHA to the URL:

```
https://github.com/fac/freeagent/blob/8d7194205cc9a234166aae323a54c36cf9feee05/app/models/invoice.rb#L45
```
