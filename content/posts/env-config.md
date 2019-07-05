---
title: "Configuration via Environment"
date: 2017-07-09T13:21:00-07:00
slug: "config-env"
---

I had finally gotten tired of fighting with Twitter lists and decided it was time to
start trimming down my follows so I could actually turn on my Home list without it
scrolling my computer into RAM exhaustion.

As luck would have it [Francesc Campoy](https://github.com/campoy) released a video
on his [Just For Func](https://www.youtube.com/channel/UC_BzFbxG2za3bp5NRRRXJSw) series
covering the Twitter API. If you haven't had an opportunity to check this out you should;
it's excellent.

In recent Go applications I had been putting configuration information in a config.toml
file alongside the binary. That had been working, but having to keep track of a configuration
file is a pain and counter to [The 12 Factor App](https://12factor.net/config) way of doing
things. In [this video in particular](https://www.youtube.com/watch?v=SQeAKSJH4vw&t=1277s)
Francesc uses it to get Twitter authentication information.

Here's the relevant code snippet:

{{< gist mrxinu e4830e73582035ae96446a7803539d5c >}}

That gets the important bits out of the way before main() even gets going. It still
feels a little awkward to throw a panic at an end-user that doesn't understand what
panic means, but for now that's working really well.
