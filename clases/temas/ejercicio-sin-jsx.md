# Ejercicio: Aplicar los conceptos sin JSX

## Objetivo

Aplicar los conceptos aprendidos creando un botón con React.createElement que al hacer clic muestre un alert. Luego, escribir el mismo botón usando JSX. Comentar las diferencias y ventajas.

## Parte 1: Sin JSX

### Código

```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('app'));

const boton = React.createElement(
  'button',
  { onClick: () => alert('¡Hola!') },
  'Haz clic'
);

root.render(boton);
```

### Explicación

En este ejemplo, usamos `React.createElement` para crear un botón. El primer argumento es el tipo de elemento (`'button'`), el segundo es un objeto con las propiedades del elemento (`{ onClick: () => alert('¡Hola!') }`), y el tercero es el contenido del botón (`'Haz clic'`).

## Parte 2: Con JSX

### Código

```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('app'));

const Boton = () => (
  <button onClick={() => alert('¡Hola!')}>Haz clic</button>
);

root.render(<Boton />);
```

### Explicación

En este ejemplo, usamos JSX para crear el botón. La sintaxis es más legible y se parece al HTML. El componente `Boton` devuelve un elemento JSX (`<button onClick={() => alert('¡Hola!')}>Haz clic</button>`), que es más fácil de entender y mantener.

## Diferencias y Ventajas

### Sin JSX

- **Ventajas**:
  - No requiere configuración adicional para transpilación.
  - Útil para entender cómo funciona React internamente.

- **Desventajas**:
  - Menos legible y más difícil de mantener.
  - Sintaxis más verbosa.

### Con JSX

- **Ventajas**:
  - Sintaxis más legible y similar a HTML.
  - Facilita la escritura y mantenimiento del código.
  - Permite incluir expresiones JavaScript de manera sencilla.

- **Desventajas**:
  - Requiere configuración adicional para transpilación (por ejemplo, Babel).

En resumen, aunque es posible escribir componentes de React sin JSX, usar JSX hace que el código sea más legible y fácil de mantener, lo que es especialmente útil en proyectos grandes y complejos.
