# Subtitle Studio Pro — Tutorial completo

Editor profesional de subtítulos en un solo archivo HTML. Convierte la voz de un vídeo o audio en subtítulos sincronizados, te permite editarlos, darles estilo (incluidos los estilos tipo Reels/TikTok) y exportarlos o quemarlos dentro del vídeo. **Todo se procesa en tu equipo: el vídeo no se sube a ningún servidor.**

---

## 1. Requisitos y primer arranque

- **Navegador recomendado:** Google Chrome o Microsoft Edge. También funciona en Firefox (con menos funciones de carpeta, ver sección 6).
- **Cómo abrirlo:** doble clic en `subtitle-studio-pro.html`.
- **Internet:** la primera vez que transcribes se necesita conexión para cargar el motor Whisper (desde jsDelivr). Los modelos pueden estar ya en tu carpeta o descargarse una sola vez y quedar guardados (sección 6).
- **Formatos que acepta:** MP4, MOV, MKV, WebM (vídeo) y MP3, WAV, M4A, OGG (audio). También puedes arrastrar el archivo a la pantalla de bienvenida.

### Flujo de trabajo recomendado

1. Cargar el vídeo.
2. (Opcional) Procesar el audio si hay música de fondo o volumen bajo.
3. Pulsar **INICIAR TRANSCRIPCIÓN**.
4. Revisar y corregir los subtítulos.
5. Elegir un estilo.
6. Exportar.

La barra de **pasos** bajo el menú superior (Vídeo cargado → Analizar voz → Transcribir → Editar → Diseñar → Exportar) te indica en qué punto estás.

---

## 2. Pantalla de bienvenida

| Elemento | Para qué sirve |
|---|---|
| **+ CARGAR VÍDEO** / zona de arrastre | Abre tu vídeo o audio. También puedes soltar el archivo encima. |
| **Abrir proyecto (.ssp)** | Continúa un proyecto que guardaste antes. |
| **Editar un SRT / VTT / ASS existente** | Importa subtítulos que ya tienes para editarlos o darles estilo. |
| **Recuperar trabajo anterior** | Aparece solo si la app guardó automáticamente un trabajo previo. |
| Indicadores de sistema | Muestran qué soporta tu navegador (WebAssembly, WebGPU, almacenamiento local…). |

---

## 3. Barra superior

| Botón | Función |
|---|---|
| **Nuevo proyecto** | Limpia todo para empezar de cero (pide confirmación si hay subtítulos). |
| **Abrir proyecto** | Carga un archivo `.ssp`. |
| **Guardar proyecto** (Ctrl+S) | Descarga un `.ssp` con subtítulos, estilos, marcadores y ajustes. **No incluye el vídeo**: al abrirlo, vuelve a cargar el vídeo. |
| **↶ Deshacer / ↷ Rehacer** (Ctrl+Z / Ctrl+Y) | Deshace o rehace cambios en los subtítulos (hasta 80 pasos). |
| **Simple / Profesional** | *Simple* oculta la línea de tiempo, las opciones avanzadas y los marcadores. *Profesional* muestra todo. |
| **Configuración** | Tema claro/oscuro, guardado automático, motor de procesamiento y estado del sistema. |
| **Ayuda** | Lista de atajos de teclado. |
| **EXPORTAR** (Ctrl+E) | Abre la ventana de exportación. |

---

## 4. Panel izquierdo

### 4.1 Proyecto

Muestra miniatura, nombre, duración, resolución, tamaño, idioma, número de subtítulos y estado de la transcripción.

- **Cargar vídeo:** abre un vídeo o audio.
- **Extraer audio:** extrae el audio a WAV 16 kHz mono (lo descarga) y dibuja la forma de onda en la línea de tiempo. Si hay audio procesado, extrae ese.
- **Importar subtítulos:** carga un `.srt`, `.vtt` o `.ass`.

### 4.2 Transcripción automática

