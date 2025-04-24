## 1. Preguntas Conceptuales

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

# Análisis de Código JavaScript

## 1. Primer Bloque de Código

### HTML
```html
<button id="btn">Haz clic</button>
<p id="mensaje"></p>
```

### JavaScript
```javascript
document.getElementById("btn").addEventListener("click", () => {
  document.getElementById("mensaje").textContent = "¡Botón presionado!";
});
```

### ¿Qué hace el código?
Este código implementa una interacción simple:
- Crea un botón con el texto "Haz clic" y un párrafo vacío
- Cuando el usuario hace clic en el botón, se ejecuta una función que cambia el texto del párrafo a "¡Botón presionado!"
- Utiliza `addEventListener` para registrar el evento de clic y una función flecha para manejar la respuesta

### ¿Qué pasaría si cambiamos `textContent` por `innerHTML`?
Si cambiamos `textContent` por `innerHTML`:
- El resultado sería visualmente igual en este caso específico (mostrar "¡Botón presionado!")
- La diferencia clave es que `innerHTML` interpreta el contenido como HTML, mientras que `textContent` lo trata como texto plano
- `innerHTML` podría representar un riesgo de seguridad (vulnerabilidad XSS) si el contenido proviene de entrada de usuario, ya que permitiría inyectar y ejecutar código HTML y JavaScript
- `textContent` es generalmente más seguro y más eficiente cuando solo se necesita mostrar texto

## 2. Segundo Bloque de Código

### HTML
```html
<form id="form-usuario">
  <input type="text" id="nombre" placeholder="Nombre">
  <button type="submit">Guardar</button>
</form>
<ul id="lista-usuarios"></ul>
```

### JavaScript
```javascript
const usuarios = []; // Array para simular persistencia

document.getElementById("form-usuario").addEventListener("submit", (e) => {
  e.preventDefault(); // ¿Por qué es importante esta línea?
  const nombre = document.getElementById("nombre").value;
  usuarios.push(nombre); // Almacena en memoria
  actualizarListaUsuarios();
});

function actualizarListaUsuarios() {
  const lista = document.getElementById("lista-usuarios");
  lista.innerHTML = usuarios.map(user => `<li>${user}</li>`).join("");
}
```

### ¿Qué hace el código al enviar el formulario?
Cuando se envía el formulario:
1. Previene el comportamiento predeterminado del formulario con `e.preventDefault()` (esto evita que la página se recargue)
2. Obtiene el valor ingresado en el campo de texto
3. Agrega este valor al array `usuarios`
4. Llama a la función `actualizarListaUsuarios()` que actualiza la interfaz de usuario

La línea `e.preventDefault()` es importante porque:
- Por defecto, al enviar un formulario HTML se recarga la página y/o se envían los datos a un servidor
- Al prevenir este comportamiento, podemos manejar el envío del formulario con JavaScript sin perder el estado actual de la aplicación ni recargar la página

### ¿Cómo se simula la "persistencia de datos" aquí?
La persistencia de datos se simula mediante:
- Un array llamado `usuarios` que almacena los nombres ingresados
- Este array mantiene los datos solo durante la sesión actual del navegador (memoria RAM)
- No es una persistencia real ya que los datos se perderán cuando:
  - Se recargue la página
  - Se cierre la pestaña o el navegador
  
Para una verdadera persistencia, habría que utilizar tecnologías como:
- localStorage/sessionStorage para almacenamiento en el navegador
- Una base de datos (con backend) para almacenamiento permanente
- Servicios de almacenamiento en la nube