
# Curso de React Básico – Clase 4

## 🎯 Objetivo de la Clase

Aprender cómo los componentes pueden comunicarse entre sí mediante el patrón de lifting state, crear custom hooks reutilizables, usar referencias (`refs`) para acceder directamente a elementos del DOM, y comprender las reglas fundamentales del uso de hooks en React.

---

## 🔁 Comunicación entre componentes (Lifting State Up)

### ¿Qué es?

Es el patrón en React donde el estado se "eleva" a un componente ancestro común para que pueda ser compartido por varios hijos.

### Ejemplo:

```tsx
function Hijo({ contador, setContador }: { contador: number, setContador: (n: number) => void }) {
  return <button onClick={() => setContador(contador + 1)}>Contar: {contador}</button>;
}

function Padre() {
  const [contador, setContador] = useState(0);

  return (
    <div>
      <Hijo contador={contador} setContador={setContador} />
    </div>
  );
}
```

---

## 🧩 Custom Hooks

### ¿Qué es un Custom Hook?

Es una función que comienza con `use` y encapsula lógica reutilizable de estado o efectos.

### Ejemplo básico:

```tsx
function useContador(inicial = 0) {
  const [contador, setContador] = useState(inicial);

  const incrementar = () => setContador((c) => c + 1);
  const resetear = () => setContador(inicial);

  return { contador, incrementar, resetear };
}

// Uso
function Componente() {
  const { contador, incrementar, resetear } = useContador(5);

  return (
    <>
      <p>{contador}</p>
      <button onClick={incrementar}>Incrementar</button>
      <button onClick={resetear}>Resetear</button>
    </>
  );
}
```

---

## 📌 Refs y uso con inputs

### ¿Qué es un ref?

`useRef` permite crear una referencia mutable a un valor o a un nodo del DOM sin causar renders.

### Ejemplo: Enfocar un input

```tsx
import { useRef } from "react";

function Formulario() {
  const inputRef = useRef<HTMLInputElement>(null);

  const enfocarInput = () => {
    inputRef.current?.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={enfocarInput}>Enfocar</button>
    </div>
  );
}
```

---

## 📜 Reglas de los Hooks

### Reglas fundamentales:

1. **Solo se llaman en la parte superior del componente** (no dentro de condicionales, bucles, etc).
2. **Solo se llaman dentro de componentes de React o custom hooks**.
3. **Deben comenzar con `use`** (ej: `useContador`, `useFetch`).

### Ejemplo inválido:

```tsx
if (condicion) {
  const [estado, setEstado] = useState(false); // ❌ No permitido
}
```

### Solución:

```tsx
const [estado, setEstado] = useState(false);
if (estado) {
  // lógica condicional
}
```

---

## 🧪 Ejercicios propuestos

1. Crear un componente `<Padre>` que pase un estado numérico a dos hijos y ambos puedan modificarlo.
2. Crear un custom hook `useToggle` para manejar un booleano (visible/oculto).
3. Crear un ref a un input y hacer foco con un botón.
4. Hacer un hook `useFormulario` que encapsule `useState` para manejar un input.
5. Revisar si las reglas de hooks se están cumpliendo con ESLint.

---

## 🔜 Próxima clase

- Routing con React Router.
- Código dividido en páginas.
- Layouts compartidos.
- Navegación y parámetros.
