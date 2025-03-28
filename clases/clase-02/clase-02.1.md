
# JavaScript Avanzado – Funciones de Manipulación de Arrays y Objetos

## 🎯 Objetivo

Comprender a profundidad funciones modernas de JavaScript para el manejo de arrays y objetos: `map`, `filter`, `reduce`, `find`, `some`, `every`, junto con el uso del **spread operator** (`...`) para crear y modificar estructuras de datos de forma inmutable y segura.

---

## 🔁 `map()`

- Transforma cada elemento de un array y devuelve un nuevo array.

```js
const numeros = [1, 2, 3];
const dobles = numeros.map(n => n * 2); // [2, 4, 6]
```

---

## 🔍 `filter()`

- Filtra elementos que cumplen una condición y devuelve un nuevo array.

```js
const numeros = [1, 2, 3, 4];
const pares = numeros.filter(n => n % 2 === 0); // [2, 4]
```

---

## ➕ `reduce()`

- Acumula valores y devuelve un único resultado.

```js
const numeros = [1, 2, 3, 4];
const suma = numeros.reduce((acum, valor) => acum + valor, 0); // 10
```

---

## 🔎 `find()`

- Devuelve el **primer** elemento que cumple la condición (o `undefined`).

```js
const usuarios = [{ id: 1 }, { id: 2 }];
const user = usuarios.find(u => u.id === 2); // { id: 2 }
```

---

## ❓ `some()` y `every()`

- `some()` → Al menos uno cumple la condición.
- `every()` → Todos cumplen la condición.

```js
[1, 2, 3].some(n => n > 2);  // true
[1, 2, 3].every(n => n > 0); // true
```

---

## 🧱 Manejo de Objetos y Arrays

### Agregar elementos a un array (sin mutar)

```js
const frutas = ['manzana', 'pera'];
const nuevas = [...frutas, 'plátano']; // ['manzana', 'pera', 'plátano']
```

---

### Modificar un objeto (sin mutar)

```js
const persona = { nombre: 'Renata', edad: 8 };
const nuevaPersona = { ...persona, edad: 9 }; // edad modificada
```

---

### Agregar propiedad a un objeto

```js
const usuario = { nombre: 'David' };
const conEmail = { ...usuario, email: 'david@example.com' };
```

---

## ✨ Spread Operator (`...`)

Sí, el **spread operator** es una característica de **JavaScript**, introducida en ES6.

- Sirve para clonar arrays y objetos, y para fusionarlos o modificarlos de forma **inmutable**.

```js
const arr1 = [1, 2];
const arr2 = [...arr1, 3]; // [1, 2, 3]

const obj1 = { a: 1 };
const obj2 = { ...obj1, b: 2 }; // { a: 1, b: 2 }
```

---

## 🔄 Ejemplo combinado

```js
const productos = [
  { id: 1, nombre: 'lápiz', stock: 10 },
  { id: 2, nombre: 'cuaderno', stock: 5 },
];

// Aumentar stock del producto con id 2
const nuevos = productos.map(p =>
  p.id === 2 ? { ...p, stock: p.stock + 1 } : p
);
```

---

## 🧪 Ejercicios

1. Usar `map()` para convertir un array de nombres a mayúsculas.
2. Filtrar productos con stock > 5.
3. Sumar el stock total con `reduce()`.
4. Agregar una nueva propiedad `activo: true` a cada producto con `map()` + spread.
5. Clonar un objeto y modificar su campo sin cambiar el original.

---

## 🏁 Conclusión

Estas funciones son fundamentales para trabajar con datos en React y JavaScript moderno. El spread operator permite modificar estructuras de forma segura, evitando mutaciones accidentales.
