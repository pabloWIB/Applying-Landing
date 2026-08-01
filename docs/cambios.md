# Registro de cambios

Reorganización completa del proyecto, 2026-07-30. Agrupado por fase.
Ningún comando de git se ejecutó: todos los cambios son locales.

---

## Fase 1 — Auditoría

- Inventario completo en `docs/auditoria.md`: 21 archivos catalogados (1 HTML, 1 CSS, 7 imágenes, 13 archivos de tipografía).
- Verificadas todas las rutas `href` y `src`: ninguna estaba rota.
- Identificadas 3 imágenes huérfanas y 10 archivos de fuente que ningún `@font-face` cargaba.
- **Hallazgo principal**: las 6 fotografías eran material promocional de terceros con marca de agua de `heytype.xyz` / `@Jazheiman` para la tipografía comercial *HappyFatFont*, sin relación con el contenido del sitio.
- Búsqueda de credenciales (`api_key`, `secret`, `token`, `password`, `bearer`, `AKIA`, `sk_live`, `ghp_`): cero coincidencias.
- Medición del estado responsive de partida en 360 / 768 / 1024 / 1440 px.

## Fase 2 — Estructura

- Creadas `assets/css/`, `assets/fonts/`, `assets/img/` y `docs/`.
- `Fonts/` → `assets/fonts/`, con nombres normalizados a minúsculas y guiones:
  - `Cinzel-VariableFont_wght.ttf` → `cinzel-variable.ttf`
  - `DancingScript-Regular.ttf` → `dancing-script-regular.ttf`
  - `OFL.txt` → `ofl.txt`
- `estilos.css` → dividido en `assets/css/base.css`, `layout.css` y `components.css`.
- Eliminada la carpeta `IMG/`.
- Añadidos `404.html`, `robots.txt`, `sitemap.xml` y `.gitignore` en la raíz.
- Todas las rutas de `<link>` e `icon` actualizadas y verificadas una a una contra disco y contra servidor HTTP.

## Fase 3 — Higiene

- **Eliminadas las 6 imágenes de terceros** (`274645148…`, `274681384…`, `274727860…`, `274803902…`, `274822028…`, `274879844…`): material promocional ajeno con marca de agua visible.
- **Eliminado `IMG/Applying.png`**: 1024×1024 y 298 KB para renderizarse a 16 px, con una paleta azul y verde que no guarda relación con la identidad en blanco y negro del sitio.
- **Eliminados 9 archivos de tipografía sin uso**: las seis estáticas de Cinzel (`Regular`, `Medium`, `SemiBold`, `Bold`, `ExtraBold`, `Black`) y tres de Dancing Script (`Medium`, `SemiBold`, `Bold`). Ninguna estaba declarada en el CSS. La variable de Cinzel cubre el rango 400–900 en un solo archivo.
- Eliminado `Fonts/README.txt`: notas de instalación de Google Fonts, irrelevantes en un repositorio web. Se conserva `ofl.txt`, que es la licencia y debe acompañar a los archivos.
- Creado `.gitignore` para stack estático: `node_modules/`, `.env`, `*.log`, `.DS_Store`, `Thumbs.db`, `desktop.ini`, carpetas de editor.
- Formato normalizado en todos los archivos: indentación de 2 espacios, comillas dobles en HTML, punto y coma en CSS, salto de línea final.

## Fase 4 — Imágenes

- El proyecto se queda **sin imágenes de mapa de bits**. No se inventaron ni se descargaron sustitutas.
- Creado `assets/img/favicon.svg`, generado a mano a partir del propio motivo del sitio: un anillo blanco con punto central sobre negro. 226 bytes frente a los 298 KB del PNG anterior, y nítido a cualquier tamaño.
- Los puntos 4.1 a 4.6 (WebP, redimensionado, `width`/`height`, `loading="lazy"`, `alt`) no aplican: no queda ningún `<img>` en el proyecto.

