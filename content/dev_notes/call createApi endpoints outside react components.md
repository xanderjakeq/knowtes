---
title: "call createApi endpoints outside react components"
enableToc: false
date: "2023-05-05"
lastmod: :git
tags:
- web
---

[[dev_notes/rtk-q createApi|rtk-q createApi]] endpoints can be called from outside react components
by dispatching the returned [[redux thunk]] from the endpoints' `.initiate()`.

Example from [[dev_notes/react forms|react forms]].
```tsx
const res = await store.dispatch(authApi.endpoints.forgotPassword.initiate(userInput.email));
```
The [[redux store]] instance needs to be imported to `.dispatch()` the endpoint. The 
response data will be added to the store and cached. More on 
[[dev_notes/rtk query|rtk query]]'s cache behavior [here](https://redux-toolkit.js.org/rtk-query/usage/cache-behavior).