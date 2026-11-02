# Plantilla «Aplicación y software» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **tecnológico**.
Una sola página para aplicaciones, programas y servicios en la nube. Todo en castellano de España, frases cortas,
sin jerga. El brief de diseño está en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa (incluida la lista `planes`); no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…). El degradado de marca es primario → acento; las bandas oscuras salen del color de texto y las suaves del primario mezclado con el fondo (`src/styles/global.css`).
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-texto`, `--fuente-titulos`, `--fuente-mono`, bandas `.banda-clara`, `.banda-suave`, `.banda-tinta` y `.banda-degradado`, botones píldora `.btn`, `.btn-sec` y `.btn-blanco`, cabecera `.cabecera--app` y pie `.pie--app`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las de relleno están en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Las fotos de partida se generan desde `fotos.json`.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial y nombre en texto.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`.
- `hero`: degradado a sangre con la foto fundida, titular enorme (`titulo` + `titulo_destacado`), dos botones, sellos (`items[].titulo`) y maqueta de la aplicación en CSS.
- `funciones`: rejilla 3×2 con icono (`items[]`: titulo, texto, icono).
- `producto`: fila 50/50 con la foto a sangre (`imagen`, `texto` en párrafos, `items[]` con check, `cta`).
- `sectores`: mosaico de fotos de borde a borde (`items[]`: titulo, texto, imagen).
- `proceso`: pasos en línea (`items[]`: titulo, texto, icono).
- `cifras`: banda en degradado con cifras enormes (`items[]`: titulo = cifra, texto). Sin cifras no se pinta.
- `planes`: columnas de precios (`planes[]`: nombre, precio, periodo, texto, incluye separado por «;», destacado, cta_texto; además `etiqueta_destacado`, `nota` y `cta`).
- `integraciones`: panel de piezas con icono (`items[]`: titulo, texto, icono; `cta`).
- `opiniones`: cita enorme y el resto en columnas (`testimonios[]`: texto, autor, cargo). Sin opiniones no se pinta.
- `preguntas`: acordeón `details/summary` (`preguntas[]`: pregunta, respuesta). Sin preguntas no se pinta.
- `cta`: banda en degradado con titular enorme y dos botones.
- `contacto`: banda partida, contacto directo en tinta y formulario `mailto` (`boton` = texto del botón).
- `texto`: diseño genérico para apartados nuevos (con `imagen`, fila 50/50 a sangre).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, fotos, precios**: solo en `site.yaml`. Precios siempre como cadena (`"3 €"`, `"Consultar"`). Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Varios valores en una cadena con «; » (`incluye: "Cuadrante; Fichaje"`). Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` importando `../layouts/Base.astro` y envolviendo el contenido en `<Base titulo="…" descripcion="…">…</Base>` (ejemplo: `src/pages/aviso-legal.astro`); enlázala en `site.yaml → menu`.
6. **Sección nueva**: un id propio en `site.yaml` con `tipo:` = el diseño de otra sección o `texto`. Solo si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` (con `seccion(id)`, banda a todo el ancho y que pinte bien con listas vacías). `src/pages/index.astro` no se toca.
7. **No tocar** `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base y salen solos de `site.yaml`. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro`, `alt` sacado del contenido (`altHero`, `altSeccion`, el `titulo` de la ficha), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral (`.contenedor`), bandas y fotos de borde a borde, botones de 44 px de alto como mínimo y sin scroll horizontal en móvil.
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.funciones.items` → `/funciones/<slug>/` (función).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/funciones/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).
