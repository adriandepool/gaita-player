# 🎶 Catálogo de Gaita Zuliana Digital

Este proyecto es un **catálogo interactivo de temas de Gaita Zuliana**, diseñado para funcionar completamente como un **sitio web estático** (HTML, CSS, JavaScript), sin necesidad de un servidor o base de datos tradicional.  
La gestión de los datos se realiza íntegramente a través de una **Hoja de Cálculo de Google Sheets**.

El diseño está optimizado para dispositivos móviles y emula la experiencia de usuario de aplicaciones de streaming de música (Spotify/YouTube Music), incluyendo una fila de reproducción persistente con soporte para **arrastrar y soltar temas**.

## Características Clave

- **Fuente de Datos sin Servidor:** Los datos se consumen directamente desde una URL pública de exportación CSV de Google Sheets.  
- **Búsqueda Robusta:** Búsqueda en tiempo real con normalización de texto (ignora tildes y acentos) y función de autocompletado para temas y agrupaciones.  
- **Filtros Avanzados:** Filtrado por Año y Ordenamiento por Agrupación, Tema y Año. Los controles de filtro se ocultan en móvil para optimizar el espacio.  
- **Reproductor Flotante Persistente:** Barra de reproducción fija en la parte inferior, que se mantiene visible durante la navegación.  
- **Fila de Reproducción Interactiva:** Permite agregar temas a la cola, reordenarlos mediante Drag and Drop y mantiene la lista guardada entre sesiones (localStorage).  
- **Descargas Directas:** Botones de descarga que fuerzan la descarga del archivo MP3 en lugar de solo reproducirlo en el navegador.  

## 🛠️ Configuración y Despliegue

El proyecto consta de un único archivo principal (`index.html`) que contiene todo el HTML, CSS (vía Tailwind CSS) y JavaScript.

### 1. Requisitos de la Fuente de Datos (Google Sheets)

Para que el sitio funcione, tu hoja de cálculo debe estar publicada como CSV y la primera fila (encabezados) debe contener exactamente las siguientes columnas:

- `ID`: Identificador único numérico (requerido para la persistencia).  
- `AGRUPACION`: Nombre de la agrupación.  
- `TEMA`: Título del tema.  
- `AÑO`: Año de lanzamiento (requerido para el filtro).  
- `AUTOR_CREDITO`, `LETRA`, `MUSICA`, `ARREGLO`: Créditos específicos.  
- `SOLISTA`, `SOLISTA_INVITADO`: Nombres de solistas.  
- `ENLACE_DESCARGA`: URL completa del archivo MP3 (ej: `https://.../tema.mp3`).  

**Pasos para la Publicación:**

1. Abre tu Hoja de Cálculo en Google Sheets.  
2. Ve a **Archivo > Compartir > Publicar en la web**.  
3. Asegúrate de que la hoja esté configurada para ser exportada como **Valores separados por comas (.csv)**.  
4. Copia la URL de exportación CSV generada.  

### 2. Librerías Externas Utilizadas

Este proyecto utiliza las siguientes librerías de terceros (cargadas vía CDN):

- **Tailwind CSS:** Framework CSS para estilos y diseño rápido.  
- **SortableJS:** Librería JavaScript ligera para la funcionalidad de arrastrar y soltar (Drag and Drop) en la Fila de Reproducción.  

### 3. Configuración de la URL de Datos

Debes actualizar la variable `GOOGLE_SHEETS_CSV_URL` dentro del archivo `index.html` con tu URL de CSV publicada:

`const GOOGLE_SHEETS_CSV_URL = 'TU_ENLACE_CSV_DE_GOOGLE_SHEETS_AQUÍ';`

## 4. Despliegue en GitHub Pages

1. Crea un nuevo repositorio en GitHub (ej: `gaitas-catalogo`).  
2. Sube el archivo `index.html` a la raíz del repositorio.  
3. Ve a la pestaña **Settings > Pages**.  
4. Configura la fuente de despliegue (**Source**) para que apunte a la rama principal (`main` o `master`).  

Una vez desplegado, el sitio estará en línea, cargando los datos directamente de Google Sheets.

## 🧑‍💻 Gestión y Mantenimiento

- **Actualización de Datos:** Cada vez que edites tu Hoja de Cálculo de Google Sheets, los cambios se reflejarán automáticamente en el sitio web (puede tardar unos minutos debido al caché de Google). No necesitas editar el código HTML.  
- **Archivos MP3:** Asegúrate de que todos los archivos MP3 estén alojados en la URL base correcta (ej: `https://www.islagaitera.com/` o tu servidor real), ya que el sitio usa la ruta absoluta para la reproducción y descarga.  
- **Fila de Reproducción:** La fila (playlist) se guarda en el `localStorage` del navegador del usuario. Si un usuario borra su caché local, la fila se reiniciará.  

## Licencia

Este proyecto está bajo la **Licencia MIT**.  
Eres libre de usar, copiar, modificar, fusionar, publicar, distribuir, sublicenciar y/o vender copias del código fuente siempre y cuando incluyas el aviso de copyright y los permisos incluidos en la licencia.

**Descargo de Responsabilidad sobre el Contenido:**  
Los datos contenidos en la Hoja de Cálculo (títulos de temas, agrupaciones y enlaces de descarga) y los archivos de audio MP3 correspondientes no están cubiertos por esta licencia de código, y su uso está sujeto a los derechos de autor de sus respectivos creadores y/o propietarios.
