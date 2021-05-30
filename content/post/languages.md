---
title: "Language Survey"
date: 2017-10-07T06:15:00-07:00
slug: "languages"
---

A little while ago I gave a primer on Go to a fellow SolarWinds engineer known
as [Dez](https://twitter.com/Dez_Sayz) on the internets. The goal was to get
her started with a programming language that she could use to wrangle some API
stuff in SolarWinds and so that's the route that I went with her:

1. Set up a development environment with [Visual Studio Code](https://code.visualstudio.com/).
1. Run through the typical "Hello World" routine.
1. Introduce 'gofmt/goimports' so there's no shock when things automatically move around on saving.
1. Show how to run the code with 'go run' and compile with 'go build/install'.
1. Illustrate compiling for different platforms by tweaking GOOS and GOARCH.
1. Run through some SolarWinds-specific examples using my very own package, [gosolar](https://github.com/mrxinu/gosolar).

That went well.

Then there was a reply from [Thomas A Ianneli](https://twitter.com/tiannelli)
asking why Go over other programming languages that we've used. I've been
thinking about writing this up for a while, so here we are. First, a quick run
through of the languages I've used already with significant enough mileage that
I can say that I can write anything I need to without much struggle.

## Shell Script (Bash/KSH)

This was my first foray into programming. I was working at a credit company
doing tech support and realized that I was running the same N commands over
and over in the same order. This was better than that.

Pros: better than running the same commands over and over // Cons: requires
mastery of dozens of linux/unix utilities to be truly useful

## Perl

I picked this one up when my car broke down one weekend (damned carburetor) and
I had nothing else to do but cuddle with a blue O'Reilly title with a lovable
dromedary on the cover. It had control structures, lots of "special" variables
with arcane names like $|, and enough regular expression to make you curl up
into a ball and cry.

Pros: regular expression at your fingertips // Cons: regular expression at
your fingertips

## Python

I can't remember when/why I tried this one, but it was in the early days of
v1 vs. v2 and v3 didn't even exist yet. I loved the enforced formatting which
may be why I really love gofmt these days. More of the usual concepts, but now
OOP was in full effect and classes were the thing. And list comprehensions that
seem like such a great idea until you forget how they work after not using them
and then you have to relearn the concept again just so you can read your own
code.

Pros: very pretty to look at // Cons: dependencies are a
challenge (see: [virtualenv](http://docs.python-guide.org/en/latest/dev/virtualenvs/))

## C#/.NET

After using a text editor and an interpreter all these years to write the
languages above I was super intrigued by the Visual Studio editor. All those
features, and a debugger, and yeah, what fun. Then I created my first winforms
application. A mad-libs thing that I must have hacked on for weeks and then
didn't actually show anyone. Then several videos/howtos later I got more
comfortable with all the various collection types. Lists and other things
with angle brackets in the description. There were so many and I feel like I
only scratched the surface.

Pros: lovely for doing GUIs in Windows // Cons: you really have to be all-in
with the .NET koolaid to navigate the language well

## PowerShell

I picked this one up on a weekend while I was visiting a friend of mine in
Austin. I think I was waiting for some game to install on his spare laptop
and I ran through [A Task-Based Guide to PowerShell](https://technet.microsoft.com/en-us/library/dd772285.aspx)
which is still a fantastic primer on the language. I recommend it to anyone
that's just getting started with this one. It gives you just enough to get
familiar with the moving parts and enough to get you going with some things
that you can use as a systems administrator (or really anyone wrangling Windows
systems) without much heartache.

Pros: found on every Windows system since 7 // Cons: managing data structures
(add-member, anyone?) is a challenge

## Go

I tried this for the first time in October of 2016 and I was bummed that I
hadn't tried it sooner. Going through the [Tour of Go](https://tour.golang.org)
followed by [Go by Example](https://gobyexample.com/) made for getting used to
the language pretty straightforward. I'll admit I had to bend my brain a little
to get through slices vs. arrays and then interfaces, but once I rounded the
bend it was full steam ahead. I've used it to write CLIs, web servers, APIs,
and then all manner of pushing, pulling, and data manipulation I've had to do
since then.

Pros: formatted nicely, runs quickly, compiles to an executable // Cons: would
be nice if it could make me a ham sandwich too, but that's probably asking too
much

## Summary: Why Go

### Deployment

I like that I'm able to compile the work that I've done and hand an executable
with a configuration file to a customer and they can run with it. I don't have
to worry about making sure their system is set up just right and they can't
get in there and muck about with the functionality of the thing without coming
back to me for the changes.

### Juggling Data

One of the things I found so frustrating with Perl and its ilk is handling
data. Arrays of references of other arrays and hashes and, ugh, just let me
sleep, I'm so tired. I had the same kind of experience with PowerShell with
its objects and properties and members (what even is a NoteProperty as
opposed to a regular Property?) With Python you could at least give your
class instances properties, but then again you had to be all in with classes.

In Go, I can create a struct, or a slice of structs and between those and
the native types I can create any kind of container I need for what I'm working
with.

### Testing/Development

I like being able to run 'go run main.go' to see what I've done recently and
I like being able to write tests against what I've written to make sure what
I've written hasn't broken horribly. It feels like an interpreted language
without leaving all my bits in the wind for anyone to tweak whenever they
feel like it.

### Concurrency

I've tried. I really have tried to grasp the await concepts in C# so that I
could flex the muscle of the mighty multi-core processor. I just can't make it
work in my head. With Go I have goroutines which I understood on the first few
passes and have actually be able to use to some great effect.

### Community

I've never used a language that had a community that was consistently awesome
as I have with Go. Between the [GoBridge](https://golangbridge.org/) Slack
team and the fine folks on Twitter I've been able to get through any problem
I've run into without having to hop on sites like Hackhands or its equivalent
just to get through the language mechanics and move a project forward.

I'll likely add to this, but for now, that's why I really enjoy Go.
