
# Curso de React Básico – Clase 2

## 🎯 Objetivo de la Clase

Profundizar en JSX, el uso de props y composición de componentes. Introducir hooks fundamentales (`useState`, `useEffect`) y avanzar a hooks más avanzados como `useCallback`, `useMemo`, `useContext`. Introducción a `useQuery` y `useAuth` como ejemplos prácticos de hooks personalizados o de librerías externas.

---

## 🔤 JSX a fondo

### ¿Qué es JSX?

JSX es una extensión de sintaxis que permite escribir estructuras similares a HTML dentro de JavaScript.

```jsx
const elemento = <h1>Hola Mundo</h1>;
```

### Características clave:

- Debe haber un solo elemento raíz.
- Puedes usar expresiones JavaScript dentro de `{}`.
- Las clases CSS se escriben con `className`.
- Los estilos en línea usan objetos:

```jsx
const estilo = { color: 'red', fontSize: '20px' };
<h1 style={estilo}>Texto rojo</h1>
```

---

## 🧩 Props y Composición de Componentes

### Props

- Son **inmutables**.
- Permiten pasar información de un componente padre a uno hijo.

```tsx
function Saludo({ nombre }: { nombre: string }) {
  return <p>Hola, {nombre}</p>;
}
<Saludo nombre="Renata" />
```

### Composición

- React fomenta la composición de componentes pequeños.

```tsx
function Layout({ children }: { children: React.ReactNode }) {
  return <div className="layout">{children}</div>;
}

<Layout>
  <Saludo nombre="David" />
</Layout>
```

---

## 🧠 useState

Permite manejar estado local dentro de un componente.

```tsx
import { useState } from 'react';

function Contador() {
  const [contador, setContador] = useState(0);

  return (
    <div>
      <p>Contador: {contador}</p>
      <button onClick={() => setContador(contador + 1)}>Incrementar</button>
    </div>
  );
}
```

---

## 🌐 useEffect

Permite ejecutar efectos secundarios (fetch, eventos, timers, etc).

```tsx
import { useEffect } from 'react';

useEffect(() => {
  console.log("Componente montado");
  return () => console.log("Componente desmontado");
}, []);
```

Dependencias:
- `[]` → solo al montar.
- `[variable]` → se ejecuta al cambiar esa variable.
- Nada → se ejecuta en cada render.

---

## 🔁 useCallback

Memoriza funciones para evitar que se redefinan en cada render.

```tsx
const handleClick = useCallback(() => {
  console.log("Clic!");
}, []);
```

Evita renders innecesarios en componentes hijos.

---

## 🧠 useMemo

Memoriza valores calculados para evitar cálculos innecesarios.

```tsx
const resultado = useMemo(() => calcularAlgo(pesado), [dependencia]);
```

---

## 🔍 useContext

Permite compartir datos entre componentes sin prop-drilling.

### Crear contexto

```tsx
const TemaContext = createContext("claro");
```

### Usar en proveedor

```tsx
<TemaContext.Provider value="oscuro">
  <App />
</TemaContext.Provider>
```

### Usar en consumidor

```tsx
const tema = useContext(TemaContext);
```

---

## ⚙️ useQuery (ejemplo con React Query)

Usado para manejar estados de fetching asincrónico, caché, loading, etc.

```tsx
import { useQuery } from '@tanstack/react-query';

const { data, isLoading, error } = useQuery({
  queryKey: ['usuarios'],
  queryFn: () => fetch('/api/usuarios').then(res => res.json()),
});
```

---

## 🔐 useAuth (hook personalizado)

Hook que encapsula la lógica de autenticación.

```tsx
function useAuth() {
  const [usuario, setUsuario] = useState(null);

  useEffect(() => {
    const token = localStorage.getItem("token");
    if (token) {
      // validar token o traer info del usuario
      setUsuario({ nombre: "David" });
    }
  }, []);

  return { usuario };
}
```

---

## 🧪 Ejercicios propuestos

1. Crear un componente `<Perfil nombre="David" edad={30} />`.
2. Agregar un botón para ocultar/mostrar el componente usando `useState`.
3. Usar `useEffect` para mostrar un mensaje en consola al montar.
4. Usar `useMemo` para calcular la edad al cuadrado.
5. Crear un contexto de tema con `useContext` y alternar entre oscuro y claro.
6. Usar `useQuery` para traer datos falsos desde una API pública (`https://jsonplaceholder.typicode.com/users`).

---

## 🔜 Próxima clase

- Eventos y manejo de formularios.
- Validación con Zod.
- Manejo de listas y keys.
- Manejo condicional de componentes.
