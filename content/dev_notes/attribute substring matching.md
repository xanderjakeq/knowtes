---
title: "attribute substring matching"
enableToc: false
date: "2023-08-02"
lastmod: :git
tags:
- web
- css
---

[src](https://www.w3.org/TR/selectors/#attribute-substrings)
For something like `document.querySelectorAll(div[class="test"])` that matches
elements with specific attribute values, the values can be matched with a pattern
to make a narrower selection.

`[att^=val]`
Represents an element with the `att` attribute whose value begins with the prefix "val". If "val" is the empty string then the selector does not represent anything.

`att$=val`
Represents an element with the `att` attribute whose value ends with the suffix "val". If "val" is the empty string then the selector does not represent anything.

`att*=val`
Represents an element with the `att` attribute whose value contains at least one instance of the substring "val". If "val" is the empty string then the selector does not represent anything.

Example:
```js
document.querySelectorAll('ul[data-tag*="75"] > li[data-id^="98"] > div[data-class$="35"] > span[class="ramp value"]'))
```

This will select `span`s whose parents are `div` with `data-class` property  value 
that ends with `35`, whose parents are `li` with `data-id` property value
that starts with `98`, whose parents are `ul` with `data-tag` property that contains
`75` at least once.

