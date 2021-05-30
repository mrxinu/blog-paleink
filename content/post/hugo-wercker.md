---
title: "Hugo and Wercker, Oh My"
date: 2017-07-08T20:48:13-07:00
slug: "hugo-wercker"
---

I had taken a swing at setting up a blog on my `mrxinu.github.io` repository a while back
but as soon as I realized that Jekyll uses ruby I was a bit lost. Fast forward 10 months
and having had some Go mileage under my belt I thought I'd give it another try with Hugo.

So, on to the Hugo quick start. That worked alright locally but then I saw that there was
a tutorial for [automating builds and deployments](https://gohugo.io/tutorials/automated-deployments/)
well of course I had to have that in my life. So I went through it and made a ton of mistakes
but finally got it to build and deploy. After all that, a 404 page and GitHub wasn't having
any of it.

The punchline was that `*.github.io` pages aren't the same as the pages served in projects
via a gh-pages branch. The tutorial was trying to do the latter. I was trying to do the
former.

This is the wercker.yml file that I finally wound up with:

```yaml
box: debian
build:
  steps:
    - install-packages:
          packages: git
    - script:
        name: download theme
        code: |
          $(git clone https://github.com/Vimux/Mainroad.git ./themes/mainroad)
    - arjen/hugo-build:
        version: "HEAD"
        theme: "mainroad"
        flags: --buildDrafts=true
deploy:
  steps:
    - uetchy/gh-pages:
        token: $GITHUB_TOKEN
        repo: mrxinu/mrxinu.github.io
        path: public
```

The tutorial recommends that you use the [gh-pages](https://app.wercker.com/applications/51f71ee369cd738a32001822/tab/details/)
deploy package by [lukevivier](https://app.wercker.com/lukevivier) but that generates the website
and pushes it to an `gh-pages` branch. That would work great, except I wanted it to run on my `github.io`
site. So a quick google search (after smashing my face into it for a while) turned up a post that mentions this
other one from [uetchy](https://app.wercker.com/uetchy) that lets you specify a separate repo to
deploy the generated site to. Finally, the blog is up and running.
