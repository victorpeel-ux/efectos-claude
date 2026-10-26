---
name: efectos
description: Añade cualquiera de 42 efectos de vídeo a un clip hablando a cámara (widgets de vidrio, iconos flotando, palabra gigante detrás, checklist, toggles de iPhone, spotlight, timeline y más). Los efectos siguen tu cara y pueden ir detrás de tu cabeza. Úsalo cuando el usuario escriba /efectos o /effects, nombre un efecto o pida añadir un efecto, zoom, color, sticker o animación a su vídeo.
---

# Efectos: 42 efectos de vídeo en español

La persona normalmente no es técnica. Respuestas cortas y cercanas, en español. Haz el trabajo por ella y no le pidas que ejecute comandos.

Todas las rutas son relativas a la carpeta de esta skill (donde está este SKILL.md). Usa su ruta absoluta en los comandos.

## 1. Primera vez: instalar (una sola vez)
Ejecuta `bash scripts/setup.sh`. Imprime `READY` cuando termina (la primera vez tarda 1–3 minutos).
- `NEED_FFMPEG`: instálalo. Mac: `brew install ffmpeg` (si falta `brew`, que instale Homebrew desde brew.sh). Windows: `winget install ffmpeg`.
- `NEED_PYTHON`: instala Python 3.12 (Mac: `brew install python@3.12`; Windows: `winget install Python.Python.3.12`) y vuelve a ejecutar el setup. En Mac, si sigue sin encontrarlo: `PATH=/opt/homebrew/bin:$PATH bash scripts/setup.sh`.
- En Windows el Python está en `.venv\Scripts\python.exe` en vez de `.venv/bin/python`.

## 2. Vídeo y efecto
- Vídeo: la persona lo arrastra al chat o da la ruta. Funciona mejor un vídeo vertical ya exportado (no RAW de cámara grabado en horizontal).
- Efecto: por `/efectos <nombre>` o por lo que describa. Búscalo en la tabla. Si no está claro, enséñale la lista.

## 3. Tiempos
- Si dice "en la palabra X" o "cuando digo…": ejecuta `.venv/bin/python scripts/words.py <video>` y usa esos tiempos.
- Si no da tiempos: todo el clip, o una sola pregunta corta sobre qué parte.
- Las ventanas cortas se ven mejor: 1,5 a 4 s por efecto.

## 4. Plan, revisión, render
1. Escribe el plan junto al vídeo como `<video>_efectos.json`:
   ```json
   {"effects": [
     {"fx": "orbit", "start": 3.2, "end": 6.0, "images": "assets/iconos-reels"},
     {"fx": "backdrop-word", "start": 14.0, "end": 16.3, "text": "CLAUDE", "color": "#F4FE5E"}
   ]}
   ```
2. Revisa fotogramas primero (rápido): `.venv/bin/python scripts/fx.py --plan <plan.json> <video> <carpeta>/check.png --still 4.5,15.2` (mitad de cada efecto). Mira los PNG tú mismo y corrige texto, tiempos u opciones si algo tapa la cara, se corta o no se lee.
3. Render: `.venv/bin/python scripts/fx.py --plan <plan.json> <video> <video>_efectos.mp4`. Mantiene el audio original, 1080p por defecto (`--width 2160` para 4K, más lento).
4. Dile dónde está el archivo y recuérdale en una línea que lo vea antes de publicar.

Un solo efecto sin plan: `.venv/bin/python scripts/fx.py orbit <video> <salida.mp4> --start 3 --end 6 --text "..." --opt clave=valor`.

