---
title: "sveltekit-on-cloudfunctions"
date: "2023-01-11"
lastmod: :git
draft: false
---
What about
[firebase-adapter-node](https://github.com/jthegedus/svelte-adapter-firebase)?
I was using this adapter for my project before sveltekit@1.0.0 came out. I think
it works fine, but the problem is that it is always behind the current version
of sveltekit. You have to use earlier versions of sveltekit. But I don't want to
wait.

So I decided to go with `@sveltejs/adapter-node`. It's better because it has the
same maintainers as sveltekit. It's a safer bet that it will always work with
the latest version of sveltekit. And there's less magic about how a sveltekit
app gets into cloudfunctions.

I assume that you:
- know firebase things especially cloud functions
- use firebase hosting
  [rewrites](https://firebase.google.com/docs/hosting/full-config#rewrite-functions)
- love sveltekit(obviously)

## sveltekit

When you are ready to deploy your sveltekit app, use
[adapter-node](https://github.com/sveltejs/kit/tree/master/packages/adapter-node)
to build it, simple.

`pnpm build`

In `firebase.json`, set the public property to the `client` subdirectory of the
adapter-node's `build` directory.

```json
{
    ...,
    "hosting": {
        "public": "path_to_build_dir/client",
        ...,
        "rewrites": [
          {
            "source": "**",
            "function": "app"
          }
        ]
        ...,
    }
}
```

## cloud functions

Then copy the `build` directory over to the `src` directory inside the cloud
functions directory. In functions `index` file, import `handler` from the
`build` and pass it to `express.use`.

[adapter-node
docs](https://github.com/sveltejs/kit/tree/master/packages/adapter-node#custom-server)

```ts
import { https } from "firebase-functions";
import express from "express";
import { handler as svelteKit } from "./build/handler.js";

const server = express();

server.use(handler);

export const app = https.onRequest(server);
```

If using typescript, run `pnpm build` or `tsc` inside functions directory.

`firebase serve` to check if everything is working properly. You should see your
sveltekit app when you go to the firebase hosting `localhost:port`.

## Notes

Firebase will only preserve a cookie named `__session`, all other cookies
will not get to cloud functions. If you are using cookies in sveltekit, you
could store the data in an object and `JSON.stringify()` then store it to the
`__session` cookie. More on this [here](https://stackoverflow.com/a/44935288).

Only initialize `firebase-admin/app` once. If you are using it in both in cloud
functions `index` file and in the sveltekit app, figure out where you you want
to initialize it that makes sense for your situation.

If you are using typescript, there might be problems with the transpiled code.
These are my relevant config that worked somehow, idk why.

```json
// functions/tsconfig.json

{
    "compilerOptions": {
        "moduleResolution": "node",
        "module": "esnext",
        ...
    }
}
```

```json
// functions/package.json

{
    "type": "module",
    ...
}
```


```json
// sveltekit/package.json

{
    "type": "module",
    ...
}
```

If I wrote something inaccurate, feel free to contact me.