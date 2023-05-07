---
title: "why vim"
date: "2023-05-07"
lastmod: :git
draft: false
enableToc: true
tags:
- tool
---

## hmm

Programmers are writers, it could be argued that we think more than we write. But
at the end of the day, writing is how something becomes real. Writing at the speed
of thought is ideal to get ideas out of our heads quickly, even when we're just writing 
to chat, or to tweet.

If you agree with the statement above, we can talk about vim. What does it solve?

When we write on a computer, we glue our eyes to where the [[misc/cursor|cursor]] 
is. It shows where the activity is. Normally, you control where it goes by typing 
something new, it follows the end of the new text. Or use the mouse to point and 
click where you want it to go. 

Using the mouse feels like the normal thing to do. However, you want to avoid it if
you're  optimizing for writing speed. Think about what the physical actions done to 
get to the mouse. Assuming you have proper finger placement, you have to move your 
hand away from the keyboard to the mouse or trackpad, then go back to your 
keyboard orienting your fingers back to their proper position. This takes 
time, if you try it now you might think It's dumb to even consider this. This 
small amount of time adds up to a lot, since when programming, you move your cursor 
all around a file. Vim saves you from this by not relying on the keyboard.

## modes

How can it do this? How can you navigate just by using the keyboard? Vim has modes,
they reflect the modes you get into when writing. When you are thinking, reading, and 
navigating, you are in `Normal` mode. Actually writing, `Insert` mode. Selecting text, 
copy and paste, `Visual` mode. And if you want to do something outside of the text file, 
like saving/creating new files,  `Command` mode. You can get into these different modes 
by pressing a key or a combination of keys.

Different modes give different meaning/function to your keys. This exact same 
thing happens when you press the modifier keys: `Shift`, `Ctrl/Cmd`, and `Alt`. On 
`Shift` mode, your keys output capital letters. On `Normal` mode your keys control
the cursor and move around the file.

It's better described in a demo, so watch this guy use vim.
<iframe width="560" height="315" src="https://www.youtube.com/embed/y6VJBeZEDZU?controls=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


## install
You don't have to install Vim the editor to try these out. Your `vsc*de` should have a 
plugin that implements vim motions. If you start being comfortable with the vim
motions, you can install the editor so you can do more with your sweet new muscle
memory. You can now say "I use vim btw".

This is not a vim tutorial, it's just an introduction and reasoning of why I use vim. I type
slow, around two years ago I started trying increase my typing speed. My average 
speed now is around 60 wpm on [monkeytype](https://monkeytype.com/). When I used `vsc*de`, I felt very slow 
since I also kept moving my hand away from the keyboard to reach the mouse. You 
might be faster than I am at typing, great! I envy you and I will keep practicing. If 
you're still using the mouse to edit code, you have room to be faster than you are 
now!

If this hasn't convinced you to try vim it's okay, it took me a while to try it 
out too. If reaching for the mouse makes you hesitate and think about vim, I'm happy.

Note that Vim is just a text editor, it doesn't have autocomplete and a file tree out of 
the box. You have to set it up and install some plugins to make it feel like `vsc*de`.

Here's some links to get you started on your vim journey:
- [neovim](https://neovim.io/) - new/better descendant of vim
- [theprimeagen](https://www.youtube.com/playlist?list=PLm323Lc7iSW_wuxqmKx_xxNtJC_hJbQ7R) - the fastest, smoothest vim user
- [neovim ide setup](https://youtu.be/stqUbv-5u2s) - neovim maintainer's guide
- instant IDE configs, if you don't want to set it up yourself.
	- [LunarVim](https://www.lunarvim.org/)
	- [NvChad](https://nvchad.com/)