| Control | Para qué sirve |
|---|---|
| **Modelo de transcripción** | *Tiny*: más rápido, menos preciso. *Base*: equilibrio recomendado. *Small*: más preciso, más memoria. |
| **Precisión del modelo** | *Cuantizado (q8)*: ligero y rápido, usa WASM. *Sin cuantizar (fp32)*: más preciso y pesado, usa WebGPU si tu equipo lo tiene. |
| **Idioma** | Detección automática o un idioma concreto (fijarlo suele dar mejor resultado). |
| **Modo** | *Transcribir* en el idioma original o *Traducir al inglés*. |
| **Tipo de subtítulo** | *Automático*, *Normal* (varias palabras), *Dinámico* (frases cortas), *Karaoke* (activa la animación por palabra), *Redes sociales* (texto grande en 2 líneas). |
| **Tiempos palabra por palabra** (experimental) | Pide tiempos exactos por palabra, útil para karaoke. Si el modelo no lo permite, la app cae al modo normal y te avisa. |
| **Opciones avanzadas** (modo Profesional) | Caracteres por línea, máximo de líneas, duración mínima y máxima, espacio mínimo entre subtítulos. |
| **INICIAR TRANSCRIPCIÓN** | Ejecuta el proceso completo. Verás las fases: extraer audio → analizar voz → cargar modelo → transcribir (con porcentaje) → calcular tiempos → dividir segmentos → generar subtítulos. |
| **Cancelar** | Detiene la transcripción en curso. |

**Cómo se sincroniza:** la app detecta dónde hay voz (VAD), transcribe solo esos tramos y ajusta el inicio y el final de cada subtítulo al sonido real del audio.

### 4.3 Modelos locales (carpeta)

Sirve para que la app encuentre tus modelos Whisper, los guarde y no los descargue de nuevo.

| Botón | Función |
|---|---|
| **Seleccionar carpeta de modelos** | Eliges la carpeta. La app la **memoriza** y la reconoce cada vez que abras la app. |
| **Verificar** | Vuelve a leer la carpeta y muestra, por modelo (Tiny/Base/Small, cuantizado/sin cuantizar), si está en carpeta, en caché o hay que descargarlo. El modelo elegido aparece marcado con ▶. |
| **Modo compatible** | Elige la carpeta de forma que funciona en cualquier navegador. Los modelos se copian a la caché del navegador y ya no hace falta volver a elegir la carpeta. |
| **Mover modelos…** | Copia o mueve los modelos a otra carpeta que indiques y la deja como carpeta memorizada. |
| **Olvidar carpeta** | La app deja de recordarla (no borra ningún archivo). |
| **Diagnóstico** | Genera un informe (navegador, permisos, archivos legibles, carga del motor). Úsalo si algo falla y envíamelo. |

**Cómo se comporta:**
- Si el modelo **está en la carpeta**, se usa sin descargar y se copia a la caché del navegador.
- Si **no está**, se descarga una vez y se guarda en la caché y en la carpeta (si hay permiso de escritura).
- Si Chrome vuelve a pedir permiso de la carpeta, el modelo sigue funcionando desde la caché.

**Formato necesario:** modelos **ONNX** con esta estructura, por ejemplo:

```
whisper-base/
  config.json
  preprocessor_config.json
  tokenizer.json
  tokenizer_config.json
  onnx/encoder_model_quantized.onnx
  onnx/decoder_model_merged_quantized.onnx
```

(Para «sin cuantizar» los archivos `.onnx` no llevan `_quantized`.) Los archivos `.bin` de whisper.cpp **no sirven** con este motor; la app te avisa si los encuentra.

### 4.4 Audio (opcional)

Por defecto se usa el audio tal como se cargó. Esta sección solo actúa cuando pulsas **Efectuar**.

