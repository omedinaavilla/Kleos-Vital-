# CLAUDE.md — Landing page Kléos Vital

Contexto para cualquier sesión de Claude que trabaje en este repo. Léelo antes de tocar archivos.

## Proyecto

Kléos Vital es una organización colombiana de formación para profesionales de la salud en medicina estética y regenerativa (talleres 100% prácticos, presenciales). Esta es su landing page: la primera impresión de la marca, casi siempre vista **desde el celular** después de un reel o una publicación de Instagram.

**Objetivo:** captar atención, presentar la marca y los 7 cursos, generar confianza en los docentes y ofrecer **dos caminos sin presión**:
1. **WhatsApp**: para quien tiene preguntas.
2. **Formulario de inscripción (Tally)**: para quien ya decidió y quiere reservar su cupo.

La página debe valer la pena leerla aunque la persona no actúe hoy. No debe sentirse insistente.

## Estructura del repo

```
index.html     Página completa (HTML + CSS + JS en un solo archivo). La escribe el Desarrollador.
DISENO.md      Especificación de diseño y tokens CSS. La escribe el Diseñador. Fuente de verdad visual.
assets/        SVG (íconos, hoja decorativa, logo placeholder, favicon, og.svg) y og.jpg.
img/           Fotos de docentes cuando existan: neira.jpg, villarreal.jpg.
CLAUDE.md      Este archivo.
.claude/agents/  Definiciones de los dos agentes (diseñador y desarrollador).
```

- Se publica en **GitHub Pages** como sitio de proyecto: `https://omedinaavilla.github.io/Kleos-Vital-/` (repo `omedinaavilla/Kleos-Vital-`, rama `main`, carpeta raíz).
- Como la URL lleva el subpath `/Kleos-Vital-/`, **usa siempre rutas relativas** (`assets/...`, `img/...`), nunca `/assets/...`. La excepción es `og:image`, que necesita URL absoluta.
- Es un sitio estático: **no hay servidor, base de datos ni API propia**. Tally envía los datos a Google Sheets.

## Flujo de trabajo con dos agentes

1. **Diseñador**: entrega `DISENO.md` y `assets/`.
2. **Desarrollador**: construye `index.html` con base en `DISENO.md`.
3. **Diseñador**: revisa `index.html` contra `DISENO.md` y entrega correcciones priorizadas (alta, media, baja).
4. **Desarrollador**: aplica las correcciones de prioridad alta y media.
5. **Orquestador**: verifica y entrega los resultados finales.

Los dos agentes están definidos en `.claude/agents/disenador-ui-ux.md` y `.claude/agents/desarrollador-web.md` (se invocan por nombre: `disenador-ui-ux`, `desarrollador-web`).

El orquestador (la sesión principal) coordina, resuelve ambigüedades y es el único que decide cuando los agentes no están de acuerdo. Si un agente encuentra algo ambiguo, lo reporta al orquestador; no lo decide por su cuenta.

---

## Agente 1: Diseñador UI/UX

**Rol:** define cómo se ve y cómo se siente la página. **No escribe ni edita `index.html`.** Entrega `DISENO.md` y los SVG con tanto detalle que el desarrollador pueda construir sin tomar decisiones visuales.

**Archivos a su cargo:** `DISENO.md`, `assets/*.svg`.

**Skills:**
- Dirección de arte para salud y educación premium: sobria, cálida y confiable, nunca "gurú" ni exagerada.
- Sistemas de diseño: tokens de color, tipografía, espaciado, radios y sombras, entregados como variables CSS (`:root`) listas para pegar.
- Jerarquía visual y ritmo de scroll: alternar secciones claras y oscuras, mucho espacio en blanco, un foco por pantalla.
- Mobile-first (360 a 430 px), con adaptación a tablet y escritorio.
- Conversión sin presión: dónde ubicar los dos caminos (WhatsApp y formulario).
- Accesibilidad: contraste WCAG AA (4.5:1 en texto normal), áreas táctiles de 44 px o más, foco visible, `prefers-reduced-motion`.
- Iconografía SVG de línea consistente (`viewBox 0 0 24 24`, `stroke="currentColor"`), hoja decorativa y logo placeholder tipográfico.
- Microinteracciones sutiles: fade-in al hacer scroll, hover y focus, acordeón.
- Microcopy en español de Colombia, con trato de "tú".
- Wireframes ASCII por sección.
- Revisión de diseño: compara `index.html` contra `DISENO.md` y entrega correcciones medibles (px, hex, ms).

