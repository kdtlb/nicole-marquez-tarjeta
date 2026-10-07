# Nicole Márquez — Tarjeta de presentación digital

Tarjeta de presentación de Nicole Márquez · Organización de Eventos (Tarija,
Bolivia). Misma línea visual que el sitio [nicolemarquez.com](https://nicolemarquez.com/)
—verde oliva, dorado y marfil—, pero es un proyecto aparte: no depende de
ningún archivo del sitio.

Publicada en <https://kdtlb.github.io/nicole-marquez-tarjeta/>.

## Estructura

```
├── index.html           # Página (estilos, textos ES/EN/FR/PT y script incluidos)
├── nicole-marquez.vcf   # Contacto para «Guardar contacto» (con foto)
└── assets/
    ├── logo.png, favicon.svg, apple-touch-icon.png
    ├── nicole.jpg       # Retrato (también es la vista previa al compartir)
    ├── portada.jpg      # Foto de cabecera, bajo un degradado oscuro
    ├── fonts/           # Cormorant Garamond, Jost y Marcellus (subconjunto latin)
    └── qrcode.min.js    # Generador de QR (Kazuhiko Arase, licencia MIT)
```

No hay compilación ni dependencias. Para verla en local:

```bash
python -m http.server 8000
```

y abrir <http://localhost:8000>.

## Cómo funciona

- **Guardar contacto** descarga `nicole-marquez.vcf`. En iPhone el enlace va
  sin el atributo `download` a propósito: así el teléfono abre directo la
  ficha de «Nuevo contacto» en vez de mandarla a Descargas.
- **Compartir tarjeta** abre el menú de compartir del teléfono; en equipos sin
  ese menú copia el enlace.
- **El código QR se dibuja solo** con la dirección desde la que se abre la
  tarjeta, así que sigue siendo correcto si se cambia de dominio. Abierta en
  local usa la dirección pública (`CANONICA` en el script de `index.html`).
  Lleva corrección de errores alta (H) para que el rombo dorado del centro no
  impida leerlo.
- **Idioma**: español por defecto. La elección se guarda con la misma clave
  que el sitio (`nm-lang`).

## Si cambia un dato de contacto

Hay que corregirlo en **dos archivos**: `index.html` y `nicole-marquez.vcf`.

La vCard tiene reglas propias: saltos de línea CRLF, líneas de 75 caracteres
como máximo (las de continuación empiezan con un espacio) y las comas del
texto escritas como `\,`. El `.gitattributes` evita que git cambie los saltos
de línea al subirla.

## Usar un subdominio propio (opcional)

Para publicarla en, por ejemplo, `tarjeta.nicolemarquez.com`:

1. En Cloudflare (DNS de nicolemarquez.com) crea un registro **CNAME**
   `tarjeta` → `kdtlb.github.io`, con la nube en **gris (solo DNS)**.
2. En **Settings → Pages** de este repositorio escribe `tarjeta.nicolemarquez.com`
   en *Custom domain* y activa *Enforce HTTPS* cuando aparezca.
3. Cambia `kdtlb.github.io/nicole-marquez-tarjeta/` por la nueva dirección en
   `index.html` (`canonical`, `og:url`, `og:image` y `CANONICA`).

Haz el paso 2 solo cuando el paso 1 ya esté hecho: si el dominio todavía no
existe, GitHub redirige a una dirección que no carga.
