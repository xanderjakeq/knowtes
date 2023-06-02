---
title: "mongodb unauthorized error"
enableToc: false
date: "2023-06-02"
lastmod: :git
tags:
- web
---

```
MongoError: (Unauthorized) not authorized on admin  to execute command
```
If this error comes up when working with MongoDB, it could be that there are
multiple databases in the mongodb instance. The `db` name should be specified
in the connection string like:

```
mongodb+srv://<username>:<password>@test-auth.3w13ht5.mongodb.net/<dbname>?retryWrites=true&w=majority
```