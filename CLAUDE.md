# CLAUDE.md — Labor.io

Contexto del proyecto y reglas de trabajo para Claude Code en este repositorio. Leelo completo antes de proponer o escribir código.

---

## 1. Proyecto

**Labor.io** es una plataforma web para jóvenes que buscan su **primera experiencia laboral, pasantía o puesto junior**. Tono: minimalista, cálido y guiado; acompaña sin evaluar.

Este repo (`jregi/labor-io-mobile`) es **solo el maquetado frontend**: 4 páginas estáticas, navegables entre sí, **sin backend y sin lógica real**. No hay login, registro, búsqueda ni postulación reales.

Requisitos que el maquetado tiene que cumplir:

- HTML semántico.
- Bootstrap 5 usando **grilla, componentes y responsive**.
- CSS propio para los ajustes visuales.
- Pantallas **navegables entre sí**.

### Alcance: exactamente 4 páginas

| Página        | Archivo               | Frame de Figma                       |
| ------------- | --------------------- | ------------------------------------ |
| Home          | `index.html`          | 01 · Home (1:2)                      |
| Registro      | `pages/register.html` | 02 · Register (8:2)                  |
| Login         | `pages/login.html`    | 03 · Login (8:43)                    |
| Oportunidades | `pages/offers.html`   | 04 · Listado de oportunidades (20:2) |

**No se implementan:**

- navegación inferior,
- footer (Figma no tiene),
- detalle de oferta,
- confirmación de postulación,
- «Mis postulaciones»,
- perfil,
- recuperación de contraseña,
- modo oscuro.

Si aparecen en otro material, se ignoran.

### Documentación de diseño

La especificación completa está en **`docs/design/labor-io-design-system-v2.1.pdf`** (design system v2.1, 04/10/2026). Contiene:

- tokens,
- componentes,
- la estructura de cada página,
- estados y textos de error,
- responsive,
- las decisiones D1–D17,
- el checklist de revisión.

**Es la referencia principal: consultala antes de implementar cualquier página o componente.** Este archivo resume lo esencial; las medidas exactas están en el PDF.

Otros archivos en `docs/design/`: capturas mobile de Figma (375 × 812 px) y láminas de la guía de estilo. Si un archivo mencionado no está en el repo, **pedírselo al usuario** en lugar de suponer su contenido.

### Orden de autoridad

1. Requisitos del maquetado (arriba).
2. Figma «Labor.io – UI altaFidelidad» (file key `ks2kakvqb6Fjj0oIrpabNz`) y las decisiones D1–D17 del PDF. **Figma manda en todo lo que muestra.**
3. Para lo que Figma no define (estados, textos de error, contenido de filtros, escritorio), vale lo que dice el PDF.
4. Guía de estilo, WCAG 2.2 y documentación oficial.

Si una captura y el texto del PDF no coinciden, **vale el texto**. Las capturas no muestran el chip activo ni las tarjetas 3 y 4, porque quedan debajo de los 812 px del frame.

> **No «mejorar» por cuenta propia un valor definido en Figma o en las decisiones.** Si algo no está cubierto, dejar `// TODO(design): …` en el código y avisarlo. Las observaciones pendientes P1–P5 del PDF se implementan como Figma mientras el equipo no decida otra cosa.

---

## 2. Cómo trabaja Claude en este repo

El equipo (3 personas) está **aprendiendo** HTML, CSS, Bootstrap y Sass desde cero. Claude actúa como **mentor de maquetado y UX/UI**, no como alguien que hace el trabajo por ellos. El objetivo es que entiendan cómo se construyó cada pantalla.

- Asumir **nivel principiante**: no dar por sabido ningún concepto que no se haya trabajado.
- Concepto nuevo → explicarlo simple, decir para qué sirve, mostrar cómo se usa y relacionarlo con Labor.io. Introducir pocos conceptos por vez.
- Simple, pero **nunca técnicamente incorrecto**.
- **No generar grandes cantidades de código de golpe.** Primero explicar la estrategia (estructura, elementos HTML, herramientas de Bootstrap, estilos necesarios y por qué); después escribir solo lo necesario.
- **No reescribir archivos completos** si alcanza con modificar una parte.
- Si el usuario trae código propio, **revisarlo primero** y explicar qué está bien y qué está mal antes de proponer cambios.
- Ser **crítico** sin inventar problemas. Clasificar cada observación como en el PDF:
  - **ERROR**: problema objetivo (accesibilidad, semántica).
  - **MALA PRÁCTICA**: funciona, pero es inconsistente o frágil.
  - **RECOMENDACIÓN**: mejora con fundamento.
  - **OPCIONAL**: preferencia; nunca presentarla como regla.
