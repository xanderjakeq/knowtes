```ts
<svelte:options
  customElement={{
    tag: "wips-editor",
    extend: (customElementConstructor) => {
      return class extends customElementConstructor {
        constructor() {
          super();
        }

        connectedCallback() {
          super.connectedCallback();
          htmx.process(this.shadowRoot);
        }
      };
    },
  }}
/>

<script lang="ts">
  import {
    Composer,
    ContentEditable,
    PlainTextPlugin,
    HistoryPlugin,
  } from "svelte-lexical";
  import { theme as PlaygroundEditorTheme } from "svelte-lexical/dist/themes/default";

  const initialConfig = {
    theme: PlaygroundEditorTheme,
    namespace: "Playground",
    nodes: [],
    onError: (error) => {
      throw error;
    },
  };

  let wrapper: HTMLElement;
  $effect(() => {
    htmx.process(wrapper);
  });
</script>

<div bind:this={wrapper}>
</div>

```


I've tried using `extend` but was unsuccessful, and i thought maybe this
way could work and surprisingly it did no clue why

compiling svelte custom elements:

had to do it in 2 compile steps.
the normal build step compiles svelte to typescript
and then it has to be transpiled to javascript then copied to
the static library for the rust server
https://stackoverflow.com/questions/75832641/how-to-compile-svelte-3-components-into-iifes-that-can-be-used-in-vanilla-js/75895650#75895650

the styling is troublesome.
the project is created as a library template. so it has default configs.
the trick is to this compiler option in `svelte.config.js`

```json
compilerOptions: {
	css: 'injected'
},
```

and in the dist-js-vite config,
```json
svelte({
	compilerOptions: {
		customElement: true,
	}
}),
```

css very annoying and i wanted to use tailwindcss

i'm trying to get around this by using the tailwind cli directly
using the same `input.css` and saving a separate output from the main project.
and wherever the custom elements are used, then the custom element tailwind
css output will be loaded