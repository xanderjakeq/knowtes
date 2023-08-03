---
title: "base64 encoding"
enableToc: false
date: "2023-08-01"
lastmod: :git
tags:
- web
- data
---

# why
[source](https://stackoverflow.com/a/201510)
> When you have some binary data that you want to ship across a network, you
> generally don't do it by just streaming the bits and bytes over the wire in a raw
> format. Why? because some media are made for streaming text. You never know --
> some protocols may interpret your binary data as control characters (like a
>  modem), or your binary data could be screwed up because the underlying protocol
>  might think that you've entered a special character combination (like how FTP
>   translates line endings).

>So to get around this, people encode the binary data into characters. Base64 is one
>of these types of encodings.

> **Why 64?**  
> Because you can generally rely on the same 64 characters being present in many
> character sets, and you can be reasonably confident that your data's going to end up on the other side of the wire uncorrupted.

[toturial](https://www.digitalocean.com/community/tutorials/how-to-encode-and-decode-strings-with-base64-in-javascript)