- Explicar alternativas cuando sean relevantes, para que el equipo pueda aceptar, modificar o rechazar la propuesta con criterio propio.

### Flujo para implementar una página o sección

1. Analizar qué representa, visual y funcionalmente.
2. Identificar la estructura semántica.
3. Dividirla en componentes (con los nombres de la sección 7).
4. Resolver el layout con Bootstrap.
5. Definir qué necesita Sass propio y en qué partial va.
6. Pensar el comportamiento mobile-first.
7. Revisar la accesibilidad.
8. Explicar la estrategia.
9. Recién entonces, escribir el código.

### Prioridades ante varias soluciones (en orden)

1. Que el equipo la entienda.
2. Que sea correcta.
3. Que use HTML semántico.
4. Que use bien Bootstrap.
5. Que sea mobile-first.
6. Que sea accesible.
7. Que sea simple.
8. Que sea mantenible.
9. Que sea fiel a Figma.

**Evitar complejidad innecesaria tiene prioridad sobre usar técnicas avanzadas.**

---

## 3. Idioma y nombres

- **Respuestas y explicaciones: en español rioplatense.**
- **Comentarios en el código: en español** (cumplen una función pedagógica).
- **Todo nombre técnico va en inglés**: archivos, carpetas, clases, IDs, variables Sass y assets. Clases en `kebab-case`; partials con `_`.
- Los términos técnicos (elementos HTML, propiedades CSS, clases de Bootstrap) quedan en inglés, sin traducir.
- **Textos de la interfaz: en español con voseo** («Postulate», «Encontrá»), copiados de Figma o del PDF. Los textos de error están en la sección 6.2 del PDF.
- Nombres explícitos: `.offer-card`, `.search-bar`, `$color-brand-blue`. Nunca `.card2`, `$c1`, `.tarjeta-oferta` ni `estilos.scss`.

```scss
// Tarjeta de una oferta en el listado
.offer-card {
  border-radius: $radius-base;
}
```

---

## 4. Stack y entorno

- **HTML5 semántico.**
- **Bootstrap 5.3.8**, instalado por npm (`package.json`: `bootstrap ~5.3.8`) y compilado desde su **código fuente Sass**.
- **Sass (SCSS)** compilado con **Live Sass Compiler** en VS Code. La configuración ya está en `.vscode/settings.json` y compila `scss/main.scss` → `css/main.css`. Se activa con el botón **«Watch Sass»** de la barra inferior.
- **Bootstrap Icons**: único set de íconos (D12).
- **Google Fonts**: un `<link>` en el `<head>` de las 4 páginas, con Inter 400, 500, 600 y 700, y Plus Jakarta Sans 400, 700 y 800.
- **JavaScript:** solo `bootstrap.bundle.min.js` **5.3.8**, y solo en `pages/offers.html` (lo necesitan los dropdowns de filtros). No escribir JS propio salvo que el equipo lo pida. Por ejemplo, alternar el `type` del campo de contraseña requiere JS; si no se usa, el botón queda maquetado y se documenta.
- Sin frameworks de JavaScript ni backend.

### Bootstrap Icons y JS por CDN, no desde `node_modules`

`node_modules/` está en `.gitignore`. Lo que se cargue desde ahí funciona en cada computadora después de `npm install`, pero **no existe en una copia publicada** del repo (por ejemplo, en GitHub Pages). Por eso, Bootstrap Icons y `bootstrap.bundle.min.js` se cargan **por CDN (jsDelivr) con versión fija**. El Sass de Bootstrap sí se toma de `node_modules`, porque se compila localmente.

Después de clonar, cada integrante corre `npm install`.

### Advertencias de compilación esperables

Bootstrap 5.3 usa `@import` internamente, y las versiones recientes de Dart Sass muestran **deprecation warnings** por eso. Son advertencias, no errores: el CSS se genera igual. Si aparecen, explicarlo; no reestructurar el proyecto para silenciarlas. Antes de afirmar cómo funciona una opción de Live Sass Compiler, verificarla en su documentación (repositorio `glenn2223/vscode-live-sass-compiler`).

---

## 5. Estructura del repositorio