## Los 42 efectos
| # | `fx` | Qué hace | Opciones |
|---|---|---|---|
| 1 | `noise` | Reels que se apilan detrás de tu cabeza | `images` (carpeta), `size` |
| 2 | `lineup` | Tarjetas numeradas en arco sobre tu cabeza | `text` (con `\|`) |
| 3 | `locked-on` | Esquinas que se clavan en tu cara y la cámara te sigue | `zoom` (1.35), `text` |
| 4 | `orbit` | Reels o iconos orbitando tu cabeza | `images`, `count`, `speed`, `size` |
| 5 | `lean-in` | Zoom rápido en una palabra | `zoom` (1.45, máx. 2), `speed` |
| 6 | `backdrop-word` | Palabra gigante que cae detrás de ti | `text`, `color`, `font` (`bold`/`serif`) |
| 7 | `spotlight` | Apaga la luz y te deja iluminado | `text`, `color`, `push` |
| 8 | `the-bill` | Recibo impreso en la pared | `text` (líneas con `\|`) |
| 9 | `moody` | Corrección de color | `grade` (`moody`, `bw`, `warm`, `cool`, `pop`) |
| 10 | `swipe` | Deslizador antes/después | `grade` |
| 11 | `todo` | Checklist clara junto a tu cabeza | `text`, `ticks`, `title` |
| 12 | `comment-box` | Barra de comentario de IG que escribe y publica | `text` |
| 13 | `tap` | Botón "+ Seguir" → "Siguiendo" | `at`, `x`, `y`, `color` |
| 14 | `pause-point` | Congela y te señala con una flecha | `text`, `color`, `label_x` |
| 15 | `uninstall` | Barra de desinstalación con glitch | `text` |
| 16 | `reel-frame` | El vídeo se encoge a tarjeta de reel | `text` (usuario) |
| 17 | `shortcut-rain` | Llueven teclas detrás de ti | `text`, `count` |
| 18 | `reject-stamp` | Sello de goma | `text`, `color`, `angle`, `y` |
| 19 | `countdown-flip` | Reloj 3, 2, 1 | `from` |
| 20 | `rabbit-hole` | Túnel girando | `ratio`, `speed`, `spin` |
| 21 | `cover-star` | Portada de revista (`look=editorial`) | `text`, `lines`, `issue`, `color` |
| 22 | `scribble` | Garabatos de marcador | `text`, `color` |
| 23 | `glass-widgets` | Widgets de vidrio alrededor de tu cabeza | `text`, `sub`, `name`, `handle`, `event`, `look=simple` |
| 24 | `red-collage` | B/N con palabra roja gigante | `text`, `lines`, `tag` |
| 25 | `split-headline` | Titular arriba, tú abajo | `text`, `hl`, `pill` |
| 26 | `pastel-word` | Cuarto lavanda + palabra gigante | `text`, `name`, `handle` |
| 27 | `check-pills` | Papel cuadriculado + píldoras azules | `text`, `images` |
| 28 | `timeline` | Timeline de edición + REC | `text`, `sub`, `tc` |
| 29 | `headline-box` | Zoom con titular en caja | `text`, `zoom` |
| 30 | `profile-wall` | Cuadrícula de reels + contador | `images`, `count`, `label` |
| 31 | `tier-list` | Tier list | `title`, `item`, `others` |
| 32 | `broll-split` | B-roll arriba con sticker, tú abajo | `images`, `text` |
| 33 | `phone-fan` | Reels en abanico de móviles | `images`, `text` |
| 34 | `dot-reveal` | Imagen hecha de puntos | `color`, `cell` |
| 35 | `headline-wall` | Titulares detrás + total | `text` (`titular::meta\|...`), `total`, `label` |
| 36 | `checklist` | Lista de tareas oscura bajo el mentón | `text` (`paso::meta\|...`), `title` |
| 37 | `liquid-glass-graph` | Gráfica en vidrio + número que sube (`look=bento`) | `text`, `from`, `to`, `color` |
| 38 | `carousel-spin` | Carrusel 3D de reels | `images`, `count`, `size`, `turns` |
| 39 | `match-cut` | Páginas de noticias que cortan en una palabra | `text`, `color` |
| 40 | `apple-toggles` | Ajustes de iPhone que se encienden | `text`, `ticks`, `color`, `pos` |
| 41 | `led-sign` | Letrero LED detrás de ti | `text`, `color`, `push` |
| 42 | `slow-push` | Zoom lento con fondo desenfocado | `zoom` (1.6), `blur` |

Looks: `glitter-spotlight` = `spotlight` con `look=sparkle`.

**Iconos incluidos:** `assets/iconos-reels/` tiene 6 iconos de reels (Reels, me gusta, reproducciones, comentario, enviar, +10/día) para usar con `images` en `orbit`, `noise` o `carousel-spin`, en vez de tu propia cara flotando.

## Reglas
- Nunca tapar la cara: si un fotograma de revisión muestra texto encima, mueve (`x`, `y`) o acorta.
- Efectos de cámara (`locked-on`, `lean-in`, `spotlight`) primero cuando se solapan.
- Zoom nunca más de 2×.
- Solo añade visuales: subtítulos y efectos de sonido van aparte.
- Son versiones de partida: si la persona lo compara con un reel que vio, dilo con honestidad.
