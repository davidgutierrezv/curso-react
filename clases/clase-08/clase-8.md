
# Curso de React Básico – Clase 8

## 🎯 Objetivo de la Clase

Aprender a desplegar aplicaciones React en producción utilizando plataformas como Vercel, Netlify y GitHub Pages. Manejar variables de entorno y configurar un flujo básico de CI/CD con GitHub Actions.

---

## 🚀 Deploy de aplicaciones React

### 📦 ¿Qué se necesita?

- Una app React terminada (`npm run build`)
- Cuenta en GitHub (para hosting gratuito y CI/CD)
- Cuenta en Vercel, Netlify o GitHub Pages

---

## 🌐 Opción 1: Despliegue en **Vercel**

### Pasos:

1. Crear cuenta en [https://vercel.com](https://vercel.com)
2. Conectar tu repositorio de GitHub
3. Seleccionar framework: **React (Vite)**
4. Vercel detecta `vite.config.ts` y ejecuta:
   - `npm install`
   - `npm run build`
5. El sitio se publica automáticamente

### Ventajas:

- Soporte para SSR y funciones backend (opcional)
- Variables de entorno desde dashboard
- Despliegue automático en cada push

---

## 🕸️ Opción 2: Despliegue en **Netlify**

### Pasos:

1. Crear cuenta en [https://netlify.com](https://netlify.com)
2. Conectar repositorio de GitHub
3. Configurar:
   - Build Command: `npm run build`
   - Publish Directory: `dist`
4. Netlify deploya automáticamente

### Extra:

- Se puede usar `netlify.toml` para configuración avanzada

```toml
[build]
  command = "npm run build"
  publish = "dist"
```

---

## 📜 Opción 3: GitHub Pages (para sitios estáticos)

### Instalación

```bash
npm install gh-pages --save-dev
```

### Configuración en `package.json`

```json
"homepage": "https://<usuario>.github.io/<repositorio>",
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d dist"
}
```

### Comandos

```bash
npm run deploy
```

---

## 🔐 Variables de entorno

React soporta variables de entorno que comienzan con `VITE_` (si usas Vite).

### Ejemplo en `.env`

```
VITE_API_URL=https://api.ejemplo.com
```

### Acceso en código

```ts
const apiUrl = import.meta.env.VITE_API_URL;
```

> **No incluir tokens secretos aquí**: serán visibles desde el navegador.

---

## ⚙️ CI/CD básico con GitHub Actions

### Crear archivo `.github/workflows/deploy.yml`

```yaml
name: Build and Deploy

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'

      - run: npm install
      - run: npm run build

      # Ejemplo: subir archivos de /dist a GitHub Pages o S3
```

> Puedes integrar Vercel o Netlify con GitHub para hacer deploy automático sin configurar Actions.

---

## 🧪 Ejercicios propuestos

1. Subir un proyecto a GitHub y desplegar en Vercel.
2. Hacer deploy de una versión alternativa en Netlify.
3. Agregar una variable de entorno `VITE_NOMBRE` y mostrarla en la app.
4. Crear un workflow de GitHub Actions que haga `build` en cada push.
5. (Avanzado) Configurar `gh-pages` para despliegue manual.

---

## 🎓 Cierre del curso

¡Felicidades por llegar hasta aquí! Ahora tienes una base sólida para construir y escalar aplicaciones modernas con React.

---

## 🔜 Próximos pasos sugeridos

- Profundizar en testing (unitarios e integración)
- Aprender TypeScript más avanzado
- Manejo de formularios con React Hook Form
- Server-side rendering con Next.js
- Pruebas E2E con Playwright o Cypress