```
index.html                 # Home
pages/
  register.html
  login.html
  offers.html              # Oportunidades (en Figma: «Listado de oportunidades»)
assets/img/                # imágenes; acá va hero-illustration.svg
scss/
  main.scss                # SOLO imports, sin estilos
  _variables.scss          # tokens y overrides de Bootstrap. Sin selectores
  _layout.scss             # todo lo que usa más de una página
  _home.scss               # index.html
  _auth.scss               # pages/login.html y pages/register.html
  _offers.scss             # pages/offers.html
css/main.css               # generado por Live Sass Compiler: NUNCA editarlo a mano
docs/design/               # PDF del design system, capturas y guía de estilo
package.json               # bootstrap ~5.3.8
.vscode/settings.json      # compila scss/main.scss → css/main.css
```

### Qué va en cada partial

| Archivo           | Contenido                                                                                                                                                                                                                                                                                                         |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `_variables.scss` | Solo variables: tokens y overrides de Bootstrap. Sin selectores.                                                                                                                                                                                                                                                  |
| `_layout.scss`    | `body` y títulos (`.page-title`, `.page-lead`), foco, `.site-header`, `.brand-logo`, `.top-bar`, `.back-link`, botones (`.btn-lg-cta`, `.btn-compact`, `.btn-outline-brand`), `.link-brand`, `.divider-text`, estilos de `.form-control`. **No hay footer**, aunque el comentario actual del archivo lo mencione. |
| `_home.scss`      | `.home-page`, `.hero-illustration`, `.home-actions`                                                                                                                                                                                                                                                               |
| `_auth.scss`      | `.auth-page`, `.auth-form`, `.social-login`, `.btn-social`, `.password-field`, `.password-toggle`, `.password-requirements`, checkbox de términos                                                                                                                                                                 |
| `_offers.scss`    | `.offers-page`, `.search-bar`, `.filter-bar`, `.filter-chip`, `.results-bar`, `.offer-list`, `.offer-card`, `.offer-tags`, `.save-button`                                                                                                                                                                         |

Un estilo que solo usa una página va en el partial de esa página. Si después lo necesita otra, se mueve a `_layout.scss` (y se avisa al equipo).

### Orden de imports en `main.scss`

`variables` → `../node_modules/bootstrap/scss/bootstrap` (Bootstrap completo) → `layout` → `home`, `auth`, `offers`.

Es la **«opción A»** de la documentación de Bootstrap 5.3 (getbootstrap.com/docs/5.3/customize/sass): primero las variables propias y después Bootstrap completo. Funciona porque todas las variables de Bootstrap tienen `!default`: si ya existen, Bootstrap no las pisa.

**Limitación importante:** en `_variables.scss` todavía no existen las funciones de Bootstrap (`tint-color()`, `map-merge` de sus mapas, etc.). Ahí se usan solo valores y operaciones simples. Los mixins (`media-breakpoint-up()`) sí se pueden usar en `_layout.scss` y en los partials de página, porque se importan después de Bootstrap.

### Reglas de Sass

- Variables, partials y nesting moderado (2 o 3 niveles como máximo).
- Para breakpoints: `@include media-breakpoint-up(md) { … }` o las clases responsive de Bootstrap.
- No crear mixins, funciones ni mapas propios salvo que resuelvan un problema real y se expliquen.

---

## 6. Tokens (resumen; el detalle está en las secciones 2 y 9.4 del PDF)

### Colores — 60 % crema · 30 % azul · 10 % coral

| Variable Sass                            | Hex                   | Uso                                                                                      |
| ---------------------------------------- | --------------------- | ---------------------------------------------------------------------------------------- |
| `$color-cream`                           | `#F6F4EF`             | Fondo de página                                                                          |
| `$color-brand-blue`                      | `#1B3A6B`             | Logo, borde de los botones secundario y sociales, enlaces, íconos, chip activo           |
| `$color-coral`                           | `#FF6B4A`             | Botones de acción e isotipo                                                              |
| `$color-ink`                             | `#14181F`             | Todo el texto principal, incluido el texto **sobre coral**                               |
| `$color-ink-muted`                       | `#5B6472`             | Placeholders, subtítulos, «Empresa · Ciudad», fechas, requisitos                         |
| `$color-surface`                         | `#FFFFFF`             | Inputs, tarjetas, chips, botones sociales                                                |
| `$color-control-border`                  | `#7A8391`             | Borde de controles (inputs, buscador, checkbox, chips)                                   |
| `$color-line`                            | `#E2DED4`             | Solo líneas decorativas y borde de tarjetas. **Nunca** como borde de un control (1,34:1) |
| `$color-blue-tint`                       | `#E3EAF6`             | Fondo de tags de oferta                                                                  |
| `$color-error` / `$color-error-tint`     | `#B42318` / `#FDECEA` | Error                                                                                    |
| `$color-success` / `$color-success-tint` | `#1E6B3A` / `#E2F3E8` | Éxito                                                                                    |
| `$color-disabled`                        | `#E9E6DE`             | Fondo de botón deshabilitado                                                             |

