
# Curso de React – Clase 10 (Avanzado)

## 🎯 Objetivo de la Clase

Profundizar en el uso de Next.js para crear aplicaciones completas con API Routes, Server-Side Rendering (SSR) e Incremental Static Regeneration (ISR). Ampliar el uso de TypeScript con utilidades como `Record`, `Partial`, `Pick` y `Omit`. Explorar librerías modernas de manejo de estado como Zustand, Jotai y Recoil. Aprender técnicas avanzadas de testing incluyendo mocks de `fetch` con MSW y pruebas de accesibilidad.

---

## 🌍 Next.js Avanzado

### 📡 API Routes

Next.js permite definir funciones backend en `pages/api`.

```tsx
// pages/api/hola.ts
import type { NextApiRequest, NextApiResponse } from 'next';

export default function handler(req: NextApiRequest, res: NextApiResponse) {
  res.status(200).json({ mensaje: "Hola desde la API" });
}
```

Acceso: `/api/hola`

---

### ⚡ SSR (Server-Side Rendering)

```tsx
export async function getServerSideProps() {
  const res = await fetch("https://api.example.com/posts");
  const posts = await res.json();
  return { props: { posts } };
}
```

---

### 🧊 ISR (Incremental Static Regeneration)

```tsx
export async function getStaticProps() {
  const res = await fetch("https://api.example.com/posts");
  const posts = await res.json();
  return {
    props: { posts },
    revalidate: 60, // re-generar cada 60 segundos
  };
}
```

---

## 🧠 TypeScript Avanzado

### `Record`

```ts
type Rol = 'admin' | 'user';
type Permisos = Record<Rol, boolean>;

const permisos: Permisos = {
  admin: true,
  user: false,
};
```

---

### `Partial`

```ts
type Usuario = {
  nombre: string;
  email: string;
};

const usuarioParcial: Partial<Usuario> = {
  email: "ejemplo@correo.com",
};
```

---

### `Pick`

```ts
type Credenciales = Pick<Usuario, "email">;
```

---

### `Omit`

```ts
type SinEmail = Omit<Usuario, "email">;
```

---

## ⚛️ State Management Avanzado

### Zustand

```bash
npm install zustand
```

```ts
import { create } from 'zustand';

type Estado = {
  contador: number;
  incrementar: () => void;
};

export const useContador = create<Estado>((set) => ({
  contador: 0,
  incrementar: () => set((state) => ({ contador: state.contador + 1 })),
}));
```

---

### Jotai

```bash
npm install jotai
```

```tsx
import { atom, useAtom } from 'jotai';

const contadorAtom = atom(0);

function Componente() {
  const [contador, setContador] = useAtom(contadorAtom);
  return <button onClick={() => setContador(c => c + 1)}>{contador}</button>;
}
```

---

### Recoil

```bash
npm install recoil
```

```tsx
import { atom, useRecoilState, RecoilRoot } from 'recoil';

const contadorState = atom({ key: 'contador', default: 0 });

function Componente() {
  const [contador, setContador] = useRecoilState(contadorState);
  return <button onClick={() => setContador(c => c + 1)}>{contador}</button>;
}
```

---

## 🧪 Testing avanzado

### Mock de fetch con MSW

```bash
npm install msw --save-dev
```

```ts
// mocks/handlers.ts
import { rest } from 'msw';

export const handlers = [
  rest.get('/api/usuario', (req, res, ctx) => {
    return res(ctx.json({ nombre: 'David' }));
  }),
];
```

```ts
// setupTests.ts
import { setupServer } from 'msw/node';
import { handlers } from './mocks/handlers';

const server = setupServer(...handlers);

beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());
```

---

### Pruebas de accesibilidad

Instalar:

```bash
npm install --save-dev @axe-core/react
```

Uso:

```tsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import axe from '@axe-core/react';

if (process.env.NODE_ENV !== 'production') {
  axe(React, ReactDOM, 1000);
}
```

Esto reportará errores de accesibilidad en consola durante el desarrollo.

---

## 🧪 Ejercicios propuestos

1. Crear una API route en Next.js para retornar un JSON de prueba.
2. Usar SSR en una página de productos.
3. Refactorizar tipos con `Partial`, `Pick` y `Omit`.
4. Implementar contador global con Zustand y con Jotai.
5. Escribir tests que usen MSW para mockear una llamada a `/api/usuario`.
6. Correr una prueba con `@axe-core/react` y corregir un error de accesibilidad.

---

## 🏁 Conclusión

Con esta clase avanzamos hacia el desarrollo profesional de aplicaciones modernas, rápidas, escalables y bien testeadas. Combinamos las mejores herramientas actuales del ecosistema React y TypeScript.

---

## 🔜 Recomendaciones siguientes

- Crear un proyecto completo Next.js fullstack
- Usar `react-query` o `tanstack-query` para manejo de datos
- Aplicar patrones de diseño (atomic design, state machines)
- Profundizar en performance y optimización
