# MyCarDisplay

> 🚧 **En desarrollo activo** · Nombre provisional · Proyecto personal sin afiliación con Google.

![Kotlin](https://img.shields.io/badge/Kotlin-2.x-7F52FF?logo=kotlin&logoColor=white)
![Android](https://img.shields.io/badge/Android-API%2032%2B-3DDC84?logo=android&logoColor=white)
![C++](https://img.shields.io/badge/C%2B%2B-JNI-00599C?logo=cplusplus&logoColor=white)
![Python](https://img.shields.io/badge/Python-tooling-3776AB?logo=python&logoColor=white)

Sistema de dos apps Android que usa una **tablet como pantalla del coche**,
proyectando navegación y multimedia desde el móvil por una conexión local.

El código aún no es público: este repositorio documenta el proyecto y su avance.

## El problema

Muchos coches no tienen una pantalla moderna, pero una tablet sí. Las soluciones
existentes dependen de hardware adicional o de configuraciones frágiles. Partí de
un sistema propio basado en proyectos de la comunidad que uso a diario, y ahora
estoy construyendo uno nuevo con un diseño propio y deliberado.

## Arquitectura

┌────────────────────┐   Wi-Fi local (LocalOnlyHotspot)   ┌────────────────────┐
│  Phone Coordinator │ ─────────────────────────────────▶ │  Tablet Receiver   │
│  emparejamiento,   │        vídeo H.264 + control       │  sesión, vídeo,    │
│  red, codificador, │ ◀───────────────────────────────── │  audio, táctil     │
│  limpieza segura   │                                    │  (Kotlin + JNI)    │
└────────────────────┘                                    └────────────────────┘

- **Kotlin** para todo el comportamiento Android; **C++/JNI** fino solo donde hace falta.
- Núcleo de sesión compartido con colas acotadas y máquinas de estado explícitas.

## Ingeniería destacada

- **RFC antes del código**: el MVP y su matriz de comportamiento se aprobaron antes de escribir producto.
- **Test-first**: cada unidad empieza con un test que falla (RED) sobre el comportamiento real.
- **Diagnóstico en lugar de prueba y error**: formato de log versionado (V1→V4) con lector
  estricto en Python y *goldens* generados por el emisor Kotlin real, verificados en ambos lenguajes.
- **Desarrollo asistido por IA, trazable**: yo dirijo, los agentes ejecutan; cada cambio
  pasa por verificación independiente y revisión antes del commit.
- **Procedencia y privacidad**: registro de origen de cada material externo; ningún dato
  personal o de dispositivos en la evidencia publicada.

## Estado

| Área | Estado |
|---|---|
| MVP y RFC | ✅ Aprobados |
| Handshake entre móvil y tablet (laboratorio) | ✅ Funciona en dispositivos reales |
| Codificador (móvil) y decodificador (tablet) | 🔧 Implementados, vídeo extremo a extremo aún sin lograr |
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

Kotlin · Android (MediaCodec, EGL, LocalOnlyHotspot) · C++/JNI · Gradle · Python (tooling y tests)

## Autor

**Santiago Castillo** · Desarrollo de Aplicaciones Multiplataforma · Madrid
[GitHub](https://github.com/santi-cast) · Buscando prácticas en empresa
