---
title: "redux state outside a component"
enableToc: false
date: "2023-05-05"
lastmod: :git
tags:
- web
---

[docs](https://redux-toolkit.js.org/rtk-query/usage/usage-without-react-hooks#accessing-cached-data--request-status)

When using [[rtk query]], you might want to access state from outside
a react component. This can be done by:
```ts
const result = api.endpoints.getPosts.select()(state);
const { data, status, error } = result;
```
`api` above is created with [createApi](https://redux-toolkit.js.org/rtk-query/usage-with-typescript#createapi).
The state is from `store.getState()`, [more](https://redux.js.org/api/createstore).