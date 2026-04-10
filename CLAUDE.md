# CLAUDE.md — Landing TiroLog (sapemaib.dev)

Contexto para futuras sesiones. No repetir decisiones ya tomadas.

---

## Qué es este proyecto

Landing page de **TiroLog** (`https://tirolog.app`), una PWA gratuita de registro de entrenamientos de tiro deportivo. La landing vive en el repositorio `Web Sapemaib` y se despliega en GitHub Pages.

- Un único archivo: `index.html` (sin bundler, sin framework, HTML+CSS+JS inline)
- La app en sí es un proyecto separado

---

## Paleta de colores

```css
--bg:        #0d0d0d   /* fondo principal */
--surface:   #1a1a1a   /* cards, nav, secciones alternadas */
--surface2:  #222222   /* elementos secundarios dentro de cards */
--gold:      #c8a84b   /* acento principal, CTAs, iconos */
--gold-dim:  #a8893a   /* hover degradado del gold */
--gold-glow: rgba(200,168,75,.18)  /* resplandores y gradientes */
--text:      #f0ede8   /* texto principal */
--text-dim:  #9e9a94   /* texto secundario, subtítulos */
--border:    rgba(200,168,75,.18)  /* bordes de cards y separadores */
```

Hover del gold sobre fondo oscuro: `#e0bd5a`. Error/negación: `#ef4444`.

---

## Tipografía

| Uso | Familia | Pesos |
|---|---|---|
| Títulos, botones, labels, nav | **Oswald** | 400, 500, 600, 700 |
| Cuerpo, descripciones | **Inter** | 400, 500, 600 |

Ambas de Google Fonts. `letter-spacing` en Oswald: `.02em` base, hasta `.14em` en labels pequeños en mayúsculas.

---

## Estructura de secciones

```
#navbar       — sticky, blur backdrop, logo + lang switcher + CTA
#hero         — grid 2 col: texto izq / mockup móvil der (oculto en <900px)
#highlights   — barra de 4 iconos/datos clave (fondo surface)
#features     — grid de cards con icono+título+desc, una card "wide" (span 2)
#privacy      — grid 2 col: texto + diagrama SVG-like con nodos
#screenshots  — scroll horizontal de 5 capturas en marco de móvil
#languages    — grid 2 col: pills de idiomas + card estadística
#cta          — caja centrada con gradiente radial gold
#footer       — flex row: marca · links · copyright
```

---

## Imágenes disponibles

Todas en `img/` con extensión `.png.jpg` (doble extensión, así están los archivos):

| Archivo | Usado en |
|---|---|
| `screenshot-home.png.jpg` | Hero (mockup) + galería Inicio |
| `screenshot-session.png.jpg` | Galería Nueva sesión |
| `screenshot-stats.png.jpg` | Galería Estadísticas |
| `screenshot-counter.png.jpg` | Galería Contador |
| `screenshot-pdf.png.jpg` | Galería Informe PDF |

**Pendiente:** `img/og-cover.jpg` (1200×630 px) para la previsualización OG al compartir en redes. El meta tag ya apunta a ella pero el archivo no existe aún.

---

## i18n

Sistema propio en JS inline, sin librería. Dos idiomas: `es` (por defecto) y `en`.

- Los elementos traducibles llevan `data-i18n="clave"` en el HTML
- El objeto `translations` al final del archivo tiene las cadenas para `es` y `en`
- La función `setLang(lang)` itera el DOM y actualiza `innerHTML`
- El lang switcher en el navbar guarda la preferencia en `localStorage`

Al añadir texto nuevo: poner `data-i18n` en el HTML **y** añadir la clave en ambos idiomas en `translations`.

---

## Componentes CSS reutilizables

```
.btn              — base de botón/enlace
.btn-primary      — fondo gold, texto oscuro
.btn-outline      — borde gold, fondo transparente
.section-label    — pill con borde gold, texto uppercase pequeño
.section-title    — clamp(1.75rem, 4vw, 2.75rem), Oswald
.section-subtitle — color text-dim, max-width 56ch
.feat-card        — card con hover lift y gradiente gold
.feat-card.wide   — ocupa 2 columnas, layout grid interno
.screen-frame     — marco de móvil para capturas
.reveal           — animación scroll (opacity+translateY, JS IntersectionObserver)
```

---

## Breakpoints

| Breakpoint | Cambios |
|---|---|
| `≤ 900px` | Hero grid → 1 col, hero-visual oculto, privacidad/idiomas/feat.wide → 1 col |
| `≤ 600px` | nav-cta oculto, cta-box padding reducido, footer en columna |

**Punto a revisar:** `#highlights` y `#screenshots` no tienen media query propia; en 375px pueden quedar ajustados.

---

## Analytics

Google Analytics 4 — measurement ID `G-VVDST34RFP`.
Snippet gtag.js en `<head>`. No añadir GTM ni otro ID de GA.

---

## URLs

- App: `https://tirolog.app` (4 referencias en el HTML, todas con `target="_blank" rel="noopener"`)
- Autor: `https://sapemaib.dev`
- Repositorio/deploy: GitHub Pages

---

## Convenciones

- Sin bundler, sin dependencias npm. Todo inline en `index.html`.
- CSS con custom properties, no clases de utilidad tipo Tailwind.
- JS mínimo: solo i18n + IntersectionObserver para `.reveal`. Sin frameworks.
- No añadir librerías externas salvo que sea estrictamente necesario.
