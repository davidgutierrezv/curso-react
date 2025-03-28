
# Curso de React Básico – Clase 6

## 🎯 Objetivo de la Clase

Aprender cómo manejar estado global en una aplicación React. Utilizar Context API de forma avanzada, conocer los fundamentos de Redux y entender cómo manejar errores y lógica global mediante middlewares o patrones equivalentes.

---

## 🌍 Manejo Global de Estado

### ¿Qué es el estado global?

Es el estado que necesita ser accedido y/o modificado por múltiples componentes a lo largo de la aplicación (por ejemplo: usuario autenticado, tema, carrito de compras, etc).

### Opciones comunes:

- Context API (nativa en React)
- Redux (popular en apps más grandes)
- Zustand, Jotai, Recoil (otras alternativas)

---

## 🧠 Context API avanzada

### Crear un contexto

```tsx
import { createContext, useContext, useState } from "react";

interface TemaContextType {
  tema: string;
  alternarTema: () => void;
}

const TemaContext = createContext<TemaContextType | null>(null);
```

### Crear un proveedor

```tsx
export function TemaProvider({ children }: { children: React.ReactNode }) {
  const [tema, setTema] = useState("claro");

  const alternarTema = () => setTema(t => (t === "claro" ? "oscuro" : "claro"));

  return (
    <TemaContext.Provider value={{ tema, alternarTema }}>
      {children}
    </TemaContext.Provider>
  );
}
```

### Consumir contexto

```tsx
const contexto = useContext(TemaContext);
if (!contexto) throw new Error("TemaContext fuera del proveedor");

const { tema, alternarTema } = contexto;
```

### Usar en `main.tsx`

```tsx
<TemaProvider>
  <App />
</TemaProvider>
```

---

## 🗃 Introducción a Redux (opcional)

Redux es una librería para manejar estado global de forma predecible.

### Instalación

```bash
npm install @reduxjs/toolkit react-redux
```

### Crear un slice

```tsx
import { createSlice } from "@reduxjs/toolkit";

const contadorSlice = createSlice({
  name: "contador",
  initialState: { valor: 0 },
  reducers: {
    incrementar: (state) => {
      state.valor++;
    },
    resetear: (state) => {
      state.valor = 0;
    },
  },
});

export const { incrementar, resetear } = contadorSlice.actions;
export default contadorSlice.reducer;
```

### Configurar el store

```tsx
import { configureStore } from "@reduxjs/toolkit";
import contadorReducer from "./contadorSlice";

export const store = configureStore({
  reducer: {
    contador: contadorReducer,
  },
});
```

### Usar en la app

```tsx
import { Provider } from "react-redux";
import { store } from "./store";

<Provider store={store}>
  <App />
</Provider>
```

### Usar en componentes

```tsx
import { useSelector, useDispatch } from "react-redux";
import { incrementar } from "./contadorSlice";

const valor = useSelector((state) => state.contador.valor);
const dispatch = useDispatch();

<button onClick={() => dispatch(incrementar())}>+</button>
```

---

## 🧱 Middleware y Manejo de Errores Globales

### ¿Qué es un middleware?

En Redux, los middlewares interceptan acciones antes de llegar al reducer.

Ejemplo: logging, manejo de errores, validación, llamadas API.

### Ejemplo de manejo global de errores

```tsx
function ErrorBoundary({ children }: { children: React.ReactNode }) {
  return (
    <ErrorBoundaryReact
      fallbackRender={({ error }) => <p>Error: {error.message}</p>}
    >
      {children}
    </ErrorBoundaryReact>
  );
}
```

También se puede usar:

- `try/catch` en llamadas `async`.
- `useErrorBoundary` de librerías como `react-error-boundary`.

---

## 🧪 Ejercicios propuestos

1. Crear un contexto para manejar el idioma (`es`, `en`), con función para cambiarlo.
2. Usar `useContext` en dos componentes hijos para mostrar el idioma actual.
3. Crear un slice de Redux con un contador y usarlo en una vista.
4. Implementar un `ErrorBoundary` que capture errores de un componente que falla intencionalmente.
5. (Avanzado) Crear un middleware en Redux para registrar acciones en consola.

---

## 🔜 Próxima clase

- Testing básico con React Testing Library.
- Pruebas de componentes.
- Mock de hooks y contextos.
- Testing de formularios.
