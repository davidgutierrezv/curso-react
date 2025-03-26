# 🧠 Clase 1 – Configuración del entorno y estructura del proyecto

## 🧩 ¿Qué es React?

React es una librería de JavaScript para construir interfaces de usuario (UI), mantenida por Meta.

- Se basa en un enfoque declarativo y componente basado.
- React no es un framework, no impone estructura de carpetas, rutas, ni sistema de estados global.
- Renderiza en el DOM virtual, luego lo reconcilia con el DOM real para optimizar la actualización de la UI.

## ⚡ ¿Qué es Vite?

Vite es un bundler y dev server de última generación para aplicaciones modernas (usando ES Modules).

- Desarrollado por Evan You (creador de Vue)
- Utiliza esbuild (escrito en Go) para ser extremadamente rápido

### En modo desarrollo:
- No bundlea todo el proyecto
- Sirve los archivos como módulos nativos desde el navegador

### En producción:
- Usa Rollup para generar bundles optimizados

## 🔗 ¿Cómo trabajan juntos Vite y React?

Vite actúa como el builder y dev server de una aplicación React.

- Usa plugins para interpretar JSX, TypeScript y más.
- Se integra con React usando @vitejs/plugin-react que habilita soporte para JSX, Fast Refresh, y más.
- Proporciona una experiencia muy rápida para desarrollo con recarga instantánea y sin bundles pesados.

## 📁 Estructura del Proyecto

Después de ejecutar:

```
npm create vite@latest mi-proyecto-react -- --template react-ts
```
Tendrás algo como esto:

```
mi-proyecto-react/
├── node_modules/
├── public/
├── src/
│   ├── App.css
│   ├── App.tsx
│   ├── index.css
│   ├── main.tsx
├── .gitignore
├── index.html
├── package.json
├── tsconfig.json
├── tsconfig.node.json
├── vite.config.ts
├── package-lock.json
```

### Archivos principales:

#### 📦 package.json
Archivo central que define:

- Dependencias (dependencies)
- Dependencias de desarrollo (devDependencies)
- Scripts (npm run dev, build, preview)
- Nombre del proyecto, versión, etc.

```json
{
  "name": "mi-proyecto-react",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
}
```

#### 🔒 package-lock.json / pnpm-lock.yaml / yarn.lock
Garantiza que todos instalen exactamente las mismas versiones de dependencias.

Generado automáticamente al correr npm install.

#### ⚙️ vite.config.ts
Archivo de configuración de Vite. Ejemplo:

```ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
})
```
Permite agregar plugins, configurar rutas alias, puertos, comportamiento de build, etc.

#### 🔠 tsconfig.json y tsconfig.node.json
Configuración de TypeScript.

Define cómo se interpretan los archivos .ts y .tsx.

Ejemplo clave:

```json
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "jsx": "react-jsx",
    "strict": true
  }
}
```
jsx: "react-jsx": para que el compilador entienda JSX moderno con React 17+ sin necesidad de importar React.

#### 📄 index.html
Punto de entrada manual, no hay template inject automático como en CRA.

Contiene:

```html
<div id="root"></div>
<script type="module" src="/src/main.tsx"></script>
```

#### 📂 src/
Contiene el código fuente principal.

main.tsx: punto de entrada JS → React se monta aquí.

```tsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.tsx'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
)
```
App.tsx: componente principal del proyecto.

## 🛠 Recomendaciones para tus estudiantes

> Antes de comenzar con componentes, estado o hooks, asegúrate que comprendan:

1. Qué hace cada archivo
2. Cómo se carga React en el navegador
3. Por qué Vite es tan rápido (no bundlea en dev)
4. Qué significa `type="module"` en el HTML
5. Qué hace el script dev

### 1. Qué hace cada archivo

