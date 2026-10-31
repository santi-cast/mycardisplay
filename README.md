# MyCarDisplay

> 🚧 **En desarrollo activo** · Nombre provisional · Proyecto personal sin afiliación con Google.

![Kotlin](https://img.shields.io/badge/Kotlin-2.1-7F52FF?logo=kotlin&logoColor=white)
![Android](https://img.shields.io/badge/Android-API%2032%2B-3DDC84?logo=android&logoColor=white)
![Python](https://img.shields.io/badge/Python-tooling-3776AB?logo=python&logoColor=white)
![AI agents](https://img.shields.io/badge/Desarrollo-con_agentes_IA-8A2BE2)

Una app Android que convierte una **tablet en la pantalla del coche**: la tablet actúa
como receptor y muestra Android Auto proyectado desde el móvil (Google Maps, música y
asistente) por una conexión Wi-Fi local, con táctil y micrófono.

Además de un producto, MyCarDisplay es mi **laboratorio para aprender a desarrollar
con agentes de IA de forma profesional**: lo construyo para ganar experiencia real con
flujos agénticos y consolidar conocimientos nuevos (Android a bajo nivel, vídeo,
protocolos y TLS) en un problema técnico exigente.

El código aún no es público: este repositorio documenta el proyecto y su avance.

## Cómo nació

Mi coche es antiguo: no tiene pantalla ni navegador. Tenía una tablet vieja y se me
ocurrió darle una segunda vida como **la pantalla de un coche moderno**:
Google Maps, música y asistente en el salpicadero, controlados desde la tablet, sin
cambiar la radio ni comprar hardware.

Las soluciones existentes dependen de hardware adicional o de configuraciones
frágiles. Primero monté un sistema propio basado en proyectos de la comunidad, que
uso a diario. Ahora construyo uno nuevo con **arquitectura y código propios**,
usando aquel sistema solo como referencia de lo que funciona.

## Arquitectura

```
┌──────────────────────┐   Wi-Fi local (hotspot del móvil)   ┌──────────────────────┐
│  Móvil               │ ──────────────────────────────────▶ │  Tablet Receiver     │
│  Android Auto        │   protocolo de proyección sobre TLS │  protocolo propio en │
│  (Maps, música,      │ ◀────────────────────────────────── │  Kotlin: vídeo,      │
│  asistente)          │   vídeo · táctil · micrófono · audio│  táctil, micrófono   │
└──────────────────────┘                                     └──────────────────────┘
```

- **Fase 1 — receptor en la tablet:** la capa de protocolo se escribe en Kotlin, canal
  por canal (vídeo, táctil, micrófono, audio del sistema, sensores, estado).
- **Fase 2 — arranque automático desde el móvil:** al conectar el Bluetooth del coche,
  preparar la red y la sesión sin tocar el móvil.
- Núcleo de sesión compartido con colas acotadas y máquinas de estado explícitas.

## Cómo lo desarrollo: agentes de IA con método

Trabajo con agentes de IA sobre **Pi** +
[**Gentle Shell**](https://github.com/Gentleman-Programming/gentle-shell) y
[**Gentle AI**](https://github.com/Gentleman-Programming/gentle-ai). Los agentes
ejecutan; yo decido el alcance, apruebo cada unidad de trabajo y nada entra sin tests.

| Práctica | Qué significa en este proyecto |
|---|---|
| **Spec-Driven Development (SDD)** | El MVP y un RFC con la matriz de comportamiento se aprueban antes de escribir código de producto; cada cambio de rumbo se registra como enmienda. |
| **Organic Driven Development (ODD)** | El trabajo grande se divide en unidades pequeñas (~400 líneas), cada una con sus tests, su documentación y su commit. |
| **Receipt-Driven Development (RDD)** | Cada cambio pasa una revisión independiente antes del commit. |
| **Memoria persistente** | [Engram](https://github.com/Gentleman-Programming/engram) conserva decisiones y contexto entre sesiones. |
| **Test-first** | Cada unidad empieza con un test que falla (RED) sobre el comportamiento real. |
| **Diagnóstico con dispositivos reales** | El agente opera `adb` con permisos por niveles que yo autorizo, captura logs acotados y compara nuestras sesiones con un sistema de referencia que ya funciona. |

Lo que estoy aprendiendo: delegar sin perder el control, verificar de forma independiente
lo que produce un agente, y escribir alcances lo bastante precisos para que un agente
no se desvíe.

## Ingeniería destacada

- **Diagnóstico en lugar de prueba y error:** formato de log versionado (V1→V4) con
  lector estricto en Python y *goldens* generados por el emisor Kotlin real,
  verificados en ambos lenguajes.
- **Sonda de protocolo propia:** una herramienta en Python que habla con el móvil real
  (negociación de versión, TLS y descubrimiento de servicios) y atribuye cada fallo a
  su fase con tiempos medidos.
- **Comparación contra una referencia:** capturas acotadas de una sesión que funciona
  y de la nuestra, para localizar exactamente dónde se separan.
- **Límites explícitos:** colas, plazos y presupuestos de memoria acotados y testeados.
- **Procedencia y privacidad:** registro del origen de cada material externo; ningún
  dato personal ni de dispositivos en la evidencia.

## Estado

| Área | Estado |
|---|---|
| MVP y RFC (incluida la enmienda del receptor propio) | ✅ Aprobados |
| Núcleo de sesión | ✅ Implementado y testeado |
| Decodificador de vídeo en la tablet | ✅ Implementado y testeado |
| Handshake entre móvil y tablet (laboratorio) | ✅ Funciona en dispositivos reales |
| Sonda de protocolo contra el móvil real | 🔧 Versión, TLS y descubrimiento alcanzados; apertura de canales en estudio |
| Arquitectura del receptor (RFC 0003) | ⏳ Pendiente |
| Arranque automático desde el móvil | ⏳ Pendiente (fase 2) |

## Roadmap

- [x] Diseño del MVP y RFC
- [x] Núcleo de sesión con colas acotadas
- [x] Handshake de laboratorio entre dispositivos
- [x] Sonda de protocolo: versión, TLS y descubrimiento
- [x] Calibración contra un sistema de referencia que funciona
- [ ] RFC 0003: arquitectura del receptor en Kotlin
- [ ] Vídeo visible de extremo a extremo
- [ ] Táctil, micrófono y audio del sistema
- [ ] Arranque automático desde el móvil (fase 2)
- [ ] Publicación del código (pendiente de revisión de licencias y procedencia)

## Stack

Kotlin · Android (MediaCodec, EGL, redes locales) · Gradle · Python · adb ·
Pi · Gentle Shell · Gentle AI · Engram

## Autor

**Santiago Castillo** · Desarrollo de Aplicaciones Multiplataforma · Madrid
[GitHub](https://github.com/santi-cast) · Buscando empresa para la formación en empresa del DAM
