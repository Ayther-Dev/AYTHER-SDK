# AYTHER SDK

> **Estado:** Experimental / Developer Preview  
> **Aviso:** Las APIs, la ABI y los contratos públicos están en desarrollo activo y sujetos a cambios incompatibles antes de la versión 1.0.

**AYTHER SDK** es el conjunto público de contratos, APIs, herramientas CLI, ejemplos y pruebas de conformidad para interactuar con **AYTHER Engine**. Permite crear, inspeccionar, firmar y validar paquetes de recursos (`.ay`) de forma abierta e independiente, sin depender de herramientas propietarias como AYTHER Lab.

### ¿Qué es AYTHER?
AYTHER remasteriza en tiempo real la capa audiovisual de videojuegos retro 2D preservando intacta la lógica original de la ROM. Intercepta los sprites, tiles y eventos de audio generados por un core de emulación y los sustituye dinámicamente por assets de alta fidelidad contenidos en un pack `.ay`.

---

## ¿A quién está dirigido?

* **Desarrolladores de emuladores y frontends:** Integración de la sesión de remasterización en runtimes, launchers y aplicaciones nativas.
* **Creadores de herramientas y pipelines:** Automatización, inspección de memoria y autoría de assets sin intermediarios.
* **Autores técnicos de packs:** Creación y firma de packs `.ay` mediante flujos basados en CLI y scripts.
* **Investigadores y preservadores:** Documentación, pruebas de conformidad e interoperabilidad abierta sobre hardware clásico.
* **Estudios y publishers:** Evaluación técnica de la tecnología de remasterización en tiempo real para catálogos retro.

---

## Capacidades

### Lo que puedes hacer hoy
* **Integración del ciclo de sesión:** Controlar el ciclo de vida de AYTHER Engine desde aplicaciones nativas (C/C++).
* **Observabilidad de hardware:** Inspeccionar sprites, planos de tiles y eventos de audio mediante el ABI observable en tiempo de ejecución.
* **Identidad bit-exacta:** Generar identificadores unívocos para patrones gráficos y sonoros.
* **Gestión de paquetes `.ay`:** Crear, validar, firmar, verificar e inspeccionar contenedores `.ay`.
* **Scripting seguro:** Desarrollar extensiones de comportamiento con scripts Lua ejecutados dentro del sandbox de AYTHER.
* **Pruebas de conformidad:** Validar integraciones y herramientas contra fixtures y especificaciones abiertas.

### Fuera del alcance
* **Distribución de ROMs, BIOS o cores:** El SDK no suministra material protegido por derechos de autor.
* **Garantía de estabilidad ABI/API:** No se garantiza compatibilidad binaria hasta el release 1.0.
* **Sustitución de UI:** No reemplaza la suite visual de edición en tiempo real de AYTHER Lab.
* **Módulos comerciales:** Extensiones propietarias o profesionales se distribuyen bajo licencias independientes.

---

## Estado de Madurez y Roadmap

El SDK se encuentra en fase de consolidación técnica.

| Componente | Estado | Situación actual |
| :--- | :--- | :--- |
| **Especificación de Formato (`.ay`)** | 🔴 En progreso | Especificación base lista; cerrando paridad entre generadores y consumidores. |
| **API C / FFI** | 🔴 En progreso | Funcional para integración nativa; superficie pública sujeta a refactorización. |
| **ABI Observable** | 🔴 En progreso | Inspección funcional en cores adaptados (ej. Genesis / Mega Drive). |
| **Herramientas CLI** | 🔴 En progreso | Empaquetado, firma e inspección funcionales; distribución binaria en preparación. |
| **Sandbox Lua** | 🔴 En progreso | Entorno seguro funcional; superficie de API de scripting en expansión. |
| **CI / Fixtures E2E** | 🔴 En progreso | Pipeline de verificación automatizada en construcción. |

---

## Soporte de Plataformas y Sistemas

### Cores y Sistemas de Juego

| Plataforma | Estado | Notas |
| :--- | :--- | :--- |
| **Sega Genesis / Mega Drive** | Experimental | Implementada sobre el core fork compatible y el modelo observable de AYTHER. |
| **Otras plataformas** | En evaluación | Solo se anunciarán cuando cuenten con pruebas de conformidad verificables en CI. |

### Sistemas Operativos (Host)

El motor utiliza **CMake, Rust, SDL3 y Vulkan**. La compatibilidad oficial se certifica exclusivamente mediante pruebas continuas en CI:

| Sistema Operativo | Arquitectura | Estado |
| :--- | :--- | :--- |
| **Windows** | x86-64 | Entorno principal de desarrollo; empaquetado público pendiente. |
| **Linux** | x86-64 | Funcional; verificación y packaging en progreso. |
| **macOS** | Universal | En evaluación técnica (no soportado oficialmente aún). |

---

## Lenguajes e Interfaces

| Capa | Lenguaje | Estado |
| :--- | :--- | :--- |
| **Integración nativa (Core/Engine)** | C / C++ | FFI C base disponible; encabezados finales en definición. |
| **Herramientas CLI / Automatización** | Rust / C++ | Se distribuirán como binarios independientes. |
| **Scripting de packs** | Lua | API en sandbox seguro (sin acceso arbitrario a disco/red). |
| **Bindings de alto nivel** | Por definir | Planificados post-1.0 según la demanda comunitaria. |

