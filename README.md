# Marisquería La Perla — Sitio web

Sitio one-page para **Marisquería La Perla**, una marisquería costera del Golfo en Lomas de Rosales, Tampico, Tamaulipas.

## Estructura del proyecto

```
La Perla/
├── marisqueria-la-perla.html   # Sitio completo (HTML + CSS + JS inline)
├── pulpo-la-perla (1).svg      # Ilustración completa del pulpo (footer)
├── pulpo-la-perla.png          # Versión PNG del pulpo (respaldo / favicon)
├── Pulpo Tentaculos svg/       # Tentáculos separados por posición
│   ├── Pulpo abajo.svg
│   ├── Completo.svg
│   ├── tentaculo 1 abajo.svg
│   ├── tentaculo 2 abajo.svg
│   ├── tentaculo 3 izquierda.svg
│   ├── tentaculo 4 derecha.svg
│   ├── tentaculo 5 abajo.svg
│   ├── tentaculo 6 arriba.svg
│   └── tentaculo 7 abajo.svg
├── guia-google-business-la-perla.md   # Guía para registrar en Google Business
├── package.json
├── .gitignore
├── AGENTS.md                   # Contexto para IDEs con IA (Antigravity, etc.)
└── README.md
```

## Cómo correrlo

El sitio es un único archivo HTML estático sin build step. Cualquier servidor estático sirve.

### Opción 1 — npm script

```bash
npm install      # solo la primera vez (instala serve)
npm run dev      # arranca en http://localhost:3000
```

Luego abre **http://localhost:3000/marisqueria-la-perla.html**.

### Opción 2 — sin Node

Doble click en `marisqueria-la-perla.html` o abre con cualquier navegador. Funciona en `file://`.

### Opción 3 — Python

```bash
python -m http.server 3000
```

## Decisiones de diseño

- **Single-file HTML**: CSS y JS están inline dentro del HTML. Es intencional — facilita el despliegue (un solo archivo) y la edición rápida para un sitio de esta escala.
- **Sin framework**: vanilla HTML/CSS/JS. No hay React, Vue, build step ni dependencias en runtime.
- **Tipografía**: DM Serif Display + Outfit + DM Mono (Google Fonts).
- **Paleta**: azul marino profundo, bronce/dorado, crema cálida, terracota como acento.
- **Tentáculos animados**: 10 instancias SVG posicionadas en bordes del viewport (top/bottom/left/right) que reaccionan al cursor con efecto wobble/jelly. Solo se muestran 2 a la vez (los de la sección activa).
- **SEO**: meta tags geo, Open Graph, y Schema.org JSON-LD tipo Restaurant con dirección y horarios verificados.

## Información verificada del negocio

| Campo | Valor |
|-------|-------|
| Nombre | Marisquería La Perla |
| Dirección | Av. Miguel Hidalgo Esq. Regiomontana 202, Col. Lomas de Rosales |
| Ciudad | Tampico, Tamaulipas, México |
| Código postal | 89106 |
| Coordenadas | 22.2654 N, 97.8724 W |
| Google Maps | https://maps.app.goo.gl/e81KN7V3GEDCG5C76 |
| Horarios | Mar-Jue 13:00-22:00 · Vie-Sab 13:00-23:30 · Dom 13:00-19:00 · Lun cerrado |

> **Pendiente de verificar y reemplazar placeholders**: teléfono (`+52 833 300 0000`), email (`hola@marisquerialaperla.mx`), URLs de Instagram y Facebook.

## Personalización rápida

| Quiero cambiar | Busca en `marisqueria-la-perla.html` |
|---|---|
| Datos de contacto | sección `id="visita"` (~línea 1167) y `<footer>` (~línea 1210) |
| Platos del menú | sección `id="menu"` (~línea 1045) — bloques `<article class="plato">` |
| Horarios | `<ul class="horarios-list">` |
| Colores | `:root` al inicio del `<style>` |
| Tentáculos (posiciones) | bloque `/* ============ TENTACULOS POR SECCION ============ */` |

## Despliegue

Cualquier hosting estático: Netlify, Vercel, GitHub Pages, Cloudflare Pages, S3+CloudFront.

El archivo `marisqueria-la-perla.html` puede renombrarse a `index.html` para que sea la raíz.
