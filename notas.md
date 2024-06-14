# Tailwind

## [Instalación](https://tailwindcss.com/docs/installation):

```sh
npm install -D tailwindcss
npx tailwindcss init
```

_tailwind.config.js_

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{html,js}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

_input.css_

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

```sh
npx tailwindcss -i ./src/input.css -o ./src/output.css --watch
```

_index.html_

```html
    <link href="./output.css" rel="stylesheet">
  </head>
  <body>
    ...
```

## Colores

```html
<h2 class="bg-lime-600 text-white">Tailwind</h2>
<h2 class="bg-lime-600 text-[#d2d255]">Tailwind</h2>
```

_tailwind.config.js_

```js
    extend: {
      colors: {
        "azul-claro": "#243cff",
        "azul-oscuro": "#0d1b3e",
      },
    },
```

- mx => margen eje X
- my => margen eje Y

Para aplicar `mx-auto` tiene que ser un elemento de bloque, así que si no lo es se agrega `block` para convertirlo

### [Cropping to Text](https://tailwindcss.com/docs/background-clip#cropping-to-text)

Se usa para realizar un gradiente en las etras

```html
<div class="text-4xl font-extrabold">
  <span
    class="bg-clip-text text-transparent bg-gradient-to-r from-pink-500 to-violet-500"
  >
    Hello World!
  </span>
</div>
```

## Medidas

```html
<div class="bg-red-500 w-40">Medidas en Tailwind</div>
<div class="bg-red-500 w-[170px]">Medidas en Tailwind</div>
<div class="bg-red-500 w-1/2">Medidas en Tailwind</div>
<div class="h-[100px]">
  <div class="bg-blue-500 w-1/2 h-full">Medidas en Tailwind</div>
</div>
<div class="bg-pink-500 w-1/2 h-screen">Medidas en Tailwind</div>
```

- h-full => todo el alto del contenedor
- h-screen => todo el alto de la pantalla

## Forms

```html
<form action="" class="bg-white w-1/2 mx-auto mt-8 rounded-lg p-5 ">
  <input
    class="border border-gray-200 w-full rounded-xl px-3 py-2 mb-4 disabled:bg-red-500"
    type="text"
    placeholder="Nombre"
    disabled
  />
  <input
    class="border border-gray-200 w-full rounded-xl px-3 py-2 m-1 focus:ring-1 focus:outline-none  focus:ring-green-400 invalid:focus:ring-red-400 peer"
    type="email"
    placeholder="Correo"
  />

  <p class="text-red-400 hidden peer-invalid:block">El correo es incorrecto</p>

  <input
    class="border border-gray-200 w-full rounded-xl px-3 py-2 mt-4 mb-4 "
    type="password"
    placeholder="Contraseña"
  />
  <input
    class="bg-blue-600 text-white hover:bg-white hover:text-blue-700 border border-blue-500 cursor-pointer w-full rounded-xl p-1 m-1"
    type="submit"
    placeholder="Ingresar"
  />
</form>
```

- Para el focus => focus:outline-none focus:ring-1 focus:ring-green-400 focus:outline-none invalid:focus:ring-red-400

- Para que un elemento cambie estado en base a la validación de un input se usa la clase `peer`, se pone en el input y en el `<p>` que debe aparecer

## Pseudoclases

### Position

```html
<button
  class="bg-orange-600 p-4 m-4 rounded-md relative after:content-['Hola'] after:absolute after:top-4 after:left-36"
>
  Haz click aquí
</button>
```

Con la psudo clase after agregamos contenido al finalizar el espacio del elemento anterior.

Para poder mover el elemento after se usa `absolute`, pero para moverlo tomando como referencia el boton se usa `relative` en el boton.

- after:content-['Hola']
- after:absolute
- after:top-0
- after:left-36

## Flex

Se pueden crear capas (@layers) de componentes con clases personalizadas, aplicando (@apply) clases de Tailwind-css

```css
@layer components {
  .card {
    @apply bg-red-500 w-40 h-40 ...;
  }
}
```

Los `div` son elementos de `bloque`, si al elemento que contiene los divs se le asigna la clase `flex` los div internos pasan a ser elementos de linea, y en vez de una columna pasan a formar una fila.

- Contenedor padre:
  - flex
  - place-content-between
  - place-content-around
  - flex-col
  - flex-col-reverse
  - flex-row -> por defecto
  - flex-row-reverse
  - items-center
  - items-end
  - items-start
- Contenedor/es hijo/s:
  - self-center
  - self-end

Cuando los elementos `flex` puestos en fila, estan pegados, al achicar la pantalla se van contrayendo sus `width`, para que mantengan su ancho definido, se usa `flex-wrap`, así se posicionan más abajo en vez de contraerse.

- Contenedor padre:
  - flex-wrap
  - gap-4
- Contenedor/es hijo/s:
  - grow -> ensacha segun la disponibilidad
  - shrink-0 -> no se contrae el ancho menos de su tamaño, pero se achican manteniendo las relaciones
  - basis-1/4 -> ocupa 1/4 de la pantalla

## Grid

Contenedor padre:

- grid
- grid-cols-4 -> define cantidad de columnas
- Contenedor/es hijo/s:
  - col-span-2 -> se expande 2 cols
  - col-start-2 col-end-4 -> desde hasta donde se expande
  - col-[2/5] -> desde hasta donde también
  - row-span-3 -> se extiende 3 filas (a lo alto)
