---
title: "go slice reallocation"
enableToc: false
date: "2023-08-09"
lastmod: :git
tags:
- go
---

The length of a slice may be changed as long as it still fits within the limits 
of the underlying array; just assign it to a slice of itself. The _capacity_ of 
a slice, accessible by the built-in function `cap`, reports the maximum length 
the slice may assume. Here is a function to append data to a slice. If the data 
exceeds the capacity, the slice is reallocated. The resulting slice is returned. 
The function uses the fact that `len` and `cap` are legal when applied to the 
`nil` slice, and return `0`.

```go
func Append(slice, data []byte) []byte {
    l := len(slice)
    if l + len(data) > cap(slice) {  // reallocate
        // Allocate double what's needed, for future growth.
        newSlice := make([]byte, (l+len(data))*2)
        // The copy function is predeclared and works for any slice type.
        copy(newSlice, slice)
        slice = newSlice
    }
	// changes the length to fit len of data
    slice = slice[0:l+len(data)]
	//actually copy(append) values of data into slice
    copy(slice[l:], data)
    return slice
}
```