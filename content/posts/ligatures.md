---
title: "Ligatures and You"
date: 2017-07-19T05:18:00-07:00
slug: "ligatures"
---

I professed my love for ligatures today on Twitter in passing but I didn't offer
any context. I got the reply below and thought I could throw something out here
explaining my start-stop-start attempt at using them.

{{< tweet 887803488729653249 >}}

I can't remember where I saw them first, but I thought I'd give them a try. The
font that the article mentioned was [FiraCode](https://github.com/tonsky/FiraCode) which I'd never used but as soon as
I saw my code I thought "oh no... no no no." It looked blurry and choppy for
reason and that just wasn't happening. I tried it with another font that I liked
and of course ligatures aren't magic - the font has to support them.

So, I ditched that idea.

Later, and I can't remember if it was [Florin Pățan](https://twitter.com/dlsniper) or [Francesc Campoy](https://twitter.com/francesc) but one of
them was using it and being the ~~lemming~~ gopher that I am I had to give it
another go. It turned out that bumping the font size a little bit made the odd
blurry business go away and I was back in business.

You can check out the [Firacode](https://github.com/tonsky/FiraCode) project for their comparison with a regular font
but I wanted to run through the reasons that I enjoy it, especially when writing
Go code:

1. I can immediately tell if I've not written `!=` correctly because it didn't convert to the ligature.
1. The `:=` initializer characters are kerned more closely than the surrounding characters.
1. Using `->` with channels feels more obvious when it looks like an arrow.

Anyway, give it a try. You might like it.

**Update: "And for the record, it was [@francesc](https://twitter.com/francesc) not me, I don't believe in ligatures :D" - [Florin Pățan](https://twitter.com/dlsniper)**
