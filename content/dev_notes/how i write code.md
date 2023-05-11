---
title: "how i write code"
enableToc: false
date: "2023-05-10"
lastmod: :git
tags:
- hmmm
---

Before writing any code, it always start with some goal.

Let's say I want to represent a string like below into a JSON object.
```
"id: 13, name: new emp, age: 20, contact: some contact, email: email@email.com"
```

After having a clear goal, I would start with just making it work somehow. Usually, I 
would just print the data I'm working with. Then see that the properties are separated
with `,` and the key value pairs are separated with `:`.

So, what I need to do is split the whole string by `,` then the substrings by `:`.
It should look something like this.
```ts
const str = "id: 13, name: new emp, age: 20, contact: some contact, email: email@email.com";
let json: Record<string, string> = {};

str.split(',').forEach((prop) => {
	const [key, val] = prop.split(':');
	//when testing on different inputs, seem like there are inconsistent
	//padding for the key and values... so do .trim()
	json[key.trim()] = val.trim();
});

// use `json` for something
```

This works, but if I need to do this again somewhere else while I'm on "just get this 
working" mode, I would just copy and paste this snippet. When the bigger goal is 
kinda working, I can switch to "make this pretty" mode, time to refactor.

If I see this string-to-json code scattered around, I would write it into a function with
a descriptive name and as short as possible.
```ts
function strToJSON(str: string) {
    let json: Record<string, string> = {};

    str.split(',').forEach((prop) => {
        const [key, val] = prop.split(':');
        json[key.trim()] = val.trim();
    });

    return json;
}
```

This function could be written within the same file if the project is small enough, or if
I don't foresee using this function anywhere else in the project. If the new function is 
used all around a bigger project, it would make sense to extract it
into a `utils` file or folder.

As I do this, I think about future readers/editors of the code (most likely me). Since I 
want future me to have an easier time, I try to write and structure the code so that it's
easy to read and extend. The code should speak for itself, I'll know what it's doing
as I read it. No need for comments. Leave `todo` comments to make note of 
what/how things can be improved. I think comments are fine when something had to 
be written a certain way and write about `why`.

When I read the snippet above in six months, I would immediately have an idea what 
the function does. And if I search for where it's defined and I see that it's in `utils`,
I would be careful changing it, it might break some code somewhere unexpected.

The "goal" can be bigger or smaller it could be the whole project. The amount of 
refactoring depends on how messy I started it and how "nice" I want it. "Good code" is 
subjective when talking beyond raw performance metrics.

My ideas about writing code are not my own. I've read these stuff around the 
interwebs and practiced what worked for me. Also, use [[posts/why vim|vim]] btw.
