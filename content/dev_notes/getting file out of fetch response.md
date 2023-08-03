---
title: "getting file out of fetch response"
enableToc: false
date: "2023-08-01"
lastmod: :git
tags:
- web
---
For an endpoint that returns a file via fetch, the file can be 
accessed by:
```js
const res = await fetch();
const blob = await res.blob();
```

Then it can be used as `src` for `<img>` `<iframe>` etc using [createObjectURL](https://developer.mozilla.org/en-US/docs/Web/API/URL/createObjectURL_static).
```js
const fileLink = URL.createObjectURL(blob);

// <img src={fileLink}/>
```

[[dev_notes/reading content from Blob|Reading content from a Blob]] can also be done.