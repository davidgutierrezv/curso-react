# esbuild

esbuild es un bundler y transpilador de JavaScript extremadamente rápido, escrito en Go.

## Características principales

- **Velocidad**: esbuild es conocido por su velocidad, siendo capaz de realizar bundling y transpilación en una fracción del tiempo que toman otras herramientas.
- **Soporte para ES6+**: esbuild soporta las últimas características de JavaScript, incluyendo ES6, ES7, y más.
- **Soporte para JSX y TypeScript**: esbuild puede transpilar JSX y TypeScript sin necesidad de configuraciones adicionales complejas.
- **Minificación**: esbuild incluye capacidades de minificación para reducir el tamaño de los archivos de salida.

## Uso en proyectos

esbuild se puede configurar mediante un archivo de configuración o directamente en la línea de comandos. Ejemplo básico de configuración:

```javascript
const esbuild = require('esbuild');

esbuild.build({
  entryPoints: ['src/main.tsx'],
  bundle: true,
  outfile: 'dist/bundle.js',
  platform: 'browser',
  jsxFactory: 'React.createElement',
  jsxFragment: 'React.Fragment',
}).catch(() => process.exit(1));
```

## Integración con Vite

Vite utiliza esbuild para la transpilación y bundling en modo desarrollo, lo que contribuye a su velocidad y eficiencia. esbuild permite a Vite realizar recargas instantáneas y servir módulos nativos sin necesidad de un bundling completo en desarrollo.
