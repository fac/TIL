## Why is my patch dated 2001?

I created a patch in Git and the "From" line is dated 2001 but the Date is not.  What gives?

```
From dba02bc08e812b1fdbf77da570662dcb68b37e1a Mon Sep 17 00:00:00 2001
From: Pat George <patrick.george@freeagent.com>
Date: Thu, 26 Jul 2018 12:53:06 +0100
Subject: [PATCH] Added why git patches are dated 2001
```

Great question and good eye on you.  [Here's the reason you're looking for](https://git-scm.com/docs/git-format-patch#_discussion).  It's a magic date to signify that the code is coming from format-patch.  So don't panic.  Everything's okay.
