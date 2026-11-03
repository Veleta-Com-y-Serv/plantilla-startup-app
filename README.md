# Plantilla NoExpertise · Aplicación y software

Web de una página para aplicaciones, programas y servicios en la nube: degradado eléctrico a sangre, maqueta de la
aplicación hecha en CSS, funciones, planes de precios, integraciones y preguntas frecuentes.

- Sectores: software, app, startup, saas, tecnologia. Estilo: tecnológico. Plan mínimo: presencia.
- Secciones: hero, funciones, producto, sectores, proceso, cifras, planes, integraciones, opiniones, preguntas, cta, contacto (y `texto` para apartados nuevos).
- Ejemplo: «Cuadra», aplicación ficticia de turnos y fichaje hecha en Málaga.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas`. Sin la clave, una sola página larga.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; fotos de partida en `fotos.json`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`.

## Campos propios

| Sección | Campo | Qué es |
|---|---|---|
| `hero` | `titulo_destacado` | Final del titular, en línea aparte y resaltado |
| `hero` | `items[].titulo` | Sellos cortos bajo los botones («Sin permanencia») |
| `planes` | `planes[]` | `nombre, precio, periodo, texto, incluye` (separado por «;»), `destacado`, `cta_texto` |
| `planes` | `etiqueta_destacado`, `nota` | Etiqueta del plan destacado y nota bajo los planes |
| `opiniones` | `testimonios[].cargo` | Quién es el autor de la opinión |
| `contacto` | `boton` | Texto del botón del formulario |

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) hechas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.funciones.items` con `detalle` tiene su página en `/funciones/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
