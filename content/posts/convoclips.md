---
title: "convoclips"
date: "2021-05-04"
lastmod: :git
---

## Idea

I like discord. I spend a lot of time on it and decreased my time on other
social media. When I talk, I generally know who I'm talking to. It is also very
customizable. Servers can be how the community wants them to work. In March,
[amreio](https://www.instagram.com/amreio/) had an event called 'Kimo' where
artists draw every day for a month. If for any reason someone missed posting a
new drawing for a day, they will be kicked out of the server. It is a good way
to motivate people to keep drawing.

A thought came about the ones who got kicked out. They are missing a lot of fun
conversations happening on the server. Some are giving very good tips and they
wouldn't be able to learn from it. More people should see the convos. That's
when I had an idea to make a way to make discord conversations shareable.

If such a thing existed, it would also be cool to see a snippet of conversation
from art celebrities like [Steven
Zapata](https://www.instagram.com/stevenzapata_art/), [Ahmed
Aldoori](https://www.instagram.com/ahmedaldoori_art/), and
[Moderndayjames](https://www.instagram.com/moderndayjames/). What are they
talking about? Not that I want to know everything, I just want the highlights.
Maybe they gave some really good critiques to each other that I could learn
from, that would be awesome. Whether it will be useful or not, I
decided to build it.

## Build

It's been a while since I built something people will use. The last one I build
was [startref.io](https://startref.io/) and it's not good. I want this project
to be my best one yet. The past year was all art, so I wasn't able to use my
coding skills. This will be an opportunity to change that and for me to improve
them. The first step was to get myself familiar with the tools I would like to
use for this project.

As a user, I will type `/clip first-message-id last-message-id` to clip a
conversation. See it on a website, and be able to share it. I want to see other
people's clips, be able to search by tags. I can assign a role to some members
of my server so they will be able to clip messages. When there is a clipped
conversation I don't want to be public, I can delete it. The project has three
parts. A webapp/website, server, and a discord bot.

Most of my webapps are built with React. I'm bored with it. Svelte had some buzz
while I was learning art, so I looked into it. It is nice to work with. The
documentation is nice, and the interactive tutorial is very helpful to go
through. Learn anytime without having to set up a dev environment. I think
it's easier to use than React. That might be because I already have some
experience, it's relative.

For the backend, I'll use Firebase since I'm already familiar with it, and seems
there are no new solutions that can compete with it. Rust was the language I
wanted to use. Unfortunately, I didn't find a good library to work with
firebase. It would have been nice to use Rust so I would learn more about it.
The development will be slow, but it's a good trade-off. Rust has a good library
to work with Discord API, but I think it better to keep languages the same for
the projects' backend. I'll save Rust for another project.

## Next

Currently, it is functional enough for testing with real users. I'm sharing it
with some friends for feedback. It would be ideal for someone with a sizeable
server to test it. The goal is to know if I made a useful thing. It's far from
being done, but I'll continue working on it if I know some people find it
useful.
