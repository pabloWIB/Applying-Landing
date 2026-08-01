# Auditoría — Applyiing

Estado del proyecto **antes** de la reorganización.
Fecha de auditoría: 2026-07-30. Documento de trabajo interno.

---

## 1. Inventario de archivos

### 1.1 HTML

| Archivo | `<title>` | `<h1>` | Propósito real | Estado |
|---|---|---|---|---|
| `index.html` | `Apply` | `Applyiing` | Landing de una sola pantalla: un manifiesto sobre aplicar el conocimiento | Único HTML del proyecto |

No existe `404.html`. No existe ninguna otra página, pese a que el menú anuncia tres secciones.

### 1.2 CSS y JS

| Archivo | Cargado por | Tamaño | Estado |
|---|---|---|---|
| `estilos.css` | `index.html` | 3,9 KB | Activo, único stylesheet |
| — | — | — | **No existe ningún archivo JavaScript en el proyecto** |

Sin CSS ni JS huérfanos: `estilos.css` es el único y sí se carga.

### 1.3 Imágenes

| Archivo | Dimensiones | Peso | Formato | ¿Referenciada? |
|---|---|---|---|---|
| `IMG/274803902_...n.jpg` | 750×748 | 119,2 KB | JPEG | Sí — 3 veces |
| `IMG/274879844_...n.jpg` | 750×748 | 177,6 KB | JPEG | Sí — 4 veces |
| `IMG/274681384_...n.jpg` | 750×748 | 134,0 KB | JPEG | Sí — 4 veces |
| `IMG/274645148_...n.jpg` | 750×748 | 119,3 KB | JPEG | **No — huérfana** |
| `IMG/274727860_...n.jpg` | 750×748 | 92,1 KB | JPEG | **No — huérfana** |
| `IMG/274822028_...n.jpg` | 750×748 | 110,8 KB | JPEG | **No — huérfana** |
| `IMG/Applying.png` | 1024×1024 | 297,7 KB | PNG | Sí — como favicon |

Total imágenes: **1.050,7 KB**.

### 1.4 Tipografías

| Archivo | Peso | ¿Declarada en CSS? |
|---|---|---|
| `Fonts/DancingScript-Regular.ttf` | 79,0 KB | Sí — única `@font-face` del proyecto |
| `Fonts/DancingScript-Medium.ttf` | 79,3 KB | **No** |
| `Fonts/DancingScript-SemiBold.ttf` | 79,3 KB | **No** |
| `Fonts/DancingScript-Bold.ttf` | 79,3 KB | **No** |
| `Fonts/Cinzel-VariableFont_wght.ttf` | 121,8 KB | **No** |
| `Fonts/Cinzel-Regular.ttf` | 74,7 KB | **No** |
| `Fonts/Cinzel-Medium.ttf` | 74,9 KB | **No** |
| `Fonts/Cinzel-SemiBold.ttf` | 75,0 KB | **No** |
| `Fonts/Cinzel-Bold.ttf` | 75,0 KB | **No** |
| `Fonts/Cinzel-ExtraBold.ttf` | 75,1 KB | **No** |
| `Fonts/Cinzel-Black.ttf` | 75,1 KB | **No** |
| `Fonts/OFL.txt` | 4,4 KB | Licencia — conservar |
| `Fonts/README.txt` | 2,2 KB | Notas de distribución — conservar |

**10 de 11 archivos de fuente nunca se cargan: 809,5 KB de peso muerto en el repositorio.**

### 1.5 Dependencias externas

Ninguna. Sin CDNs, sin Google Fonts, sin librerías, sin `package.json`. Las fuentes están autoalojadas. Esto es un acierto del proyecto original y se conserva.

### 1.6 Archivos basura

Ninguno. No hay `.bak`, `.DS_Store`, `Thumbs.db`, `node_modules`, copias ni versionados en el nombre.

---

## 2. Problemas detectados

### 2.1 Grave — Las imágenes no son del proyecto

