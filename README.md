# HTML5 y accesibilidad. Ejemplos de aplicación.
Este documento presenta un serie de ejemplos de código, referente a los temas expuestos en la presentación de "HTML5 y accesibilidad", la cual forma parte de un análisis e investigación sobre esta temática.

# Índice

1. [HTML Semántico](#id-1)  
2. [ARIA](#id-2)  
3. [Soportes para tablas](#id-3)  
4. [Soporte para multimedia (audio-video)](#id-4)

## 1. HTML Semántico<a name="id-1"></a>
Se presenta un código que no utiliza HTML semántico. Si no se utiliza HTML semántico la alternativa directa es el uso de la etiqueta \<div\>, lo cual no proporciona alguna información para tecnologías de asistencia (Ej: lector de pantalla).

~~~html
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>HTML5 y la accesibilidad</title>
</head>
<body>

  <!-- Encabezado -->
  <div id="header">
    <a href="/"><img src="logo.jpg" alt="Logo"></a>
  </div>

  <!-- Navegación principal -->
  <div id="navigation"> Menú de navegación: 
      <a href="/html-semantico">HTML Semántico</a>     
      <a href="/html-ARIA">ARIA</a>
      <a href="/soporte-tablas">Soporte Tablas</a>
      <a href="/soporte-audio-video">Soporte audio y video</a>
  </div>

  <!-- Contenido principal -->
  <div id="content">
    <div class="section">
      <div class="article">
        <h3>Novedades HTML</h3>
        <p><strong>Esto corresponde a un artículo sobre novedades en HTML</strong></p>
      </div>
    </div>
  </div>

  <!-- Barra lateral -->
  <div id="sidebar"> Menú lateral:
    <h4>Guías</h4>
    <ul><li>items</li></ul>

    <h4>Documentación</h4>
    <ul><li>items</li></ul>

    <h4>Códigos de ejemplo</h4>
    <ul><li>items</li></ul>
  </div>

  <!-- Pie de página -->
  <div id="footer">
    <div>Copyright © 2025</div>
    <div><a href="">Privacy Policy</a></div>
  </div>

</body>
</html>
~~~
<p style="font-size: 0.85em; font-style: italic; color: gray;">
Código 1. Ejemplo de documento sin HTML
</p>

Para mejorar la accesibilidad del documento, se utilizan los elementos semánticos proporcionados en HTML5. Así, las tecnologías de asistencia pueden realizar una correcta identificación de los diferentes elementos del documento
```html
<!doctype html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>HTML5 y la accesibilidad</title>
</head>
<body>
  <!-- Encabezado -->
  <header>
    <a href="/"><img src="logo.jpg" alt="Logo"></a>
  </header>

  <!-- Navegación principal -->
  <nav>
    <ul>
      <li><a href="/html-semantico">HTML Semántico</a></li>
      <li><a href="/html-ARIA">ARIA</a></li>
      <li><a href="/soporte-tablas">Soporte Tablas</a></li>
      <li><a href="/soporte-audio-video">Soporte audio y video</a></li>
    </ul>
  </nav>

  <!-- Contenido principal -->
  <main>
    <section>
      <article>
        <h3>Novedades HTML</h3>
        <p><strong>Esto corresponde a un artículo sobre novedades en HTML</strong></p>
      </article>
    </section>
  </main>

  <!-- Barra lateral -->
  <aside>
    <h4>Guías</h4>
    <ul><li>items</li></ul>

    <h4>Documentación</h4>
    <ul><li>items</li></ul>

    <h4>Códigos de ejemplo</h4>
    <ul><li>items</li></ul>
  </aside>

  <!-- Pie de página -->
  <footer>
    <div>Copyright © 2025</div>
    <div><a href="">Política de privacidad</a></div>
  </footer>

</body>
</html>
```
<p style="font-size: 0.85em; font-style: italic; color: gray;">
Código 2. Ejemplo de documento con HTML semántico
</p>

## 2. ARIA <a name="id-2"></a>
ARIA (Accessible Rich Internet Applications), a nivel de html presenta tres atributos o características
- **Roles**: Los roles indican el tipo del elemento en forma descriptiva
- **Estados**: Describe el estado dinámico de un elemento.
- **Propiedades**: Similar a los estados, pero aplica a expresar estados estáticos o que no cambian.

Un ejemplo aplicable de role es alert, debido a que no presenta un equivalente semántico en HTML nativo:
~~~html
<div role="alert" onclick="this.parentElement.style.display='none';">
  ¡Mensaje de alerta! Presione para eliminar este mensaje.
</div>
~~~
<p style="font-size: 0.85em; font-style: italic; color: gray;">
Código 3. ARIA roles, aplicación.
</p>


En cuanto a los estados y propiedades, un menú expandible permite aplicar ambos conceptos
~~~html
<button aria-expanded="false" aria-controls="contenido" id="expandedButton">
  Mostrar más
</button>

<div id="contenido" hidden>
  Contenido adicional al expandir
</div>

<script>
  const btn = document.getElementById('expandedButton');
  const content = document.getElementById('contenido');

  btn.addEventListener('click', () => {
    const expanded = btn.getAttribute('aria-expanded') === 'true';
    // Se cambia el estado ARIA
    btn.setAttribute('aria-expanded', String(!expanded));
    content.hidden = expanded;
  });
</script>
~~~
<p style="font-size: 0.85em; font-style: italic; color: gray;">
Código 4. ARIA propiedades y estados, aplicación.
</p>
En este último ejemplo, se utiliza el estado aria-expanded que indica la "apertura" del elemento. La propiedad aria-controls indica que el elemento tiene control sobre la presencia o contenido de otro elemento, en este caso el botón controla el div que se utiliza como "contenido".

## 3. Soportes para tablas <a name="id-3"></a>
HTML5 introdujo un soporte para tablas a través de diferentes etiquetas, permitiendo una mejora en la identificación de los elementos y una mejor organización para contenidos o información adicional, mejorando así la experiencia al utilizar tecnologías de asistencia. En adelante, se presenta una "tabla accesible" con las diferentes etiquetas y elementos de soporte.
~~~html
<h4>Tabla accesible</h4>
<table>
  <caption>
    <strong>Ejemplo de tabla accesible</strong>

    <!-- details proporciona información adicional que el usuario puede visualizar u ocultar>
    <details>
      
      <!-- summary se anuncia antes de que el lector de pantalla lea los datos mismos de la tabla. -->
      <summary>Se da una breve descripción de la tabla o alguna ayuda</summary>
    
    </details>
  </caption>
  <thead>
    <tr>
      <th>Título Columna 1</th>
      <th>Título Columna 2</th>
      <th>Título Columna 3</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Footer columna 1</td>
      <td>Footer columna 2</td>
      <td>Footer columna 3</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Dato columna 1</td>
      <td>Dato columna 2</td>
      <td>Dato columna 3</td>
    </tr>
  </tbody>
</table>
~~~
<p style="font-size: 0.85em; font-style: italic; color: gray;">
Código 5. Tabla accesible
</p>

## 4. Soporte para multimedia (audio-video) <a name="id-4"></a>
Como elementos principales para soporte multimedia se destacan los elementos \<audio> y \<video>.

~~~html
<audio controls>
  <source src="audio.mp3" type="audio/mp3" />
  <source src="audio.ogg" type="audio/ogg" />
  <p>
    Su navegador no es compatible con audio HTML5. Aquí hay un
    <a href="audio-alt.mp3">enlace al audio</a> en su lugar.
  </p>
</audio>

<video>
  poster="poster.png">
  <source src="video.mp4" type="video/mp4" />
  <source src="video.webm" type="video/webm" />
  <p>
    Su navegador no soporta vídeo HTML5. Este es un
    <a href="video-alt.mp4">enlace al vídeo</a> alternativo.
  </p>
</video>
~~~
Como puede observarse \<source> permite indicar múltiples fuentes en distintos formatos para la disponibilidad del navegador. Además el contenido interno (denominado fallback content) se muestra únicamente si el navegador no soporta el archivo multimedia. Finalmente el atributo controls permite incluir la interfaz de control del browser, o construir una personalizada a través de la "Api Javascript".

Otro elemento importante es \<track> que permite la inclusión de transcripción de audio/video a texto:

~~~html
<video controls>
  <source src="video.mp4" type="video/mp4" />
  <source src="video.webm" type="video/webm" />
  <track kind="subtitles" src="subtitles_en.vtt" srclang="en" />
</video>
~~~
<p style="font-size: 0.85em; font-style: italic; color: gray;">
Código 6. Elemento track, aplicación.
</p>

Tener en cuenta que \<track> debe colocarse dentro de \<audio> o \<video>, pero después de todos los elementos <source>. El atributo kind para especifica si las pistas son "subtítulos", " leyendas" o "descripciones". Además, srclang indica en qué idioma ha escrito los subtítulos.