| Control | Para qué sirve |
|---|---|
| **Reducir música / ruido de fondo** + **Intensidad** | Baja la música y el ruido, sobre todo entre frases, para ayudar a la transcripción. |
| **Normalizar volumen** + **Nivel objetivo** | Lleva la voz a un nivel estándar (−14, −16, −18 o −20 dB). Útil si el audio está bajo. |
| **Nivelar todo a la misma altura** | Sube las partes bajas y baja las fuertes para que todo suene parejo. |
| **Efectuar** | Aplica los cambios. El audio y la forma de onda de la línea de tiempo se actualizan, y la transcripción usa ese audio. |
| **Deshacer** | Vuelve al estado anterior (al procesado previo o al original). |
| **A/B** | Alterna entre escuchar el original y el procesado. Al exportar vídeo se usa el que tengas seleccionado. |

> **Importante:** el reductor de música es procesado de señal, **no** separación con inteligencia artificial. Funciona bien para bajar la música entre frases y el ruido constante; con música mezclada bajo la voz ayuda a transcribir, pero no deja una voz perfectamente limpia.

### 4.5 Marcadores (modo Profesional)

Puntos de referencia en la línea de tiempo: *Inicio de frase*, *Cambio de escena*, *Cambio de hablante*, *Punto importante*. **+ En el cursor** crea uno en la posición actual; haz clic en uno para saltar a él o en ✕ para borrarlo.

---

## 5. Zona central

### 5.1 Reproductor

| Control | Función |
|---|---|
| **▶ Reproducir / ⏸ Pausar** (Espacio) | Reproduce con los subtítulos superpuestos en tiempo real. |
| **■** | Detiene y vuelve al inicio. |
| **−5 s / −1 s / +1 s / +5 s** | Saltos de tiempo. |
| **Tiempo** | Posición actual (`hh:mm:ss.mmm`). |
| **🔊 / deslizador** | Silenciar y volumen. |
| **Velocidad** | De 0.25× a 2×. |
| **Zona segura** | Muestra guías 9:16 y 1:1 y el área libre de la interfaz de Reels/TikTok/Shorts, para colocar el texto donde no se tape. |
| **⛶** | Pantalla completa. |
| **Subtítulo #n** (a la derecha) | Muestra el subtítulo que se está reproduciendo. |

### 5.2 Línea de tiempo (modo Profesional)

Muestra la **forma de onda** del audio, las zonas con voz (línea cian bajo la regla) y los **bloques de subtítulos**.

- **Clic en un hueco:** mueve la reproducción a ese instante (y arrastrando, recorres el vídeo).
- **Arrastrar un bloque:** cambia cuándo aparece el subtítulo.
- **Arrastrar el borde izquierdo o derecho:** cambia el inicio o el final.
- **Rueda del ratón:** desplaza; **Ctrl + rueda:** zoom.
- **Zoom − / Zoom + / Ajustar al proyecto** y la barra inferior: navegación y zoom.
- Los marcadores se ven como líneas discontinuas amarillas.

---

## 6. Panel derecho — pestaña «Subtítulos»

### 6.1 Herramientas

| Botón | Función |
|---|---|
| **+ Nuevo** | Crea un subtítulo en la posición actual del vídeo. |
| **Buscar y reemplazar** | Busca palabras, las sustituye una a una o todas a la vez (con opción de distinguir mayúsculas). |
| **Corregir texto** | Arregla espacios, signos de puntuación, mayúscula inicial y palabras repetidas (en los seleccionados o en todos). |
| **Quitar muletillas** | Elimina «eh», «em», «mm», «um», «o sea,», «este,» y similares. |
| **Analizar subtítulos** | Revisa duración, solapamientos, velocidad de lectura, texto demasiado largo, repetidos, vacíos y tiempos inválidos. Con **Corregir automáticamente** los arregla. |
| **Eliminar selección** | Borra los subtítulos seleccionados (se puede deshacer). |
| **Sincronía: Desplazar** | Adelanta o retrasa los subtítulos seleccionados (o todos) los segundos que escribas (negativo = adelantar). Sirve para corregir un desfase general. |
| **Inicio = cursor / Fin = cursor** | Ajusta el inicio o el final del subtítulo seleccionado a la posición actual del vídeo. Ideal para afinar a ojo. |

