---
title: "Get History"
date: 2017-08-21T17:46:00-07:00
slug: "get-history"
---

Knowing how long something you did on the command line is a time-honored
tradition going back many generations to our UNIX ancestors. You could run
anything on the command line, groan about how long it took, and then re-run
the command with `time` slapped on the front and find out down to the nanosecond
how long your pain lasted.

I didn't have this at my fingertips in Windows which saddened me, but I would
just glance at a clock or my computer before I started something and then do
the math. Of course if I were doing it in code I'd do a time span of some kind.

Then the other day I was watching someone (and I can't remember who) and they
did this:

```powershell
Get-History -Count 1 | fl *
```

It generated the following glorious output:

```plain
Id                 : 4
CommandLine        : gci -recurse
ExecutionStatus    : Stopped
StartExecutionTime : 8/3/2017 8:48:26 PM
EndExecutionTime   : 8/3/2017 8:48:31 PM
```

It'll even tell you if it completed successfully or if you killed it. Very very
cool.
