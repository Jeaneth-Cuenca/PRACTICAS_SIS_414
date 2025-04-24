# Práctica: Teoría DOM y Formularios en JavaScript

## 1. Parte Teórica

### a) ¿Qué es el DOM y cómo se relaciona con HTML?

El **DOM** (Document Object Model) es una representación en forma de árbol de todos los elementos que conforman una página web. Cada etiqueta, atributo o texto se convierte en un nodo que puede ser accedido y modificado mediante JavaScript. Gracias al DOM, podemos interactuar dinámicamente con la página sin tener que recargarla. Esta estructura está directamente relacionada con el HTML, ya que es generado a partir de la estructura HTML de la página.

---

### b) Diferencias entre:

#### `document.getElementById()` vs `document.querySelector()`

- **`document.getElementById()`**: Permite seleccionar un único elemento mediante su atributo `id`. Es un método más específico, pero solo funciona con IDs.
- **`document.querySelector()`**: Permite seleccionar cualquier elemento usando selectores CSS, lo que lo hace más versátil. Se puede usar con IDs, clases, etiquetas, combinaciones de selectores, etc.

#### `textContent` vs `innerHTML`

- **`textContent`**: Retorna o establece solo el texto de un elemento, sin interpretar etiquetas HTML. Es útil cuando solo necesitamos trabajar con texto plano.
- **`innerHTML`**: Retorna o establece el contenido HTML de un elemento, lo que permite incluir etiquetas HTML, como `<b>`, `<i>`, etc.

---

### c) ¿Para qué sirve `addEventListener()`?

`addEventListener()` se utiliza para asociar un manejador de eventos a un elemento del DOM, permitiendo que el código reaccione a eventos como clics, teclas presionadas o cambios en un formulario. Esto es esencial para hacer que las páginas web sean interactivas.

---

### d) ¿Qué métodos del DOM se usan para capturar valores de un formulario?

Para obtener los valores de los campos de un formulario, podemos usar el método `.value` de un elemento, como `getElementById()` o `querySelector()`.

---

### e) ¿Cómo prevenir el envío por defecto de un formulario con JavaScript?

Para evitar que un formulario se envíe de forma predeterminada (lo que recargaría la página), se utiliza el método `preventDefault()` dentro del evento `submit`.

---

### f) ¿Qué es el almacenamiento en memoria y en qué se diferencia de `localStorage`?

- **Almacenamiento en memoria**: Se refiere a los datos guardados temporalmente durante la vida útil de la página (en variables o estructuras de datos como arrays). Estos datos se pierden cuando la página se recarga o se cierra el navegador.
- **`localStorage`**: Permite almacenar datos de manera persistente en el navegador, incluso después de que se cierre o recargue la página. Los datos se conservan hasta que se eliminen explícitamente.

---

## 2. Análisis de Código

### Código:

```html
<button id="btn">Haz clic</button>
<p id="mensaje"></p>