## Fase 5 — HTML, SEO y accesibilidad

- Estructura semántica real: `<header>`, `<main>`, `<footer>`, un solo `<h1>` por página y jerarquía de encabezados sin saltos.
- El `<h1>` pasa de ser la marca a ser la afirmación de la página, que es su contenido real.
- Eliminado el `<aside>` que contenía un `<nav>` sin un solo enlace.
- **Eliminado el menú de navegación** (`Menu`, `Información`, `Sobre Nosotros`): anunciaba tres secciones que no existen y no había contenido real con el que crearlas.
- `lang` corregido de `es` a `en`: todo el texto de cuerpo está en inglés.
- Viewport corregido. Se eliminan `user-scalable=no`, `minimun-scale` y `maximun-scale` (las dos últimas mal escritas, y la primera bloquea el zoom con pinza: WCAG 1.4.4).
- `<head>` completo en las dos páginas: `title` y `description` únicos y dentro de rango, canonical, Open Graph (`og:type`, `og:url`, `og:title`, `og:description`, `og:site_name`, `og:locale`) y favicon.
- **Sin `og:image`**: no existe ningún archivo de imagen real para esa etiqueta y no se inventa la ruta.
- `noindex, follow` en `404.html`.
- Añadido enlace «Skip to content» como primer elemento focalizable.
- Foco visible global mediante `:focus-visible`, con contorno de 2 px y separación de 4 px.
- Creados `robots.txt` y `sitemap.xml` con la URL real del sitio, `https://applyiing.wib.digital/`.
- Añadido `prefers-reduced-motion` para desactivar las animaciones.

## Fase 6 — CSS y sistema de diseño

- Paleta derivada de la que el sitio ya usaba (negro y blanco puros). Se añaden dos grises calculados para jerarquizar sin bajar del ratio 4.5:1.
- 28 variables en `:root`: color, tipografía, espaciado, layout, bordes y movimiento.
- Escala de espaciado 4 / 8 / 16 / 24 / 32 / 48 / 64 / 96 px. Eliminados todos los números mágicos (`top: -2.4%`, `left: 31%`, `right: -26%`, `translate(71.3px, -14px)`…).
- Escala tipográfica fluida con `clamp()`.
- Corregido `transition: 0.3` (sin unidad, declaración inválida que el navegador descartaba) en las dos reglas donde aparecía.
- Eliminados los seis `;;` duplicados.
- **Los siete bloques `@keyframes` casi idénticos (`mover2`–`mover7`) se reducen a uno solo**, `orbit-breathe`, parametrizado con una propiedad personalizada `--angle` por círculo.
- Las siete reglas `.cajita`–`.cajita7` se reducen a una clase `.orbit__circle` más un modificador.
- Sustituido el layout basado en `position: fixed` y porcentajes por una rejilla CSS de tres filas.
- Añadidos reset y `box-sizing: border-box`, que no existían.
- Estilos movidos de `html` a `body`.
- Nomenclatura de clases normalizada a BEM en minúsculas.
- Orden dentro de cada archivo: variables → reset → base → layout → componentes → utilidades → media queries.

## Fase 7 — Responsive

- Reescrito mobile-first. Media queries con `min-width` en 768 y 1024 px.
- Verificado con medición real del DOM en 360, 480, 768, 1024 y 1440 px.
- **Corregido un desbordamiento horizontal real detectado en la verificación**: el anillo decorativo medía 860 px en un viewport de 768 px. Resuelto con `overflow: clip` en `.hero` y un tope de `94vw` en el tamaño del anillo.
- `scrollWidth > innerWidth` es `false` en los cinco anchos medidos.
- **Corregidas dos áreas táctiles por debajo del mínimo**: la marca (76×28 px) y el enlace de salto (162×39 px) pasan a 44 px de alto. El CTA ya cumplía, con 228×44 px.
- No se implementa menú móvil porque no hay menú: la navegación de relleno se eliminó en la fase 5.

