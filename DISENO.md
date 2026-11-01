# DISENO.md — Landing Kléos Vital

Especificación visual y de interacción para construir `index.html`. Fuente de contenido: el brief. Si algo de este documento choca con el brief, manda el brief. Si algo no está definido aquí, **pregunta al orquestador; no lo decidas tú**.

Convenciones del documento:
- `px` son píxeles CSS. `rem` asume `html { font-size: 100% }` (1rem = 16px).
- "Móvil" = 360–599 px · "Tablet" = 600–1023 px · "Escritorio" = ≥1024 px.
- Los nombres de token (`--c-…`, `--fs-…`) son los del bloque `:root` de la sección 2. No uses hex sueltos en el CSS fuera de ese bloque.

---

## 1. Principios de dirección de arte

1. **Sobrio antes que llamativo.** Azul marino, blanco y celeste dominan; el turquesa es un acento (íconos, líneas, enlaces, botón principal). Nada de degradados intensos, brillos, sellos de "oferta", contadores, mayúsculas gritonas ni signos de exclamación.
2. **Cálido y humano.** Serif clásica (Cormorant Garamond) en títulos y citas, esquinas redondeadas generosas (16–20 px), una hoja fina como motivo orgánico recurrente. La calidez viene de la tipografía y el espacio, no de fotos.
3. **Confiable y clínico sin ser frío.** Textos cortos, datos solo del brief, íconos de línea finos (1.5 px), sin imágenes clínicas ni rostros. Los placeholders se ven intencionales (círculo con iniciales), no rotos.
4. **Un foco por pantalla.** Cada sección tiene un solo mensaje (eyebrow + título + contenido). Mucho aire: 64 px de padding vertical por sección en móvil, hasta 120 px en escritorio.
5. **Informativo, no insistente.** Botones grandes solo en hero, formulario y cierre. En el resto, enlaces discretos. El botón flotante de WhatsApp se oculta cuando ya hay un botón de WhatsApp a la vista.
6. **Ritmo claro/oscuro.** Blanco y celeste alternan; el azul marino aparece tres veces (por qué elegir, formulario, pie) para marcar los momentos de decisión.
7. **Nada "gurú".** Prohibido: "transforma tu vida", "secretos", "método único", "garantizado", "¡últimos cupos!", emojis, cifras no dadas. "Cupos limitados" se dice una sola vez (cierre), en tamaño pequeño.

---

## 2. Tokens (pegar tal cual)

### 2.1 Google Fonts (en `<head>`, en este orden)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,600;1,500&family=Inter:wght@400;600&display=swap">
```

Solo se cargan 4 estilos: Cormorant Garamond 600 (títulos), Cormorant Garamond 500 itálica (subtítulo del hero, cita, frases de cierre), Inter 400 (texto) e Inter 600 (botones, enlaces, eyebrows, etiquetas). No uses otros pesos (el navegador los sintetizaría mal).

### 2.2 Bloque `:root`

```css
:root {
  /* ===== COLOR · Marca ===== */
  --c-navy: #0E3A56;          /* títulos, fondos oscuros */
  --c-navy-700: #264E67;      /* hover de botón secundario sobre oscuro */
  --c-navy-900: #0A2C42;      /* fondo del pie; active de secundario sobre oscuro */
  --c-turquesa: #1E9AA0;      /* SOLO decorativo/no textual: hoja, líneas, borde hover de tarjeta, punto "Cupos limitados" */
  --c-turquesa-700: #147278;  /* texto turquesa sobre claro, botón primario, íconos sobre claro, foco sobre claro */
  --c-turquesa-800: #116468;  /* hover de primario y enlaces */
  --c-turquesa-900: #0E5A5E;  /* active de primario y enlaces */
  --c-turquesa-300: #7FD1D4;  /* texto/íconos turquesa sobre oscuro, foco sobre oscuro */
  --c-turquesa-200: #A6E0E2;  /* hover de enlaces sobre oscuro */
  --c-celeste: #EAF4F8;       /* fondos claros alternos */
  --c-celeste-200: #D9ECF2;   /* hover de secundario y enlaces de barra */
  --c-celeste-300: #CFE8EC;   /* active de secundario; final del degradado del avatar */
  --c-blanco: #FFFFFF;

  /* ===== COLOR · Texto ===== */
  --c-titulo: #0E3A56;
  --c-texto: #1A2B36;
  --c-texto-suave: #4A5F6D;
  --c-texto-claro: #FFFFFF;          /* texto sobre navy */
  --c-texto-claro-suave: #C5D9E3;    /* texto secundario sobre navy */

  /* ===== COLOR · Bordes y foco ===== */
  --c-borde: #D3E3EA;                         /* bordes de tarjeta y divisores (decorativos) */
  --c-borde-oscuro: rgba(255, 255, 255, 0.14);/* divisores sobre navy */
  --c-borde-icono-oscuro: rgba(127, 209, 212, 0.40);
  --c-foco: #147278;                          /* se sobrescribe a #7FD1D4 dentro de .seccion--oscura */

  /* ===== TIPOGRAFÍA ===== */
  --font-serif: "Cormorant Garamond", Garamond, "Times New Roman", serif;
  --font-sans: "Inter", system-ui, -apple-system, "Segoe UI", Roboto, Arial, sans-serif;
  --fw-regular: 400;
  --fw-semibold: 600;   /* Inter 600 y Cormorant 600 */
  --fw-italic: 500;     /* Cormorant itálica */

  /* Escala fluida (valores en 360 px → valor máximo) */
  --fs-display: clamp(2.5rem, 1.6rem + 4vw, 4.5rem);               /* H1 hero: 40 → 72 px */
  --fs-h2: clamp(2rem, 1.5rem + 2.2222vw, 3.25rem);                /* H2: 32 → 52 px */
  --fs-h3: clamp(1.5rem, 1.35rem + 0.6667vw, 1.875rem);            /* H3: 24 → 30 px */
  --fs-cita: clamp(1.75rem, 1.25rem + 2.2222vw, 2.75rem);          /* cita: 28 → 44 px */
  --fs-sub: clamp(1.375rem, 1.1875rem + 0.8333vw, 1.75rem);        /* subtítulo serif / frases: 22 → 28 px */
  --fs-lead: clamp(1.125rem, 1.0313rem + 0.4167vw, 1.3125rem);     /* entradilla: 18 → 21 px */
  --fs-body: clamp(1rem, 0.9625rem + 0.1667vw, 1.0625rem);         /* texto: 16 → 17 px */
  --fs-ui: 1rem;          /* botones: 16 px */
  --fs-link: 0.9375rem;   /* enlaces discretos, barra en ≥768: 15 px */
  --fs-small: 0.875rem;   /* avisos, meta, pie: 14 px */
  --fs-eyebrow: 0.8125rem;/* eyebrow en mayúsculas: 13 px */

  --lh-display: 1.08;
  --lh-titulo: 1.12;
  --lh-h3: 1.2;
  --lh-cita: 1.25;
  --lh-lead: 1.55;
  --lh-body: 1.65;
  --lh-ui: 1.2;

  --tracking-display: -0.01em;
  --tracking-eyebrow: 0.14em;
  --tracking-vital: 0.5em;

  /* ===== ESPACIADO (base 4 px) ===== */
  --space-1: 0.25rem;  /* 4 */
  --space-2: 0.5rem;   /* 8 */
  --space-3: 0.75rem;  /* 12 */
  --space-4: 1rem;     /* 16 */
  --space-5: 1.25rem;  /* 20 */
  --space-6: 1.5rem;   /* 24 */
  --space-7: 2rem;     /* 32 */
  --space-8: 2.5rem;   /* 40 */
  --space-9: 3rem;     /* 48 */
  --space-10: 4rem;    /* 64 */
  --space-11: 5rem;    /* 80 */
  --space-12: 6rem;    /* 96 */
  --space-seccion: clamp(4rem, 2.75rem + 5.5556vw, 7.5rem);  /* padding vertical de sección: 64 → 120 px */
  --space-bloque: clamp(2.5rem, 2rem + 2.2222vw, 3.5rem);    /* encabezado de sección → contenido: 40 → 56 px */
  --gutter: clamp(1.25rem, 0.5rem + 3.3333vw, 2.5rem);       /* margen lateral: 20 → 40 px */

  /* ===== CONTENEDORES ===== */
  --container: 1160px;        /* ancho general */
  --container-texto: 760px;   /* FAQ, cierre, párrafos centrados */
  --medida-parrafo: 40rem;    /* 640 px máx. de línea de texto */
  --header-h: 64px;           /* 72px en ≥1024 (ver media query abajo) */
  --tap: 44px;                /* área táctil mínima */

  /* ===== RADIOS ===== */
  --radius-xs: 6px;    /* contorno de foco en enlaces */
  --radius-sm: 10px;   /* skip link, placeholder del form */
  --radius-md: 16px;   /* ítems de beneficio, chip flotante */
  --radius-lg: 20px;   /* tarjetas, contenedor del formulario, cita */
  --radius-pill: 999px;/* botones, chips */
  --radius-arco: 999px 999px 24px 24px; /* panel en arco del hero */

  /* ===== SOMBRAS (tinte navy) ===== */
  --shadow-sm: 0 1px 2px rgba(14, 58, 86, 0.06), 0 1px 3px rgba(14, 58, 86, 0.08);
  --shadow-md: 0 2px 4px rgba(14, 58, 86, 0.05), 0 8px 20px rgba(14, 58, 86, 0.08);
  --shadow-lg: 0 6px 12px rgba(14, 58, 86, 0.06), 0 18px 40px rgba(14, 58, 86, 0.12);
  --shadow-form: 0 8px 20px rgba(4, 20, 31, 0.25), 0 24px 60px rgba(4, 20, 31, 0.45);
  --shadow-btn: 0 1px 2px rgba(14, 58, 86, 0.12), 0 4px 12px rgba(20, 114, 120, 0.22);
  --shadow-btn-hover: 0 2px 4px rgba(14, 58, 86, 0.12), 0 8px 20px rgba(20, 114, 120, 0.28);
  --shadow-float: 0 0 0 2px #FFFFFF, 0 8px 24px rgba(14, 58, 86, 0.28);
  --shadow-float-foco: 0 0 0 3px #FFFFFF, 0 0 0 6px #0E3A56, 0 8px 24px rgba(14, 58, 86, 0.28);

  /* ===== MOVIMIENTO ===== */
  --dur-rapida: 150ms;   /* color, subrayado, flecha */
  --dur-base: 250ms;     /* tarjetas, barra, flotante, chevron */
  --dur-acordeon: 300ms;
  --dur-revelar: 600ms;
  --dur-arco: 800ms;
  --stagger: 80ms;
  --ease-out: cubic-bezier(0.22, 0.61, 0.36, 1);
  --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);

  /* ===== CAPAS ===== */
  --z-decor: 0;
  --z-contenido: 1;
  --z-flotante: 90;
  --z-header: 100;
  --z-skip: 200;
}

@media (min-width: 1024px) {
  :root { --header-h: 72px; }
}

