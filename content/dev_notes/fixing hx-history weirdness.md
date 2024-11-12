---
title: fixing hx-history weirdness
enableToc: false
date: 2024-11-12
lastmod: :git
tags:
---
the [hx-history-elt](https://htmx.org/attributes/hx-history-elt/) is used to specify the navigation with the
arrow buttons on the browser itself.

as you make changes to html fragments and different paths
to render new content, it may behave weirdly. for me 
it rendered the whole html document within the target element 
creating a recursive looking page

to fix this, go to the clear the localStorage. 
[hx-history](https://htmx.org/attributes/hx-history/) saves snapshots in localStorage. i'm not completely
sure but what i think happened is that when i was making updates
the snapshots in localStorage is not updated. so clearing
it updates the snapshots with the latest contents