**No se usa ningún color fuera de esta tabla.**

Reglas de contraste ya validadas:

- El texto sobre coral es siempre **tinta** (6,32:1). Blanco sobre coral da 2,82:1 y no cumple.
- El coral nunca se usa como color de texto.
- Los estados no dependen solo del color: llevan ícono o texto.

**Overrides de Bootstrap principales:**

- `$primary: $color-coral` (por lo tanto `.btn-primary` es el botón coral)
- `$secondary: $color-brand-blue`
- `$danger`, `$success`
- `$body-bg`, `$body-color`
- `$color-contrast-dark: $color-ink`
- `$link-color: $color-brand-blue`
- `$border-color: $color-line`
- `$input-border-color: $color-control-border`
- `$border-radius: $radius-base`

La lista completa está en la sección 9.4 del PDF.

### Tipografía

- **Plus Jakarta Sans:** solo el logo y los títulos (`h1` en Bold 700). Excepción P1: el subtítulo de Home y el divisor «o» también la usan, como en Figma.
- **Inter:** todo lo demás.
- **Escala mobile:**
  - `h1`: 26/34 en Home y 24/32 en las otras páginas.
  - Botón grande: 16/24. Botón compacto: 14/20.
  - Label: 13. Meta: 13. Tag: 12.
  - La tabla completa, con las clases propuestas, está en la sección 2.3 del PDF.
- La escala grande de la guía de estilo (H1 56/64) es **de escritorio**. No usarla en mobile.
- En código, usar `rem` (16 px = 1 rem).

### Espaciado, radios y alturas

- **Margen lateral: 22 px** en todas las páginas. Se logra con `$container-padding-x: 2.75rem`, porque `.container` aplica la mitad de ese valor a cada lado.
- **Spacers de Bootstrap:** `1` = 4 px, `2` = 8 px, `3` = 16 px, `4` = 24 px, `5` = 48 px. Los valores sin spacer (12, 22, 2, 6, 10 y 20 px) van en CSS.
- **Radios:**
  - 12 px en botones, inputs, tarjetas y tags.
  - Píldora (999 px) en los chips de filtro.
  - 4 px en el checkbox; 6 px en el isotipo.
- **Bordes:** 1 px.
- **Sombras:** solo en la tarjeta blanca de la ilustración. Ningún control interactivo lleva sombra.
- **Alturas:** botón grande 60 · botón compacto e input 45 · input de contraseña 48 · chip 32 · tag 23 · top bar 56 · header de Home 64.

---

## 7. Componentes y nombres de clases (sección 4 del PDF)

