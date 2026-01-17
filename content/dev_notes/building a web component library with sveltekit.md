---
title: "building a web component ui library with sveltekit"
enableToc: false
date: "2026-01-17"
lastmod: :git
tags:
- web
- svelte
---

I want to explore creating a UI library of Web Components with Sveltekit. Web
components can be used like any other html element so it is framework
agnostic. Since svelte is it's own language it has a "compiler" that outputs
vanilla js and is able to generate web components. I'm sure it's possible to do
with other frameworks like React but it svelte has built-in support for it so
it's convenient.

For whatever reason, Sveltekit cli `npx sv create` doesn't have an option to
create a library that compiles to web components. Theres some setup required.
I followed this [guide](https://lukaswhite.com/blog/building-web-components-with-svelte/)
it took me a while to get it working though.

The most relevate part of it though is the plugins in `vite.config.ts`.
```ts
...
plugins: [
    // Process normal Svelte files (exclude .wc.svelte files)
    svelte({
        exclude: '**/*.wc.svelte',
    }),
    // Process web component files (only include .wc.svelte files) and compile them as custom elements
    svelte({
        include: '**/*.wc.svelte',
        compilerOptions: {
            customElement: true,
        }
    }),
    ...
],
...
```

The first call to `svelte()` should exclude files that ends with `.wc.svelte`
and the second exclusively operates on the files that matches it. However, when 
I did this (svelte@5.45.6) I get a bunch of build errors.

```
vite v7.3.1 building client environment for production...
✓ 79 modules transformed.
✗ Build failed in 239ms
error during build:
[vite-plugin-svelte:compile] [plugin vite-plugin-svelte:compile] src/lib/Button.svelte 
(7:22): /home/xanderjakeq/dev/uilib/src/lib/Button.svelte:7:22 Expected token } 
https://svelte.dev/e/expected_token
file: /home/xanderjakeq/dev/uilib/src/lib/Button.svelte:7:22

  5 |  
  6 |  export default function Button($$anchor, $$props) {
  7 |    $.push($$props, true);
                              ^
  8 |  
  9 |    /** Is this the principal call to action on the page? */
```

It is compiling `Button.svelte` twice. The first time it is compiled, the file
contents are replaced with the generated code in-place? But that's another
question. The second time, it is trying to compile the generated code which is
not a valid svelte code. Thus we have the errors.

This might be a bug with `include/exclude` properties. If I undestand correctly,
the `include` will only operate on the files that matches the pattern. So it
should not match any other file but those that end with `.wc.svelte`. Why is it
trying to compile `Button.svelte`?

The workaround for now is to edit the `extensions` property which defaults to 
['.svelte']. Then it should work as expected.

```
...
plugins: [
    // Process normal Svelte files (exclude .wc.svelte files)
    svelte({
        exclude: '**/*.wc.svelte',
    }),
    // Process web component files (only include .wc.svelte files) and compile them as custom elements
    svelte({
        extensions: ['.wc.svelte'],
        compilerOptions: {
            customElement: true,
        }
    }),
    ...
],
...
```

Should I file a bug report for this?