Las seis fotografías JPEG son **material promocional de terceros con marca de agua visible**. Todas llevan impreso:

- `HappyFatFont_Typeface` · `RELEASED NOW` (arriba)
- `www.heytype.xyz` · `@Jazheiman` (abajo)

Son las piezas de lanzamiento de una tipografía comercial ajena, descargadas y usadas como relleno decorativo. No guardan ninguna relación con el contenido de la página, y publicarlas atribuye visualmente el sitio a otro estudio. Es el hallazgo más grave de la auditoría.

### 2.2 Enlaces rotos y elementos sin destino

| Elemento | Problema |
|---|---|
| `<li>Menu</li>` | Texto plano, sin `<a>`, sin destino. No existe página ni sección |
| `<li>Información</li>` | Ídem. No existe página ni sección |
| `<li>Sobre Nosotros</li>` | Ídem. No existe página ni sección |
| `<button>APPLY</button>` | Sin `type`, sin `form`, sin JS asociado. No hace absolutamente nada |

El menú anuncia una arquitectura de tres secciones que no existe: es relleno heredado de un ejercicio de maquetación.

### 2.3 Rutas rotas

Ninguna. Todas las rutas de `href`/`src` apuntan a archivos que existen en disco.

### 2.4 Accesibilidad

| Problema | Detalle |
|---|---|
| `user-scalable=no` en el viewport | Bloquea el zoom con pinza. Violación directa de WCAG 1.4.4 |
| `alt=""` en 11 imágenes de contenido | Marcadas como decorativas sin serlo |
| Contraste del botón APPLY | La animación `crecerbut` lleva el color del texto a `black` sobre fondo `black`: el CTA principal queda **invisible durante la mitad de cada ciclo de 5 s**. Contraste efectivo 1:1 |
| Sin estilos de `:focus` | Ningún elemento interactivo es visible al navegar con teclado |
| `cursor: pointer` sobre `<li>` y `<div>` | Elementos no focalizables ni accionables con teclado, pero simulan ser interactivos |
| Texto corrido en Dancing Script | Una tipografía caligráfica a ~16 px para 90 palabras de cuerpo: legibilidad muy baja |
| Sin `prefers-reduced-motion` | Siete animaciones infinitas sin posibilidad de desactivarlas |

### 2.5 SEO y `<head>`

| Falta | Estado |
|---|---|
| `<meta name="description">` | Ausente |
| Open Graph (`og:title`, `og:description`, `og:url`, `og:type`) | Ausentes |
| `<link rel="canonical">` | Ausente |
| `robots.txt` | Ausente |
| `sitemap.xml` | Ausente |
| `<title>` | Existe pero dice `Apply`, 5 caracteres, y no coincide con la marca `Applyiing` |
| Idioma | `lang="es"` declarado, pero **todo el texto de cuerpo está en inglés** |

También hay erratas en el viewport: `minimun-scale` y `maximun-scale` (ambas mal escritas, por lo que el navegador las descarta).

### 2.6 Semántica HTML

- `<aside class="Imagenes">` contiene un `<nav>` cuyo único contenido son once `<img>`. Un `<nav>` sin un solo enlace.
- Los `<div class="cajita">` … `cajita7` son elementos puramente decorativos expuestos al árbol de accesibilidad.
- `<section>` sin encabezado asociado.
- El `<h1>` es la marca, no el contenido de la página.
- Nomenclatura de clases en mayúsculas y mezclando idiomas: `Applyiing`, `NavSec`, `Imagenes`, `Textarea`, `JustApply`, `caja`, `cajita2`.

### 2.7 CSS