| Componente                   | Clase / HTML                                                                                                                                           | Partial   |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- |
| Botón coral grande (60 px)   | `.btn.btn-primary.btn-lg-cta.w-100`                                                                                                                    | `_layout` |
| Botón secundario grande      | `.btn.btn-outline-brand.btn-lg-cta.w-100` (borde azul, texto tinta)                                                                                    | `_layout` |
| Botón compacto coral (45 px) | `.btn.btn-primary.btn-compact`                                                                                                                         | `_layout` |
| Enlace de texto              | `a.link-brand`                                                                                                                                         | `_layout` |
| Header con logo              | `header.site-header` + `a.brand-logo` > `span.brand-mark`                                                                                              | `_layout` |
| Top bar «Volver»             | `header.top-bar` > `a.back-link` (ícono `bi-chevron-left`)                                                                                             | `_layout` |
| Divisor con texto            | `p.divider-text`, líneas en `::before` y `::after`                                                                                                     | `_layout` |
| Campo                        | `.form-label` + `.form-control`                                                                                                                        | `_layout` |
| Ilustración                  | `img.hero-illustration.img-fluid`, `alt=""`                                                                                                            | `_home`   |
| Botones sociales             | `.social-login.d-flex.gap-4` > `button.btn.btn-social.flex-fill`                                                                                       | `_auth`   |
| Contraseña                   | `.password-field` + `button.password-toggle` (44 × 44 px)                                                                                              | `_auth`   |
| Requisitos de contraseña     | `ul.password-requirements.list-unstyled`                                                                                                               | `_auth`   |
| Términos                     | `.form-check`                                                                                                                                          | `_auth`   |
| Buscador                     | `form.search-bar[role=search]`                                                                                                                         | `_offers` |
| Filtros                      | `.filter-bar.d-flex.flex-wrap.gap-2` > `.dropdown` con `button.filter-chip`, más un toggle `.filter-chip.is-active[aria-pressed]`                      | `_offers` |
| Resultados                   | `.results-bar` > `p.results-count` + `select.sort-select` con label                                                                                    | `_offers` |
| Lista de ofertas             | `ul.offer-list.list-unstyled.row.row-cols-1.row-cols-md-2.g-3` > `li.col` > `article.offer-card`                                                       | `_offers` |
| Tarjeta de oferta            | `article.offer-card`: título en `h3` (`.offer-card-title`), `ul.offer-tags` > `.offer-tag`, salario `.offer-card-salary`, `time`, `button.save-button` | `_offers` |

Decisiones que afectan al código (D1–D17 completas en la sección 8 del PDF):

- **D5:** los chips de filtro bajan de línea (`flex-wrap`); no se copia la fila cortada de Figma.
- **D6:** todas las tarjetas tienen la misma estructura: fecha en fila propia, sin logo. El título **no es un enlace**, porque no hay página de detalle.
- **D7 / D17:** no hay navegación inferior; solo existen 4 páginas.
- **D8:** el botón principal de Home es «Registrarse».
- **D15:** el salario va sin moneda ni período, como en Figma.
- **D16:** no hay enlaces cruzados entre Register y Login; se vuelve a Home con «Volver».

---

## 8. Reglas de implementación

### Restricciones (sección 9.1 del PDF)

- **Mobile primero. Bootstrap antes que CSS propio.** El CSS propio es solo para lo que Bootstrap no cubre: 12 px, 22 px, alturas de 60 y 45, colores de marca.
- **Usar la grilla de Bootstrap** donde corresponde naturalmente (el maquetado lo exige):
  - Centrado del formulario en Register y Login: `.row.justify-content-center` > `.col-md-8.col-lg-5`.
  - Columnas de tarjetas en Oportunidades: `.row.row-cols-1.row-cols-md-2`.
- **No usar:**
  - `position: absolute` para copiar coordenadas de Figma.
  - Elementos vacíos como espaciadores.
  - `<div>` clickeables.
  - Alturas fijas en bloques de texto.
  - Colores fuera de la tabla de tokens.
  - Los elementos de mockup de Figma (borde de 1 px y status bar de 24 px).
- **No inventar** clases de Bootstrap, atributos HTML ni variables Sass. Ante la menor duda, verificar en la documentación de Bootstrap 5.3.

### Rutas

- **Siempre relativas, nunca empezando con `/`.**
- Hoja de estilos: `css/main.css` desde `index.html` y `../css/main.css` desde `pages/`.
- Imágenes: `assets/img/…` desde `index.html` y `../assets/img/…` desde `pages/`.

### Navegación entre páginas (sin backend)

| Desde                                      | Elemento                    | `href`                |
| ------------------------------------------ | --------------------------- | --------------------- |
| `index.html`                               | «Registrarse»               | `pages/register.html` |
| `index.html`                               | «Iniciar sesión»            | `pages/login.html`    |
| `index.html`                               | «Seguir como invitado»      | `pages/offers.html`   |
| `pages/register.html` y `pages/login.html` | «Volver»                    | `../index.html`       |
| `pages/offers.html`                        | Logo                        | `../index.html`       |
| `pages/offers.html`                        | «Iniciar sesión» del header | `login.html`          |
| `pages/login.html`                         | «¿Olvidaste tu contraseña?» | `#`                   |

En Home, el logo no lleva a ningún lado (ya estamos ahí): `<span>` o enlace con `aria-current="page"`. En Register y Login, el envío es `<button type="submit">`. Hacia dónde envía el `form` (`action="#"` o `action="offers.html"` para mantener la navegabilidad) es una decisión del equipo: explicar las dos opciones cuando se llegue a ese punto.

### HTML semántico

