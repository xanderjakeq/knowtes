---
title: "firebase auth"
enableToc: false
tags:
- auth
- web
---

Firebase auth is free for without limit on the number of users. It could be
a great option to use for new projects. It's also easy to set up.

When using firebase auth on the frontend with a custom backend, the backend
needs to verify the user for authorization.
[verify id tokens](https://firebase.google.com/docs/auth/admin/verify-id-tokens)
Firestore or realtimeDB authorization can be done using 
[db security rules](https://firebase.google.com/docs/firestore/security/get-started)

## manage session cookies
[manage cookies](https://firebase.google.com/docs/auth/admin/manage-cookies)

Firebase hosting has some weird behavior with cookies. It only stores a cookie
named `__session`. If more data needs to be in cookies, they will have to be stored
within `__session`. More [here](https://stackoverflow.com/questions/44929653/firebase-cloud-function-wont-store-cookie-named-other-than-session)

