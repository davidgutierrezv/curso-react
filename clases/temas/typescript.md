# TypeScript

TypeScript es un superset de JavaScript que añade tipado estático y otras características avanzadas.

## Ventajas

- Detecta errores en tiempo de desarrollo.
- Mejora la mantenibilidad del código.
- Soporte para las últimas características de JavaScript.

## Configuración

TypeScript se configura mediante un archivo `tsconfig.json`. Ejemplo básico:

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

## Integración con Vite

Vite soporta TypeScript de forma nativa y utiliza `tsconfig.json` para la configuración del compilador.
