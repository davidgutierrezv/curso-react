# Babel

Babel es un transpilador de JavaScript que permite usar características modernas de JavaScript en navegadores antiguos.

## Características principales

- Transpila código ES6+ a ES5.
- Soporta JSX, TypeScript y más.
- Extensible mediante plugins y presets.

## Uso en proyectos

Babel se configura mediante un archivo `.babelrc` o `babel.config.js`. Ejemplo básico:

```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

## Integración con Vite

Vite utiliza Babel para transpilar JSX y otras características modernas de JavaScript.
