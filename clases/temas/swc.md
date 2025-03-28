# SWC

SWC (Speedy Web Compiler) es un compilador de JavaScript escrito en Rust, diseñado para ser extremadamente rápido.

## Características principales

- Transpilación rápida de ES6+ a ES5.
- Soporte para JSX y TypeScript.
- Compilación paralela gracias a Rust.

## Uso en proyectos

SWC se configura mediante un archivo `.swcrc`. Ejemplo básico:

```json
{
  "jsc": {
    "parser": {
      "syntax": "typescript",
      "tsx": true
    },
    "transform": {
      "react": {
        "runtime": "automatic"
      }
    }
  }
}
```

## Integración con Vite

Vite puede utilizar SWC para la transpilación rápida de código, mejorando los tiempos de desarrollo y build.
