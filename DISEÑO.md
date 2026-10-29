# Aplicación y software: brief de diseño

Plantilla `startup-app` creada el 29/10/2026 a partir de `una-pagina` con `php artisan plantillas:nueva` y
rediseñada entera. Este fichero se queda en el repo: es lo que lee quien (persona o agente) la rediseñe después.

## Brief

- **Para quién**: empresas que venden una aplicación, un programa o un servicio en la nube (sectores `software`,
  `app`, `startup`, `saas`, `tecnologia`). Quien entra quiere saber en diez segundos qué resuelve, cuánto cuesta y
  cómo probarlo.
- **Qué tiene que conseguir**: que pidan la prueba gratis o una demostración (formulario `mailto`, botón de cabecera).
- **Tono y estilo** (`tecnologico`): eléctrico, claro y directo. Sí: páginas de producto con degradados vivos,
  maquetas de pantalla y bandas a todo el ancho. No: la caja centrada estrecha con tarjetas blancas ni el hero de
  `una-pagina` (centrado, oscuro, imagen con halo).
- **Paleta de ejemplo**: primario `#2f54ff` (azul eléctrico), acento `#8a3ffc` (violeta), fondo `#f6f7ff`
  (blanco azulado), texto `#0e0c2b` (tinta). Derivados en `global.css`: `--degradado` (primario → acento),
  `--degradado-hondo` (el mismo con un 16-20 % de tinta, para que el texto blanco aguante colores claros),
  `--tinta` (bandas oscuras), `--suave` (bandas claras teñidas) y `--linea`. Aguanta que el cliente cambie los cuatro.
- **Tipografía**: del sistema. Titulares en sans de sistema a 850-900 con interletrado muy cerrado (−0,04 a
  −0,05 em); hero de 2,6 a 6,6 rem; antetítulos y datos en monoespaciada (`--fuente-mono`) en mayúsculas
  espaciadas con una línea en degradado delante.
- **Forma**: botones píldora de 48 px de alto, esquinas de 1,5 rem (`--radio`), iconos en cuadros de degradado,
  rejilla de líneas finas de fondo en las bandas de degradado.
- **Ritmo de bandas**: degradado (hero) → clara (funciones) → 50/50 con foto a sangre (producto) → tinta con
  mosaico a sangre (para quién) → clara (proceso) → degradado (cifras) → suave (planes) → tinta (integraciones) →
  clara (opiniones) → suave (preguntas) → degradado (cta) → partida tinta/clara (contacto) → pie en tinta con el
  nombre gigante en degradado.
- **Cabecera**: fija a todo el ancho; transparente sobre el hero y sólida al bajar (script pequeño en línea; sin
  JavaScript, siempre sólida). Menú móvil `details/summary`.

## Apartados

| id | Qué enseña | Lista propia |
|---|---|---|
| `hero` | Degradado a sangre con la foto fundida, titular enorme con final resaltado, dos botones, sellos y maqueta CSS (ventana con cuadrante de turnos y móvil con botón de fichar). Sube por debajo de la cabecera si abre la página | `items` (titulo) |
| `funciones` | Rejilla 3×2 separada por líneas finas, sin tarjetas, con número e icono | `items` (titulo, texto, icono) |
| `producto` | Fila 50/50: foto a sangre a la izquierda con un anillo de color, texto y checks a la derecha | `items` (titulo, texto) |
| `sectores` | Mosaico de fotos de borde a borde (1, 2 o 3 columnas) con velo y título | `items` (titulo, texto, imagen) |
| `proceso` | Pasos en línea con número monoespaciado en degradado | `items` (titulo, texto, icono) |
| `cifras` | Banda en degradado con cifras de 6 rem | `items` (titulo, texto) |
| `planes` | Columnas pegadas que llenan el ancho; la destacada en degradado | `planes` (nombre, precio, periodo, texto, incluye, destacado, cta_texto) |
| `integraciones` | Titular fijo y panel de piezas con icono | `items` (titulo, texto, icono) |
| `opiniones` | Cita enorme con comilla gigante y el resto en columnas | `testimonios` (texto, autor, cargo) |
| `preguntas` | Acordeón en filas con «+» en círculo de degradado | `preguntas` (pregunta, respuesta) |
| `cta` | Banda en degradado de 70 svh con anillos y titular de 7 rem | — |
| `contacto` | Banda partida: contacto directo en tinta y formulario en claro | — |
| `texto` | Genérico: titular y párrafos; con foto, fila 50/50 a sangre | `items` (titulo, texto, icono) |

## Fotos (`fotos.json`, 8)
Portada (mostrador de cafetería al atardecer con un móvil encendido, sin texto), producto (manos con un móvil,
sin caras) y seis sectores (restaurante, tienda, clínica, taller, gimnasio, hotel), todas sin personas
reconocibles, sin rótulos ni logotipos. La de portada va fundida en el degradado: cualquier foto sirve.

## Qué no hacer
- Nada de secciones encajonadas en una columna estrecha ni tarjetas blancas flotando sobre gris.
- Nada de capturas de pantalla reales en la maqueta: es CSS y solo lleva el nombre del negocio.
- Nada de cifras ni precios en los componentes: todo sale de `site.yaml`.
