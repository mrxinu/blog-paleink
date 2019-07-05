---
title: "Slicing and Dicing with PowerShell"
date: 2017-07-16T05:24:00-07:00
slug: "slicing-dicing"
---

I'm used to using things like cut, grep, sed and friends in Linux/UNIX to take the output
of some command and get the columns, rows, etc. that I want to use. In Windows it's not as
straightforward but PowerShell is making it a little easier. Obviously you can select properties
from PowerShell objects like Get-Service and then whittling that down to the name of the
service, the current status, short name, and the like, but what about regular old commands
like netstat and arp?

I'm writing something to control the lights in my house but before I can do any of that
I need to be able to find the Hue Phillips bridge on the home LAN. The only way I know to
do that is to have a look at the ARP table to find something that has the right OUI. I remember
reading an article about using PowerShell to slice up netstat output so I figured I ought
to be able to do the same thing.

The default output of `arp -a` here is:

```
PS> arp -a

Interface: 192.168.1.2 --- 0x8
  Internet Address      Physical Address      Type
  192.168.1.1           10-0d-7f-6d-c7-f0     dynamic
  192.168.1.3           74-c2-46-a6-c5-67     dynamic
  192.168.1.8           00-17-88-24-89-9e     dynamic
  192.168.1.255         ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static
```

I want the middle column without the header stuff. Evidently assigning the results of
the command gives me an array of strings which I can see by using the `GetType()` method
against the new `$arp` variable and then again against the first element of the array
`$arp[0]`:

```
PS> $arp.GetType()

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     True     Object[]                                 System.Array

PS> $arp[0].GetType()

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     True     String                                   System.Object
```

So the first order or business is getting rid of those header rows so that they don't
interfere with the column slicing. Since `$arp` now has an array of the lines, I can
get the lines I want by asking for a range of lines. I need to give it a start and
end for the range. It looks like a start of 3 will skip the leading blank line, the
interface address line, and the column headers. For the end value I need the index
or the last element in the array and I can get that by using `$arp.Count`.

```
PS> $arp[3..$arp.Count]
  192.168.1.1           10-0d-7f-6d-c7-f0     dynamic
  192.168.1.3           74-c2-46-a6-c5-67     dynamic
  192.168.1.8           00-17-88-24-89-9e     dynamic
  192.168.1.255         ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static
```

Now I need to extract that middle column. The columns are aligned nicely and the
MAC column has exactly 17 characters (12 hex digits + 6 hyphens). One approach would
be to use the string method `Substring` to grab 17 characters starting at position
24 to collect them all:

```
PS> $arp[3..$arp.Count] | %{ $_.Substring(24, 17) }
10-0d-7f-6d-c7-f0
74-c2-46-a6-c5-67
00-17-88-24-89-9e
ff-ff-ff-ff-ff-ff
01-00-5e-00-00-16
01-00-5e-00-00-fb
01-00-5e-00-00-fc
01-00-5e-7f-ff-fa
ff-ff-ff-ff-ff-ff
```

That gets me what I want, but if the columns weren't aligned as well as they
are here or the width of the column wasn't exactly the same it might be more flexible
to say "give me the stuff in the second column which is separated from the others by
1 or more whitespace characters." To do that I can use the `-split` operator:

```
PS> $arp[3..$arp.Count] | %{ $columns = $_ -split "\s+"; $columns[2] }
10-0d-7f-6d-c7-f0
74-c2-46-a6-c5-67
00-17-88-24-89-9e
ff-ff-ff-ff-ff-ff
01-00-5e-00-00-16
01-00-5e-00-00-fb
01-00-5e-00-00-fc
01-00-5e-7f-ff-fa
ff-ff-ff-ff-ff-ff
```

That's a little more wordy than the substring option and I'm not sure which I prefer
but they both get me to the same place. Now that I've done all this I'm going to have
to come up with a different solution anyway because I'm writing this light utility in
Go of course. Ah well, still learned something.
