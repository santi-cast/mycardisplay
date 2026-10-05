# MyCarDisplay

  > 🚧 **En desarrollo activo** · Nombre provisional · Proyecto personal sin afiliación con Google.

  ![Kotlin](https://img.shields.io/badge/Kotlin-2.1-7F52FF?logo=kotlin&logoColor=white)
  ![Android](https://img.shields.io/badge/Android-API%2032%2B-3DDC84?logo=android&logoColor=white)
  ![C++](https://img.shields.io/badge/C%2B%2B-JNI-00599C?logo=cplusplus&logoColor=white)
  ![Python](https://img.shields.io/badge/Python-tooling-3776AB?logo=python&logoColor=white)
  ![AI agents](https://img.shields.io/badge/Desarrollo-con_agentes_IA-8A2BE2)

  Dos apps Android que convierten una **tablet en la pantalla del coche**, proyectando
  navegación y multimedia desde el móvil por una conexión Wi-Fi local.

  Además de un producto, MyCarDisplay es mi **laboratorio para aprender a desarrollar
  con agentes de IA de forma profesional**: lo construyo para ganar experiencia real con
  flujos agénticos y consolidar conocimientos nuevos (Android a bajo nivel, vídeo,
  C++/JNI) en un problema técnico exigente.

  El código aún no es público: este repositorio documenta el proyecto y su avance.

  ## El problema

  Muchos coches no tienen una pantalla moderna, pero una tablet sí. Las soluciones
  existentes dependen de hardware adicional o de configuraciones frágiles. Partí de
  un sistema propio basado en proyectos de la comunidad, que uso a diario, y ahora
  construyo uno nuevo con un diseño propio y deliberado.

  ## Arquitectura

  ```
  ┌────────────────────┐   Wi-Fi local (LocalOnlyHotspot)   ┌────────────────────┐
  │  Phone Coordinator │ ─────────────────────────────────▶ │  Tablet Receiver   │
  │  emparejamiento,   │        vídeo H.264 + control       │  sesión, vídeo,    │
  │  red, codificador, │ ◀───────────────────────────────── │  audio, táctil     │
  │  limpieza segura   │                                    │  (Kotlin + JNI)    │
  └────────────────────┘                                    └────────────────────┘
  ```

  - **Kotlin** para todo el comportamiento Android; **C++/JNI** fino solo donde hace falta.
  - Núcleo de sesión compartido con colas acotadas y máquinas de estado explícitas.

  ## Cómo lo desarrollo: agentes de IA con método

  Trabajo con agentes de IA sobre **Pi** +
  [**Gentle Shell**](https://github.com/Gentleman-Programming/gentle-shell) y
  [**Gentle AI**](https://github.com/Gentleman-Programming/gentle-ai). Los agentes
  ejecutan; yo decido el alcance, apruebo cada unidad de trabajo y nada entra sin tests.

  | Práctica | Qué significa en este proyecto |
  |---|---|
  | **Spec-Driven Development (SDD)** | El MVP y un RFC con la matriz de comportamiento se aprobaron antes de escribir código de producto. |
  | **Organic Driven Development (ODD)** | El trabajo grande se divide en unidades pequeñas (~400 líneas), cada una con sus tests, su documentación y su commit. |
  | **Receipt-Driven Development (RDD)** | Cada cambio pasa una revisión independiente antes del commit. |
  | **Memoria persistente** | [Engram](https://github.com/Gentleman-Programming/engram) conserva decisiones y contexto entre sesiones. |
  | **Test-first** | Cada unidad empieza con un test que falla (RED) sobre el comportamiento real. |

  Lo que estoy aprendiendo: delegar sin perder el control, verificar de forma independiente
  lo que produce un agente, y escribir alcances lo bastante precisos para que un agente
  no se desvíe.

  ## Ingeniería destacada

  - **Diagnóstico en lugar de prueba y error:** formato de log versionado (V1→V4) con
    lector estricto en Python y *goldens* generados por el emisor Kotlin real,
    verificados en ambos lenguajes.
  - **Límites explícitos:** colas, plazos y presupuestos de memoria acotados y testeados.
  - **Procedencia y privacidad:** registro del origen de cada material externo; ningún
    dato personal ni de dispositivos en la evidencia.
- **Procedencia y privacidad:** registro del origen de cada material externo; ningún
  dato personal ni de dispositivos en la evidencia.

## Estado

| Área | Estado |
|---|---|
| MVP y RFC | ✅ Aprobados |
| Núcleo de sesión | ✅ Implementado y testeado |
| Handshake entre móvil y tablet (laboratorio) | ✅ Funciona en dispositivos reales |
| Codificador (móvil) y decodificador (tablet) | 🔧 Implementados; vídeo de extremo a extremo en curso |
| Diagnóstico integral V4 | 🔧 Móvil completo, tablet en curso |
| Audio, táctil, integración final | ⏳ Pendiente |

## Roadmap

- [x] Diseño del MVP y RFC
- [x] Núcleo de sesión con colas acotadas
- [x] Handshake de laboratorio entre dispositivos
- [x] Diagnóstico V4 del móvil
- [ ] Diagnóstico V4 de la tablet
- [ ] Vídeo visible de extremo a extremo
- [ ] Táctil y audio
- [ ] Publicación del código (pendiente de revisión de licencias y procedencia)

## Stack

Kotlin · Android (MediaCodec, EGL, LocalOnlyHotspot) · C++/JNI · Gradle · Python ·
Pi · Gentle Shell · Gentle AI · Engram

## Autor

**Santiago Castillo** · Desarrollo de Aplicaciones Multiplataforma · Madrid
[GitHub](https://github.com/santi-cast) · Buscando empresa para la formación en empresa del DAM
