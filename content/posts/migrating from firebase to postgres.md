---
title: "migrating from firebase to postgres"
date: "2025-03-14"
lastmod: :git
draft: true
enableToc: true
tags:
- 
---
when exporting users, the created at timestamp from firebase is
in milliseconds and postgres timestamp is in seconds  so divide by 1000
https://stackoverflow.com/a/42884828

autogenerate uuid
```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

insert user_id into users values (uuid_generate_v4());
```
https://stackoverflow.com/a/12505220
https://www.postgresql.org/docs/current/uuid-ossp.html