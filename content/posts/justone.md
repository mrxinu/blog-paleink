---
title: "Just One Row"
date: 2017-07-30T10:43:00-07:00
date: 2019-03-22T15:15:00-07:00
slug: "just-one"
---

There are so many a-ha moments when you're writing code and I really wish
I had started writing them down at some point because I feel like I could
write a book by now.

Last night I was copying some code from a previously-written function that
feeds JSON data to a website via an API endpoint. For some reason no matter
how much data I sent, a single row would show up on the page and nothing
else. This was infuriating.

Finally I skipped the website altogether and loaded it up on Postman to
make sure something wasn't getting swallowed on the way. Sure enough, one
row is being produced. I also realized I wasn't sending an `application/json`
header so I fixed that, but still, one row.

Next I started combing through the code (for the umpteenth time) and then
it hit me - the write to the website was happening INSIDE the loop that was
gathering up the records to send instead of happening outside the loop once
the records were completely gathered. Hence, a single row.

Check your loops y'all.