### 6.2 Cada subtítulo en la lista

Cada bloque muestra número, **inicio**, **final**, duración, un estado (✓ correcto / ⚠ aviso), el texto y un contador de caracteres y palabras.

- **Clic en el bloque:** lo selecciona y lleva el vídeo a su inicio. **Ctrl/Mayús + clic en el número:** selección múltiple.
- Los tiempos y el texto se editan directamente (formato `hh:mm:ss.mmm`).

| Botón | Función |
|---|---|
| **−.1 / +.1** | Adelanta o retrasa ese subtítulo 0,1 s. |
| **✂** | Divide el subtítulo (en el cursor del texto o en la posición del vídeo). |
| **↑∪ / ∪↓** | Une con el anterior o con el siguiente. |
| **★** | Resalta la parte del texto seleccionada (la rodea con `*asteriscos*` y se verá con el color de resaltado). |
| **🎨** | Abre el estilo solo para ese subtítulo. |
| **🗑** | Elimina el subtítulo. |

Debajo de la lista, un panel de **información** muestra para el subtítulo elegido: tiempos, duración, caracteres, palabras, velocidad de lectura y estado.

---

## 7. Panel derecho — pestaña «Estilo»

Los cambios se ven al instante sobre el vídeo (si no hay subtítulo en pantalla, aparece uno de ejemplo).

| Sección | Para qué sirve |
|---|---|
| **Aplicar a** | *Todos los subtítulos* o *Seleccionados* (estilo propio solo para esos). |
| **Estilo predefinido** | Aplica un estilo completo (ver lista abajo). |
| **Guardar como nuevo estilo** | Guarda el estilo actual con tu nombre para reutilizarlo. |
| **Quitar estilo propio a seleccionados** | Devuelven esos subtítulos al estilo general. |
| **Tipografía** | Fuente, tamaño, peso, cursiva, subrayado y MAYÚSCULAS. |
| **Color del texto** | Color en selector o HEX. |
| **Fondo** | Sin fondo o caja (color, opacidad, bordes redondeados, relleno). |
| **Contorno** | Color, grosor y opacidad del borde del texto. |
| **Sombra** | Color, opacidad, desplazamiento X/Y y desenfoque. |
| **Posición y alineación** | Cuadrícula de 9 posiciones o modo avanzado X/Y en %; alineación, ancho máximo, interlineado y espaciado. |
| **Efectos** | Animación de entrada (aparecer, pop, deslizar, zoom), brillo/neón y degradado de texto. |
| **Resaltado y karaoke** | Color y peso de las palabras entre `*asteriscos*` y la **animación por palabra** (ver abajo). |

### Estilos predefinidos

**Clásicos:** Classic, Cinematic, Social, Viral, YouTube, Reels, TikTok, Minimal.
**Nuevos:** Barrido karaoke, Relleno progresivo, Hormozi, Caja activa, Una palabra, Máquina de escribir, Neón, Degradado, Cómic, Retro.

### Tipos de animación por palabra (activa «Animación por palabra»)

| Tipo | Efecto |
|---|---|
| **Palabra activa (color)** | La palabra que se está diciendo cambia de color. |
| **Relleno progresivo** | Las palabras ya dichas se quedan coloreadas. |
| **Barrido suave** | El color se desplaza de izquierda a derecha dentro de cada palabra mientras se lee. |
| **Pop** | La palabra activa crece un poco y cambia de color. |
| **Caja sobre la palabra** | Una caja de color sigue a la palabra activa. |
| **Aparece palabra a palabra** | El texto va apareciendo a medida que se dice. |
| **Una palabra cada vez** | Solo se muestra la palabra que se está diciendo, grande y centrada. |

---

## 8. Exportar

