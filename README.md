<div align="center">

<img src="./themes/glassmorphism/images/logo.png" alt="CODES++ UNLu" width="260" />

# linkyee

### Tu página de enlaces, 100% gratuita y de código abierto

Una alternativa a LinkTree totalmente personalizable, desplegada directamente en **GitHub Pages**.

[![Build automático](../../actions/workflows/build.yml/badge.svg)](../../actions/workflows/build.yml) [![Despliegue en Pages](../../actions/workflows/pages/pages-build-deployment/badge.svg)](../../actions/workflows/pages/pages-build-deployment)

[**Ver demo en vivo →**](https://codes-unlu.github.io/linkyee/)

<img width="1158" height="1092" alt="Vista previa de linkyee" src="https://github.com/user-attachments/assets/45b1ae8f-dfca-40e0-a14e-064c7f45ad1b" />

</div>

> **En una frase:** haz clic en *Use this template*, edita un archivo YAML y haz push. Tu página de enlaces queda publicada en GitHub Pages con un dominio `*.github.io` gratuito (o el tuyo propio). Sin SaaS, sin cuota mensual y sin dependencia de un proveedor. Incluye temas y plugins asistidos por IA.

## Índice

- [¿Por qué linkyee?](#por-qué-linkyee)
- [Configuración](#configuración)
- [Temas 🎨](#temas-)
- [Plugins 🔌](#plugins-)
- [Primeros pasos: despliegue en GitHub Pages](#primeros-pasos-despliegue-en-github-pages)
- [Pruebas locales](#pruebas-locales)
- [Despliegue con contenedores](#despliegue-con-contenedores)
- [Dominio propio](#dominio-propio-)
- [Proyectos que usan linkyee ✨](#proyectos-que-usan-linkyee-)
- [Créditos](#créditos)

---

## ¿Por qué linkyee?

- **100% gratuito.** Se aloja en GitHub Pages. Sin suscripciones, sin publicidad y sin pagos ocultos.
- **100% tuyo.** La configuración, los temas, los plugins y el contenido viven en tu propio repositorio de GitHub. Puedes llevártelo cuando quieras.
- **8 temas listos para usar.** Cambia de tema editando una sola línea de `config.yml`.
- **Diseñador de estilos con IA.** Describe el look que quieres en lenguaje natural. La skill de Claude [`linkyee-style-designer`](./.claude/skills/linkyee-style-designer/SKILL.md) genera el tema completo (HTML + CSS + JS).
- **6 plugins integrados** para datos en vivo: estrellas de GitHub, último commit, estadísticas de perfil, feeds RSS/Atom, cuentas regresivas y el último video de YouTube.
- **Generador de plugins con IA.** ¿Necesitas datos de otra fuente? Descríbela y la skill [`linkyee-plugin-builder`](./.claude/skills/linkyee-plugin-builder/SKILL.md) escribe el plugin en Ruby y lo conecta.
- **SEO y accesibilidad incluidos.** Contraste WCAG AA, modo oscuro, diseño responsivo desde 320 px, metadatos OG/Twitter y foco visible para navegación por teclado.
- **Vista previa local con recarga automática.** `./preview.sh` reconstruye el sitio al guardar. Solo recarga el navegador.

---

## Configuración

Todo lo que aparece en tu página se controla desde un único archivo: [`config.yml`](./config.yml). Es un YAML renderizado con Liquid, con cinco secciones principales:

```yaml
theme: default                     # ← carpeta dentro de ./themes/
lang: "es"

plugins:                           # ← datos opcionales obtenidos al construir el sitio
  - GithubRepoStarsCountPlugin: [ZhgChgLi/linkyee]

title: "Tu nombre"                 # ← encabezado del perfil
avatar: "./images/profile.jpeg"
name: "@tuusuario"
tagline: "Una frase sobre ti."

links:                             # ← botones de la lista de enlaces
  - link:
      icon: "fa-brands fa-github"
      text: "GitHub ({{ vars.GithubRepoStarsCountPlugin['ZhgChgLi/linkyee'] }} ⭐)"
      url: "https://github.com/tuusuario"
      target: "_blank"

socials: [ ... ]                   # ← fila de íconos de redes sociales
footer: "HTML libre."
copyright: "© 2026 Tú."
```

El [`config.yml`](./config.yml) incluido es un ejemplo completo que usa **todos los plugins integrados**. Tómalo como referencia. Edita los campos, haz push, espera a que GitHub Actions reconstruya el sitio y recarga la página.

### Sitios multilenguaje

Configura `i18n` para generar un sitio estático por cada idioma. La página raíz elige un idioma guardado o el del navegador y, si no hay coincidencia, usa `default_locale`.

```yaml
i18n:
  default_locale: en
  locales:
    en: locales/en.yml
    es: locales/es.yml
```

Cada archivo de idioma sobrescribe el contenido del perfil y puede incluir etiquetas de interfaz:

```yaml
lang: es
og_locale: es_ES
locale_label: Español
title: Página de enlaces
name: Ejemplo
ui:
  language_switcher: Idioma
  primary_links: Enlaces principales
```

Los hashes del idioma se combinan con `config.yml`. Los arreglos, como `links` y `socials`, reemplazan los valores base. Al construir se crean directorios `/<idioma>/` y una página de redirección en la raíz. Sin `i18n`, la salida de una sola página no cambia. Consulta [`examples/i18n`](./examples/i18n) para una configuración genérica completa.

### Redespliegue automático

El sitio se reconstruye una vez al día para que los datos de los plugins (cantidad de estrellas, últimas publicaciones, etc.) estén actualizados. La programación está en [`build.yml`](../../actions/workflows/build.yml):

```yaml
schedule:
    - cron: '0 0 * * *'   # todos los días a las 00:00 UTC
```

Elimina el bloque `schedule:` si no quieres reconstrucciones programadas.

---

## Temas 🎨

linkyee incluye **8 temas integrados**, listos para usar. Cambia de tema editando una línea de `config.yml`:

```yaml
theme: minimal-mono   # cualquier carpeta dentro de ./themes/
```

| Nombre | Claro | Oscuro | Estilo / para quién |
|---|---|---|---|
| `default` | <img width="200" alt="default claro" src="./themes/default/preview-light.png"> | <img width="200" alt="default oscuro" src="./themes/default/preview-dark.png"> | Tarjetas limpias · opción segura para cualquiera |
| `minimal-mono` | <img width="200" alt="minimal-mono claro" src="./themes/minimal-mono/preview-light.png"> | <img width="200" alt="minimal-mono oscuro" src="./themes/minimal-mono/preview-dark.png"> | Minimalismo suizo · monoespaciada · ingenieros, escritores |
| `editorial-serif` | <img width="200" alt="editorial-serif claro" src="./themes/editorial-serif/preview-light.png"> | <img width="200" alt="editorial-serif oscuro" src="./themes/editorial-serif/preview-dark.png"> | Estilo revista con serif · letra capital · blogueros, periodistas |
| `neo-brutalism` | <img width="200" alt="neo-brutalism claro" src="./themes/neo-brutalism/preview-light.png"> | <img width="200" alt="neo-brutalism oscuro" src="./themes/neo-brutalism/preview-dark.png"> | Bordes gruesos · colores primarios · desarrolladores indie, artistas |
| `glassmorphism` | <img width="200" alt="glassmorphism claro" src="./themes/glassmorphism/preview-light.png"> | <img width="200" alt="glassmorphism oscuro" src="./themes/glassmorphism/preview-dark.png"> | Tarjetas de vidrio esmerilado · diseñadores, agencias |
| `paper-card` | <img width="200" alt="paper-card claro" src="./themes/paper-card/preview-light.png"> | <img width="200" alt="paper-card oscuro" src="./themes/paper-card/preview-dark.png"> | Tarjetas pastel · bordes redondeados · creadores, ilustradores |
| `newsprint` | <img width="200" alt="newsprint claro" src="./themes/newsprint/preview-light.png"> | <img width="200" alt="newsprint oscuro" src="./themes/newsprint/preview-dark.png"> | Cabecera de periódico · serif + monoespaciada · filas numeradas |
| `terminal-retro` | <img width="200" alt="terminal-retro claro" src="./themes/terminal-retro/preview-light.png"> | <img width="200" alt="terminal-retro oscuro" src="./themes/terminal-retro/preview-dark.png"> | CRT · líneas de escaneo · verde fósforo sobre negro (oscuro) / oliva sobre crema de impresora (claro) · hackers |

Todos los temas integrados cumplen el mismo mínimo: contraste WCAG AA, **modo oscuro que cambia solo según la apariencia del sistema** (sin botón manual), diseño responsivo desde 320 px, foco accesible por teclado y soporte para `prefers-reduced-motion`.

Para probarlos localmente antes de hacer commit, consulta [Pruebas locales](#pruebas-locales). Para regenerar las capturas de arriba después de un cambio visual, ejecuta `./scripts/screenshot-themes.sh` (requiere `npx playwright`).

### Modificar un tema a mano

Cada tema está en `./themes/<nombre-del-tema>/` y tiene tres archivos:

- `index.html`: plantilla Liquid que consume `config.yml`
- `styles.css`: el estilo visual
- `scripts.js`: puede estar vacío, pero el archivo debe existir

El tema `default` sirve Font Awesome desde `themes/default/fontawesome/`. Los demás temas lo cargan desde un CDN para mantener las carpetas pequeñas.

### 🤖 Diseñador de estilos con IA

¿No encuentras el estilo que buscas? Descríbelo en lenguaje natural y la skill de Claude [`linkyee-style-designer`](./.claude/skills/linkyee-style-designer/SKILL.md) escribe un tema completo.

**Cómo usarlo:**

1. Instala [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) y abre este repositorio con él.
2. Pídelo en lenguaje natural. Por ejemplo:

   > *"Diseña un tema de linkyee inspirado en las portadas de Penguin de los años 60."*
   >
   > *"Quiero que mis enlaces se vean como la web de un ryokan japonés: sobrio, elegante y con mucho espacio en blanco."*
   >
   > *"Quiero una estética vaporwave, pero accesible."*
3. La skill lee tu `config.yml`, hace preguntas si el pedido es vago, genera `themes/<tu-tema>/`, cambia `theme:` en `config.yml` y ejecuta la construcción.
4. Ejecuta `./preview.sh <nuevo-tema>` para ver el resultado en local.

La skill aplica el mismo estándar de calidad que los temas integrados: nada de estética genérica de IA (sin degradados morado-rosa sin motivo, sin emojis como íconos, sin todo centrado sin jerarquía), jerarquía tipográfica real, mínimos de accesibilidad y **diseño responsivo estricto**: mobile-first, áreas táctiles de al menos 44 px y sin scroll horizontal a 320 px.

**Herramientas de diseño más avanzadas.** Si quieres una experiencia de diseño más rica (exploración de varias direcciones, revisión experta, exportación de animaciones), instala junto a ella la skill [`huashu-design`](https://github.com/alchaincyf/huashu-design). La skill de linkyee la usa si está presente.

---

## Plugins 🔌

Los plugins son pequeñas clases de Ruby que obtienen datos **al momento de construir** el sitio y los inyectan en tu página. Sirven para mostrar valores en vivo dentro de cualquier enlace, en la frase de perfil o en el pie de página: en cualquier texto que Liquid procese.

### Plugins integrados

| Plugin | Qué devuelve | Forma de uso |
|---|---|---|
| `GithubRepoStarsCountPlugin` | Cantidad de estrellas de uno o varios repositorios | `{{ vars.GithubRepoStarsCountPlugin['dueño/repo'] }}` |
| `GithubLastCommitPlugin` | Último commit: `sha` / `date` / `message` | `{{ vars.GithubLastCommitPlugin['dueño/repo'].date }}` |
| `GithubProfilePlugin` | `followers` / `following` / `repos` | `{{ vars.GithubProfilePlugin['usuario'].followers }}` |
| `RSSFeedPlugin` | Últimas entradas (feeds de Medium, blogs, podcasts, YouTube) | `{{ vars.RSSFeedPlugin['url'][0].title }}` |
| `CountdownPlugin` | Días hasta o desde una fecha objetivo | `{{ vars.CountdownPlugin.label.days }}` |
| `YouTubeChannelLatestVideoPlugin` | Último video: título, URL y miniatura | `{{ vars.YouTubeChannelLatestVideoPlugin['@handle'].title }}` |

Actívalos en `config.yml`:

```yaml
plugins:
  - GithubRepoStarsCountPlugin:
      - ZhgChgLi/linkyee
  - RSSFeedPlugin:
      - https://tublog.example/feed.xml
```

…y luego úsalos donde quieras que Liquid procese texto:

```yaml
links:
  - link:
      icon: "fa-brands fa-github"
      text: "linkyee ({{ vars.GithubRepoStarsCountPlugin['ZhgChgLi/linkyee'] }} ⭐)"
      url: "https://github.com/ZhgChgLi/linkyee"
```

Si un plugin falla al construir (error de red, cambio en la API, token vencido, etc.), la construcción igual termina con éxito: el valor queda vacío y el error se registra en la salida de GitHub Actions. Tu sitio nunca se rompe por una API externa inestable.

### 🤖 Generador de plugins con IA

¿Necesitas datos que linkyee no trae de fábrica? Abre el repositorio con [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) y descríbelos. La skill [`linkyee-plugin-builder`](./.claude/skills/linkyee-plugin-builder/SKILL.md) conoce el contrato de los plugins.

**Ejemplos:**

> *"Agrega un plugin que muestre mis 3 últimas publicaciones de medium.com/@mihandle como enlaces nuevos."*
>
> *"Obtén el clima actual de Luján desde wttr.in y muestra la temperatura en el pie de página."*
>
> *"Agrega un plugin que traiga mi tiempo total de juego en Steam usando la API Web de Steam."*

La skill va a:

1. Confirmar contigo la fuente de datos y su forma.
2. Generar `plugins/<TuPlugin>.rb`, usando los helpers de HTTP, JSON y caché de la clase base (sin `Net::HTTP` directo).
3. Conectarlo en `config.yml` bajo `plugins:` y usar su salida donde lo pediste.
4. Ejecutar `bundle exec ruby ./scaffold.rb` y verificar que el valor aparezca en `_output/index.html`.

### Wiki para desarrolladores

Para el contrato completo de los plugins (helpers de la clase base, patrones comunes de HTTP, JSON, scraping y caché, reglas de renderizado de Liquid y consejos de depuración), lee **[`plugins/README.md`](./plugins/README.md)**. Es la referencia que la skill de IA carga para generar un plugin.

---

## Primeros pasos: despliegue en GitHub Pages

### ¿Qué es GitHub Pages?
> GitHub Pages es un servicio de alojamiento gratuito de GitHub, pensado para crear y publicar sitios web directamente desde un repositorio. Permite a desarrolladores, diseñadores y cualquier persona con una cuenta de GitHub alojar sitios personales, de proyecto o de organización sin usar servicios externos. Funciona de forma integrada con los repositorios y genera el sitio estático automáticamente cada vez que haces push.

#### Paso 1. Haz clic en el botón “Use this template”, arriba a la derecha del repositorio [linkyee](https://github.com/ZhgChgLi/linkyee), y luego en “Create a new repository”:
![imagen](https://github.com/user-attachments/assets/4b88da62-df4b-4f3b-a22c-e78b7527a92d)

#### Paso 2. Marca “Include all branches”, escribe el nombre del repositorio de GitHub Pages que quieras y haz clic en “Create repository” cuando termines:
![imagen](https://github.com/user-attachments/assets/d3611204-7507-41a1-8221-707200a3e269)

> El nombre del repositorio afecta la URL de acceso. Si usas `tu-usuario.github.io` como nombre, esa será la URL directa de tu sitio.
> Si ya tienes un repositorio `tu-usuario.github.io`, la URL de GitHub Pages será `tu-usuario.github.io/Nombre-del-repo`.

#### Espera a que termine la copia. Durante la configuración inicial puede haber errores de despliegue por permisos del repositorio copiado. Ajústalos con los siguientes pasos.
![imagen](https://github.com/user-attachments/assets/038fac9e-83eb-4f2f-ba9a-88712b4af022)

#### Paso 4. Ve a Settings → Actions → General y verifica estas opciones:
![imagen](https://github.com/user-attachments/assets/6851c4e6-9466-4800-862f-e9e5e5b65b11)

- Actions permissions: `Allow all actions and reusable workflows`
- Workflow permissions: `Read and write permissions`

Luego haz clic en Save.

#### Paso 5. Ve a Settings → Pages y verifica que la rama de GitHub Pages sea “gh-pages”:
![imagen](https://github.com/user-attachments/assets/1802bc78-4615-4d29-b180-9c84f3fb8d6d)

> El mensaje `Your site is live at: XXXX` que aparece arriba es tu URL pública de GitHub Pages.

#### Paso 6. Ve a Settings → Actions y espera a que termine el primer despliegue:
![imagen](https://github.com/user-attachments/assets/e57336ef-2f35-4455-abc0-76dce07470ee)

#### Paso 7. Abre la URL de GitHub Pages para comprobar que la copia funciona:
![imagen](https://github.com/user-attachments/assets/023c39f7-9351-4175-8c9f-5eb42e2ecdb9)

> ¡Listo! El despliegue fue exitoso. Ya puedes editar los archivos de configuración con tus datos. 🎉

#### Cada vez que modifiques un archivo, espera a que GitHub Actions termine las tareas `Automatic build` y `pages build and deployment`.

![imagen](https://github.com/user-attachments/assets/0ba637cc-3bb6-4458-a076-5f754c7429b3)

Recarga la página para ver los cambios. 🚀

---

## Pruebas locales

Construye y sirve el sitio en `http://localhost:8080`:

```bash
./preview.sh                    # construye con el tema definido en config.yml
./preview.sh minimal-mono       # cambia temporalmente a <nombre-del-tema>, construye y sirve;
                                # restaura config.yml con Ctrl-C
PORT=4000 ./preview.sh          # usa otro puerto
```

Cuando pasas un tema como argumento, `preview.sh` guarda una copia de tu `config.yml`, cambia al tema pedido solo para esa sesión y restaura el original con `Ctrl-C`. Tu configuración versionada nunca se modifica.

### Recarga automática al guardar

Mientras la vista previa está activa, `preview.sh` observa:

- `themes/`
- `plugins/`
- `config.yml`
- `scaffold.rb`

Cualquier cambio dispara una reconstrucción inmediata. Solo recarga el navegador. Instala [`fswatch`](https://github.com/emcrisostomo/fswatch) (`brew install fswatch` en macOS) para reaccionar en menos de un segundo; si no está, usa un sondeo cada segundo que no necesita dependencias extra.

Si una construcción falla (por ejemplo, una referencia Liquid rota), el observador muestra el error y sigue activo. Corrige el problema, guarda de nuevo y se reconstruye.

### Requisitos

- Ruby (ejecuta `bundle install` una vez para instalar `liquid` y `nokogiri`)
- Python 3 (o Ruby) para el servidor de archivos estáticos que levanta `preview.sh`

---

## Despliegue con contenedores

Construye y ejecuta el sitio generado con Docker Compose:

```bash
docker compose up -d --build
```

El servicio escucha en el puerto `8080` por defecto. Cambia el puerto con `PORT` y define `REBUILD_INTERVAL` (en segundos) si quieres que los datos de los plugins se actualicen periódicamente:

```bash
PORT=8081 REBUILD_INTERVAL=3600 docker compose up -d --build
```

La imagen contiene el código fuente de la aplicación. Un volumen de Docker con nombre conserva la caché de los plugins, mientras que la salida generada permanece dentro del contenedor.

---

## Dominio propio

Puedes configurar un dominio propio para GitHub Pages. Por ejemplo, así se ve el [sitio del autor original](https://link.zhgchg.li).

Sigue el [tutorial para vincular un dominio](https://en.zhgchg.li/posts/zrealm-dev/github-pages-custom-domain-setup-replace-github-io-with-your-own-domain-483af5d93297) (en inglés).

---

## Proyectos que usan linkyee ✨

> ¿Hiciste tu propia página con linkyee? ⭐ Abre un PR para agregarla aquí y inspirar a otros.

| Vista previa | Sitio web | Descripción |
|--------|--------|-------------|
| <img width="180" height="180" alt="CODES++ UNLu" src="./themes/glassmorphism/images/logo.png" /> | [codes-unlu.github.io/linkyee](https://codes-unlu.github.io/linkyee/) | Página de enlaces del Centro Organizado de Estudiantes de Sistemas de la UNLu (CODES++) |
| <img width="180" height="180" alt="ZhgChgLi" src="https://github.com/user-attachments/assets/9052e290-f6b8-4a94-a71e-85ec36cd2900" /> | [link.zhgchg.li](https://link.zhgchg.li) | Página de enlaces personal de ZhgChgLi (Harry Li), autor original |
| - | Tu sitio | ¡Tu sitio podría aparecer aquí! 🚀 |

---

## Créditos

**linkyee** fue creado por [ZhgChgLi](https://zhgchg.li/) y se distribuye como software libre. Esta versión es mantenida por **CODES++ — Centro Organizado de Estudiantes de Sistemas, UNLu**.

¿Te ayudó el proyecto? Puedes invitar un café al autor original:

[![Buy Me A Beer](https://github.com/user-attachments/assets/63f01edf-2aa5-4d91-8f8a-861e5b6b4feb)](https://www.paypal.com/ncp/payment/CMALMPT8UUTY2)

Abre un issue o envía un PR con tu corrección o contribución. ¡Gracias! :)