| Problema | Ubicación |
|---|---|
| `transition: 0.3` sin unidad → declaración inválida, se descarta | `.JustApply button`, `.JustApply button:hover` |
| `;;` duplicado | 6 apariciones (`cajita2`–`cajita7`) |
| `font-family: Dancing` sin comillas y sin familia de reserva | `html`, `.JustApply button` |
| Estilos aplicados a `html` en lugar de `body` | Línea 5 |
| Sin reset ni `box-sizing` | Todo el archivo |
| Sin variables CSS | El blanco `#fff` se repite 11 veces; el borde `1.4px solid white`, 7 veces |
| Números mágicos | `top: -2.4%`, `left: 1.4%`, `left: 31%`, `right: -26%`, `translate(71.3px, -14px)`, `translate(-28px, -34.8px)` |
| Siete bloques `@keyframes` casi idénticos | `mover2`–`mover7` |
| `position: fixed`/`absolute` como sistema de layout | `.Imagenes`, `.Textarea`, `.caja`, `.JustApply` |
| Cero media queries | El archivo completo |
| Duplicación estructural | `.cajita`–`.cajita7` repiten las mismas 5 declaraciones siete veces |

### 2.8 Responsive

Verificado en navegador antes de tocar nada:

| Ancho | Resultado |
|---|---|
| 1440 px | La tira de imágenes queda cortada por el borde derecho (`right: -26%` la empuja fuera del lienzo a propósito). Enormes zonas vacías. El CTA cae fuera del área visual útil |
| 1024 px | Se agrava el solapamiento entre texto y círculos |
| 768 px | El texto invade la zona de los círculos |
| 360 px | **Roto**: el párrafo se superpone a los círculos animados, la marca choca con el menú, y la tira de imágenes sigue ocupando el borde derecho |

No hay una sola media query en el proyecto. El layout depende íntegramente de porcentajes fijos calculados para una única resolución de escritorio.

### 2.9 Rendimiento

| Métrica | Valor |
|---|---|
| Peso total del repositorio (sin `.git`) | ~1,9 MB |
| Peso de la primera carga | ~630 KB (3 JPEG únicos + 1 PNG favicon de 298 KB + 1 TTF) |
| Peso muerto en el repositorio | ~1,13 MB (10 fuentes sin usar + 3 imágenes huérfanas) |
| Favicon | PNG de 1024×1024 y 298 KB para renderizarse a 16 px |
| `font-display` | Ausente → FOIT |
| Scripts | Ninguno (no aplica `defer`) |

### 2.10 Contradicciones entre el README y el código

| Afirmación del README | Realidad |
|---|---|
| «Cinzel … for the statements» | Cinzel no se declara ni se usa en ningún punto del CSS |
| «The nav labels are anchors» | Son `<li>` de texto plano, sin un solo `<a>` |
| «Content is in Spanish» | Los tres ítems del menú están en español; el resto del contenido está en inglés |
| «the six static files are there as a fallback» | No hay `@font-face` que los referencie: no son fallback de nada |
| Bloque de código con `@font-face` de Cinzel | Ese bloque no existe en `estilos.css` |

### 2.11 Credenciales

Ninguna. Búsqueda de `api_key`, `secret`, `token`, `password`, `bearer`, `AKIA`, `sk_live`, `ghp_` sobre todos los archivos de código: **cero coincidencias**. No hay nada que retirar.

---

## 3. Resumen en cinco líneas

1. **Qué es**: una landing de una sola pantalla, sin JavaScript, construida alrededor de una única frase — que el conocimiento sin aplicación no vale nada — con un anillo de siete círculos animados en CSS como pieza gráfica central.
2. **Estado**: ejercicio de maquetación temprano. El concepto y la animación son propios y funcionan; el andamiaje que los rodea es de prueba.
3. **Lo más grave**: las seis imágenes son material promocional ajeno con marca de agua de `heytype.xyz` / `@Jazheiman`, sin ninguna relación con la página. Se eliminan todas.
4. **Segundo problema**: el menú anuncia tres secciones que no existen y el botón APPLY no lleva a ningún sitio; además su animación lo vuelve invisible la mitad del tiempo.
5. **Deuda de peso**: 1,13 MB de archivos que ninguna página carga — diez de las once tipografías y tres de las siete imágenes.