**Reglas:**
- Usa solo el contenido aprobado (ver "Contenido" más abajo). No inventa textos, cifras, testimonios ni credenciales.
- Sin fotos clínicas ni rostros de pacientes. Usa íconos, gráficos y placeholders marcados.
- Máximo dos familias tipográficas: una serif para títulos (Cormorant Garamond) y una sans para texto.
- Paleta base: azul marino `#0E3A56`, turquesa `#1E9AA0`, celeste claro `#EAF4F8`, blanco `#FFFFFF`.

---

## Agente 2: Desarrollador web (frontend + capa de integración)

**Rol:** construye `index.html` a partir de `DISENO.md` y del contenido aprobado. También cubre la capa de integración: embed de Tally, enlaces de WhatsApp, parámetros de URL y despliegue.

**Archivos a su cargo:** `index.html` (y `assets/og.jpg` si se exporta).

**Skills:**
- *Frontend:* HTML5 semántico (`header`, `main`, `section`, `nav`, `footer`) con jerarquía de encabezados correcta. CSS moderno (variables, grid, flexbox, `clamp()`, mobile-first). JavaScript vanilla: `IntersectionObserver`, scroll suave, `URLSearchParams`, `encodeURIComponent`.
- *Accesibilidad:* acordeón con `<button>`, `aria-expanded` y `aria-controls`, usable con teclado. `alt` en imágenes, foco visible y `prefers-reduced-motion`.
- *Rendimiento:* Lighthouse móvil de 90 o más, sin imágenes pesadas.
- *SEO y Open Graph:* `title`, `description`, `og:title`, `og:description`, `og:image`, `twitter:card`.
- *Integración:* iframe de Tally con el script oficial, recarga dinámica del iframe y alternativa si no carga. Enlaces `wa.me` con mensaje prellenado y bien codificado (tildes, ñ, espacios). Atribución con `?src=`.
- *Despliegue:* GitHub Pages (repo, rama, carpeta raíz, Settings > Pages).
- *Calidad:* lista de pruebas manuales y comentarios en el código que marcan cada placeholder.

**Reglas:**
- Un solo `index.html`, sin frameworks ni dependencias que requieran instalación. Lo único externo permitido: Google Fonts y `https://tally.so/widgets/embed.js`.
- No cambia decisiones visuales sin consultar al diseñador (a través del orquestador).
- Placeholders siempre visibles y marcados con `[COMPLETAR]` o con un comentario `<!-- [COMPLETAR] ... -->`.

### Lógica de integración (contrato)

**Tally**
- iframe con URL base `[URL_TALLY]` (p. ej. `https://tally.so/embed/XXXXXX`) más `alignLeft=1&hideTitle=1&transparentBackground=1&dynamicHeight=1`.
- Campos ocultos llamados exactamente `curso` y `src`:
  - `curso`: "Inscribirme" en una tarjeta → scroll suave a `#inscripcion` y recarga del iframe con `&curso=<encodeURIComponent(nombre)>`. Desde cualquier otro botón, `curso` va vacío.
  - `src`: el valor de `?src=` de la página (p. ej. `instagram`). Si no viene, `src=directo`.
- Debajo del formulario: "¿Problemas para ver el formulario? Ábrelo aquí" (abre la URL de Tally en una pestaña nueva) y "Tus datos se usan solo para contactarte sobre los cursos de Kléos Vital."

**WhatsApp**
- Número: `[57XXXXXXXXXX]` (indicativo sin `+`).
- Mensaje general (hero, formulario, cierre, flotante, barra): "Hola, quiero información de los cursos de Kléos Vital".
- Mensaje por curso: "Hola, quiero información del curso de <Nombre del curso>".
- Si la URL trae `?src=valor`, se agrega " (vengo de valor)" al final del mensaje.
- Botón flotante discreto abajo a la derecha. Los botones grandes van solo en el hero, la sección del formulario y el cierre.

---

## Contenido aprobado (no inventar más)

