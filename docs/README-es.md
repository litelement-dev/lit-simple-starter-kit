lang: [en](https://dev.to/herberthobregon/lit-simple-starter-kit-with-vitejs-typescript-2188) | ***es***

Al momento de iniciar con un nuevo framework o super clase como Lit Element, Vue, React o angular nos encontramos con "starter kits" que tienen demasiada información que en principio no nos es util o no sabemos para que sirven ciertos archivos.

Hoy en dia tenemos muchos archivos de configuración lo que hacer que el desarrollo Web cada dia se vuelva mas complejo pero a la vez mas robusto.

La idea de este post es intruducir a nuevo desarrolladores a `Lit` con un template bastante simple que le permita jugar con él en local y luego de jugar con él un rato y ya comprenda como funciona todo, pueda empezar a integrar mas configuraciones al proyecto.

Recomiendo encarecidamente usar `typescript`. Programar en `javascript` puro en el 2021 ya no es una opción. Personalmente lo considero una mala practica. Si aun no sabe typescript, te recomiendo aprenderlo y si no deseas usarlo simplemente omite la configuración de `tsc` y usa extensiones `.js` o `.mjs`

### TLDR;

### Requisitos
-   Tener instalado `npm` o `yarn`
-   Usar VS code
-   Tener instalado `lit-plugin` para VS Code. Descarga: [`lit-plugin by Rune Mehlsen`](https://marketplace.visualstudio.com/items?itemName=runem.lit-plugin)

### Conceptos clave

`Yarn`: Para este tutorial usaremos `yarn` ya que en lo personal resuelve mejor las dependencias, tiene mas funciones que `npm` no tiene yuso en otros proyectos. Los comandos son muy parecidos no te preocupes si aún no haz visto `yarn`.

[`lit-plugin`](https://marketplace.visualstudio.com/items?itemName=runem.lit-plugin) Is a syntax highlighting, type checking and code completion for `lit` in VS Code.

[`Vite`](https://vitejs.dev/) is a build tool that aims to provide a faster and leaner development experience for modern web projects.

## 🚀 Tutorial

Primero incializaremos el proyecto con yarn y dejamos los valores predeterminados que nos da tocando `enter` en todas.

```bash
yarn init
```

### ⚙️ Instalación de dependencias 
Luego de ello instalamos `lit`, `vite` y `typescript` los cuales será lo unico que necesitamos para iniciar. También necesitamos instalar `@types/node` unicamente para que VS code nos autocomplete algunas sugerencias en el editor.

```bash
yarn add lit
yarn add -D vite @types/node typescript
```

### ⚡️ Configuración de Vitejs

Creamos un archivo que se llame `vite.config.ts` y dentro del él colocamos lo siguiente

```typescript
import { defineConfig } from "vite";

export default defineConfig({});
```

Por defecto `vite` usa nuestro `index.html` como entrypoint. Esta configuración la puedes cambiar deacuerdo a su [documentación](https://vitejs.dev/config/)


### ⚔️ Configuracion de Typescript

La configuracion de TypeScrip es sencilla. Primero debemos inicializar `typescript`.

Como ya instalamos `typescript` con `yarn`, este permite ejecutar los binarios instalados en `node_modules/.bin` con `yarn <bin>` a diferencia de `npm` que tenemos que agregar la palabra `npm run <bin>`

```bash
yarn tsc --init
```

Luego en el archivo de configuración debemos de buscar y cambiar/habilitar las siguientes opciones.
```json
{
    "target": "es2020", // Specify ECMAScript target version
    "module": "es2020", //  Specify module code generation
    "moduleResolution": "node", // Specify module resolution strategy
    "experimentalDecorators": true //  Enables experimental support for ES7 decorators.
}
```

### 💻 Crear nuestro Hello world

Creamos un archivo `my-element.ts`

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


Y ahora creamos un archivo `index.html` que importe por medio de `type="module` nuestro script

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

### 💯 Ejecución de DevServer

Por último en nuestro package.json agregar un script `dev` para que nos sea mas fácil ejecutar nuestro servidor de desarrollo.

```json
"scripts": {
    "dev": "vite"
}
```

y ahora ejecutamos nuestro servidor de pruebas con `yarn dev`

```bash
$ yarn dev

vite v2.3.6 dev server running at:

> Local: http://localhost:3000/
> Network: use `--host` to expose
```

Ingresamos a [https://localhost:3000/](http://localhost:3000/) y tendrémos nuestro hello world 😃

# Github
Este ejemplo esa subido a github [https://github.com/litelement-dev/lit-simple-starter-kit](https://github.com/litelement-dev/lit-simple-starter-kit)
