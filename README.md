lang: [es](./docs/README-es.md) | ***en***

When starting with a new framework or super class such as Lit Element, Vue, React or angular, we find "starter kits" that have too much information that in principle is not useful or we do not know what certain files are for.

Today we have many configuration files which make Web development more complex but at the same time more robust.

The idea of ​​this post is to introduce new developers to `Lit` with a fairly simple template that allows them to play with it locally and after playing with it for a while and you understand how everything works, you can start integrating more configurations to the project .

I highly recommend using `typescript`. Programming in pure `javascript` in 2021 is no longer an option. I personally consider it a bad practice. If you don't know typescript yet, I recommend you learn it and if you don't want to use it just skip the `tsc` setting and use` .js` or `.mjs` extensions

### TLDR;

### Requirements
- Have `npm` or` yarn` installed
- Use VS code
- Have installed `lit-plugin` for VS Code. Download: [`lit-plugin by Rune Mehlsen`] (https://marketplace.visualstudio.com/items?itemName=runem.lit-plugin)

### Key concepts

`Yarn`: For this tutorial we will use` yarn` since personally it solves dependencies better, it has more functions that `npm` does not have and is used in other projects. The commands are very similar, don't worry if you haven't seen `yarn` yet.

[`lit-plugin`] (https://marketplace.visualstudio.com/items?itemName=runem.lit-plugin) Is a syntax highlighting, type checking and code completion for `lit` in VS Code.

[`Vite`] (https://vitejs.dev/) is a build tool that aims to provide a faster and leaner development experience for modern web projects.

## 🚀 Tutorial

First we will initialize the project with yarn and leave the default values ​​that it gives us by touching `enter` in all of them.

```bash
yarn init
```

### ⚙️ Dependency installation
After that we install `lit`,` vite` and `typescript` which will be the only thing we need to start. We also need to install `@ types / node` just for VS code to autocomplete some suggestions in the editor.

```bash
yarn add lit
yarn add -D vite @types/node typescript
```

### ⚡️ Vitejs Settings

We create a file called `vite.config.ts` and inside it we place the following

```typescript
import { defineConfig } from "vite";

export default defineConfig({});
```

By default `vite` uses our `index.html` as entrypoint. You can change this configuration according to its [documentation](https://vitejs.dev/config/)


### ⚔️ Typescript Configuration

The TypeScrip configuration is simple. First we must initialize `typescript`.

As we already installed `typescript` with` yarn`, it allows us to run the binaries installed in `node_modules/.bin` with `yarn <bin>` unlike `npm` that we have to add `npm run <bin>`

```bash
yarn tsc --init
```

Then in the configuration file we must find and change / enable the following options.
```json
{
    "target": "es2020", // Specify ECMAScript target version
    "module": "es2020", //  Specify module code generation
    "moduleResolution": "node", // Specify module resolution strategy
    "experimentalDecorators": true //  Enables experimental support for ES7 decorators.
}
```

### 💻 Create our Hello world

We create a file `my-element.ts`

```typescript
import { LitElement, html, css } from "lit";
import { customElement, property } from "lit/decorators.js";

@customElement("my-element")
export class MyElement extends LitElement {
	static styles = [
		css`
			:host {
				display: block;
			}
		`
	];

	@property() name = "World";

	render() {
		return html`<h1>Hello, ${this.name}</h1>`;
	}
}
```


And now we create a file `index.html` that imports by means of` type = "module` our script
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lit Simple Starter Kit</title>
</head>
<body>
    <my-element></my-element>
    <script type="module" src="/src/my-element.ts"></script>
</body>
</html>
```

### 💯 Execution of DevServer

Finally in our package.json add a `dev` script to make it easier for us to run our development server.

```json
"scripts": {
    "dev": "vite"
}
```

and now we run our test server with `yarn dev`

```bash
$ yarn dev

vite v2.3.6 dev server running at:

> Local: http://localhost:3000/
> Network: use `--host` to expose
```

We enter [https://localhost:3000/](http://localhost:3000/) and we will have our hello world 😃

# Github
This example is uploaded to github [https://github.com/litelement-dev/lit-simple-starter-kit](https://github.com/litelement-dev/lit-simple-starter-kit)