| Opción | Qué hace |
|---|---|
| **SRT / VTT / TXT** | Archivos de subtítulos estándar (texto sin estilos). |
| **ASS** | Conserva fuente, tamaño, color, contorno, sombra, posición, alineación y el karaoke de color. El brillo, el degradado y algunos efectos no se exportan en ASS. |
| **Exportar vídeo** | Genera el vídeo con los subtítulos **quemados** en las imágenes, tal como los ves en la previsualización. |

Opciones del vídeo: **resolución** (720p, 1080p u original), **FPS** (24, 25, 30, 60), **calidad** (baja, media, alta) y **contenedor** (MP4 si tu navegador lo permite, o WebM).

> El vídeo se renderiza **en tiempo real**: tarda lo mismo que dura el vídeo y debes **mantener la pestaña visible** hasta terminar. Se puede cancelar en cualquier momento.

---

## 9. Proyectos y guardado

- **Autoguardado:** la app guarda sola tu trabajo en el navegador. En la barra inferior verás «Guardado automáticamente hace X s». Si cierras sin querer, en la pantalla de bienvenida aparece **Recuperar trabajo anterior**.
- **Guardar proyecto (.ssp):** copia de seguridad que puedes abrir otro día o en otro equipo (recuerda volver a cargar el vídeo).

---

## 10. Atajos de teclado

| Atajo | Acción |
|---|---|
| `Espacio` | Reproducir / pausar |
| `←` `→` | Mover la reproducción 1 s |
| `Mayús + ←` `→` | Desplazar el subtítulo seleccionado 0,1 s |
| `Enter` | Reproducir el subtítulo seleccionado |
| `Supr` | Eliminar los seleccionados |
| `S` | Dividir el subtítulo en el cursor de reproducción |
| `M` | Unir con el siguiente |
| `Ctrl + Z` / `Ctrl + Y` | Deshacer / rehacer |
| `Ctrl + S` | Guardar proyecto |
| `Ctrl + E` | Exportar |

---

## 11. Solución de problemas

| Problema | Qué hacer |
|---|---|
| No carga el modelo | Pulsa **Diagnóstico** en «Modelos locales», copia el informe y envíamelo. Comprueba que tienes Internet la primera vez (el motor se descarga) y que el modelo está en formato ONNX. |
| Chrome no deja usar mi carpeta | Chrome bloquea Documentos, Descargas, Escritorio y carpetas con archivos del sistema. Crea una carpeta propia (por ejemplo `WhisperModels`) o usa **Modo compatible**. |
| Chrome vuelve a pedir permiso de la carpeta | Es normal. Pulsa **Seleccionar carpeta** o **Iniciar transcripción** para reactivarla; el modelo ya guardado sigue funcionando desde la caché. |
| No veo la línea de tiempo | Comprueba que estás en modo **Profesional** (arriba a la derecha). |
| Los subtítulos salen desfasados | Usa **Sincronía → Desplazar** para mover todos, o **Inicio/Fin = cursor** para afinar uno. |
| Salen subtítulos de ruido o música | Procesa el audio (sección 4.4) y vuelve a transcribir, y fija el idioma en vez de «automático». |
| Error de memoria | Prueba con el modelo *Tiny* cuantizado o con un archivo más corto. |
| El audio procesado no suena | Comprueba que **A/B** esté en «procesado» y que el volumen no esté silenciado. |

---

## 12. Límites que conviene conocer

- El reductor de música es de procesado de señal, no de IA.
- La exportación de vídeo funciona en tiempo real.
- El ASS exporta de forma aproximada los efectos avanzados.
- No detecta distintos hablantes ni se instala como aplicación (PWA).
- Los `.bin` de whisper.cpp no son compatibles; se necesitan modelos ONNX.

---

## ¿Necesitas ayuda?

Si necesitas una explicación o tienes alguna duda, contáctame:

- **WhatsApp:** 5355081288
- **Email:** corderorauly@gmail.com
