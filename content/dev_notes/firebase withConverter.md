---
title: "firebase withConverter"
enableToc: false
tags:
- web
---

I'm trying to get correct types when I get data from firebase.

[withConverter docs](https://firebase.google.com/docs/reference/js/v8/firebase.firestore.FirestoreDataConverter)

Problem:
```ts
type User = {uid: string, ...}
let user = fb.collection().data().get().data() as User;
```
I can do this without errors even though actual data is missing `uid`. This should not happen.
[[dev_notes/zod]] might help here.
