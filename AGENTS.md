# AGENTS.md — Contexto para IDEs con IA

Este archivo es para asistentes de IA (Antigravity, Cursor, Claude Code, etc.) que abran el proyecto. Lee esto antes de proponer cambios.

## Qué es este proyecto

Sitio one-page para **Marisquería La Perla**, restaurante de mariscos del Golfo en Tampico, Tamaulipas. Es un sitio de presentación con menú, espacio físico, datos de contacto y reservaciones.

## Stack

- HTML5 + CSS3 + JavaScript vanilla, **todo en un solo archivo** (`marisqueria-la-perla.html`)
- Sin framework, sin bundler, sin TypeScript, sin build step
- Fuentes vía Google Fonts (DM Serif Display, Outfit, DM Mono)
- Solo dependencia de desarrollo: `serve` (servidor estático local)

## Filosofía del código

- **Edita el HTML directamente**. CSS y JS están inline a propósito — no los extraigas a archivos separados. Lo más importante de este proyecto es la facilidad de despliegue como un único archivo.
- **No introduzcas un framework**. Si una funcionalidad requiere React/Vue/Svelte, propón primero la alternativa vanilla.
- **Sin npm packages en runtime**. Solo Google Fonts vía CDN. Cualquier propuesta de agregar una librería JS necesita justificación fuerte.
- **Respeta la accesibilidad existente**: `prefers-reduced-motion`, `aria-hidden` en decorativos, navegación por teclado, contraste de color.

## Arquitectura visual

```
┌─ <header> sticky con logo + nav + CTA reservar
├─ <section class="hero">         — Hero con titular grande
├─ <section id="casa">            — Historia del lugar
├─ <section id="menu">            — Grid de 6 platos
├─ <section id="espacio">         — Galería del local (cards de color)
├─ <section id="visita">          — Dirección + horarios + servicios + mapa estilizado
├─ <footer>                       — Brand + nav + contacto + redes
└─ Pulpo full SVG al fondo del footer (revela con scroll)
```

## Sistema de tentáculos animados (lo más complejo)

7 SVGs base de tentáculos (en `Pulpo Tentaculos svg/`) se renderizan como **10 instancias** distribuidas: 2 únicos por sección, en bordes distintos (arriba/abajo/izquierda/derecha).

**Comportamiento:**
- Solo los 2 tentáculos de la sección "más visible" tienen `.visible`. Los demás se ocultan suavemente.
- Cada tentáculo se mueve individualmente con interpolación lineal (lerp) y wobble continuo basado en `Math.sin`/`Math.cos`.
- Responden al cursor con fuerza, dirección y suavizado únicos por instancia.
- Se ocultan todos cuando el footer entra al viewport (para no competir con el pulpo grande).

**Por sección:**

| Sección | Tentáculos (bordes) |
|---------|---------------------|
| Hero    | arriba + abajo |
| Casa    | izquierda + abajo |
| Menu    | derecha + abajo |
| Espacio | izquierda + derecha |
| Visita  | derecha + abajo |

**z-index importante**: tentáculos están en `z-index: 5` porque las `<section>` tienen `position: relative; z-index: 2` (crea stacking context que oculta `fixed` elements).

## Datos sensibles del negocio

Estos están en el HTML como **placeholders** y deben verificarse antes de publicar:

- Teléfono: `+52 833 300 0000` (placeholder)
- Email: `hola@marisquerialaperla.mx` (placeholder)
- Instagram/Facebook URLs en footer: `#` (placeholder)

Estos están **verificados** desde Google Maps:

- Nombre: Marisquería La Perla
- Dirección completa: Av. Miguel Hidalgo Esq. Regiomontana 202, Col. Lomas de Rosales, Tampico, Tamaulipas, México 89106
- Coordenadas: 22.2654 N, 97.8724 W
- Google Maps URL: https://maps.app.goo.gl/e81KN7V3GEDCG5C76
- Horarios: ver `class="horarios-list"`

## Convenciones de texto

- Sin acentos en HTML (el cliente prefiere así para evitar problemas de codificación visual en algunos navegadores antiguos). Excepción: la palabra "Marisquería" del título y meta tags, donde sí se respeta.
- Voz: cálida, de barrio, sin hipérbole. Evitar palabras como "increíble", "único", "el mejor".
- Precios en pesos mexicanos sin decimales: `$260`, `$420`.

## Cómo correrlo

```bash
npm install
npm run dev
# abre http://localhost:3000/marisqueria-la-perla.html
```

O simplemente abre el `.html` con doble click.

## Tareas frecuentes y dónde tocarlas

- **Cambiar un plato del menú** → bloque `<article class="plato">` dentro de `id="menu"`
- **Cambiar horarios** → `<ul class="horarios-list">` dentro de `id="visita"`
- **Cambiar paleta de colores** → variables CSS en `:root`
- **Agregar/quitar tentáculo** → HTML (`<div class="tentaculo-borde">`) + CSS (`.tb-*` rules) + actualizar `data-section` y `data-edge`
- **Actualizar JSON-LD/SEO** → bloque `<script type="application/ld+json">` en `<head>`

## Qué no hacer

- No agregues archivos JS o CSS externos sin justificación. Mantén el sitio como un único HTML.
- No reescribas el sistema de tentáculos en un framework. Funciona y es performante.
- No quites los metadatos `geo.*` ni el JSON-LD — son críticos para SEO local.
- No cambies el nombre del archivo `marisqueria-la-perla.html` a `index.html` sin avisar — algunas referencias externas pueden apuntar a la URL completa.
