---
title: "reading content from Blob"
enableToc: false
date: "2023-08-02"
lastmod: :git
tags:
- web
- js
---

[src](https://stackoverflow.com/a/35670491)
```js
var myBlob = new Blob(["Hello"], {type : "text/plain"});
var myReader = new FileReader();
//handler executed once reading(blob content referenced to a variable) from blob is finished. 
myReader.addEventListener("loadend", function(e){
	console.log(e.target.result);
});
//start the reading process.
myReader.readAsText(myBlob);
```

Might need this after [[dev_notes/getting file out of fetch response|getting file out of fetch response]].