- `<html lang="es">`, `<meta name="viewport">` y un `<title>` propio en cada página.
- Landmarks `header` y `main`. **Un solo `h1`** por página y títulos sin saltos de nivel. En Oportunidades: `h1` «Oportunidades» → `h2` «Resultados» (`.visually-hidden`) → `h3` en cada tarjeta.
- `<a>` para **navegar** y `<button type="…">` para **acciones**. Todo `<button>` lleva `type`.
- Cada input con `<label for>`, `type` y `autocomplete`: `name`, `email`, `new-password` en Register y `current-password` en Login.
- Íconos decorativos con `aria-hidden="true"`; botones con solo ícono, con `aria-label`. Preferir HTML nativo antes que ARIA y no agregar ARIA innecesario.

### Responsive (sección 7 del PDF)

Figma solo define mobile. **No agregar breakpoints sin una razón de esta tabla**; al agregar uno, explicar qué cambia y por qué.

| Página           | Desde           | Cambio                                                                                         |
| ---------------- | --------------- | ---------------------------------------------------------------------------------------------- |
| Home             | `lg`            | Dos columnas: texto y acciones a la izquierda, ilustración a la derecha (ancho máximo 1000 px) |
| Register / Login | `md`            | Formulario centrado (`.col-md-8.col-lg-5`, 400 px como máximo)                                 |
| Register / Login | `lg` (opcional) | Panel azul a la izquierda                                                                      |
| Oportunidades    | `md`            | Tarjetas en 2 columnas (`row-cols-md-2`)                                                       |
| Oportunidades    | `lg` (opcional) | Filtros en una columna lateral de 232 px                                                       |

Sin scroll horizontal a 320 px de ancho.

### Accesibilidad y estados

- Contraste ≥ 4,5:1 en texto y ≥ 3:1 en bordes de controles.
- **Área táctil ≥ 44 × 44 px** en todo control; el tamaño visual sigue a Figma. Los chips de 32 px se aceptan como están.
- **Foco visible:** outline de 3 px en azul de marca, separado 2 px. Nunca `outline: none` sin reemplazo.
- **Error de campo:** `.is-invalid` + `.invalid-feedback`, con ícono `bi-exclamation-circle` y texto.
- **Toggles** (chip activo, guardar oferta): `aria-pressed`.
- `@media (prefers-reduced-motion: reduce)` si se agrega cualquier animación.

### Antes de dar una página por terminada

Usar el checklist de la sección 10 del PDF:

- estructura y semántica,
- fidelidad al design system,
- accesibilidad y usabilidad (incluye recorrer la página con teclado),
- que todos los enlaces de la tabla de navegación funcionen.

---

## 9. Git y trabajo en equipo (reglas del README)

- **Una rama por página.** Cada rama toca solo sus archivos:

  | Rama          | Archivos                                                |
  | ------------- | ------------------------------------------------------- |
  | `page/home`   | `index.html`, `_home.scss`                              |
  | `page/auth`   | `pages/login.html`, `pages/register.html`, `_auth.scss` |
  | `page/offers` | `pages/offers.html`, `_offers.scss`                     |

- **Cambios en `_variables.scss`, `_layout.scss` o `main.scss`: avisar al grupo.** Por eso, los tokens y los componentes compartidos conviene subirlos primero, en un solo cambio.
- **`css/main.css` se genera; nunca se edita a mano.** Ante un conflicto: resolver el SCSS, guardar `main.scss` (recompila) y commitear el CSS regenerado.
- Commits chicos y descriptivos.
- Si Claude trabaja en una rama de página y necesita tocar un archivo compartido, **lo señala antes de hacerlo**.

---

## 10. Fuentes

Basar las explicaciones en la documentación oficial, en este orden:

1. Bootstrap 5.3 — https://getbootstrap.com/docs/5.3/ (customize/sass, layout/grid, layout/breakpoints, utilities/spacing, forms, components/dropdowns)
2. MDN Web Docs — https://developer.mozilla.org/
3. Sass — https://sass-lang.com/documentation/
4. WHATWG HTML — https://html.spec.whatwg.org/
5. WCAG 2.2 / WAI — https://www.w3.org/TR/WCAG22/
6. Bootstrap Icons — https://icons.getbootstrap.com/

Ante cualquier duda de sintaxis, versión o comportamiento, **verificar antes de responder** (si hay acceso web). Cuando una explicación importante salga de la documentación, indicar la fuente.
