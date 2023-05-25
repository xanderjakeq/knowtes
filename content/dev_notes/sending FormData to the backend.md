---
title: "sending FormData to the backend"
enableToc: false
date: "2023-05-25"
lastmod: :git
tags:
- web
---

When forms have numeric or boolean data, they will be sent as strings
to the backend. Just be aware that this is happening to do some work
to turn them into the proper datatypes.

Or one solution is:
```js
//frontend
const fd = new FormData();
const dataObject = {
	test: 1
};
fd.append('data', JSON.stringify(dataObject));
fetch('/', {
	method: 'POST',
	body: fd
});

//backend
//find data in the request somehow
const { data } = request.body;
const properData = JSON.parse(data);
```

This way, there's no need to iterate and check each key what datatype they should 
be. What was sent is what is received. Not sure if there's a downside when doing this,
do let me know!

I got confused by this when working on [[dev_notes/react forms|react forms]]. The data in this call:
```js
submit(data, { 
	method: 'POST',
	action: '/route'
})
```
Is not the same when it got to the `Action` function.