- **package.json**: Define las dependencias, scripts y metadatos del proyecto.
- **vite.config.ts**: Configuración de Vite, incluyendo plugins y opciones de build.
- **tsconfig.json**: Configuración de TypeScript, define cómo se interpretan los archivos .ts y .tsx.
- **index.html**: Punto de entrada manual, contiene el div root y el script principal.
- **src/**: Contiene el código fuente principal, incluyendo App.tsx y main.tsx.

### 2. Cómo se carga React en el navegador

React se carga en el navegador a través del archivo `main.tsx`, que monta el componente raíz (`App.tsx`) en el div con id `root` en `index.html`.

### 3. Por qué Vite es tan rápido (no bundlea en dev)

Vite es rápido porque en modo desarrollo no bundlea todo el proyecto. En su lugar, sirve los archivos como módulos nativos desde el navegador, lo que reduce el tiempo de espera para recargar cambios.

### 4. Qué significa `type="module"` en el HTML

El atributo `type="module"` en el script de `index.html` indica que el archivo es un módulo ES6. Esto permite el uso de import/export y otras características de ES6.

### 5. Qué hace el script dev

El script `dev` en `package.json` ejecuta Vite en modo desarrollo, iniciando un servidor local y habilitando la recarga instantánea de cambios.

## 💡 Introducción técnica a React

### 🎯 Objetivo de la clase

Comprender qué es React, cómo funciona a nivel conceptual y cómo se diferencia del desarrollo con JavaScript puro. Introducir funciones puras, el Virtual DOM, y sentar las bases para JSX y componentes.

### 🛠️ Paso 0: Configuración del entorno

#### ✅ Requisitos previos
- Tener instalado Node.js (v18 o superior recomendado)
- Tener instalado Visual Studio Code
- Tener instalado Git (opcional, pero recomendado)

#### 📦 Verificar Node y npm
```bash
node -v
npm -v
```

#### 🧰 Extensiones recomendadas para VS Code
- ESLint
- Prettier
- React Developer Tools (como extensión de navegador también)
- Volar / TypeScript (ya viene incluido en VS Code)

#### 🚀 Crear el proyecto con Vite y React + TypeScript
```bash
npm create vite@latest mi-proyecto-react -- --template react-ts
cd mi-proyecto-react
npm install
npm run dev
```
Explicar qué hace cada comando, qué significa cada carpeta:
/src, App.tsx, main.tsx, vite.config.ts, tsconfig.json.

#### 🧪 Validar instalación
El navegador debe abrir http://localhost:5173 con una app mínima funcionando.

Mostrar cómo editar App.tsx y ver los cambios en tiempo real.

### 🧱 1. ¿Qué es React?
Definición:

- Librería de JavaScript para construir interfaces de usuario (UI).
- Declarativa, basada en componentes reutilizables.
- Mantenida por Meta (Facebook).

#### ¿Por qué React?:
- Escalabilidad.
- Reutilización.
- Rendimiento (gracias al Virtual DOM).
- Ecosistema y comunidad.

### ⚙️ 2. ¿Cómo funciona React por dentro?
#### DOM real vs Virtual DOM:
- El DOM es costoso de manipular directamente.
- React crea un árbol en memoria (Virtual DOM), hace un diffing entre estados y aplica los cambios necesarios en el DOM real (reconciliación).

#### React es JavaScript:
- JSX es solo azúcar sintáctico.
- Los componentes son funciones puras que devuelven una representación de UI.

#### Reactividad:
- El estado cambia → React renderiza nuevamente.
- Unidirectional data flow (flujo de datos hacia abajo).

### 🧪 3. JavaScript puro vs React (antes de JSX)
#### 🧼 JavaScript sin React:
```javascript
const root = document.getElementById('app');
const button = document.createElement('button');
button.innerText = 'Haz clic';
button.addEventListener('click', () => {
  alert('¡Hola!');
});
root.appendChild(button);
```

#### ⚛️ React sin JSX:
```javascript
import React from 'react';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('app'));

const element = React.createElement(
  'button',
  { onClick: () => alert('¡Hola!') },
  'Haz clic'
);

root.render(element);
```
Explicar: React.createElement(tag, props, children).

### 🧼 4. Funciones puras en React
Una función pura no tiene efectos secundarios y siempre devuelve lo mismo con los mismos argumentos.

Los componentes de React son funciones puras:

```javascript
function Saludo(props) {
  return `Hola, ${props.nombre}`;
}
```
Contrastar con funciones que modifican el DOM directamente o dependen de variables externas.

### 🔀 5. ¿Qué es JSX?
JSX = JavaScript + XML.

Azúcar sintáctico para React.createElement.

No es obligatorio, pero mejora la legibilidad.

```jsx
const elemento = <button onClick={() => alert('Hola')}>Haz clic</button>;
```
Transpilación con Babel:

JSX → React.createElement(...)

Es necesario transpilar para que el navegador lo entienda.

### ⚙️ 6. ¿Qué es la transpilación?
Es el proceso de convertir código moderno (JSX, ES6+) a código que entienden los navegadores.

Herramientas: [Babel](./content/babel.md), [TypeScript](./content/typescript.md), [SWC](./content/swc.md) (usado en Vite).

Mencionar que Vite utiliza ES Modules y una transpilación mucho más rápida (mediante esbuild/SWC).

### 🧩 7. ¿Qué es un componente?
Función pura que retorna JSX.

Composición: un componente puede usar otros componentes.

Se puede pasar estado y props.

```tsx
function Boton(props: { texto: string }) {
  return <button>{props.texto}</button>;
}
```

### 🔁 8. Hooks (breve mención)
useState, useEffect, etc.

Permiten manejar estado y ciclo de vida.

Se verá en profundidad más adelante.

### 🛠️ 9. Configuración básica del proyecto con Vite + TypeScript
```bash
npm create vite@latest nombre-proyecto -- --template react-ts
cd nombre-proyecto
npm install
npm run dev
```
Explicar estructura de carpetas.

Mostrar dónde vive el componente raíz (App.tsx).

Cómo se monta en main.tsx.

### 📚 10. Ejercicio para la clase
Objetivo: Aplicar los conceptos sin JSX.

Crear un botón con React.createElement que al hacer clic muestre un alert.

Luego, escribir el mismo botón usando JSX.

Comentar las diferencias y ventajas.

### 🧠 Para la próxima clase:
JSX a fondo.

Props y composición de componentes.

Introducción a useState.



