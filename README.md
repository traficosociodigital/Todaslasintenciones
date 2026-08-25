# Todas las Intenciones — Landing Page

Landing de captación para una consultora de **automatización de procesos e inteligencia artificial**.
Página estática, un solo archivo HTML, sin dependencias ni proceso de compilación.

**Objetivo de conversión:** solicitar un diagnóstico de procesos.

---

## Contenido del repositorio

```
index.html            La página completa (HTML + CSS + JS en línea)
assets/hero.webp      Ilustración principal: brote, tierra y raíces (tratada para fondo oscuro)
assets/og-image.jpg   Vista previa para redes sociales (1200×630)
assets/favicon.svg    Isotipo del brote
robots.txt
.nojekyll             Evita que GitHub Pages procese el sitio con Jekyll
```

Peso total de la página: **~62 KB de HTML + 353 KB de imagen**. Un solo recurso externo: Google Fonts (Cormorant Garamond y Jost).

---

## Publicar en GitHub Pages

Repositorio previsto: **`todas-las-intenciones`**, público.

### 1. Crear el repositorio vacío

En GitHub → **New repository** → nombre `todas-las-intenciones`, visibilidad **Public**.
**No marques** «Add a README», ni `.gitignore`, ni licencia: el repositorio ya trae su commit inicial y esas opciones provocarían un conflicto en el primer push.

### 2. Subirlo

Este directorio ya está inicializado con git y con el commit inicial en la rama `main`.
Abre una terminal dentro de la carpeta descomprimida y ejecuta:

```bash
git remote add origin https://github.com/TU-USUARIO/todas-las-intenciones.git
git push -u origin main
```

En Windows necesitas [Git for Windows](https://git-scm.com/download/win). La primera vez te pedirá autenticarte con tu cuenta de GitHub.

Si prefieres empezar el historial de cero: `rm -rf .git && git init -b main && git add . && git commit -m "Landing"`.

### 3. Activar Pages

**Settings → Pages → Build and deployment**
*Source*: `Deploy from a branch` · *Branch*: `main` · *Folder*: `/ (root)` · **Save**.

En uno o dos minutos la página estará en:

```
https://TU-USUARIO.github.io/todas-las-intenciones/
```

### 4. Fijar la URL en el código

Mientras las URLs sigan siendo marcadores de posición, el marcado structured data no valida y la vista previa al compartir el enlace no se genera. Con la dirección ya conocida, ejecuta una de estas dos órdenes dentro de la carpeta y vuelve a hacer commit y push.

**PowerShell (Windows):**

```powershell
$sitio = "https://TU-USUARIO.github.io/todas-las-intenciones"
(Get-Content index.html -Raw) `
  -replace 'https://TU-DOMINIO\.com', $sitio `
  -replace 'content="assets/og-image\.jpg"', "content=`"$sitio/assets/og-image.jpg`"" |
  Set-Content index.html -Encoding UTF8
```

**Bash (Linux / macOS / Git Bash):**

```bash
SITIO="https://TU-USUARIO.github.io/todas-las-intenciones"
sed -i "s#https://TU-DOMINIO.com#$SITIO#g; s#content=\"assets/og-image.jpg\"#content=\"$SITIO/assets/og-image.jpg\"#" index.html
```

Después:

```bash
git commit -am "URLs absolutas del sitio publicado"
git push
```

### Con dominio propio

Añade el dominio en **Settings → Pages → Custom domain**, crea un archivo `CNAME` en la raíz con el dominio, y en tu DNS un registro `CNAME` apuntando a `TU-USUARIO.github.io`. Activa *Enforce HTTPS* cuando GitHub lo permita. Repite el paso 4 con el dominio definitivo.

---

## Pendiente antes de considerarla publicada

Estos puntos están marcados también dentro de la propia página, en el recuadro del pie.

| # | Tarea | Por qué bloquea |
|---|---|---|
| 1 | **Conectar el formulario** a un CRM, a un correo o a un servicio tipo Formspree | Hoy valida los campos pero no envía nada: es un prototipo |
| 2 | Confirmar que la oferta es un **diagnóstico gratuito de 45 minutos** y que las cuatro garantías del bloque final son asumibles | Son la promesa central de la página |
| 3 | Sustituir `https://TU-DOMINIO.com` en el bloque `application/ld+json` | Sin dominio real, el marcado structured data no valida |
| 4 | Poner la URL **absoluta** en `og:image` (`https://.../assets/og-image.jpg`) | Varios servicios ignoran las rutas relativas al generar la vista previa |
| 5 | Añadir aviso legal, política de privacidad y cookies, y la casilla de consentimiento del formulario | Obligatorio en cuanto el formulario trate datos personales. **Revisar con un asesor legal**: la normativa depende del país |
| 6 | Sustituir los tres espacios reservados de casos de éxito por casos reales con permiso por escrito | Sin prueba social la página pierde su argumento más fuerte |
| 7 | Instalar analítica y medir: scroll, clic en cada CTA, inicio y envío de formulario | Sin medición no se puede saber si el problema está en el tráfico, el mensaje o el formulario |

Nada de lo que aparece en la página ha sido inventado: las cifras están etiquetadas como rangos orientativos, el ejemplo de 23 h → 4 h como ilustrativo, y no hay ningún testimonio ni cliente ficticio.

---

## Notas técnicas

- **Accesibilidad:** contrastes verificados por cálculo (todos superan WCAG 2.1 AA; la mayoría alcanza AAA), foco visible, acordeón con `aria-expanded` / `aria-controls`, enlace de salto al contenido y `prefers-reduced-motion` respetado.
- **Tema oscuro único**, decisión deliberada por coherencia con los activos de marca. Todos los colores se pintan explícitamente; la página no hereda el fondo del contenedor.
- **Sin JavaScript de terceros.** Unas 150 líneas de JS nativo: revelado al hacer scroll, contadores, acordeón, emparejado de filas en la comparativa y los nodos animados del hero.
- **Optimizaciones opcionales para producción:** autoalojar las dos tipografías en `woff2` con `preload`, generar variantes AVIF de la ilustración con `srcset`, y servir con compresión Brotli.
