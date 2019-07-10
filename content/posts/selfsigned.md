---
title: "Using a Self-Signed SSL Certificate"
date: 2019-07-10T11:54:03-07:00
draft: false
slug: "selfsigned"
---

You've been hacking on your project and you're about to move it into a client's
environment. You ask them for a valid SSL cert and they say "use self-signed
for now". Okay, alright, I can do that, but now I have to convince my
application that's it's okay to blow off the lack of authority for this
certificate. Until then it's `NET::ERR_CERT_INVALID` in the console log every
time the API gets accessed.

No big deal, right? I'm using `axios` and I know that I can create an instance
of it with a custom HTTPS agent that will ignore the unauthorized cert like
this:

```js
const instance = axios.create({
    httpsAgent: new https.Agent({
    rejectUnauthorized: false
    })
});

// use instance as you would normally (e.g., instance.get(), instance.post())
```

The problem is that error won't go away until the _browser_ believes that
it's done its due diligence in warning you. If your website and your API are
on the same host/port, that's no big deal, you probably already said "proceed
anyway" when the page loaded. If it's not on the same host/port then your
API is still sitting there off to the side and your browser hasn't had that
chat with you about _that_ site yet.

For example, your front-end is on `https://example.com` (typical `TCP/443`) and
your API is on `https://example.com:8080`. If you don't head to the second
URL and port and do the "yes, I know this is a really bad idea" routine it's
still going to fail. Once you do, it's happy sailing.

![bad ssl is okay](/img/bad-ssl-is-okay.png)

I hope this helps someone. It was making me slightly insane.
