---
title: "cors in go"
enableToc: false
date: "2023-08-19"
lastmod: :git
tags:
- go
---

[src](https://www.stackhawk.com/blog/golang-cors-guide-what-it-is-and-how-to-enable-it/)

```go
func enableCors(w *http.ResponseWriter) {   
	(*w).Header().Set("Access-Control-Allow-Origin", "*")   
}

func handleArticles(w http.ResponseWriter, r *http.Request) {
	enableCors(&w)
	js, err := json.Marshal(Articles)   
	if err != nil {   
		http.Error(w, err.Error(), http.StatusInternalServerError)   
		return   
	}
	w.Header().Set("Content-Type", "application/json")   
	w.Write(js)   
}
```

with websockets using gorilla/websocket
```go
var upgrader = websocket.Upgrader{
	Subprotocols: []string{"echo"},
    CheckOrigin: func (r *http.Request) bool  {
        return true
    },
}
```

both allows all. (modify for prod)