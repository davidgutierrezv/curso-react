
# Curso de React Básico – Clase 7

## 🎯 Objetivo de la Clase

Aprender los fundamentos del testing en aplicaciones React utilizando **React Testing Library (RTL)**. Realizar pruebas de componentes, simular (mockear) hooks y contextos, y testear formularios con validaciones.

---

## 🧪 ¿Por qué hacer testing en React?

- Asegura el comportamiento esperado de los componentes.
- Reduce errores en producción.
- Permite refactorizar con mayor confianza.
- Mejora la mantenibilidad del código.

---

## 🧰 Instalación de herramientas de testing

Para Vite + React + TypeScript:

```bash
npm install --save-dev vitest @testing-library/react @testing-library/jest-dom jsdom @testing-library/user-event
```

### Configuración en `vite.config.ts`

```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  test: {
    environment: 'jsdom',
    globals: true,
    setupFiles: './src/setupTests.ts',
  },
});
```

### Crear archivo `src/setupTests.ts`

```ts
import '@testing-library/jest-dom';
```

---

## 🧪 Pruebas de componentes

### Componente a testear:

```tsx
export function Saludo({ nombre }: { nombre: string }) {
  return <h1>Hola, {nombre}</h1>;
}
```

### Test:

```tsx
import { render, screen } from '@testing-library/react';
import { Saludo } from './Saludo';

test('muestra el nombre correctamente', () => {
  render(<Saludo nombre="David" />);
  expect(screen.getByText(/Hola, David/i)).toBeInTheDocument();
});
```

---

## 🧩 Mock de hooks

### Hook personalizado:

```tsx
export function useContador() {
  const [valor, setValor] = useState(0);
  return { valor, incrementar: () => setValor((v) => v + 1) };
}
```

### Mock en test:

```tsx
vi.mock('./useContador', () => ({
  useContador: () => ({
    valor: 10,
    incrementar: vi.fn(),
  }),
}));
```

---

## 🌐 Mock de contexto

### Crear contexto:

```tsx
export const UsuarioContext = createContext({ nombre: '' });
```

### Consumidor:

```tsx
const { nombre } = useContext(UsuarioContext);
```

### Mock:

```tsx
render(
  <UsuarioContext.Provider value={{ nombre: 'Renata' }}>
    <ComponenteQueUsaContexto />
  </UsuarioContext.Provider>
);
```

---

## 📝 Testing de formularios

### Componente:

```tsx
function Formulario() {
  const [nombre, setNombre] = useState('');

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    alert(`Hola ${nombre}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={nombre}
        onChange={(e) => setNombre(e.target.value)}
        placeholder="Nombre"
      />
      <button type="submit">Enviar</button>
    </form>
  );
}
```

### Test:

```tsx
import userEvent from '@testing-library/user-event';

test('envía el formulario correctamente', async () => {
  render(<Formulario />);
  await userEvent.type(screen.getByPlaceholderText('Nombre'), 'Renata');
  await userEvent.click(screen.getByText('Enviar'));
  expect(screen.getByDisplayValue('Renata')).toBeInTheDocument();
});
```

---

## ✅ Buenas prácticas

- Testear comportamiento, no implementación.
- Usar `screen` para acceder al DOM virtual.
- Evitar `act()` manual salvo casos muy específicos.
- Usar `userEvent` en vez de `fireEvent`.

---

## 🧪 Ejercicios propuestos

1. Crear una prueba para un componente `<Contador />` que aumente al hacer clic.
2. Simular el uso de `useAuth()` con un mock que devuelva un usuario falso.
3. Probar un formulario que valide email y password.
4. Crear test para una lista que se renderiza a partir de props.
5. Probar un componente que use contexto de tema (`claro`/`oscuro`).

---

## 🔜 Próxima clase

- Deploy de aplicaciones React.
- Opciones: Vercel, Netlify, GitHub Pages.
- Variables de entorno.
- CI/CD básico con GitHub Actions.
