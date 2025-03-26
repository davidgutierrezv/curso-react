# DOM (Document Object Model)

## ¿Qué es el DOM?

El DOM (Document Object Model) es una interfaz de programación para documentos HTML y XML. Representa la estructura del documento como un árbol de nodos, donde cada nodo es una parte del documento (elementos, atributos, texto, etc.).

## Estructura del DOM

El DOM organiza el documento en una estructura jerárquica de nodos. Los tipos de nodos más comunes son:

- **Elementos**: Representan las etiquetas HTML (por ejemplo, `<div>`, `<p>`, `<a>`).
- **Atributos**: Representan los atributos de los elementos (por ejemplo, `class`, `id`).
- **Texto**: Representa el contenido textual dentro de los elementos.

## Manipulación del DOM

El DOM permite a los desarrolladores manipular la estructura, estilo y contenido del documento de manera dinámica. Algunas operaciones comunes incluyen:

- **Acceder a elementos**: Usando métodos como `getElementById`, `getElementsByClassName`, `querySelector`, etc.
- **Modificar contenido**: Cambiar el texto o HTML interno de un elemento usando propiedades como `innerText` o `innerHTML`.
- **Modificar atributos**: Cambiar los atributos de un elemento usando métodos como `setAttribute` o propiedades como `className`.
- **Agregar o eliminar elementos**: Usar métodos como `appendChild`, `removeChild`, `insertBefore`, etc.

## Ejemplo de manipulación del DOM

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Manipulación del DOM</title>
</head>
<body>
  <div id="app">
    <p id="mensaje">Hola, mundo!</p>
    <button id="boton">Cambiar mensaje</button>
  </div>

  <script>
    const boton = document.getElementById('boton');
    const mensaje = document.getElementById('mensaje');

    boton.addEventListener('click', () => {
      mensaje.innerText = '¡Mensaje cambiado!';
    });
  </script>
</body>
</html>
```

En este ejemplo, se accede a los elementos del DOM usando `getElementById` y se modifica el contenido de un párrafo cuando se hace clic en un botón.

## Virtual DOM

El Virtual DOM es una técnica utilizada por bibliotecas como React para optimizar la manipulación del DOM. En lugar de realizar cambios directamente en el DOM real, React mantiene una copia en memoria (Virtual DOM) y realiza un "diffing" para determinar los cambios mínimos necesarios. Luego, aplica esos cambios al DOM real de manera eficiente.

## Beneficios del Virtual DOM

- **Rendimiento**: Minimiza las operaciones costosas en el DOM real.
- **Simplicidad**: Facilita la programación declarativa y basada en componentes.
- **Reactividad**: Permite actualizaciones eficientes y re-renderizados basados en cambios de estado.

Para más información sobre el Virtual DOM, consulta la sección correspondiente en la documentación de React.

