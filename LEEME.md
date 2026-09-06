# Web de Kálamos

Sitio estático: cinco páginas HTML, una hoja de estilo y una carpeta de imágenes. Sin frameworks, sin compilar nada, sin dependencias. Se abre con doble clic y se edita con cualquier editor de texto.

---

## 0. Antes de publicar: borrar los recuadros rojos

Hay **cuatro recuadros de aviso** repartidos por el sitio con texto que escribí yo de borrador. Se ven en pantalla a propósito, para que no se os pasen. Antes de publicar, escribid vuestra versión y borrad el bloque entero.

Búscalos por la clase `nota-borrador`:

| Archivo | Qué hay que reescribir |
|---|---|
| `index.html` | Los dos párrafos de «Quiénes somos» |
| `sobre.html` | Todo el texto de «Cómo nace» |
| `cajon-desastre.html` | La descripción del pódcast (me la he inventado a partir del nombre) |
| `actividades.html` | Las tres fichas de «Lo que viene» son inventadas |

Para encontrarlos todos de golpe, desde la carpeta del proyecto:

```bash
grep -rn "nota-borrador" *.html
```

Hay además dos cosas más que cambiar:

- **`el-pedante.html`**, botón «Leer el número en curso»: apunta a `https://elpedantedh.blogspot.com`, que es un ejemplo. Cambiadlo por la dirección real del blog cuando lo creéis.
- **`sobre.html`**, sección del equipo: comprobad que los nombres y los papeles son correctos.

---

## 1. Qué hay en la carpeta

```
index.html              Inicio
el-pedante.html         La revista
cajon-desastre.html     El pódcast
actividades.html        Talleres y encuentros
sobre.html              Quiénes somos y contacto

css/estilo.css          TODO el diseño está aquí
img/                    imágenes que usa la web
marca/                  originales en alta (logo, paleta, portada del pódcast)
```

---

## 2. Cómo está montado el diseño

El sitio imita vuestros carteles: **campos de color planos a sangre**, tipografía grande y nada de sombras ni esquinas redondeadas.

**Cada proyecto tiene su color de fondo**, y ese color es lo que le dice al visitante dónde está:

| Sección | Fondo | Clase CSS |
|---|---|---|
| Kálamos | crema `#E8E6C9` | `campo campo--crema` |
| El Pedante | negro tinta `#1A1A1A` | `campo campo--tinta` |
| Cajón Desastre | azul petróleo `#1B3A54` | `campo campo--petroleo` |
| Actividades | granate `#7A1015` | `campo campo--granate` |

Cada clase `campo--*` redefine por dentro los colores de texto, enlaces y botones. **Eso significa que para cambiar una sección de color solo hay que cambiar su clase**, y todo lo de dentro se recolorea solo. No hace falta tocar nada más.

Los seis colores son los de vuestra paleta (`marca/paleta-kalamos.png`), sin inventar ninguno. El único añadido es un gris cálido (`--gris`) para el texto secundario, elegido para que tenga contraste suficiente sobre la crema.

**Tipografías** (se cargan de Google Fonts, gratis):

- **Bodoni Moda** para los titulares. Es una serif de alto contraste con remates afilados, la más parecida a la palabra KÁLAMOS del logotipo.
- **Schibsted Grotesk** para el texto corrido.
- **IBM Plex Mono** para etiquetas, fechas y datos.

---

## 3. Cómo editar

**Cambiar un texto:** abre el `.html`, busca la frase, cámbiala. Ya está.

**Cambiar un color:** todos están arriba del todo de `css/estilo.css`, en el bloque `:root`. Cambia el valor una vez y cambia en todo el sitio.

**Añadir una actividad:** en `actividades.html`, copia un bloque `<article class="ficha">` entero y cambia los datos.

**Añadir un episodio del pódcast:** en `cajon-desastre.html` hay un bloque comentado con el hueco listo. Descoméntalo, duplica el `<article>` por cada episodio y pega dentro el `iframe` que te da Spotify en *Compartir → Insertar*.

**Ojo con la cabecera y el pie:** están copiados igual en las cinco páginas. Si cambias el menú o el correo, hay que cambiarlo en las cinco. Están marcados con un comentario `<!-- ===== CABECERA ... -->` para que se localicen rápido.

---

## 4. Publicarla gratis en Cloudflare Pages

Sin tarjeta y sin límite de visitas.

### Opción rápida (sin Git, dos minutos)

1. Crea una cuenta en [dash.cloudflare.com](https://dash.cloudflare.com).
2. Menú izquierdo → **Workers y Pages** → **Crear** → pestaña **Pages** → **Cargar recursos**.
3. Nombre del proyecto: `kalamos`.
4. Arrastra **el contenido** de esta carpeta (los `.html`, `css/`, `img/`, `marca/`), no la carpeta en sí.
5. **Implementar**. En un minuto está en `https://kalamos.pages.dev`.

Para actualizar: mismo sitio → **Crear implementación** → arrastra la carpeta otra vez.

### Opción con Git (recomendada si vais a tocarla a menudo)

1. Sube la carpeta a un repositorio de GitHub.
2. En Cloudflare: **Workers y Pages → Crear → Pages → Conectar a Git**.
3. Elige el repositorio. Cuando pregunte por la configuración de compilación, **déjalo todo vacío**: no hay comando de build y el directorio de salida es la raíz (`/`).
4. **Guardar e implementar**.

A partir de ahí, cada `git push` actualiza la web sola en unos treinta segundos. Además guarda todas las versiones anteriores, así que si algo se rompe se vuelve atrás con un clic.

---

## 5. Dominio propio, cuando lo decidáis

Ahora mismo la dirección es `kalamos.pages.dev`, que es gratis y funciona perfectamente.

Si algún día compráis un dominio (un `.es` cuesta unos 10-12 € al año en Dondominio, Namecheap o el propio Cloudflare):

1. En vuestro proyecto de Pages → **Dominios personalizados** → **Configurar un dominio**.
2. Escribid el dominio y seguid los pasos que os da.
3. El certificado de seguridad (el candado del navegador) lo pone Cloudflare solo y es gratis.

La dirección `.pages.dev` sigue funcionando después, así que ningún enlace que hayáis compartido se rompe.

---

## 6. Las otras dos piezas

La web es solo una de las tres. El plan completo:

- **La web** (esto) en Cloudflare Pages. Cambia poco.
- **El Pedante** en Blogger, para que podáis publicar cada número sin tocar código. La plantilla y el número 0 están en el otro paquete que os pasé.
- **Cajón Desastre** en [Spotify for Creators](https://creators.spotify.com). Alojamiento gratis e ilimitado, y os da un RSS con el que el pódcast entra también en Apple Podcasts e iVoox. La portada cuadrada que pide está en `marca/cajon-desastre-portada-1400.png` (1400 × 1400, que es justo el mínimo que exigen).

---

## 7. Detalles técnicos, por si acaso

- Todo el HTML es estático y válido. No hay JavaScript en ninguna página.
- Las imágenes de debajo del primer pantallazo usan `loading="lazy"`.
- Hay enlace de «saltar al contenido», textos alternativos en las imágenes y foco visible en el teclado.
- El contraste de texto cumple AA en todas las combinaciones de la paleta. El ocre `#C89B3C` se usa solo sobre fondos oscuros: sobre la crema no tiene contraste suficiente y no debe usarse como texto ahí.
- El sitio está diseñado a un solo tema (papel claro), como los carteles. No cambia con el modo oscuro del móvil, y es a propósito.
