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

# Análisis de Código

## 1. Código para mostrar un mensaje al hacer clic en un botón

```html
<button id="btn">Haz clic</button>
<p id="mensaje"></p>

<script>
  document.getElementById("btn").addEventListener("click", () => {
    document.getElementById("mensaje").textContent = "¡Botón presionado!";
  });
</script>

Preguntas:

¿Qué hace el código?

El código agrega un "event listener" (escuchador de eventos) al botón con el id btn. Cuando el usuario hace clic en este botón, se cambia el contenido del elemento <p> con el id mensaje, actualizándolo con el texto "¡Botón presionado!".

¿Qué pasaría si cambiamos textContent por innerHTML?

Si cambiamos textContent por innerHTML, el comportamiento sigue siendo el mismo en este caso, ya que solo estamos asignando texto al elemento <p>. Sin embargo, innerHTML permite interpretar y renderizar código HTML dentro del contenido, lo que podría ser útil si en el futuro quieres insertar elementos HTML (como enlaces o imágenes) en lugar de solo texto. Por ejemplo:

javascript
Copiar
Editar
document.getElementById("mensaje").innerHTML = "<b>¡Botón presionado!</b>";
Esto mostraría el mensaje en negrita, pero también podría ser un riesgo de seguridad si no se controla adecuadamente el contenido, ya que permitiría la inyección de HTML malicioso (por ejemplo, JavaScript).

¿Qué ocurre si se presiona el botón múltiples veces?

Cada vez que el botón es presionado, el mensaje se actualizará a "¡Botón presionado!". No se acumulan los mensajes, solo se reemplaza el contenido dentro del <p>.

2. Código para agregar usuarios a una lista con un formulario
html
Copiar
Editar
<form id="form-usuario">
  <input type="text" id="nombre" placeholder="Nombre">
  <button type="submit">Guardar</button>
</form>
<ul id="lista-usuarios"></ul>

<script>
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
</script>
Preguntas:

¿Qué hace el código al enviar el formulario?

Al enviar el formulario, se captura el valor que el usuario ingresa en el campo de texto con el id nombre. Este valor (el nombre) se agrega al array usuarios. Luego, se llama a la función actualizarListaUsuarios, que actualiza el contenido de la lista <ul> con los nombres de los usuarios almacenados en el array.

¿Por qué es importante la línea e.preventDefault()?

La línea e.preventDefault() se utiliza para evitar que el formulario se envíe de la manera tradicional, lo que provocaría que la página se recargara. Al evitar este comportamiento predeterminado, podemos manejar el envío del formulario de manera personalizada, permitiendo agregar el nombre al array y actualizar la lista sin recargar la página.

¿Cómo se simula la "persistencia de datos" aquí?

En este caso, la persistencia de datos se simula utilizando un array (usuarios) que almacena los nombres de los usuarios en memoria. Sin embargo, esta "persistencia" solo se mantiene mientras la página esté abierta. Si recargas la página, el array se perderá porque no se está utilizando una base de datos o almacenamiento persistente como LocalStorage, archivos, o bases de datos reales.

Si quisieras simular persistencia de datos de manera más duradera, podrías usar localStorage para guardar los datos en el navegador entre sesiones.

¿Qué pasa si el usuario deja el campo de nombre vacío?

Si el campo nombre está vacío y se envía el formulario, el valor vacío será agregado al array usuarios, lo cual puede causar que se muestre un usuario vacío en la lista. Para evitar esto, se podrían agregar validaciones que verifiquen que el campo no esté vacío antes de permitir que se agregue un nuevo usuario.

¿Es posible eliminar un usuario de la lista?

El código actual no incluye una funcionalidad para eliminar usuarios, pero se podría agregar un botón de "Eliminar" junto a cada usuario, y un manejador de eventos para eliminar al usuario de la lista cuando se haga clic en dicho botón. Esto se puede hacer modificando el array y actualizando la lista después de la eliminación.

3. Código para contar caracteres en un textarea
html
Copiar
Editar
<textarea id="textarea" placeholder="Escribe algo..."></textarea>
<p id="contador">Caracteres: 0</p>

<script>
  document.getElementById("textarea").addEventListener("input", (e) => {
    const texto = e.target.value;
    const contador = document.getElementById("contador");
    contador.textContent = `Caracteres: ${texto.length}`;
  });
</script>
Preguntas:

¿Qué hace el código?

El código agrega un evento de "input" al área de texto (textarea). Cada vez que el usuario escribe o borra algo en el campo, el código actualiza el contador de caracteres en el elemento <p> con el id contador.

¿Qué sucedería si se usara keyUp en lugar de input?

Usar keyUp desencadenaría el evento solo después de que la tecla haya sido soltada. Sin embargo, input se activa en tiempo real mientras se escribe, lo que permite una actualización instantánea del contador de caracteres. Por lo tanto, con input el contador se actualiza más rápidamente.

¿Cómo se podría modificar el código para contar las palabras en lugar de los caracteres?

Para contar las palabras en lugar de los caracteres, se podría modificar el código para dividir el texto en palabras utilizando el método split() y luego contar cuántas palabras hay. Ejemplo:

javascript
Copiar
Editar
const palabras = texto.trim().split(/\s+/).filter(Boolean);
contador.textContent = `Palabras: ${palabras.length}`;
r
Copiar
Editar

Con este formato, al pegarlo en tu archivo `README.md`, las preguntas se mostrarán correctamente dentro de cada sección de código. ¡Listo para usar!







