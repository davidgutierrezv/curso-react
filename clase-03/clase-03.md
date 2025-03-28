
# Curso de React Básico – Clase 3

## 🎯 Objetivo de la Clase

Aprender a manejar eventos y formularios en React, validar datos con Zod, trabajar con listas dinámicas y usar renderizado condicional de componentes.

---

## 🖱️ Eventos y Manejo de Formularios

React usa un sistema de eventos sintéticos (`SyntheticEvent`) que funciona de forma similar a los eventos del DOM, pero con una capa de compatibilidad entre navegadores.

### Ejemplo de evento de clic:

```tsx
function Boton() {
  const handleClick = () => {
    alert("Botón presionado");
  };

  return <button onClick={handleClick}>Haz clic</button>;
}
```

### Formulario controlado con `useState`:

```tsx
import { useState } from "react";

function Formulario() {
  const [nombre, setNombre] = useState("");

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    alert(`Hola ${nombre}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={nombre}
        onChange={(e) => setNombre(e.target.value)}
      />
      <button type="submit">Enviar</button>
    </form>
  );
}
```

---

## ✅ Validación con Zod

Zod es una librería de validación de esquemas para JavaScript/TypeScript.

### Instalación

```bash
npm install zod
```

### Uso básico

```tsx
import { z } from "zod";

const schema = z.object({
  nombre: z.string().min(1, "El nombre es requerido"),
  edad: z.number().min(18, "Debes ser mayor de edad"),
});

const resultado = schema.safeParse({ nombre: "", edad: 17 });

if (!resultado.success) {
  console.log(resultado.error.format());
}
```

### Integración en un formulario

```tsx
function validarFormulario(data: any) {
  const schema = z.object({
    email: z.string().email(),
    password: z.string().min(6),
  });

  const result = schema.safeParse(data);
  return result;
}
```

---

## 📋 Manejo de listas y keys

### Renderizar listas:

```tsx
const frutas = ["manzana", "pera", "plátano"];

function ListaFrutas() {
  return (
    <ul>
      {frutas.map((fruta, index) => (
        <li key={index}>{fruta}</li>
      ))}
    </ul>
  );
}
```

### Importancia de las `key`:

- Ayudan a React a identificar qué elementos cambiaron.
- Deben ser **únicas y estables**.

```tsx
usuarios.map((u) => <li key={u.id}>{u.nombre}</li>);
```

---

## 🔀 Manejo condicional de componentes

### Condicional simple con operador ternario

```tsx
{usuario ? <p>Bienvenido {usuario.nombre}</p> : <p>Inicia sesión</p>}
```

### Condicional con `&&`

```tsx
{mostrarMensaje && <p>Este es un mensaje importante</p>}
```

### Renderizado condicional por estado

```tsx
function Panel() {
  const [autenticado, setAutenticado] = useState(false);

  return (
    <div>
      {autenticado ? <Dashboard /> : <Login />}
      <button onClick={() => setAutenticado(!autenticado)}>
        Cambiar estado
      </button>
    </div>
  );
}
```

---

## 🧪 Ejercicios propuestos

1. Crear un formulario con nombre y edad. Validar con Zod.
2. Renderizar una lista de tareas con botón para eliminar cada una.
3. Agregar un botón que muestre u oculte una sección usando `useState`.
4. Mostrar un mensaje solo si el input está vacío.
5. Crear una vista protegida: si el usuario está autenticado muestra el panel, si no el login.

---

## 🔜 Próxima clase

- Comunicación entre componentes (lifting state).
- Custom hooks.
- Refs y uso con inputs.
- Reglas de los hooks.
