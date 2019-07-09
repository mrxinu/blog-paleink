---
title: "Gitconfig"
date: 2019-07-09T14:10:59-07:00
draft: false
---

Whenever I have to work on a remote system (usually Windows) I'll do my typical
`git clone <repo here>` routine but then I'm immediately missing my local
aliases for doing things. My `git co -am "message"` falls over and wants
`git commit` instead. My `git lga` with all the colorful abbreviated output
for my logs doesn't work because none of that formating is here.

Normally I'd just fire up `vim ~/.gitconfig` and paste in the same configuration
I use locally but of course on Windows that doesn't work without something like
`Git Bash` or `Windows Linux Subsystem`. It turns out there is a way to do it
with the git command that'll fire up an editor (default: vim) no matter what OS
you're using.

```powershell
PS> git config --edit --global
```

Then I can paste in my time-tested and loved configuration:

```plain
[user]
        name = Steven Klassen
        email = sklassen@gmail.com
[color]
        ui = true
[push]
        default = simple
        followTags = true
[alias]
        lga = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
        co = checkout
        br = branch
        ci = commit
        st = status
        df = diff
        unstage = reset HEAD --
        last = log -1 HEAD
        pushall = push --recurse-submodules=on-demand
        stat = log --stat
        dc = diff --cached
        branches = !legit branches
        graft = !legit graft
        harvest = !legit harvest
        publish = !legit publish
        unpublish = !legit unpublish
        sprout = !legit sprout
        sync = !legit sync
        switch = !legit switch
        resync = !legit resync
        alias = config --get-regexp ^alias\\.
[core]
        autocrlf = true
[pull]
        rebase = true
[rerere]
        enabled = true
[credential]
        helper = wincred
```

The majority of it works out of the box except for the `legit` entries.
Depending how long this engagement is going to work on this remote system I
may install python and do legit's install with pip.

```plain
python -m pip install legit
```

The final result is something that looks like this:

![example of working git config](/static/img/working-git-config.png)