- **Nombre:** Kléos Vital. **Lema:** "Educación que transforma tu práctica clínica". **Frase de impacto:** "Lleva tus conocimientos al siguiente nivel".
- **Descripción:** "En Kléos Vital creemos en una educación práctica, actualizada y con sentido clínico. Nuestros cursos están diseñados para que los profesionales de la salud adquieran y perfeccionen habilidades en procedimientos estéticos y terapias regenerativas, con un enfoque seguro, ético y basado en la evidencia."
- **Cita:** "La ciencia y la estética, cuando van de la mano, transforman vidas".
- **Frases de cierre:** "Tu crecimiento profesional también es parte del bienestar de tus pacientes." / "Más que un curso, es una experiencia de aprendizaje que impulsa tu carrera." / "Juntos por una medicina más humana, segura y estética." / "Tu vocación también merece formación de alto nivel" / "Porque la ciencia, la técnica y la ética... también se enseñan."
- **Beneficios (5):** Talleres 100% prácticos · Modalidad presencial · Grupos reducidos · Material de apoyo · Certificación de asistencia.
- **Cursos (7):**
  1. Toxina botulínica: manejo, dosis, anatomía y seguridad.
  2. Ácido hialurónico: técnicas, zonas, indicaciones y complicaciones.
  3. Bioestimuladores de colágeno: mecanismos de acción y protocolos.
  4. Plasma rico en plaquetas (PRP): obtención, aplicación y usos clínicos.
  5. Hilos de tensión y de colágeno: técnicas, tipos de hilos y zonas de aplicación.
  6. Sueroterapia básica y avanzada: protocolos, mezclas, indicaciones y seguimiento.
  7. Terapia neural: aplicaciones clínicas, puntos de inyección y abordaje integral.
  - Fechas y precios: `[COMPLETAR]`. Mientras no existan, mostrar "Próximas fechas: consúltalas por WhatsApp" y **no mostrar precio**.
- **Docentes (credenciales exactas, no agregar otras):**
  - Dr. Andrés Neira, Médico Estético. Experiencia en medicina estética y procedimientos mínimamente invasivos. Enfoque en resultados naturales, seguros y personalizados.
  - Dra. Erlinda Villarreal, Médica Funcional y Regenerativa, Magíster en Calidad de los Servicios de Salud. Experiencia en optimización de la salud, longevidad y bienestar integral.
  - Fotos: círculo con iniciales como placeholder; reemplazar por `img/neira.jpg` e `img/villarreal.jpg`.
- **Por qué elegir (5):** Médicos con experiencia clínica y docente · Enfoque práctico, con pacientes reales y supervisión directa · Técnicas y protocolos basados en evidencia · Fortaleces tu perfil profesional y amplías tus servicios · Inversión en tu futuro y en el de tus pacientes.

## Orden de secciones

1. Barra superior (logo + "Inscríbete" + "WhatsApp") · 2. Hero · 3. Quiénes somos + cita · 4. Propuesta de formación (5 beneficios) · 5. Cursos (7 tarjetas) · 6. Docentes · 7. ¿Por qué elegir esta formación? · 8. Cómo reservar tu cupo en 3 pasos · 9. Formulario `id="inscripcion"` + apoyo de WhatsApp · 10. Preguntas frecuentes (acordeón, 5 preguntas) · 11. Cierre ("Tu vocación también merece formación de alto nivel", dos botones y "Cupos limitados") · 12. Pie de página (logo, lema, Instagram `[@USUARIO]`, ciudad `[CIUDAD]`).

## Reglas globales (ambos agentes)

- No inventar testimonios, cifras, convenios, avales ni credenciales.
- La certificación es **"de asistencia"**. Nunca decir que es un título, un diplomado ni una certificación avalada por una entidad.
- No prometer resultados clínicos ni usar lenguaje exagerado. Es publicidad dirigida a profesionales de la salud.
- Lo que falte se deja como `[COMPLETAR]` visible o se resuelve con "consulta por WhatsApp".
- Tono profesional, sobrio y cálido. Español de Colombia, con trato de "tú".

## Placeholders pendientes

| Placeholder | Dónde |
|---|---|
| `[57XXXXXXXXXX]` número de WhatsApp | constante JS en `index.html` |
| `[URL_TALLY]` URL del embed | constante JS en `index.html` |
| `[@USUARIO]` Instagram | pie de página |
| `[CIUDAD]` | pie de página |
| Fotos de docentes | `img/neira.jpg`, `img/villarreal.jpg` |
| Logo definitivo | `assets/logo-kleos-vital.svg` |
| Fechas, horarios y precios | tarjetas de curso |
| `assets/og.jpg` (1200×630) | exportar desde `assets/og.svg` |
