---
title: "View Data Types"
date: 2017-10-09T15:55:00-07:00
slug: "view-types"
---

So I'm working with a customer on some programming and they're going to offer
me a view from their application which pulls from a hojillion (that's a
technical metric) different tables. Since I have to worry about the types of
data I ultimately get I need to know where we finally land with each field.

To that end, I googled and the glorious
[Stack Overflow gods answered](https://stackoverflow.com/questions/7254380/how-to-find-the-derived-column-types-of-a-view-in-sql-server-2005)
as they usually do - with delicious answers. I tested it and sure enough it
gives me just what I wanted.

{{< gist mrxinu c1c490c41071612cf657e5d1f9788108 >}}

Which produces the following:

![view data types](/img/view-data-types.png)
