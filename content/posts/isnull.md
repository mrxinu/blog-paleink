---
title: "ISNULL"
date: 2019-03-07T04:24:00-07:00
slug: "isnull"
---

This tip comes from my friend Laura the uber DBA. If you're testing a value
for being NULL or being an empty string, do both at the same time with this
handy dandy magic:

```sql
WHERE ISNULL(fieldname, '') != ''
```