/* Dentro de secciones navy */
.seccion--oscura { --c-foco: #7FD1D4; color: var(--c-texto-claro); }
```

### 2.3 Breakpoints (las variables CSS no funcionan dentro de `@media`; usa estos números literales)

| Nombre | Media query | Uso |
|---|---|---|
| base | (sin media query) | móvil 360–599, mobile-first |
| sm | `(min-width: 600px)` | beneficios en 3+2 |
| md | `(min-width: 768px)` | encabezados centrados, botones en línea, cursos 2 columnas, pasos horizontales |
| lg | `(min-width: 1024px)` | layouts en 2 columnas, cursos 3 columnas, beneficios 5 columnas, header 72 px |
| xl | `(min-width: 1280px)` | solo se alcanza el máximo de las escalas; no hay cambios de layout |

Contenedor: `.contenedor { width: min(100% - 2 * var(--gutter), var(--container)); margin-inline: auto; }`. Variante `.contenedor--texto` con `var(--container-texto)`.

---

## 3. Tabla de contraste (WCAG 2.x, calculada con la fórmula de luminancia relativa)

### 3.1 Texto

| Texto | Fondo | Ratio | Uso | Cumple |
|---|---|---|---|---|
| #1A2B36 | #FFFFFF | 14.56:1 | texto de párrafo | AA/AAA |
| #1A2B36 | #EAF4F8 | 13.03:1 | texto en secciones celeste | AA/AAA |
| #0E3A56 | #FFFFFF | 11.94:1 | títulos, botón secundario | AA/AAA |
| #0E3A56 | #EAF4F8 | 10.69:1 | títulos en celeste | AA/AAA |
| #0E3A56 | #D9ECF2 | 9.80:1 | secundario hover, enlace de barra hover | AA/AAA |
| #0E3A56 | #CFE8EC | 9.33:1 | secundario active, iniciales del avatar (peor punto del degradado) | AA/AAA |
| #4A5F6D | #FFFFFF | 6.67:1 | texto suave, descripciones | AA |
| #4A5F6D | #EAF4F8 | 5.97:1 | texto suave en celeste | AA |
| #147278 | #FFFFFF | 5.66:1 | eyebrow, enlaces discretos, números de curso, rol de docente | AA |
| #147278 | #EAF4F8 | 5.07:1 | ídem sobre celeste; subtítulo del hero | AA |
| #147278 | #D9ECF2 | 4.65:1 | ícono WhatsApp de la barra en hover | AA |
| #FFFFFF | #147278 | 5.66:1 | botón primario; flotante | AA |
| #FFFFFF | #116468 | 6.89:1 | botón primario hover | AA |
| #FFFFFF | #0E5A5E | 7.95:1 | botón primario active | AA/AAA |
| #FFFFFF | #0E3A56 | 11.94:1 | texto en secciones navy | AA/AAA |
| #C5D9E3 | #0E3A56 | 8.19:1 | texto suave en navy | AA/AAA |
| #7FD1D4 | #0E3A56 | 6.81:1 | eyebrow y enlaces en navy | AA |
| #A6E0E2 | #0E3A56 | 8.18:1 | enlaces en navy, hover | AA/AAA |
| #FFFFFF | #264E67 | 8.87:1 | secundario sobre oscuro, hover | AA/AAA |
| #7FD1D4 | #264E67 | 5.06:1 | ícono del secundario oscuro en hover | AA |
| #FFFFFF | #0A2C42 | 14.46:1 | pie, secundario oscuro active | AA/AAA |
| #C5D9E3 | #0A2C42 | 9.92:1 | texto suave del pie | AA/AAA |
| #7FD1D4 | #0A2C42 | 8.25:1 | íconos/enlaces del pie | AA/AAA |
| #0E3A56 | #7FD1D4 | 6.81:1 | primario sobre oscuro (reserva) | AA |
| #0E3A56 | #A6E0E2 | 8.18:1 | ídem hover | AA/AAA |

**Prohibido** (no cumple 4.5:1): texto #1E9AA0 sobre blanco (3.40), sobre celeste (3.04) o sobre navy (3.52); texto blanco sobre #1E9AA0 (3.40). El turquesa base nunca lleva texto ni es fondo de texto.

### 3.2 Elementos no textuales (mínimo 3:1)

| Elemento | Color / Fondo | Ratio | Cumple |
|---|---|---|---|
| Íconos de contenido sobre claro | #147278 / #FFFFFF · #EAF4F8 | 5.66 · 5.07 | Sí |
| Íconos sobre navy | #7FD1D4 / #0E3A56 | 6.81 | Sí |
| Anillo de foco sobre claro | #147278 / #FFFFFF | 5.66 | Sí |
| Anillo de foco sobre navy | #7FD1D4 / #0E3A56 | 6.81 | Sí |
| Borde botón secundario claro | #0E3A56 / #FFFFFF | 11.94 | Sí |
| Borde botón secundario oscuro | #C5D9E3 / #0E3A56 | 8.19 | Sí |
| Borde hover de tarjeta, borde de número de paso | #1E9AA0 / #FFFFFF | 3.40 | Sí |
| Flotante sobre navy | #147278 / #0E3A56 = 2.11 → **se resuelve con anillo blanco de 2 px** (#FFFFFF / #0E3A56 = 11.94) | — | Sí (con anillo) |
| Bordes de tarjeta y divisores | #D3E3EA / #FFFFFF = 1.32 | — | Decorativos: la tarjeta se identifica por su contenido y sombra; no requieren 3:1 |
| Hoja decorativa, línea del eyebrow | #1E9AA0 | — | Decorativos (`aria-hidden`) |

---

## 4. Tipografía por elemento

| Elemento | Familia / peso | Tamaño | Interlineado | Color (claro / oscuro) | Notas |
|---|---|---|---|---|---|
| H1 hero | Cormorant 600 | `--fs-display` 40→72 | 1.08 | `--c-titulo` | `letter-spacing: -0.01em; text-wrap: balance; max-width: none` (corregido en revisión: `13ch` en Cormorant ≈ 208–374 px y dejaba "nivel" huérfano; el ancho lo limita la columna) |
| H2 de sección | Cormorant 600 | `--fs-h2` 32→52 | 1.12 | `--c-titulo` / `#FFFFFF` | `text-wrap: balance; max-width: 20ch` (centrados: 22ch) |
| H3 (curso, docente, ayuda) | Cormorant 600 | `--fs-h3` 24→30 | 1.2 | `--c-titulo` / `#FFFFFF` | |
| Subtítulo hero (lema) | Cormorant 500 itálica | `--fs-sub` 22→28 | 1.3 | `--c-turquesa-700` | |
| Cita | Cormorant 500 itálica | `--fs-cita` 28→44 | 1.25 | `--c-titulo` | |
| Frases de cierre (en secciones) | Cormorant 500 itálica | `--fs-sub` 22→28 | 1.3 | `--c-titulo` / `#FFFFFF` | |
| Eyebrow | Inter 600, MAYÚSCULAS | 13 px | 1.2 | `--c-turquesa-700` / `--c-turquesa-300` | `letter-spacing: 0.14em`; precedido de línea 24×1.5 px `--c-turquesa` (sobre navy: `--c-turquesa-300`), gap 10 px |
| Entradilla (lead) | Inter 400 | `--fs-lead` 18→21 | 1.55 | `--c-texto-suave` / `--c-texto-claro-suave` | `max-width: 40rem` |
| Párrafo | Inter 400 | `--fs-body` 16→17 | 1.65 | `--c-texto` / `#FFFFFF` | `max-width: 40rem` |
| Botón | Inter 600 | 16 px | 1.2 | ver componentes | `letter-spacing: 0.01em` |
| Enlace discreto | Inter 600 | 15 px | 1.2 | `--c-turquesa-700` / `--c-turquesa-300` | |
| Etiqueta beneficio | Inter 600 | 17 px (1.0625rem) | 1.35 | `--c-titulo` | |
| Meta / aviso / pie | Inter 400 | 14 px | 1.5 | `--c-texto-suave` / `--c-texto-claro-suave` | |
| Número de curso | Cormorant 600 | 30 px | 1 | `--c-turquesa-700` | formato `01`…`07`, `font-variant-numeric: lining-nums` |
| Número de paso | Cormorant 600 | 24 px | 1 | `--c-turquesa-700` | |
| Iniciales avatar | Cormorant 600 | 40 px (móvil) / 48 px (≥1024) | 1 | `--c-titulo` | `letter-spacing: 0.04em` |

Reglas generales: `body { font-family: var(--font-sans); font-size: var(--fs-body); line-height: var(--lh-body); color: var(--c-texto); background: #FFFFFF; -webkit-font-smoothing: antialiased; }`. Títulos con `margin: 0`. Nunca uses Cormorant por debajo de 22 px (se vuelve frágil); nunca uses Inter en H1, H2 ni en los H3 de tarjetas (curso, ayuda, docente). **Excepción (aclarada en revisión):** el título de cada paso (§6.10) y la pregunta del acordeón (§6.11) son H3 por semántica pero van en Inter 600, porque son etiquetas de lectura rápida; manda la especificación del componente. Sin `hyphens`. Sin cursivas en Inter.

**Cifras en Cormorant (añadido en revisión):** Cormorant usa por defecto números de estilo antiguo (el "3" baja de la línea). Aplica `font-variant-numeric: lining-nums;` a todo elemento en Cormorant: `h1, h2, h3, .frase, .paso__num, .curso__num, .cita, .docente__avatar`.

---

## 5. Iconografía e inserción de SVG

- Todos los íconos están en `assets/` con `viewBox="0 0 24 24"`, `stroke="currentColor"`, `stroke-width="1.5"`, extremos redondeados. Toman el color de la propiedad CSS `color` del contenedor.
- **`currentColor` no funciona si el SVG se usa con `<img>`** (saldría negro). Por eso: copia el contenido de cada archivo de ícono a un **sprite inline** al inicio del `<body>`:
  ```html
  <svg width="0" height="0" style="position:absolute" aria-hidden="true" focusable="false">
    <symbol id="i-curso-toxina" viewBox="0 0 24 24"> …contenido interno del archivo… </symbol>
    …
  </svg>
  ```
  y úsalo con `<svg class="icono" aria-hidden="true"><use href="#i-curso-toxina"/></svg>`. Al copiar, el `<symbol>` no lleva `stroke`/`fill`; ponlos en CSS: `.icono { width: 24px; height: 24px; fill: none; stroke: currentColor; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; flex-shrink: 0; }`. Los detalles con relleno (`fill="currentColor"` en el punto de `ui-instagram` y en las burbujas de `porque-evidencia`) se conservan tal cual dentro del símbolo.
- El grosor de trazo es fijo 1.5 en todos los tamaños (no escales el trazo).
- Todos los íconos son decorativos (`aria-hidden="true"`); el texto adyacente da el significado. Excepción: el botón flotante, que lleva `aria-label`.
- `hoja-decorativa.svg` (viewBox 0 0 120 240) también se inserta inline (o como `<img>`; trae `color="#1E9AA0"` por defecto, por eso funciona en `<img>` en turquesa base). Siempre `aria-hidden="true"`, `pointer-events: none`, `position: absolute`, `z-index: var(--z-decor)`.

---

## 6. Componentes

Regla común de foco (todo lo interactivo): `:focus-visible { outline: 3px solid var(--c-foco); outline-offset: 3px; }` (botones con `border-radius` pill: el outline sigue la forma). Nunca `outline: none` sin reemplazo. `:focus:not(:focus-visible) { outline: none; }`.

### 6.1 Botón primario (`.btn .btn--primario`)

| Propiedad | Valor |
|---|---|
| Display | `inline-flex; align-items: center; justify-content: center; gap: 10px` |
| Altura | `min-height: 52px` (área táctil 52 ≥ 44) |
| Padding | `0 28px` |
| Ancho | Móvil: `width: 100%; max-width: 420px`. ≥768: `width: auto` |
| Tipografía | Inter 600, 16 px, `line-height: 1.2`, `letter-spacing: 0.01em`, sin subrayado |
| Radio | `var(--radius-pill)` |
| Borde | `1.5px solid transparent` (para medir igual que el secundario) |
| Default | fondo `#147278`, texto `#FFFFFF`, sombra `--shadow-btn` |
| Hover | fondo `#116468`, `transform: translateY(-1px)`, sombra `--shadow-btn-hover` |
| Active | fondo `#0E5A5E`, `transform: translateY(0)`, sombra `--shadow-sm` |
| Focus-visible | outline 3 px `#147278`, offset 3 px (más el estado default) |
| Transición | `background-color 150ms, box-shadow 150ms, transform 150ms` con `--ease-out` |
| Ícono | opcional, 20 px, a la izquierda del texto |

Variante **sobre oscuro** (`.btn--primario-oscuro`, reservada, no se usa en esta versión): fondo `#7FD1D4`, texto `#0E3A56`; hover `#A6E0E2`; active `#6CCACE`; foco `#7FD1D4`; sombra `0 6px 18px rgba(0,0,0,.25)`.

### 6.2 Botón secundario (`.btn .btn--secundario`)

Mismas medidas, tipografía, radio y transiciones que el primario. Sin sombra.

| Estado | Sobre claro (blanco o celeste) | Sobre oscuro (`.seccion--oscura`) |
|---|---|---|
| Default | fondo transparente, borde `1.5px solid #0E3A56`, texto `#0E3A56`, ícono `#147278` | fondo transparente, borde `1.5px solid #C5D9E3`, texto `#FFFFFF`, ícono `#7FD1D4` |
| Hover | fondo `#D9ECF2`, `translateY(-1px)` | fondo `#264E67`, borde `#FFFFFF`, `translateY(-1px)` |
| Active | fondo `#CFE8EC`, `translateY(0)` | fondo `#0A2C42` |
| Focus-visible | outline 3 px `#147278`, offset 3 px | outline 3 px `#7FD1D4`, offset 3 px |

Los secundarios que abren WhatsApp llevan `ui-whatsapp` 20 px a la izquierda del texto, `target="_blank" rel="noopener"`.

Grupo de botones (`.botones`): `display: flex; flex-direction: column; gap: 12px; align-items: stretch; max-width: 420px` en móvil. Alineación del grupo (aclarada en revisión): sigue la del texto de su sección → hero y formulario a la izquierda; cierre centrado (`margin-inline: auto`). En ≥768: `flex-direction: row; flex-wrap: wrap; gap: 12px 16px; align-items: center`.

### 6.3 Enlace discreto (`.enlace`)

| Propiedad | Valor |
|---|---|
| Display | `inline-flex; align-items: center; gap: 8px; min-height: 44px` |
| Tipografía | Inter 600, 15 px, `line-height: 1.2` |
| Default | color `#147278` (en navy: `#7FD1D4`), sin subrayado |
| Hover | color `#116468` (en navy: `#A6E0E2`), `text-decoration: underline; text-decoration-thickness: 1px; text-underline-offset: 4px`; la flecha (`ui-flecha`) se desplaza `translateX(3px)` |
| Active | color `#0E5A5E` (en navy: `#FFFFFF`) |
| Focus-visible | outline 3 px `var(--c-foco)`, offset 2 px, `border-radius: 6px` |
| Íconos | 18 px. Flecha a la derecha del texto; WhatsApp, calendario y externo a la izquierda o derecha según cada caso (se indica abajo) |

**Enlace en línea** (dentro de un párrafo, en el pie, "Ábrelo aquí"): mismo color, Inter 600 en el tamaño del texto que lo rodea, **subrayado siempre** (1 px, offset 3 px); hover: color `#116468` y grosor 2 px.

### 6.4 Barra superior (`.barra`)

| Propiedad | Valor |
|---|---|
| Posición | `position: sticky; top: 0; z-index: 100` |
| Altura | 64 px (≥1024: 72 px) |
| Contenido | `.contenedor` con `display: flex; align-items: center; justify-content: space-between` |
| Fondo inicial (scroll ≤ 8 px) | `#EAF4F8` (se funde con el hero), sin borde, sin sombra |
| Fondo con scroll (clase `.barra--scroll` cuando `scrollY > 8`) | `rgba(255,255,255,0.92)` + `backdrop-filter: saturate(140%) blur(12px)`; `border-bottom: 1px solid #D3E3EA`; `box-shadow: var(--shadow-sm)`. Si `@supports not (backdrop-filter: blur(1px))` → fondo `#FFFFFF` sólido |
| Transición | `background-color 250ms, box-shadow 250ms, border-color 250ms` |
| Logo (izquierda) | HTML+CSS (ver 6.15), enlace a `#inicio`, `aria-label="Kléos Vital, ir al inicio"`, `min-height: 44px` |
| Enlaces (derecha) | `display: flex; gap: 4px`. Cada enlace: `min-height: 44px; padding: 0 12px; border-radius: 999px; display: inline-flex; align-items: center; gap: 6px`; Inter 600 14 px (≥768: 15 px), color `#0E3A56`. Hover: fondo `#D9ECF2`. Active: fondo `#CFE8EC`. Foco: outline 3 px `#147278` offset 2 px |
| "Inscríbete" | solo texto → `#inscripcion` |
| "WhatsApp" | ícono `ui-whatsapp` 18 px color `#147278` + texto "WhatsApp" → wa.me general, nueva pestaña |

No se oculta al bajar, no hay menú hamburguesa, no hay más enlaces. Medida de control a 360 px: logo ≈ 64 px + "Inscríbete" ≈ 96 px + "WhatsApp" ≈ 118 px = 278 px < 320 px útiles.

### 6.5 Encabezado de sección (`.encabezado`)

Eyebrow → (12 px) → H2 → (16 px) → entradilla opcional. Separación con el contenido: `margin-bottom: var(--space-bloque)`. Alineación: izquierda en móvil siempre; en ≥768 centrado (`text-align: center; margin-inline: auto`) en las secciones marcadas como "centrado" en la sección 7. Cuando está centrado, la línea del eyebrow sigue a la izquierda del texto (eyebrow como `inline-flex`).

### 6.6 Ítem de beneficio (`.beneficio`)

| | Móvil (<600) | ≥600 |
|---|---|---|
| Layout | fila: `display: flex; align-items: center; gap: 16px` | columna: `flex-direction: column; align-items: center; text-align: center; gap: 16px; justify-content: flex-start` (corregido en revisión: con `center` los íconos quedaban a distinta altura según el texto ocupara 1 o 2 líneas) |
| Caja | fondo `#FFFFFF`, borde `1px solid #D3E3EA`, radio 16 px, padding `16px 20px`, `min-height: 76px` | padding `28px 20px`, `min-height: 184px` |
| Círculo del ícono | 48×48, radio 50 %, fondo `#EAF4F8`, color `#147278`, ícono 24 px | 64×64, ícono 30 px |
| Texto | Inter 600, 17 px, `#0E3A56` | ídem |
| Sombra | ninguna; hover: ninguno (no es interactivo) | ídem |

### 6.7 Tarjeta de curso (`.curso`)

| Parte | Especificación |
|---|---|
| Caja | `display: flex; flex-direction: column`; fondo `#FFFFFF`; borde `1px solid #D3E3EA`; radio 20 px; padding 24 px (≥1024: 28 px); sombra `--shadow-sm`; altura igual entre tarjetas de una fila (grid `align-items: stretch`) |
| Fila superior | `display: flex; justify-content: space-between; align-items: center`. Izquierda: número `01` (Cormorant 600, 30 px, `#147278`). Derecha: círculo 52×52 fondo `#EAF4F8`, ícono del curso 26 px color `#147278` |
| Título (H3) | `margin-top: 20px`, Cormorant 600 `--fs-h3`, `#0E3A56` |
| Descripción | `margin-top: 8px`, Inter 400 16 px, `line-height: 1.6`, `#4A5F6D` |
| Meta fechas | `margin-top: 16px`, `display: flex; gap: 8px; align-items: flex-start`; ícono `ui-calendario` 16 px `#147278` (con `margin-top: 2px`); texto Inter 400 14 px `#4A5F6D`: **"Próximas fechas: consúltalas por WhatsApp"**. Sin precio. |
| Pie de tarjeta | `margin-top: auto; padding-top: 20px`. Dentro: lista de 2 enlaces, cada uno `display: flex; width: 100%; justify-content: space-between; min-height: 48px; border-top: 1px solid #D3E3EA` |
| Enlace 1 | "Inscribirme" + `ui-flecha` 18 px a la derecha. Color `#147278` |
| Enlace 2 | "Preguntar por WhatsApp" + `ui-whatsapp` 18 px a la derecha. Color `#0E3A56` (hover `#147278`). `target="_blank" rel="noopener"` |
| Hover tarjeta | borde `#1E9AA0`, sombra `--shadow-md`, `transform: translateY(-3px)`, transición 250 ms `--ease-out` |
| `:focus-within` | borde `#1E9AA0` (sin mover la tarjeta) |
| La tarjeta entera NO es clicable | solo los dos enlaces |

Tarjeta de ayuda (`.curso--ayuda`, 8.º elemento del grid): fondo `#0E3A56` (aplicar `.seccion--oscura` a la tarjeta), sin borde, radio 20 px, padding igual; círculo 52×52 con fondo `rgba(255,255,255,0.06)`, borde `1px solid rgba(127,209,212,.40)`, ícono `ui-whatsapp` 26 px `#7FD1D4`; H3 blanco "¿No sabes por cuál empezar?"; texto 16 px `#C5D9E3` "Escríbenos y te contamos los detalles de cada curso."; enlace discreto oscuro "Preguntar por WhatsApp" (`#7FD1D4`, flecha a la derecha) con el mensaje general. En móvil y tablet se apila igual que una tarjeta de curso (aclarado en revisión): círculo → H3 a 20 px → texto a 8 px → enlace al pie (`margin-top: auto; padding-top: 20px`); el wireframe ASCII es solo orientativo. En ≥1024 ocupa 2 columnas (`grid-column: span 2`) y su contenido pasa a fila: `display: grid; grid-template-columns: 52px 1fr auto; gap: 24px; align-items: center`. Sin hover de elevación.

### 6.8 Tarjeta de docente (`.docente`)

| Parte | Especificación |
|---|---|
| Caja | fondo `#FFFFFF`, borde `1px solid #D3E3EA`, radio 20 px, padding 28 px (≥1024: 40 px), sombra `--shadow-md`. Sin hover |
| Avatar placeholder | círculo 112×112 (≥1024: 128×128), `border-radius: 50%`, fondo `linear-gradient(145deg, #EAF4F8 0%, #CFE8EC 100%)`, `box-shadow: 0 0 0 6px #FFFFFF, 0 0 0 7px #1E9AA0`, iniciales centradas "AN" / "EV" (Cormorant 600, 40 px; ≥1024: 48 px; `#0E3A56`; `letter-spacing: .04em`). `aria-hidden="true"` (el nombre está al lado). Comentario en el código: `<!-- [COMPLETAR] Reemplazar por <img src="img/neira.jpg" alt="Dr. Andrés Neira" width="128" height="128" loading="lazy"> -->` (ídem `img/villarreal.jpg`, "Dra. Erlinda Villarreal"). Con foto: mismo tamaño, `object-fit: cover`, mismo anillo |
| Nombre (H3) | `margin-top: 28px`, Cormorant 600 `--fs-h3`, `#0E3A56` |
| Rol | `margin-top: 6px`, Inter 600 15 px, `#147278` |
| Rol 2 (solo Villarreal) | `margin-top: 2px`, Inter 400 15 px, `#4A5F6D` |
| Divisor | `1px solid #D3E3EA`, `margin: 24px 0` |
| Lista de experiencia | `display: grid; gap: 12px`; cada ítem `display: grid; grid-template-columns: 20px 1fr; gap: 12px`; ícono `ui-check` 20 px `#147278` con `margin-top: 3px`; texto Inter 400 16 px, `line-height: 1.6`, `#1A2B36` |

### 6.9 Ítem "por qué elegir" (`.razon`, sobre navy)

`display: grid; grid-template-columns: 48px 1fr; gap: 20px; align-items: center; padding: 20px 0; border-top: 1px solid rgba(255,255,255,.14)`; el último también `border-bottom`. Círculo 48×48 con fondo `rgba(255,255,255,0.04)` y borde `1px solid rgba(127,209,212,.40)`; ícono 24 px `#7FD1D4`. Texto Inter 400 `--fs-body`, `line-height: 1.55`, `#FFFFFF`. No interactivo.

### 6.10 Pasos (`.pasos`, 3)

| | Móvil | ≥768 |
|---|---|---|
| Layout | lista vertical; cada paso `display: grid; grid-template-columns: 48px 1fr; column-gap: 20px; row-gap: 0; padding-bottom: 32px` (el último 0); el número ocupa `grid-row: 1 / span 2` | `grid-template-columns: repeat(3, 1fr); gap: 32px`; cada paso centrado (`text-align: center`, número centrado) |
| Número | círculo 48×48, fondo `#FFFFFF`, borde `1.5px solid #1E9AA0`, número Cormorant 600 24 px `#147278`, `position: relative; z-index: 1` | ídem |
| Conector | `::before` del paso (menos el último), paso con `position: relative`: `position: absolute; left: 23px; top: 56px; bottom: 8px; width: 2px; background: #D3E3EA` | horizontal: `position: absolute; top: 23px; left: calc(50% + 32px); width: calc(100% - 32px); height: 2px; background: #D3E3EA` (deja 8 px de aire a cada lado entre círculos, con gap de 32 px) |
| Título | Inter 600 18 px `#0E3A56`, `margin: 0; padding-top: 12px` (queda alineado con el centro del círculo) | `padding-top: 0; margin-top: 20px` |
| Texto | Inter 400 16 px `#4A5F6D`, `margin-top: 6px`, `max-width: 30ch` | ídem, centrado con `margin-inline: auto` |

### 6.11 Acordeón (`.faq`)

| Parte | Especificación |
|---|---|
| Ítem | `border-top: 1px solid #D3E3EA`; el último también `border-bottom` |
| Pregunta | `<h3>` que contiene un `<button aria-expanded aria-controls>`. Botón: `width: 100%; min-height: 64px; padding: 20px 0; display: flex; justify-content: space-between; align-items: center; gap: 16px; text-align: left; background: none; border: 0`; Inter 600 17 px (`1.0625rem`), `line-height: 1.4`, `#0E3A56` |
| Indicador | círculo 36×36 a la derecha, fondo `#EAF4F8`, ícono `ui-chevron` 20 px `#147278` |
| Hover | texto `#147278`; círculo fondo `#D9ECF2` |
| Focus-visible | outline 3 px `#147278`, offset 4 px, radio 8 px |
| Abierto (`aria-expanded="true"`) | chevron `rotate(180deg)`; círculo fondo `#147278`, ícono `#FFFFFF` |
| Panel | contenedor `display: grid; grid-template-rows: 0fr` → abierto `1fr`, transición 300 ms `--ease-in-out`; hijo con `overflow: hidden`. Contenido: `padding: 0 52px 24px 0` (móvil `0 0 24px 0`), Inter 400 16 px, `line-height: 1.65`, `#4A5F6D`. Cerrado: `visibility: hidden` en el hijo (para que no sea enfocable) |
| Comportamiento | todos cerrados al cargar; cada uno abre/cierra independiente (no se cierran los demás). Enter/Espacio por ser `<button>` |

### 6.12 Contenedor del formulario (`.formulario`)

| Parte | Especificación |
|---|---|
| Tarjeta | fondo `#FFFFFF` (obligatorio: Tally con `transparentBackground=1` pinta texto oscuro; **nunca** se pone sobre el navy directamente), radio 20 px, padding `24px 20px` (≥768: 32 px; ≥1024: 40 px), sombra `--shadow-form`. Color de texto interno: `--c-texto`; `--c-foco: #147278` |
| Chip de curso seleccionado | solo visible si hay `curso`: `display: inline-flex; gap: 8px; align-items: center; padding: 8px 14px; border-radius: 999px; background: #EAF4F8; margin-bottom: 20px`; ícono `ui-check` 16 px `#147278`; texto Inter 600 14 px `#0E3A56`: "Curso seleccionado: {Nombre del curso}". `aria-live="polite"` |
| Iframe | `width: 100%; border: 0; min-height: 560px; display: block` (Tally lo redimensiona con `dynamicHeight`). `title="Formulario de inscripción a los cursos de Kléos Vital"` |
| Cargando | texto "Cargando formulario…" Inter 400 15 px `#4A5F6D`, centrado, visible detrás/encima del iframe hasta su evento `load` |
| Placeholder sin URL | caja `min-height: 320px`, `border: 2px dashed #D3E3EA`, radio 10 px, centrado, texto Inter 600 15 px `#0E3A56`: "[COMPLETAR] URL del formulario de Tally" |
| Pie de la tarjeta | `border-top: 1px solid #D3E3EA; margin-top: 24px; padding-top: 16px` |
| Aviso de datos | `display: flex; gap: 8px`; ícono `ui-candado` 16 px `#147278` (`margin-top: 2px`); Inter 400 14 px `#4A5F6D`: "Tus datos se usan solo para contactarte sobre los cursos de Kléos Vital." |
| Enlace de respaldo | `margin-top: 4px`; texto Inter 400 14 px `#4A5F6D` "¿Problemas para ver el formulario?" + enlace en línea "Ábrelo aquí" (Inter 600 14 px `#147278`, subrayado) + ícono `ui-externo` 14 px; el `<a>` con `min-height: 44px; display: inline-flex; align-items: center`; `target="_blank" rel="noopener"` |

### 6.13 Botón flotante de WhatsApp (`.flotante`)

| Propiedad | Valor |
|---|---|
| Posición | `position: fixed; right: 16px; bottom: calc(16px + env(safe-area-inset-bottom)); z-index: 90`. ≥1024: `right: 24px; bottom: 24px` |
| Tamaño | 56×56 px, `border-radius: 50%` (también en escritorio) |
| Colores | fondo `#147278`, ícono `ui-whatsapp` 28 px `#FFFFFF`, sombra `--shadow-float` (anillo blanco de 2 px + sombra) |
| Hover | fondo `#116468`, `translateY(-2px)` |
| Active | fondo `#0E5A5E`, `translateY(0)` |
| Focus-visible | `outline: none; box-shadow: var(--shadow-float-foco)` (anillo blanco + anillo navy: visible sobre claro y oscuro) |
| Accesibilidad | `<a href="https://wa.me/…" aria-label="Escríbenos por WhatsApp" target="_blank" rel="noopener">` |
| Visibilidad | ver sección 12.2 |
| Sin texto, sin globo, sin animación de pulso, sin contador | |

### 6.14 Pie (`.pie`)

Ver sección 7.12. Enlaces del pie: Instagram como enlace en línea blanco `#FFFFFF` subrayado (hover `#A6E0E2`), con ícono `ui-instagram` 20 px `#7FD1D4`; `min-height: 44px`.

### 6.15 Logo (HTML + CSS, recomendado)

Renderiza el logo como texto, no como `<img>`, para que use exactamente las fuentes cargadas:

```html
<a class="logo" href="#inicio" aria-label="Kléos Vital, ir al inicio">
  <span class="logo__kleos">Kléos</span>
  <span class="logo__vital">VITAL</span>
</a>
```

| | Barra | Pie |
|---|---|---|
| Layout | `display: inline-flex; flex-direction: column; align-items: center; line-height: 1` | ídem |
| "Kléos" | Cormorant 600, 26 px, `#0E3A56`, `letter-spacing: 0.01em` | 34 px, `#FFFFFF` |
| "VITAL" | Inter 600, 9 px, `letter-spacing: 0.5em; margin-right: -0.5em` (compensa el espaciado final), `#147278`, `margin-top: 3px` | 11 px, `#7FD1D4`, `margin-top: 5px` |

Los archivos `logo-kleos-vital.svg` (sobre claro) y `logo-kleos-vital-claro.svg` (sobre oscuro) son respaldo (correos, documentos) y referencia; su texto depende de las fuentes instaladas. El favicon es `favicon.svg` (monograma K en trazos, sin texto, no depende de fuentes).

---

## 7. Secciones (en orden)

Resumen de fondos y ritmo:

| # | Sección | `id` | Fondo | Encabezado |
|---|---|---|---|---|
| 1 | Barra superior | — | `#EAF4F8` → blanco translúcido al hacer scroll | — |
| 2 | Hero | `inicio` | `#EAF4F8` + luz blanca abajo a la izquierda | izquierda |
| 3 | Quiénes somos | `quienes-somos` | `#FFFFFF` | izquierda |
| 4 | Propuesta de formación | `propuesta` | `#EAF4F8` | centrado (≥768) |
| 5 | Cursos | `cursos` | `#FFFFFF` | centrado (≥768) |
| 6 | Docentes | `docentes` | `#EAF4F8` | centrado (≥768) |
| 7 | ¿Por qué elegir? | `por-que` | `#0E3A56` (oscura) | izquierda |
| 8 | Cómo reservar (3 pasos) | `pasos` | `#FFFFFF` | centrado (≥768) |
| 9 | Formulario | `inscripcion` | `#0E3A56` (oscura) + tarjeta blanca | izquierda |
| 10 | Preguntas frecuentes | `preguntas` | `#FFFFFF` | centrado (≥768) |
| 11 | Cierre | `cierre` | `#EAF4F8` | centrado (siempre) |
| 12 | Pie | — | `#0A2C42` (oscura) | — |

Todas las secciones 2–11: `padding-block: var(--space-seccion)`; `position: relative; overflow: hidden; overflow: clip;` (por las hojas decorativas; `clip` va después de `hidden` como mejora progresiva, para no romper el `position: sticky` de §7.7). Contenido con `position: relative; z-index: 1`.

### 7.1 Barra superior

Especificada en 6.4. HTML: `<header class="barra">` antes de `<main>`. Antes de la barra, el skip link (ver 9).

```
MÓVIL (360)                              ESCRITORIO (≥1024)
+----------------------------------+     +--------------------------------------------------------------+
| Kléos         Inscríbete (o)WhatsApp| | Kléos                                     Inscríbete   (o) WhatsApp |
| VITAL                            |     | VITAL                                                        |
+----------------------------------+     +--------------------------------------------------------------+
  64 px · fondo celeste → blanco 92 %       72 px · contenedor 1160 px
```

### 7.2 Hero (`#inicio`)

- **Fondo:** `background: radial-gradient(90% 70% at 0% 100%, #FFFFFF 0%, rgba(255,255,255,0) 70%), #EAF4F8;` (la luz va abajo a la izquierda para que no se note la unión con la barra).
- **Padding:** móvil `40px` arriba / `64px` abajo; ≥1024 `96px` / `120px`.
- **Contenido y textos exactos:**
  1. Eyebrow: **FORMACIÓN PARA PROFESIONALES DE LA SALUD**
  2. H1 (`margin-top: 12px` respecto al eyebrow): **Lleva tus conocimientos al siguiente nivel**
  3. Subtítulo (`<p>`, Cormorant itálica, `#147278`, `margin-top: 16px`, `text-wrap: balance`): **Educación que transforma tu práctica clínica**
  4. Párrafo (`--fs-lead`, `#4A5F6D`, `margin-top: 20px`, `max-width: 34rem`): **Cursos de capacitación en medicina estética y regenerativa. Talleres 100% prácticos y presenciales para personal de salud.**
  5. Botones (`margin-top: 32px`): primario **Inscríbete ahora** → `#inscripcion`; secundario **Tengo preguntas** (con ícono WhatsApp) → wa.me general.
- **Decoración móvil/tablet:** `hoja-decorativa` 120×240 px, `top: 12px; right: -36px`, color `#1E9AA0`, `opacity: 0.22`. Se oculta en ≥1024.
- **Escritorio (≥1024):** `display: grid; grid-template-columns: 7fr 5fr; gap: 64px; align-items: center`. Columna derecha: **panel en arco** `width: 100%; max-width: 440px; aspect-ratio: 4 / 5; border-radius: var(--radius-arco); background: linear-gradient(180deg, #FFFFFF 0%, #D9ECF2 100%); border: 1px solid #D3E3EA; position: relative; justify-self: end`. Dentro, la hoja centrada `height: 72%`, color `#1E9AA0`, `opacity: 0.9`. **Chip flotante** sobre el arco: `position: absolute; left: -32px; bottom: 48px`; fondo blanco, radio 16 px, sombra `--shadow-lg`, padding `14px 18px`, `display: flex; gap: 12px; align-items: center`; círculo 40×40 `#EAF4F8` con `beneficio-practico` 22 px `#147278`; dos líneas: "Talleres 100% prácticos" (Inter 600 15 px `#0E3A56`) y "Presenciales · Grupos reducidos" (Inter 400 14 px `#4A5F6D`). Todo el arco, chip incluido, es `aria-hidden="true"` (su contenido ya está en el párrafo del hero).
- **Tablet (600–1023):** igual que móvil, botones en fila desde 768.

```
MÓVIL (360–430)
+----------------------------------+
|                       \  (hoja    |
| -- FORMACIÓN PARA        \  22 %) |
|    PROFESIONALES DE LA SALUD     |
|                                  |
| Lleva tus                        |
| conocimientos al                 |  H1 40 px Cormorant
| siguiente nivel                  |
|                                  |
| Educación que transforma tu      |  serif itálica turquesa
| práctica clínica                 |
|                                  |
| Cursos de capacitación en        |  18 px gris
| medicina estética y regenera-    |
| tiva. Talleres 100% prácticos... |
|                                  |
| [        Inscríbete ahora      ] |  52 px, ancho completo
| [ (o)    Tengo preguntas       ] |  secundario
+----------------------------------+

ESCRITORIO (≥1024)
+------------------------------------------------------------------------+
| -- FORMACIÓN PARA PROFESIONALES DE LA SALUD          .--''''''--.       |
|                                                     /            \      |
| Lleva tus conocimientos                            |   \  hoja    |     |
| al siguiente nivel                (72 px)          |    \/        |     |
|                                                    |    /\        |     |
| Educación que transforma tu práctica clínica       |              |     |
|                                               +-----------------+ |     |
| Cursos de capacitación en medicina estética...|(mano) Talleres  | |     |
|                                               | 100% prácticos  | |     |
| [ Inscríbete ahora ]  [ (o) Tengo preguntas ] +-----------------+-+     |
+------------------------------------------------------------------------+
   columna 7fr                                    arco 5fr, máx. 440 px
```

### 7.3 Quiénes somos (`#quienes-somos`)

- **Fondo:** `#FFFFFF`.
- **Textos:** eyebrow **QUIÉNES SOMOS**; H2 **Educación práctica, actualizada y con sentido clínico**; párrafo (`--fs-lead`, `#4A5F6D`, `margin-top: 20px`): **"En Kléos Vital creemos en una educación práctica, actualizada y con sentido clínico. Nuestros cursos están diseñados para que los profesionales de la salud adquieran y perfeccionen habilidades en procedimientos estéticos y terapias regenerativas, con un enfoque seguro, ético y basado en la evidencia."**
- **Cita destacada** (`<figure>` con `<blockquote>` y `<figcaption>`): tarjeta fondo `#EAF4F8`, radio 20 px, padding `32px 24px` (≥1024: `56px 48px`), `position: relative; overflow: hidden`. Arriba, comilla de apertura “ decorativa (`aria-hidden`), Cormorant 600 80 px, `#1E9AA0`, `line-height: 0.6; display: block; margin-bottom: 16px`. Texto: **La ciencia y la estética, cuando van de la mano, transforman vidas** (Cormorant 500 itálica `--fs-cita`, `#0E3A56`). Figcaption (`margin-top: 24px`): **— KLÉOS VITAL** (estilo eyebrow sin línea, `#147278`). Hoja decorativa 96×192 `right: -24px; bottom: -48px; opacity: 0.18; transform: rotate(18deg)`.
- **Layout:** móvil apilado, cita a `margin-top: 40px`. ≥1024: `grid-template-columns: 1fr 1fr; gap: 64px; align-items: center`.

```
MÓVIL                                   ESCRITORIO
+----------------------------------+    +-----------------------------------------------------------+
| -- QUIÉNES SOMOS                 |    | -- QUIÉNES SOMOS              +-------------------------+ |
| Educación práctica,              |    | Educación práctica,           | “                       | |
| actualizada y con sentido        |    | actualizada y con             | La ciencia y la estética,| |
| clínico                          |    | sentido clínico               | cuando van de la mano,  | |
|                                  |    |                               | transforman vidas       | |
| En Kléos Vital creemos en una    |    | En Kléos Vital creemos en     |                         | |
| educación práctica, ...          |    | una educación práctica...     | — KLÉOS VITAL     hoja  | |
| +------------------------------+ |    |                               +-------------------------+ |
| | “                            | |    +-----------------------------------------------------------+
| | La ciencia y la estética,    | |
| | cuando van de la mano,       | |
| | transforman vidas            | |
| | — KLÉOS VITAL          hoja  | |
| +------------------------------+ |
+----------------------------------+
```

### 7.4 Nuestra propuesta de formación (`#propuesta`)

- **Fondo:** `#EAF4F8`.
- **Textos:** eyebrow **CÓMO APRENDES**; H2 **Nuestra propuesta de formación**. Sin entradilla.
- **Ítems (en este orden, con su ícono):**
  1. `beneficio-practico` — **Talleres 100% prácticos**
  2. `beneficio-presencial` — **Modalidad presencial**
  3. `beneficio-grupos` — **Grupos reducidos**
  4. `beneficio-material` — **Material de apoyo**
  5. `beneficio-certificado` — **Certificación de asistencia**
- **Layout:** móvil `display: grid; gap: 12px` (1 columna, ítem en fila). 600–1023: `display: flex; flex-wrap: wrap; justify-content: center; gap: 16px`, cada ítem `flex: 0 1 calc((100% - 32px) / 3)` → 3 + 2 centrados. ≥1024: `grid-template-columns: repeat(5, 1fr); gap: 20px`.
- **Frase de cierre de la sección** (`margin-top: 48px`, centrada en todos los tamaños, `max-width: 32ch; margin-inline: auto`, Cormorant itálica `--fs-sub`, `#0E3A56`): **Tu crecimiento profesional también es parte del bienestar de tus pacientes.**

```
MÓVIL                                    ESCRITORIO
+----------------------------------+     +-------------------------------------------------------------+
| -- CÓMO APRENDES                 |     |                    -- CÓMO APRENDES                         |
| Nuestra propuesta de             |     |            Nuestra propuesta de formación                   |
| formación                        |     |                                                             |
| +------------------------------+ |     | +---------+ +---------+ +---------+ +---------+ +---------+ |
| | (ic) Talleres 100% prácticos | |     | |  (ic)   | |  (ic)   | |  (ic)   | |  (ic)   | |  (ic)   | |
| +------------------------------+ |     | | Talleres| |Modalidad| | Grupos  | |Material | |Certific.| |
| | (ic) Modalidad presencial    | |     | |  100%   | |presencial| |reducidos| |de apoyo | |de asist.| |
| +------------------------------+ |     | +---------+ +---------+ +---------+ +---------+ +---------+ |
| | (ic) Grupos reducidos        | |     |                                                             |
| | (ic) Material de apoyo       | |     |     Tu crecimiento profesional también es parte del         |
| | (ic) Certificación de asist. | |     |          bienestar de tus pacientes.   (itálica)            |
| +------------------------------+ |     +-------------------------------------------------------------+
| Tu crecimiento profesional       |
| también es parte del bienestar   |
| de tus pacientes.                |
+----------------------------------+
```

### 7.5 Nuestros cursos (`#cursos`)

- **Fondo:** `#FFFFFF`.
- **Textos:** eyebrow **NUESTROS CURSOS**; H2 **Siete áreas de formación para tu práctica clínica**; entradilla: **Más que un curso, es una experiencia de aprendizaje que impulsa tu carrera.**
- **Tarjetas** (componente 6.7). Número, ícono, título y descripción exactos:

| # | Ícono | Título (H3) — también valor de `curso` | Descripción |
|---|---|---|---|
| 01 | `curso-toxina` | Toxina botulínica | Manejo, dosis, anatomía y seguridad. |
| 02 | `curso-hialuronico` | Ácido hialurónico | Técnicas, zonas, indicaciones y complicaciones. |
| 03 | `curso-bioestimuladores` | Bioestimuladores de colágeno | Mecanismos de acción y protocolos. |
| 04 | `curso-prp` | Plasma rico en plaquetas (PRP) | Obtención, aplicación y usos clínicos. |
| 05 | `curso-hilos` | Hilos de tensión y de colágeno | Técnicas, tipos de hilos y zonas de aplicación. |
| 06 | `curso-sueroterapia` | Sueroterapia básica y avanzada | Protocolos, mezclas, indicaciones y seguimiento. |
| 07 | `curso-terapia-neural` | Terapia neural | Aplicaciones clínicas, puntos de inyección y abordaje integral. |

  + 8.º elemento: tarjeta de ayuda (6.7) "¿No sabes por cuál empezar?".
- **Grid:** móvil 1 columna, `gap: 16px`. 768–1023: `repeat(2, 1fr)`, `gap: 20px` (7 + ayuda = 4 filas completas). ≥1024: `repeat(3, 1fr)`, `gap: 24px`; la ayuda ocupa 2 columnas en la última fila (7.º + ayuda = fila completa).

```
MÓVIL                                   ESCRITORIO (≥1024)
+----------------------------------+    +---------------------------------------------------------------+
| -- NUESTROS CURSOS               |    |                     -- NUESTROS CURSOS                        |
| Siete áreas de formación         |    |      Siete áreas de formación para tu práctica clínica        |
| para tu práctica clínica         |    |   Más que un curso, es una experiencia de aprendizaje...      |
| Más que un curso, es una ...     |    |                                                               |
| +------------------------------+ |    | +-----------------+ +-----------------+ +-----------------+   |
| | 01                     (ic)  | |    | | 01         (ic) | | 02         (ic) | | 03         (ic) |   |
| | Toxina botulínica            | |    | | Toxina          | | Ácido           | | Bioestimuladores|   |
| | Manejo, dosis, anatomía y    | |    | | botulínica      | | hialurónico     | | de colágeno     |   |
| | seguridad.                   | |    | | Manejo, dosis...| | Técnicas, zonas.| | Mecanismos de...|   |
| | [cal] Próximas fechas:       | |    | | [cal] Próximas..| | [cal] Próximas..| | [cal] Próximas..|   |
| |       consúltalas por WhatsApp| |    | |-----------------| |-----------------| |-----------------|   |
| |------------------------------| |    | | Inscribirme  -> | | Inscribirme  -> | | Inscribirme  -> |   |
| | Inscribirme               -> | |    | |-----------------| |-----------------| |-----------------|   |
| |------------------------------| |    | | Preguntar por   | | Preguntar por   | | Preguntar por   |   |
| | Preguntar por WhatsApp    (o)| |    | | WhatsApp    (o) | | WhatsApp    (o) | | WhatsApp    (o) |   |
| +------------------------------+ |    | +-----------------+ +-----------------+ +-----------------+   |
|   ... 02 a 07 ...                |    |   04  05  06 (igual)                                          |
| +------------------------------+ |    | +-----------------+ +-----------------------------------+     |
| | (o) ¿No sabes por cuál       | |    | | 07 Terapia      | | (o) ¿No sabes por cuál empezar?   |     |
| |     empezar?  (fondo navy)   | |    | |    neural       | |     Escríbenos y te contamos...   |     |
| | Preguntar por WhatsApp    -> | |    | |                 | |           Preguntar por WhatsApp->|     |
| +------------------------------+ |    | +-----------------+ +-----------------------------------+     |
+----------------------------------+    +---------------------------------------------------------------+
```

### 7.6 Conoce a tus docentes (`#docentes`)

- **Fondo:** `#EAF4F8`.
- **Textos:** eyebrow **DOCENTES**; H2 **Conoce a tus docentes**. Sin entradilla.
- **Tarjetas** (componente 6.8), contenido exacto:
  - **Dr. Andrés Neira** · iniciales **AN** · Rol: **Médico Estético** · Lista:
    - Experiencia en medicina estética y procedimientos mínimamente invasivos.
    - Enfoque en resultados naturales, seguros y personalizados.
  - **Dra. Erlinda Villarreal** · iniciales **EV** · Rol: **Médica Funcional y Regenerativa** · Rol 2: **Magíster en Calidad de los Servicios de Salud** · Lista:
    - Medicina funcional y regenerativa.
    - Experiencia en optimización de la salud, longevidad y bienestar integral.
    - (No repetir "Magíster en calidad de los servicios de salud" en la lista: ya está como Rol 2. Mismas credenciales, sin duplicar.)
- **Layout:** móvil 1 columna, `gap: 20px`, contenido de tarjeta alineado a la izquierda. ≥1024: `grid-template-columns: 1fr 1fr; gap: 32px`, contenido alineado a la izquierda.

```
MÓVIL                                   ESCRITORIO
+----------------------------------+    +-------------------------------------------------------------+
| -- DOCENTES                      |    |                       -- DOCENTES                           |
| Conoce a tus docentes            |    |                 Conoce a tus docentes                       |
| +------------------------------+ |    | +----------------------------+ +----------------------------+|
| |  .---.                       | |    | |  .----.                    | |  .----.                    ||
| | ( AN  )  112 px              | |    | | (  AN  )  128 px           | | (  EV  )                   ||
| |  '---'                       | |    | |  '----'                    | |  '----'                    ||
| | Dr. Andrés Neira             | |    | | Dr. Andrés Neira           | | Dra. Erlinda Villarreal    ||
| | MÉDICO ESTÉTICO (turquesa)   | |    | | Médico Estético            | | Médica Funcional y Regen.  ||
| | ---------------------------- | |    | | -------------------------- | | Magíster en Calidad de ... ||
| | v Experiencia en medicina... | |    | | v Experiencia en medicina  | | -------------------------- ||
| | v Enfoque en resultados...   | |    | | v Enfoque en resultados... | | v Medicina funcional y ... ||
| +------------------------------+ |    | +----------------------------+ | v Experiencia en optimiz...||
| +------------------------------+ |    |                                +----------------------------+|
| | ( EV ) Dra. Erlinda ...      | |    +-------------------------------------------------------------+
+----------------------------------+
```
(El rol va en Inter 600 15 px sin mayúsculas; en el wireframe se marca solo para distinguirlo.)

### 7.7 ¿Por qué elegir esta formación? (`#por-que`, `.seccion--oscura`)

- **Fondo:** `#0E3A56`.
- **Textos:** eyebrow **POR QUÉ KLÉOS VITAL** (`#7FD1D4`, línea `#7FD1D4`); H2 **¿Por qué elegir esta formación?** (`#FFFFFF`).
- **Ítems** (componente 6.9):
  1. `porque-medicos` — Aprenderás de médicos con experiencia clínica y docente.
  2. `porque-practica` — Enfoque práctico, con pacientes reales y supervisión directa.
  3. `porque-evidencia` — Actualización en técnicas y protocolos basados en evidencia.
  4. `porque-perfil` — Fortaleces tu perfil profesional y amplías tus servicios.
  5. `porque-futuro` — Inversión en tu futuro y en el de tus pacientes.
- **Frase:** línea 32×1.5 px `#1E9AA0`, debajo (`margin-top: 16px`) **Porque la ciencia, la técnica y la ética… también se enseñan.** (Cormorant itálica `--fs-sub`, `#FFFFFF`, `max-width: 22ch`). Usar el carácter "…" (U+2026).
- **Layout:** móvil: encabezado → lista (`margin-top: 32px`) → frase (`margin-top: 40px`). ≥1024: `grid-template-columns: 5fr 7fr; gap: 64px; align-items: start`; columna izquierda = encabezado + frase (`margin-top: 40px`), con `position: sticky; top: calc(var(--header-h) + 32px)`; columna derecha = lista.
- **Decoración:** hoja 160×320 px, `left: -48px; bottom: -64px`, color `#7FD1D4`, `opacity: 0.12`. En móvil `right: -56px; left: auto; top: 24px; bottom: auto; width: 120px; height: 240px; opacity: 0.10`.

```
MÓVIL                                   ESCRITORIO
+----------------------------------+    +---------------------------------------------------------------+
| -- POR QUÉ KLÉOS VITAL     hoja  |    | -- POR QUÉ KLÉOS VITAL      | ---------------------------------|
| ¿Por qué elegir esta             |    | ¿Por qué elegir esta        | (ic) Aprenderás de médicos con   |
| formación?          (blanco)     |    | formación?                  |      experiencia clínica y docente|
| -------------------------------- |    |                             | ---------------------------------|
| (ic) Aprenderás de médicos con   |    | ---                         | (ic) Enfoque práctico, con ...   |
|      experiencia clínica y ...   |    | Porque la ciencia, la       | ---------------------------------|
| -------------------------------- |    | técnica y la ética…         | (ic) Actualización en técnicas...|
| (ic) Enfoque práctico, con ...   |    | también se enseñan.         | ---------------------------------|
| ...(5 ítems)                     |    |   (sticky)                  | (ic) Fortaleces tu perfil ...    |
| -------------------------------- |    |                             | ---------------------------------|
| ---                              |    |  hoja 12 %                  | (ic) Inversión en tu futuro ...  |
| Porque la ciencia, la técnica    |    |                             | ---------------------------------|
| y la ética… también se enseñan.  |    +---------------------------------------------------------------+
+----------------------------------+        fondo navy #0E3A56
```

### 7.8 Cómo reservar tu cupo (`#pasos`)

- **Fondo:** `#FFFFFF`.
- **Textos:** eyebrow **PASO A PASO** (corregido en revisión: antes decía "INSCRIPCIÓN", repetido con la sección siguiente); H2 **Cómo reservar tu cupo en 3 pasos**.
- **Pasos** (componente 6.10). Marcar en el código `<!-- Texto editable -->`:
  1. **Completa el formulario** — Déjanos tus datos y el curso que te interesa.
  2. **Te contactamos por WhatsApp** — Confirmamos contigo el curso, la fecha y el pago.
  3. **Reservas tu lugar** — Con todo confirmado, tu cupo queda separado.
- Sin botón en esta sección (la siguiente es el formulario).

```
MÓVIL                                   ESCRITORIO (≥768)
+----------------------------------+    +-------------------------------------------------------------+
| -- PASO A PASO                   |    |                     -- PASO A PASO                          |
| Cómo reservar tu cupo            |    |            Cómo reservar tu cupo en 3 pasos                 |
| en 3 pasos                       |    |                                                             |
| (1)  Completa el formulario      |    |      (1)-----------------(2)-----------------(3)            |
|  |   Déjanos tus datos y el ...  |    |  Completa el        Te contactamos      Reservas tu         |
|  |                               |    |  formulario         por WhatsApp        lugar               |
| (2)  Te contactamos por WhatsApp |    |  Déjanos tus datos  Confirmamos contigo Con todo            |
|  |   Confirmamos contigo el ...  |    |  y el curso que ... el curso, la ...    confirmado, tu ...  |
|  |                               |    +-------------------------------------------------------------+
| (3)  Reservas tu lugar           |
|      Con todo confirmado, ...    |
+----------------------------------+
```

### 7.9 Formulario de inscripción (`#inscripcion`, `.seccion--oscura`)

- **Fondo:** `#0E3A56`. Sin hoja decorativa (que el foco sea el formulario).
- **Textos columna de texto:** eyebrow **INSCRIPCIÓN** (`#7FD1D4`); H2 **Reserva tu cupo** (`#FFFFFF`, `tabindex="-1"` e `id="inscripcion-titulo"` para recibir el foco tras el scroll desde una tarjeta); entradilla (`#C5D9E3`): **Completa el formulario y te contactamos por WhatsApp para confirmar curso, fecha y pago.**
- **Apoyo WhatsApp** (`margin-top: 40px`; en móvil va DESPUÉS de la tarjeta del formulario, `margin-top: 32px`): texto Inter 600 17 px `#FFFFFF`: **¿Prefieres resolver tus dudas primero?** y debajo (`margin-top: 16px`) botón secundario sobre oscuro con ícono: **Escríbenos por WhatsApp** → wa.me general.
- **Tarjeta del formulario** (componente 6.12).
- **Layout:** móvil: encabezado → tarjeta (`margin-top: 32px`) → apoyo WhatsApp (`margin-top: 32px`). En el HTML el orden es: encabezado, tarjeta, apoyo. En ≥1024, `grid-template-areas` pone el apoyo bajo el encabezado (sin `position: sticky` en esta sección):
  ```css
  @media (min-width:1024px){
    .inscripcion__grid{display:grid;grid-template-columns:5fr 7fr;column-gap:64px;
      grid-template-areas:"enc form" "apoyo form";grid-template-rows:auto 1fr;align-items:start;}
    .inscripcion__enc{grid-area:enc} .inscripcion__form{grid-area:form;margin-top:0}
    .inscripcion__apoyo{grid-area:apoyo;margin-top:40px}
  }
  ```

```
MÓVIL                                   ESCRITORIO
+----------------------------------+    +---------------------------------------------------------------+
| -- INSCRIPCIÓN        (navy)     |    | -- INSCRIPCIÓN               +-------------------------------+ |
| Reserva tu cupo                  |    | Reserva tu cupo              | [v Curso seleccionado: Toxina]| |
| Completa el formulario y te      |    |                              |                               | |
| contactamos por WhatsApp para... |    | Completa el formulario y te  |   [ iframe de Tally ]         | |
| +------------------------------+ |    | contactamos por WhatsApp...  |   Nombre completo ________    | |
| | [v Curso seleccionado: ...]  | |    |                              |   WhatsApp ________           | |
| |                              | |    | ¿Prefieres resolver tus      |   ...                         | |
| |   [ iframe Tally ]           | |    | dudas primero?               |                               | |
| |   min 560 px                 | |    | [ (o) Escríbenos por WhatsApp]| ----------------------------- | |
| |------------------------------| |    |                              | (candado) Tus datos se usan...| |
| | (candado) Tus datos se usan  | |    |                              | ¿Problemas para ver el        | |
| | solo para contactarte...     | |    |                              | formulario? Ábrelo aquí [ext] | |
| | ¿Problemas para ver el       | |    |                              +-------------------------------+ |
| | formulario? Ábrelo aquí [ext]| |    +---------------------------------------------------------------+
| +------------------------------+ |
| ¿Prefieres resolver tus dudas    |
| primero?                         |
| [ (o) Escríbenos por WhatsApp  ] |
+----------------------------------+
```

### 7.10 Preguntas frecuentes (`#preguntas`)

- **Fondo:** `#FFFFFF`. Contenedor `--container-texto` (760 px).
- **Textos:** eyebrow **ANTES DE INSCRIBIRTE**; H2 **Preguntas frecuentes**.
- **Acordeón** (componente 6.11) con las 5 preguntas de la sección 8.
- **Debajo** (`margin-top: 32px`, centrado en ≥768, izquierda en móvil): texto Inter 400 16 px `#4A5F6D` **¿Tienes otra pregunta?** seguido de enlace discreto **Escríbenos por WhatsApp** (ícono WhatsApp 18 px a la izquierda) → wa.me general.

```
MÓVIL                                   ESCRITORIO (contenedor 760 px centrado)
+----------------------------------+    +-------------------------------------------------+
| -- ANTES DE INSCRIBIRTE          |    |            -- ANTES DE INSCRIBIRTE              |
| Preguntas frecuentes             |    |              Preguntas frecuentes               |
| -------------------------------- |    | ----------------------------------------------- |
| ¿Qué certificado recibo al   (v) |    | ¿Qué certificado recibo al terminar?        (v) |
| terminar un taller?              |    | ----------------------------------------------- |
| -------------------------------- |    | ¿Los cursos son presenciales o virtuales?   (^) |
| ¿Los cursos son presenciales (^) |    |   Todos nuestros talleres son presenciales...   |
| o virtuales?                     |    | ----------------------------------------------- |
|   Todos nuestros talleres son    |    | ...                                             |
|   presenciales...                |    | ----------------------------------------------- |
| -------------------------------- |    |   ¿Tienes otra pregunta? (o) Escríbenos por ... |
| ... (5)                          |    +-------------------------------------------------+
| ¿Tienes otra pregunta?           |
| (o) Escríbenos por WhatsApp      |
+----------------------------------+
```

### 7.11 Cierre (`#cierre`)

- **Fondo:** `#EAF4F8`. Contenedor `--container-texto`. Todo centrado en todos los tamaños.
- **Textos:** H2 (sin eyebrow) **Tu vocación también merece formación de alto nivel** (`max-width: 18ch; margin-inline: auto`). Botones (`margin-top: 32px`, grupo centrado): primario **Inscríbete** → `#inscripcion`; secundario con ícono **Escríbenos por WhatsApp** → wa.me general. Aviso (`margin-top: 24px`): punto 8×8 `#1E9AA0` + **CUPOS LIMITADOS** (estilo eyebrow, `#147278`, `gap: 10px`, sin línea).
- **Decoración:** móvil: una hoja 120×240 `right: -40px; top: -16px; opacity: 0.18`. ≥768: dos hojas 160×320, una `left: 4%; bottom: -80px; opacity: 0.22` y otra espejada (`transform: scaleX(-1)`) `right: 4%; bottom: -80px; opacity: 0.22`.

```
MÓVIL                                   ESCRITORIO
+----------------------------------+    +-------------------------------------------------------------+
|                           hoja   |    |                                                             |
|   Tu vocación también merece     |    |  hoja      Tu vocación también merece              hoja     |
|   formación de alto nivel        |    |  \|/        formación de alto nivel                 \|/     |
|                                  |    |   |                                                  |      |
| [         Inscríbete           ] |    |       [ Inscríbete ]  [ (o) Escríbenos por WhatsApp ]       |
| [ (o) Escríbenos por WhatsApp  ] |    |                     •  CUPOS LIMITADOS                      |
|        •  CUPOS LIMITADOS        |    +-------------------------------------------------------------+
+----------------------------------+
```

### 7.12 Pie de página (`<footer class="pie seccion--oscura">`)

- **Fondo:** `#0A2C42`. Padding: móvil `56px` arriba / `32px` abajo; ≥1024 `72px` / `40px`.
- **Contenido:**
  - Logo HTML versión pie (6.15).
  - Lema (`margin-top: 12px`): **Educación que transforma tu práctica clínica** (Cormorant itálica 20 px, `#C5D9E3`).
  - Contacto (lista sin viñetas, `margin-top: 28px`, `gap: 4px`; cada ítem `display: flex; align-items: center; gap: 8px; min-height: 44px`):
    - `ui-instagram` 20 px `#7FD1D4` + enlace **[@USUARIO]** (`https://instagram.com/[USUARIO]`, nueva pestaña; placeholder visible) 
    - `ui-ubicacion` 20 px `#7FD1D4` + texto **[CIUDAD]** (`#C5D9E3`, 16 px, no enlace)
  - Divisor `1px solid rgba(255,255,255,.14)`, `margin: 32px 0 24px`.
  - Línea inferior: frase **Juntos por una medicina más humana, segura y estética.** (Cormorant itálica 18 px, `#C5D9E3`) y **© 2026 Kléos Vital** (Inter 400 13 px, `#C5D9E3`).
- **Layout:** móvil apilado, alineado a la izquierda; línea inferior apilada con `gap: 8px`. ≥1024: fila superior `display: flex; justify-content: space-between; align-items: flex-start` (logo + lema a la izquierda, contacto a la derecha); línea inferior `display: flex; justify-content: space-between; align-items: baseline`.

```
MÓVIL                                   ESCRITORIO
+----------------------------------+    +-------------------------------------------------------------+
| Kléos                            |    | Kléos                                     [ig] [@USUARIO]   |
| VITAL                            |    | VITAL                                     [pin] [CIUDAD]    |
| Educación que transforma tu      |    | Educación que transforma tu práctica clínica                |
| práctica clínica                 |    | ----------------------------------------------------------- |
| [ig]  [@USUARIO]                 |    | Juntos por una medicina más humana...      © 2026 Kléos Vital|
| [pin] [CIUDAD]                   |    +-------------------------------------------------------------+
| -------------------------------- |
| Juntos por una medicina más      |
| humana, segura y estética.       |
| © 2026 Kléos Vital               |
+----------------------------------+
```

---

## 8. Preguntas frecuentes (texto final)

1. **¿Qué certificado recibo al terminar un taller?**
   Al finalizar el taller recibes una certificación de asistencia, que deja constancia de tu participación. Si quieres conocer los detalles de este documento antes de inscribirte, escríbenos por WhatsApp.

2. **¿Los cursos son presenciales o virtuales?**
   Todos nuestros talleres son presenciales, porque la práctica directa es la base de la formación. La ciudad, el lugar y el horario de cada fecha te los confirmamos por WhatsApp.

3. **¿Por qué trabajan con grupos reducidos?**
   En un taller práctico cada participante necesita tiempo para practicar y recibir retroalimentación directa del docente. Trabajar con grupos reducidos lo hace posible. Pregúntanos por WhatsApp cuántos cupos hay disponibles para la fecha que te interesa.

4. **¿Incluyen material de apoyo?**
   Sí. Cada taller incluye material de apoyo sobre los temas del curso. Si quieres saber qué incluye el curso que te interesa, pregúntanos por WhatsApp.

5. **¿Cómo reservo mi cupo?**
   Completa el formulario de inscripción de esta página. Luego te contactamos por WhatsApp para confirmar el curso, la fecha y el pago; con eso, tu lugar queda reservado. Si prefieres hablar con nosotros primero, escríbenos por WhatsApp.

En las respuestas, "escríbenos por WhatsApp" / "pregúntanos por WhatsApp" van como **enlace en línea** (6.3) al wa.me general. No se mencionan horas, cupos numéricos, precios, ciudades ni avales.

---

## 9. Microcopy completo

| Lugar | Texto exacto | Destino / comportamiento |
|---|---|---|
| Skip link (primer elemento del body) | Saltar al contenido | `#contenido` (el `<main id="contenido">`). Oculto hasta recibir foco; al enfocarse: `position: fixed; top: 8px; left: 8px; z-index: 200; background: #0E3A56; color: #FFFFFF; padding: 12px 16px; border-radius: 10px;` Inter 600 15 px |
| Barra | Inscríbete | `#inscripcion` (curso vacío) |
| Barra | WhatsApp | wa.me general |
| Hero, primario | Inscríbete ahora | `#inscripcion` (curso vacío) |
| Hero, secundario | Tengo preguntas | wa.me general |
| Tarjeta curso, meta | Próximas fechas: consúltalas por WhatsApp | texto (no enlace) |
| Tarjeta curso, enlace 1 | Inscribirme | scroll a `#inscripcion` con `curso` = título del curso; foco al H2 del formulario |
| Tarjeta curso, enlace 2 | Preguntar por WhatsApp | wa.me con "Hola, quiero información del curso de {Título}" |
| Tarjeta de ayuda, título | ¿No sabes por cuál empezar? | — |
| Tarjeta de ayuda, texto | Escríbenos y te contamos los detalles de cada curso. | — |
| Tarjeta de ayuda, enlace | Preguntar por WhatsApp | wa.me general |
| Formulario, chip | Curso seleccionado: {Título} | visible solo con curso |
| Formulario, cargando | Cargando formulario… | hasta `load` del iframe |
| Formulario, placeholder | [COMPLETAR] URL del formulario de Tally | si no hay URL |
| Formulario, aviso | Tus datos se usan solo para contactarte sobre los cursos de Kléos Vital. | — |
| Formulario, respaldo | ¿Problemas para ver el formulario? **Ábrelo aquí** | URL de Tally (no embed) con los mismos `curso` y `src`, nueva pestaña |
| Formulario, apoyo | ¿Prefieres resolver tus dudas primero? | — |
| Formulario, botón | Escríbenos por WhatsApp | wa.me general |
| FAQ, cierre | ¿Tienes otra pregunta? **Escríbenos por WhatsApp** | wa.me general |
| Cierre, primario | Inscríbete | `#inscripcion` (curso vacío) |
| Cierre, secundario | Escríbenos por WhatsApp | wa.me general |
| Cierre, aviso | Cupos limitados | texto |
| Flotante (`aria-label`) | Escríbenos por WhatsApp | wa.me general |
| Pie | [@USUARIO] · [CIUDAD] · © 2026 Kléos Vital | placeholders visibles |
| Mensaje WhatsApp general | Hola, quiero información de los cursos de Kléos Vital | + " (vengo de {src})" si hay `?src=` |
| Mensaje WhatsApp por curso | Hola, quiero información del curso de {Título} | + " (vengo de {src})" si hay `?src=` |

Todos los enlaces wa.me: `target="_blank" rel="noopener"`.

---

## 10. Frases de cierre y cita: dónde va cada una

Cada frase aparece **una sola vez**, en una sección distinta, para no saturar:

| Frase | Ubicación | Estilo |
|---|---|---|
| "La ciencia y la estética, cuando van de la mano, transforman vidas" (cita) | 7.3 Quiénes somos, tarjeta de cita | Cormorant itálica `--fs-cita` |
| "Tu crecimiento profesional también es parte del bienestar de tus pacientes." | 7.4 Propuesta, bajo los beneficios | Cormorant itálica `--fs-sub`, centrada |
| "Más que un curso, es una experiencia de aprendizaje que impulsa tu carrera." | 7.5 Cursos, entradilla | Inter `--fs-lead` |
| "Porque la ciencia, la técnica y la ética… también se enseñan." | 7.7 Por qué elegir, columna izquierda / bajo la lista | Cormorant itálica `--fs-sub`, blanca |
| "Tu vocación también merece formación de alto nivel" | 7.11 Cierre, H2 | Cormorant 600 `--fs-h2` |
| "Juntos por una medicina más humana, segura y estética." | 7.12 Pie, línea inferior | Cormorant itálica 18 px |

No se agrega ninguna otra frase motivacional.

---

## 11. Animaciones

### 11.1 Aparición al hacer scroll (`.revelar`)

- **Solo** si el documento tiene la clase `js` (añadida por el script en `<head>`: `document.documentElement.classList.add('js')`) **y** no hay `prefers-reduced-motion: reduce`. Sin JS, todo se ve.
- Estado inicial: `opacity: 0; transform: translateY(16px)`.
- Estado visible (`.revelar.es-visible`): `opacity: 1; transform: none`.
- Transición: `opacity 600ms var(--ease-out), transform 600ms var(--ease-out)`, `transition-delay: var(--retraso, 0ms)`.
- IntersectionObserver: `threshold: 0.15`, `rootMargin: "0px 0px -10% 0px"`; al entrar, añade `.es-visible` y deja de observar (una sola vez). Lo que ya está en pantalla al cargar se revela de inmediato.
- `will-change` no se usa.

| Elemento con `.revelar` | `--retraso` |
|---|---|
| Bloque `.encabezado` de cada sección 3–11 (eyebrow+H2+entradilla juntos) | 0 ms |
| Cita (7.3) | 120 ms |
| Ítems de beneficio (5) | índice × 80 ms → 0, 80, 160, 240, 320 |
| Frase de 7.4 | 0 ms |
| Tarjetas de curso (8) | (índice mod 3) × 80 ms → 0, 80, 160, 0, 80, 160, 0, 80 |
| Tarjetas de docente (2) | 0, 120 ms |
| Ítems "por qué" (5) | índice × 80 ms |
| Frase de 7.7 | 0 ms |
| Pasos (3) | índice × 120 ms → 0, 120, 240 |
| Tarjeta del formulario | 0 ms |
| Acordeón completo (un bloque) | 0 ms |
| Contenido del cierre (un bloque) | 0 ms |

**No se animan:** barra, texto del hero (se pinta de inmediato para no retrasar el LCP), pie.

### 11.2 Hero

Solo el panel en arco (≥1024): `@keyframes arco { from { opacity: 0; transform: scale(.98); } to { opacity: 1; transform: none; } }`, 800 ms, `--ease-out`, `animation-delay: 150ms`, `animation-fill-mode: both`.

### 11.3 Microinteracciones

| Interacción | Propiedades | Duración / easing |
|---|---|---|
| Botones hover/active | fondo, sombra, `translateY(-1px)` | 150 ms `--ease-out` |
| Enlace discreto | color, subrayado; flecha `translateX(3px)` | 150 ms `--ease-out` |
| Tarjeta de curso hover | borde, sombra, `translateY(-3px)` | 250 ms `--ease-out` |
| Barra al hacer scroll | fondo, sombra, borde | 250 ms `--ease-out` |
| Acordeón | `grid-template-rows` 0fr↔1fr; chevron `rotate(180deg)`; color de círculo | 300 ms `--ease-in-out` (filas), 250 ms (chevron) |
| Flotante mostrar/ocultar | `opacity`, `transform: translateY(16px) scale(.9)` → `none`; `visibility` | 250 ms `--ease-out` (al ocultar, `visibility` con `transition-delay: 250ms`) |
| Scroll a anclas | `html { scroll-behavior: smooth; scroll-padding-top: calc(var(--header-h) + 16px); }` | nativo |

### 11.4 `prefers-reduced-motion: reduce` (alternativa exacta)

```css
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    transition-delay: 0ms !important;
  }
  .revelar { opacity: 1 !important; transform: none !important; }
  .btn:hover, .curso:hover, .flotante:hover { transform: none; }
}
```
Y en JS: si `matchMedia('(prefers-reduced-motion: reduce)').matches`, no se observa nada con IntersectionObserver y `scrollIntoView` usa `behavior: 'auto'`. Los cambios de color en hover/foco se mantienen (son instantáneos). El acordeón abre sin animación.

---

## 12. Comportamiento de barra y flotante

### 12.1 Barra
Sticky siempre visible (no se esconde). Cambia a `.barra--scroll` cuando `window.scrollY > 8` (escuchar `scroll` con `{ passive: true }`; comprobar también al cargar). Detalle en 6.4.

### 12.2 Botón flotante
- Visible en **todas** las anchuras (móvil, tablet, escritorio), mismo tamaño.
- **Oculto** mientras alguna de estas zonas esté en pantalla, porque ya ofrecen WhatsApp o están al final: hero (`#inicio`), formulario (`#inscripcion`), cierre (`#cierre`) y pie. Implementación: un IntersectionObserver con `threshold: 0` sobre esas 4 zonas, un contador/Set de zonas visibles; si está vacío → mostrar, si no → ocultar.
- Al cargar arriba (hero visible) arranca oculto. Sin JS: visible siempre (el estado oculto lo pone el JS con una clase `.flotante--oculto`).
- Estado oculto: `opacity: 0; transform: translateY(16px) scale(.9); visibility: hidden; pointer-events: none;` (sale del orden de tabulación).
- No debe tapar contenido: como se oculta en pie y cierre, no se necesita padding extra al final.

---

## 13. Assets

Todos en `assets/`. Íconos: 24×24, trazo 1.5, `currentColor`.

| Archivo | Uso | Tamaño de render | Color |
|---|---|---|---|
| `beneficio-practico.svg` (mano) | Beneficio 1; chip del hero | 24 px (móvil) / 30 px (≥600); 22 px en chip | `#147278` |
| `beneficio-presencial.svg` (pizarra de aula) | Beneficio 2 | 24 / 30 px | `#147278` |
| `beneficio-grupos.svg` (tres personas) | Beneficio 3 | 24 / 30 px | `#147278` |
| `beneficio-material.svg` (libro abierto) | Beneficio 4 | 24 / 30 px | `#147278` |
| `beneficio-certificado.svg` (documento con sello) | Beneficio 5 | 24 / 30 px | `#147278` |
| `porque-medicos.svg` (estetoscopio) | Por qué 1 | 24 px | `#7FD1D4` |
| `porque-practica.svg` (portapapeles con check) | Por qué 2 | 24 px | `#7FD1D4` |
| `porque-evidencia.svg` (matraz) | Por qué 3 | 24 px | `#7FD1D4` |
| `porque-perfil.svg` (persona + flecha arriba) | Por qué 4 | 24 px | `#7FD1D4` |
| `porque-futuro.svg` (brote) | Por qué 5 | 24 px | `#7FD1D4` |
| `curso-toxina.svg` (jeringa) | Curso 01 | 26 px | `#147278` |
| `curso-hialuronico.svg` (labios, línea) | Curso 02 | 26 px | `#147278` |
| `curso-bioestimuladores.svg` (moléculas) | Curso 03 | 26 px | `#147278` |
| `curso-prp.svg` (tubo con capas + gota) | Curso 04 | 26 px | `#147278` |
| `curso-hilos.svg` (hilos de tensión) | Curso 05 | 26 px | `#147278` |
| `curso-sueroterapia.svg` (bolsa de suero + gota) | Curso 06 | 26 px | `#147278` |
| `curso-terapia-neural.svg` (red de nodos) | Curso 07 | 26 px | `#147278` |
| `ui-whatsapp.svg` | barra (18), enlaces (18), botones (20), ayuda (26), flotante (28) | ver uso | según contexto |
| `ui-flecha.svg` | "Inscribirme", enlaces de ayuda | 18 px | color del enlace |
| `ui-chevron.svg` | acordeón | 20 px | `#147278` / `#FFFFFF` abierto |
| `ui-calendario.svg` | meta de fechas en tarjetas | 16 px | `#147278` |
| `ui-check.svg` | lista de docentes (20), chip de curso (16) | 20 / 16 px | `#147278` |
| `ui-candado.svg` | aviso de datos | 16 px | `#147278` |
| `ui-externo.svg` | "Ábrelo aquí" | 14 px | `#147278` |
| `ui-instagram.svg` | pie | 20 px | `#7FD1D4` |
| `ui-ubicacion.svg` | pie | 20 px | `#7FD1D4` |
| `hoja-decorativa.svg` (viewBox 0 0 120 240) | hero, cita, por qué, cierre | ver cada sección | `#1E9AA0` / `#7FD1D4`, con opacidad indicada |
| `logo-kleos-vital.svg` | respaldo del logo sobre claro (no se usa en la página; el logo va en HTML) | 132×64 | navy + turquesa |
| `logo-kleos-vital-claro.svg` | respaldo sobre oscuro | 132×64 | blanco + `#7FD1D4` |
| `favicon.svg` | `<link rel="icon" type="image/svg+xml" href="assets/favicon.svg">` | 16–64 px | navy + blanco |
| `og.svg` (1200×630) | **fuente** de `assets/og.jpg` (la exporta el orquestador). La página referencia `og.jpg`, no el SVG | 1200×630 | — |

Rutas: el sitio se publica en `https://omedinaavilla.github.io/Kleos-Vital-/`, así que **todas las rutas en el HTML son relativas** (`assets/…`, `img/…`), nunca con `/` inicial. Excepción: `og:image` debe ser absoluta: `https://omedinaavilla.github.io/Kleos-Vital-/assets/og.jpg`.

`<meta name="theme-color" content="#EAF4F8">` (coincide con la barra al cargar).

---

## 14. Decisiones para el desarrollador

1. **Colores:** solo los tokens. El turquesa base `#1E9AA0` nunca para texto ni como fondo de texto.
2. **Clase `.seccion--oscura`** en `#por-que`, `#inscripcion`, `.curso--ayuda` y el pie: cambia `--c-foco` a `#7FD1D4` y el color de texto a blanco. Los eyebrows, enlaces y secundarios dentro de ella usan sus variantes oscuras.
3. **Íconos:** sprite inline con `<symbol>` + `<use>` (sección 5). No `<img>` para íconos. No librerías de íconos.
4. **Logo:** HTML+CSS (6.15), no `<img>`.
5. **Tamaños mínimos:** todo lo clicable mide al menos 44×44 px de área (enlaces con `min-height: 44px`; botones 52 px; flotante 56 px; acordeón 64 px).
6. **Textos:** usar exactamente los de este documento. Títulos con `text-wrap: balance`. Párrafos `max-width: 40rem`. Sin mayúsculas forzadas salvo eyebrows y "VITAL".
7. **Alineación:** encabezados a la izquierda en móvil; centrados en ≥768 solo en Propuesta, Cursos, Docentes, Pasos, FAQ; el cierre siempre centrado.
8. **Jerarquía de encabezados:** un solo `<h1>` (hero). H2 por sección. H3 en tarjetas de curso, de ayuda, de docente, títulos de pasos y preguntas del acordeón. El eyebrow es `<p>`, no encabezado.
9. **Sin sombras ni bordes extra** fuera de los indicados. Sin `text-shadow`. Sin degradados salvo: fondo del hero, panel en arco y avatar.
10. **Imágenes:** no hay fotos. Las fotos futuras de docentes van con `width/height` fijos (128×128), `loading="lazy"`, `object-fit: cover`.
11. **Tarjetas de curso:** la tarjeta no es un enlace; sólo sus dos enlaces. "Inscribirme" es `<a href="#inscripcion" data-curso="{Título}">` para que funcione sin JS.
12. **Al pulsar "Inscribirme":** scroll a `#inscripcion`, recargar iframe con `curso`, mostrar chip "Curso seleccionado", mover el foco al H2 `#inscripcion-titulo` con `focus({ preventScroll: true })`. Los botones generales ("Inscríbete", "Inscríbete ahora") limpian el curso y ocultan el chip.
13. **Formulario siempre en tarjeta blanca** aunque la sección sea navy.
14. **El flotante** se oculta en hero, formulario, cierre y pie (12.2). No añadir más botones grandes en otras secciones.
15. **Unidades:** tipografía con los tokens `clamp()`; espaciados con `--space-*`. Valores sueltos en px solo donde este documento los da.
16. **Ellipsis tipográfica:** "…" (U+2026) en "la ética… también" y "Cargando formulario…".
17. **Idioma:** `<html lang="es-CO">`.
18. **Placeholders visibles:** `[COMPLETAR]` en número de WhatsApp (comentario), URL de Tally, `[@USUARIO]`, `[CIUDAD]`, fotos (comentario). No se ocultan con CSS.
19. **Cualquier duda visual no cubierta aquí → preguntar al orquestador.**