## Fase 8 — UX / UI

- Jerarquía clara: afirmación, desarrollo y una sola acción.
- **El botón APPLY tenía un problema grave**: la animación `crecerbut` llevaba el color del texto a `black` sobre fondo `black`, dejando el CTA invisible durante la mitad de cada ciclo de 5 s. Animación eliminada.
- El botón, que no hacía nada, pasa a ser un enlace real a `https://wib.digital`, con el texto «See the work», que describe su destino de verdad.
- Estados completos en los elementos interactivos: reposo, hover, focus y active, con transiciones de 150–220 ms.
- Ancho de línea limitado a 68 caracteres.
- El párrafo original se divide en dos, sin cambiar una sola palabra.
- Sin formularios: no había ninguno y no se añade uno que no esté conectado a nada.
- Sin gradientes ni sombras. El anillo se rebaja a un 13 % de opacidad para que funcione como fondo y no compita con el texto.

## Fase 9 — JavaScript

- El proyecto no tenía JavaScript y sigue sin tenerlo. No se crea `main.js` vacío: sería un archivo de relleno.
- Todo el comportamiento (animación, foco, responsive, movimiento reducido) se resuelve en CSS.
- Cero errores y cero avisos en consola en las dos páginas.

## Fase 10 — Rendimiento

- Peso de la primera carga: **215 KB**, frente a los ~630 KB anteriores.
- Peso total del repositorio sin `.git`: de ~1,9 MB a ~250 KB.
- `font-display: swap` en las dos familias, que evita el FOIT que había antes.
- Sin `preconnect`: las fuentes son locales y no hay ningún origen externo al que conectarse.
- **Se retiró un `<link rel="preload">` de la fuente**: el atributo `crossorigin` que el preload de fuentes exige provoca un fallo de CORS al abrir el archivo con `file://`, y el requisito es que el sitio funcione también así, sin errores de consola. La fuente se descubre igualmente pronto porque `base.css` es la primera hoja de estilo.
- Sin scripts, luego no aplica `defer`. Sin librerías. Sin peticiones a terceros.

## Fase 11 — QA

Verificado sobre servidor HTTP local y también abriendo los archivos directamente:

- Los 10 recursos referenciados responden 200.
- Cero mensajes en consola en `index.html` y en `404.html`.
- Sin scroll horizontal en 360, 480, 768, 1024 y 1440 px.
- Los 4 elementos focalizables se alcanzan por teclado en orden y muestran foco visible.
- El enlace del 404 devuelve al inicio; comprobado navegando con teclado.
- Contraste medido: 21:1 el texto blanco, 8,63:1 el texto secundario, 21:1 el botón en hover. Mínimo exigido: 4,5:1.
- Ni un `href="#"`, ni un enlace vacío, ni una imagen rota, ni texto de plantilla.
- `title` y `description` únicos y dentro de rango en las dos páginas.
- Sin rutas absolutas de la máquina local.

## Fase 12 — Documentación

- `docs/auditoria.md` — inventario y hallazgos del estado de partida.
- `docs/cambios.md` — este archivo.
- `README.md` reescrito. El anterior describía un proyecto que no coincidía con el código: atribuía a Cinzel un uso que no tenía, afirmaba que los ítems del menú eran anclas cuando eran `<li>` de texto plano, daba el contenido por escrito en español cuando está en inglés, presentaba las seis estáticas de Cinzel como *fallback* de un `@font-face` inexistente e incluía un bloque de código CSS que no estaba en el archivo.

## Fase 13 — Deploy

- Verificado abriendo `index.html` directamente y sobre servidor local.
- Sin rutas absolutas de la máquina. Todas las rutas internas son relativas y en minúsculas.
- No se creó configuración de hosting: no se indicó destino.
- No se ejecutó ningún despliegue.
