# Efectos para Claude · 42 efectos de vídeo en español

![Vista previa](assets/preview.jpg)

Un clip. 42 efectos. Cero apps.

Una skill para **Claude Code** que añade efectos a tus vídeos hablando a cámara: widgets de vidrio, tus reels flotando a tu alrededor, zooms que se clavan en tu cara, portada tipo serie, checklist, toggles de iPhone, titulares y más. Siguen tu cara, pueden ir detrás de tu cabeza y salen en 1080p o 4K con tu audio original.

Todo en español: las instrucciones y los textos que aparecen dentro de los efectos.

## Cómo instalarla
1. Descarga este repo (botón verde **Code → Download ZIP**) o clónalo:
   ```bash
   git clone https://github.com/victorpeel-ux/efectos-claude ~/efectos-claude
   ```
2. Abre Claude Code y dile: *"Instala la skill de efectos que está en ~/efectos-claude"*.
3. Arrastra tu vídeo al chat y escribe, por ejemplo: `/efectos orbit` o *"pon CLAUDE gigante detrás de mí en la palabra Claude"*.

La primera vez instala lo que necesita (ffmpeg y Python 3.12) y tarda 1–3 minutos.

## Qué necesitas
- Claude Code con un plan de pago de Claude.
- Mac o Windows.
- Un vídeo vertical tuyo hablando a cámara.

## Créditos
Basado en el pack open source **[claude-video-effects](https://github.com/Vibha-Ramprakash/claude-video-effects)** de [@vibha.in.progress](https://www.instagram.com/vibha.in.progress/) (licencia MIT). Esta versión la traduce al español y ajusta textos y estilo.

Detección de cara: [OpenCV YuNet](https://github.com/opencv/opencv_zoo) (MIT). Recorte de persona: [MediaPipe Selfie Segmenter](https://ai.google.dev/edge/mediapipe/solutions/vision/image_segmenter) (Apache 2.0). Fuentes con licencia SIL OFL / Apache 2.0 (ver `fonts/`).

Hecho por **Victor Jaimes** · IA y negocio en [@victorgrowth_](https://www.instagram.com/victorgrowth_/).
