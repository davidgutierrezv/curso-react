
# Curso de React Básico – Clase 9 (Extensión Avanzada)

## 🎯 Objetivo de la Clase

Ampliar los conocimientos adquiridos con temas más avanzados como testing unitario e integración, uso de TypeScript avanzado en componentes, manejo de formularios con React Hook Form, introducción al renderizado del lado del servidor con Next.js y pruebas end-to-end con Playwright o Cypress.

---

## 🧪 Testing unitario vs testing de integración

### Testing unitario

- Prueba **una unidad** de código de forma aislada (ej: una función, un componente simple).
- Usa mocks para aislar dependencias.

```tsx
function suma(a: number, b: number): number {
  return a + b;
}

test('suma correctamente', () => {
  expect(suma(2, 3)).toBe(5);
});
```

### Testing de integración

- Prueba **la interacción entre múltiples unidades**.
- Incluye interacción de usuario y renderizado de componentes con dependencias reales.

```tsx
test('formulario envía datos correctamente', async () => {
  render(<MiFormulario />);
  await userEvent.type(screen.getByLabelText('Nombre'), 'David');
  await userEvent.click(screen.getByText('Enviar'));
  expect(await screen.findByText(/Gracias/)).toBeInTheDocument();
});
```

---

## 🧠 TypeScript avanzado en React

### Tipos explícitos de props

```tsx
type BotonProps = {
  texto: string;
  onClick: () => void;
};

function Boton({ texto, onClick }: BotonProps) {
  return <button onClick={onClick}>{texto}</button>;
}
```

### Composición con `React.FC` y `React.PropsWithChildren`

```tsx
const Layout: React.FC<React.PropsWithChildren> = ({ children }) => {
  return <div className="layout">{children}</div>;
};
```

### Tipado de formularios

```tsx
type FormData = {
  email: string;
  password: string;
};
```

---

## 📄 Manejo de formularios con React Hook Form

### Instalación

```bash
npm install react-hook-form
```

### Uso básico

```tsx
import { useForm } from "react-hook-form";

type Inputs = {
  nombre: string;
};

function Formulario() {
  const { register, handleSubmit, formState: { errors } } = useForm<Inputs>();

  const onSubmit = (data: Inputs) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("nombre", { required: true })} />
      {errors.nombre && <span>Este campo es requerido</span>}
      <button type="submit">Enviar</button>
    </form>
  );
}
```

---

## 🌍 Introducción al Server-Side Rendering con Next.js

### ¿Qué es SSR?

Renderizado de componentes en el servidor antes de enviarlos al navegador → mejor SEO y carga inicial más rápida.

### Crear proyecto Next.js

```bash
npx create-next-app@latest
```

### Páginas y rutas automáticas

```tsx
// pages/index.tsx
export default function Home() {
  return <h1>Inicio</h1>;
}
```

### SSR con `getServerSideProps`

```tsx
export async function getServerSideProps() {
  return {
    props: {
      mensaje: "Hola desde el servidor"
    }
  };
}
```

---

## 🔍 Pruebas E2E con Playwright o Cypress

### 📦 Playwright

```bash
npm install -D @playwright/test
npx playwright install
```

```ts
// tests/example.spec.ts
import { test, expect } from '@playwright/test';

test('título de la página', async ({ page }) => {
  await page.goto('http://localhost:5173');
  await expect(page).toHaveTitle(/React/);
});
```

### 📦 Cypress

```bash
npm install -D cypress
npx cypress open
```

```ts
describe('Mi App', () => {
  it('muestra la página principal', () => {
    cy.visit('http://localhost:5173');
    cy.contains('Bienvenido');
  });
});
```

---

## 🧪 Ejercicios propuestos

1. Crear pruebas unitarias para funciones de utilidad (formateo, cálculos).
2. Testear un formulario con React Hook Form + validaciones.
3. Crear una app en Next.js y renderizar datos con SSR.
4. Escribir pruebas E2E básicas con Cypress o Playwright.
5. Tipar un componente con múltiples props opcionales y funciones.

---

## 🏁 Cierre del Módulo

Con esta clase se completa el nivel intermedio-avanzado. Estás preparado para construir y mantener aplicaciones modernas, robustas y listas para producción con React.

---

## 🔜 Recomendaciones futuras

- Profundizar en Next.js (API Routes, ISR, SSR)
- TypeScript avanzado (utilizar `Record`, `Partial`, `Pick`, `Omit`)
- State Management avanzado: Zustand, Jotai, Recoil
- Testing avanzado: mocks de fetch, MSW, pruebas de accesibilidad
