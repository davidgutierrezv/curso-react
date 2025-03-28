
# Curso de React Básico – Clase 5

## 🎯 Objetivo de la Clase

Aprender a manejar navegación y enrutamiento con React Router, organizar el código dividiendo la aplicación en páginas, reutilizar layouts compartidos y manejar parámetros en las rutas.

---

## 🌐 Routing con React Router

### Instalación

```bash
npm install react-router-dom
```

### Configuración básica

```tsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import Acerca from "./pages/Acerca";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/acerca" element={<Acerca />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## 📁 Código dividido en páginas

Crear una carpeta `src/pages/`:

```
src/
├── pages/
│   ├── Home.tsx
│   └── Acerca.tsx
```

### Ejemplo de página:

```tsx
// pages/Home.tsx
export default function Home() {
  return <h1>Bienvenido a la página principal</h1>;
}
```

Esto permite tener una estructura modular y escalable.

---

## 🧱 Layouts compartidos

React Router permite definir rutas con layouts compartidos mediante rutas anidadas.

### Crear un layout:

```tsx
import { Outlet, Link } from "react-router-dom";

export default function Layout() {
  return (
    <div>
      <nav>
        <Link to="/">Inicio</Link> | <Link to="/acerca">Acerca</Link>
      </nav>
      <hr />
      <Outlet />
    </div>
  );
}
```

### Usar layout con rutas hijas:

```tsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<Layout />}>
      <Route index element={<Home />} />
      <Route path="acerca" element={<Acerca />} />
    </Route>
  </Routes>
</BrowserRouter>
```

---

## 🧭 Navegación

### Con enlaces `<Link>`:

```tsx
import { Link } from "react-router-dom";

<Link to="/acerca">Ir a Acerca</Link>
```

### Navegación programática con `useNavigate`:

```tsx
import { useNavigate } from "react-router-dom";

const navigate = useNavigate();
navigate("/acerca");
```

---

## 🔢 Parámetros de ruta

### Rutas dinámicas

```tsx
<Route path="usuario/:id" element={<Usuario />} />
```

### Acceder a parámetros

```tsx
import { useParams } from "react-router-dom";

function Usuario() {
  const { id } = useParams();
  return <p>ID del usuario: {id}</p>;
}
```

---

## 🧪 Ejercicios propuestos

1. Crear tres páginas: Home, Contacto, Acerca.
2. Agregar navegación entre ellas usando `<Link>`.
3. Crear un layout compartido con menú superior.
4. Crear una ruta dinámica `/producto/:id` y mostrar el ID del producto.
5. Navegar programáticamente a otra ruta desde un botón.

---

## 🧰 Buenas prácticas

- Agrupar componentes por tipo: `pages/`, `components/`, `layouts/`.
- Evitar rutas duplicadas, usar rutas anidadas cuando sea posible.
- Crear un archivo `routes.ts` para centralizar rutas si la app crece.

---

## 🔜 Próxima clase

- Manejo global de estado.
- Context API avanzada.
- Introducción a Redux (si aplica).
- Middleware y manejo de errores globales.