---

## Flujo de Trabajo (Pipeline Abierto)

El SDK permite desacoplar la creación del pack de cualquier entorno gráfico comercial:

```text
  ┌───────────────────┐
  │  ROM + Core Local │
  └─────────┬─────────┘
            ▼
  ┌────────────────────────┐
  │ Herramienta de         │
  │ Observación / Captura  │
  └─────────┬──────────────┘
            ▼
  ┌────────────────────────┐
  │ observed_*.toml        │ ◄─── Assets remasterizados (PNG, WAV, etc.)
  └─────────┬──────────────┘
            ▼
  ┌────────────────────────┐
  │ Herramienta de Build   │ ◄─── Reglas, metadatos y scripts Lua
  └─────────┬──────────────┘
            ▼
  ┌────────────────────────┐
  │ Validación y Firma     │
  └─────────┬──────────────┘
            ▼
       Paquete .ay
```

> **Importante:** Los fixtures, ejemplos y repositorios del SDK **nunca** deben incluir ROMs comerciales ni material sujeto a copyright. Utilice únicamente homebrew, assets propios o material de dominio público.

---

## Instalación

Actualmente el código reside en el monorepo principal y no cuenta con paquetes precompilados en gestores de dependencias externos.

### Distribución planificada (v0.1+)
Las entregas oficiales incluirán:
* Headers C/C++ públicos (`include/ayther/`).
* Archivos de configuración CMake (`AytherConfig.cmake`) y `pkg-config`.
* Binarios CLI para inspección, validación y firma (`ayther-cli`).
* Esquemas JSON/TOML de validación formal para metadatos.
* Fixtures sintéticos redistribuibles para testing.
* Checksums SHA-256 y SBOM (Software Bill of Materials).

---

## Ecosistema AYTHER

| Componente | Rol en el ecosistema | Relación con el SDK |
| :--- | :--- | :--- |
| **AYTHER Core** | Hashing, gestión de packs, criptografía y sandbox. | Provee las primitivas expuestas vía FFI. |
| **AYTHER Engine** | Emulación, renderizado Vulkan/SDL3 y mezcla de audio. | Motor de ejecución principal consumido por integradores. |
| **AYTHER Runtime** | Host de referencia para sesiones de juego. | Aplicación de referencia que demuestra el uso del SDK. |
| **AYTHER Play** | Launcher de usuario final e integración con Hub. | Consume los contratos de ejecución y catálogo. |
| **AYTHER Lab** | IDE visual para edición y captura en tiempo real. | Produce packs `.ay` usando los mismos contratos públicos. |
| **AYTHER Hub** | Servicio de distribución e indexación de packs. | Valida manifiestos, identidades y firmas generadas vía SDK. |

*Nota: AYTHER Lab aporta productividad visual (timelines, captura asistida, depuración gráfica), pero el formato `.ay` y el SDK son 100% abiertos y programables sin él.*

---

## Principios Legales: BYOR y BYOC

El diseño técnico y legal de AYTHER se fundamenta en la estricta separación de responsabilidades:

* **BYOR (Bring Your Own ROM):** AYTHER no incluye, comercializa ni aloja ROMs o BIOS. Los packs `.ay` solo contienen reemplazos visuales/sonoros, metadatos e instrucciones de inyección. El usuario final debe aportar su propia copia legítima del software.
* **BYOC (Bring Your Own Core):** El SDK no redistribuye núcleos de emulación de terceros (como cores libretro). Los integradores y usuarios deben suministrar núcleos compatibles respetando sus respectivas licencias (GPL, MIT, etc.).

> *BYOR y BYOC establecen un límite técnico de distribución; los desarrolladores, integradores y autores son responsables de garantizar los derechos sobre los assets, marcas y código que utilicen.*

---

## Seguridad

Los archivos `.ay`, scripts y cores externos deben tratarse siempre como **entradas no confiables (*untrusted input*)**.

El SDK implementa y exige:
* Validación estricta de rutas relativas dentro de los packs (prevención de *Directory Traversal*).
* Límites duros de descompresión (protección contra *Zip Bombs*).
* Verificación criptográfica de manifiestos y firmas digitales.
* Ejecución de scripts en entornos Lua con sandbox hermético (sin acceso a sockets, procesos ni sistema de archivos no asignado).

---

## Licencia, Compatibilidad y Marcas

* **Licencia de Código:** En proceso de definición. La ausencia actual de un archivo `LICENSE` en la raíz implica que todos los derechos están reservados hasta la publicación de las licencias abiertas oficiales.
* **Versionado:**
  * El SDK adoptará **SemVer** a partir de la versión `1.0.0`.
  * La especificación del formato `.ay` y la ABI del motor mantienen ciclos de versionado independientes de la distribución del SDK.
* **Marcas Registradas:** `AYTHER`, sus logotipos y elementos de identidad visual son marcas del proyecto AYTHER. Los nombres comerciales de consolas, fabricantes o videojuegos mencionados pertenecen exclusivamente a sus respectivos titulares y se usan solo con fines de identificación técnica e interoperabilidad.

---
