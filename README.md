<div align="center">
    <img src="./media/logo_large.webp" alt="Logo de Spec Kit" width="200" height="200"/>
    <h1>🌱 Spec Kit</h1>
    <h3><em>Construye software de alta calidad más rápido.</em></h3>
</div>

<p align="center">
    <strong>Un toolkit de código abierto que te permite enfocarte en escenarios de producto y resultados predecibles en lugar de codificar cada pieza desde cero.</strong>
</p>

<p align="center">
    <a href="https://github.com/github/spec-kit/actions/workflows/release.yml"><img src="https://github.com/github/spec-kit/actions/workflows/release.yml/badge.svg" alt="Release"/></a>
    <a href="https://github.com/github/spec-kit/stargazers"><img src="https://img.shields.io/github/stars/github/spec-kit?style=social" alt="Estrellas en GitHub"/></a>
    <a href="https://github.com/github/spec-kit/blob/main/LICENSE"><img src="https://img.shields.io/github/license/github/spec-kit" alt="Licencia"/></a>
    <a href="https://github.github.io/spec-kit/"><img src="https://img.shields.io/badge/docs-GitHub_Pages-blue" alt="Documentación"/></a>
</p>

---

## Tabla de Contenidos

- [🤔 ¿Qué es el Desarrollo Dirigido por Especificaciones?](#-qué-es-el-desarrollo-dirigido-por-especificaciones)
- [⚡ Primeros Pasos](#-primeros-pasos)
- [📽️ Video General](#️-video-general)
- [🚶 Guías de la Comunidad](#-guías-de-la-comunidad)
- [🤖 Agentes de IA Soportados](#-agentes-de-ia-soportados)
- [🔧 Referencia del CLI Specify](#-referencia-del-cli-specify)
- [📚 Filosofía Central](#-filosofía-central)
- [🌟 Fases de Desarrollo](#-fases-de-desarrollo)
- [🎯 Objetivos Experimentales](#-objetivos-experimentales)
- [🔧 Prerrequisitos](#-prerrequisitos)
- [📖 Más Información](#-más-información)
- [📋 Proceso Detallado](#-proceso-detallado)
- [🔍 Solución de Problemas](#-solución-de-problemas)
- [💬 Soporte](#-soporte)
- [🙏 Agradecimientos](#-agradecimientos)
- [📄 Licencia](#-licencia)

## 🤔 ¿Qué es el Desarrollo Dirigido por Especificaciones?

El Desarrollo Dirigido por Especificaciones **invierte el guion** del desarrollo de software tradicional. Durante décadas, el código ha sido el rey — las especificaciones eran solo el andamiaje que construíamos y descartábamos una vez que comenzaba el "trabajo real" de codificar. El Desarrollo Dirigido por Especificaciones cambia esto: **las especificaciones se vuelven ejecutables**, generando directamente implementaciones funcionales en lugar de solo guiarlas.

## ⚡ Primeros Pasos

### 1. Instalar el CLI Specify

Elige tu método de instalación preferido:

#### Opción 1: Instalación Persistente (Recomendada)

Instala una vez y úsalo en cualquier lugar:

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

Luego usa la herramienta directamente:

```bash
# Create new project
specify init <PROJECT_NAME>

# Or initialize in existing project
specify init . --ai claude
# or
specify init --here --ai claude

# Check installed tools
specify check
```

Para actualizar Specify, consulta la [Guía de Actualización](./docs/upgrade.md) con instrucciones detalladas. Actualización rápida:

```bash
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
```

#### Opción 2: Uso Único

Ejecuta directamente sin instalar:

```bash
# Create new project
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>

# Or initialize in existing project
uvx --from git+https://github.com/github/spec-kit.git specify init . --ai claude
# or
uvx --from git+https://github.com/github/spec-kit.git specify init --here --ai claude
```

**Beneficios de la instalación persistente:**

- La herramienta permanece instalada y disponible en el PATH
- No es necesario crear alias de shell
- Mejor gestión de herramientas con `uv tool list`, `uv tool upgrade`, `uv tool uninstall`
- Configuración de shell más limpia

### 2. Establecer los principios del proyecto

Inicia tu asistente de IA en el directorio del proyecto. Los comandos `/speckit.*` están disponibles en el asistente.

Usa el comando **`/speckit.constitution`** para crear los principios rectores y las directrices de desarrollo de tu proyecto que guiarán todo el desarrollo posterior.

```bash
/speckit.constitution Create principles focused on code quality, testing standards, user experience consistency, and performance requirements
```

### 3. Crear la especificación

Usa el comando **`/speckit.specify`** para describir lo que quieres construir. Enfócate en el **qué** y el **por qué**, no en el stack tecnológico.

```bash
/speckit.specify Build an application that can help me organize my photos in separate photo albums. Albums are grouped by date and can be re-organized by dragging and dropping on the main page. Albums are never in other nested albums. Within each album, photos are previewed in a tile-like interface.
```

### 4. Crear un plan de implementación técnica

Usa el comando **`/speckit.plan`** para proporcionar tu stack tecnológico y decisiones de arquitectura.

```bash
/speckit.plan The application uses Vite with minimal number of libraries. Use vanilla HTML, CSS, and JavaScript as much as possible. Images are not uploaded anywhere and metadata is stored in a local SQLite database.
```

### 5. Desglosar en tareas

Usa **`/speckit.tasks`** para crear una lista de tareas accionables a partir de tu plan de implementación.

```bash
/speckit.tasks
```

### 6. Ejecutar la implementación

Usa **`/speckit.implement`** para ejecutar todas las tareas y construir tu funcionalidad según el plan.

```bash
/speckit.implement
```

Para instrucciones detalladas paso a paso, consulta nuestra [guía completa](./spec-driven.md).

## 📽️ Video General

¿Quieres ver Spec Kit en acción? ¡Mira nuestro [video general](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)!

[![Encabezado del video de Spec Kit](/media/spec-kit-video-header.jpg)](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)

## 🚶 Guías de la Comunidad

Observa el Desarrollo Dirigido por Especificaciones en acción en diferentes escenarios con estas guías contribuidas por la comunidad:

- **[Herramienta CLI .NET desde cero (Greenfield)](https://github.com/mnriem/spec-kit-dotnet-cli-demo)** — Construye una utilidad de zonas horarias como herramienta CLI de binario único en .NET desde un directorio vacío, cubriendo el flujo completo de spec-kit: constitution, specify, plan, tasks e implement en múltiples pasadas usando agentes de GitHub Copilot.

- **[Plataforma Spring Boot + React desde cero (Greenfield)](https://github.com/mnriem/spec-kit-spring-react-demo)** — Construye una plataforma de análisis de rendimiento de LLM (API REST, gráficos, seguimiento de iteraciones) desde cero usando Spring Boot, React embebido, PostgreSQL y Docker Compose, con un paso de clarify y un análisis de consistencia entre artefactos incluido.

- **[Extensión CMS ASP.NET existente (Brownfield)](https://github.com/mnriem/spec-kit-aspnet-brownfield-demo)** — Extiende un CMS .NET de código abierto existente (CarrotCakeCMS-Core, ~307,000 líneas de C#, Razor, SQL, JavaScript y archivos de configuración) con dos nuevas funcionalidades — infraestructura Docker Compose multiplataforma y una API REST headless con autenticación por token — demostrando cómo spec-kit se integra en bases de código existentes sin especificaciones ni constitución previas.

- **[Extensión de runtime Java existente (Brownfield)](https://github.com/mnriem/spec-kit-java-brownfield-demo)** — Extiende un runtime Jakarta EE de código abierto existente (Piranha, ~420,000 líneas de Java, XML, JSP, HTML y archivos de configuración en 180 módulos Maven) con una Consola de Administración del Servidor protegida por contraseña, demostrando spec-kit en un proyecto Java grande con múltiples módulos sin especificaciones ni constitución previas.

- **[Demo de dashboard Go / React existente (Brownfield)](https://github.com/mnriem/spec-kit-go-brownfield-demo)** — Demuestra spec-kit dirigido completamente desde la **terminal usando GitHub Copilot CLI**. Extiende el sistema de soporte terrestre de código abierto Hermes de la NASA (Go) con un dashboard web de telemetría ligero basado en React, mostrando que el flujo completo de constitution → specify → plan → tasks → implement funciona desde la terminal.

- **[Aplicación Spring Boot MVC desde cero con preset personalizado (Greenfield)](https://github.com/mnriem/spec-kit-pirate-speak-preset-demo)** — Construye una aplicación Spring Boot MVC desde cero usando un preset personalizado con habla pirata, demostrando cómo los presets pueden transformar toda la experiencia de spec-kit: las especificaciones se convierten en "Manifiestos de Viaje", los planes en "Planes de Batalla" y las tareas en "Asignaciones de Tripulación" — todo generado en jerga pirata completa sin cambiar ninguna herramienta.

## 🤖 Agentes de IA Soportados

| Agente                                                                               | Soporte | Notas                                                                                                                                     |
| ------------------------------------------------------------------------------------ | ------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| [Qoder CLI](https://qoder.com/cli)                                                   | ✅      |                                                                                                                                           |
| [Kiro CLI](https://kiro.dev/docs/cli/)                                               | ✅      | Usa `--ai kiro-cli` (alias: `--ai kiro`)                                                                                                 |
| [Amp](https://ampcode.com/)                                                          | ✅      |                                                                                                                                           |
| [Auggie CLI](https://docs.augmentcode.com/cli/overview)                              | ✅      |                                                                                                                                           |
| [Claude Code](https://www.anthropic.com/claude-code)                                 | ✅      |                                                                                                                                           |
| [CodeBuddy CLI](https://www.codebuddy.ai/cli)                                        | ✅      |                                                                                                                                           |
| [Codex CLI](https://github.com/openai/codex)                                         | ✅      |                                                                                                                                           |
| [Cursor](https://cursor.sh/)                                                         | ✅      |                                                                                                                                           |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli)                            | ✅      |                                                                                                                                           |
| [GitHub Copilot](https://code.visualstudio.com/)                                     | ✅      |                                                                                                                                           |
| [IBM Bob](https://www.ibm.com/products/bob)                                          | ✅      | Agente basado en IDE con soporte de slash commands                                                                                        |
| [Jules](https://jules.google.com/)                                                   | ✅      |                                                                                                                                           |
| [Kilo Code](https://github.com/Kilo-Org/kilocode)                                    | ✅      |                                                                                                                                           |
| [opencode](https://opencode.ai/)                                                     | ✅      |                                                                                                                                           |
| [Pi Coding Agent](https://pi.dev)                                                    | ✅      | Pi no tiene soporte MCP por defecto, por lo que `taskstoissues` no funcionará como se espera. Se puede añadir soporte MCP mediante [extensiones](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent#extensions) |
| [Qwen Code](https://github.com/QwenLM/qwen-code)                                     | ✅      |                                                                                                                                           |
| [Roo Code](https://roocode.com/)                                                     | ✅      |                                                                                                                                           |
| [SHAI (OVHcloud)](https://github.com/ovh/shai)                                       | ✅      |                                                                                                                                           |
| [Tabnine CLI](https://docs.tabnine.com/main/getting-started/tabnine-cli)             | ✅      |                                                                                                                                           |
| [Mistral Vibe](https://github.com/mistralai/mistral-vibe)                            | ✅      |                                                                                                                                           |
| [Kimi Code](https://code.kimi.com/)                                                  | ✅      |                                                                                                                                           |
| [Windsurf](https://windsurf.com/)                                                    | ✅      |                                                                                                                                           |
| [Antigravity (agy)](https://antigravity.google/)                                     | ✅      | Requiere `--ai-skills` |
| [Trae](https://www.trae.ai/)                                                         | ✅      |                                                                                                                                           |
| Genérico                                                                             | ✅      | Trae tu propio agente — usa `--ai generic --ai-commands-dir <path>` para agentes no soportados                                            |

## 🔧 Referencia del CLI Specify

El comando `specify` soporta las siguientes opciones:

### Comandos

| Comando | Descripción                                                                                                                                             |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `init`  | Inicializar un nuevo proyecto Specify desde la plantilla más reciente                                                                                   |
| `check` | Verificar herramientas instaladas (`git`, `claude`, `gemini`, `code`/`code-insiders`, `cursor-agent`, `windsurf`, `qwen`, `opencode`, `codex`, `kiro-cli`, `shai`, `qodercli`, `vibe`, `kimi`, `pi`) |

### Argumentos y Opciones de `specify init`

| Argumento/Opción       | Tipo     | Descripción                                                                                                                                                                                  |
| ---------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<project-name>`       | Argumento | Nombre para el directorio de tu nuevo proyecto (opcional si usas `--here`, o usa `.` para el directorio actual)                                                                              |
| `--ai`                 | Opción   | Asistente de IA a utilizar: `claude`, `gemini`, `copilot`, `cursor-agent`, `qwen`, `opencode`, `codex`, `windsurf`, `kilocode`, `auggie`, `roo`, `codebuddy`, `amp`, `shai`, `kiro-cli` (alias `kiro`), `agy`, `bob`, `qodercli`, `vibe`, `kimi`, `pi`, o `generic` (requiere `--ai-commands-dir`) |
| `--ai-commands-dir`    | Opción   | Directorio para archivos de comandos del agente (requerido con `--ai generic`, ej. `.myagent/commands/`)                                                                                     |
| `--script`             | Opción   | Variante de script a usar: `sh` (bash/zsh) o `ps` (PowerShell)                                                                                                                              |
| `--ignore-agent-tools` | Flag     | Omitir verificaciones de herramientas de agentes de IA como Claude Code                                                                                                                     |
| `--no-git`             | Flag     | Omitir la inicialización del repositorio git                                                                                                                                                 |
| `--here`               | Flag     | Inicializar el proyecto en el directorio actual en lugar de crear uno nuevo                                                                                                                  |
| `--force`              | Flag     | Forzar merge/sobrescritura al inicializar en el directorio actual (omitir confirmación)                                                                                                     |
| `--skip-tls`           | Flag     | Omitir verificación SSL/TLS (no recomendado)                                                                                                                                                 |
| `--debug`              | Flag     | Habilitar salida de depuración detallada para solución de problemas                                                                                                                          |
| `--github-token`       | Opción   | Token de GitHub para solicitudes a la API (o establece la variable de entorno GH_TOKEN/GITHUB_TOKEN)                                                                                         |
| `--ai-skills`          | Flag     | Instalar plantillas Prompt.MD como skills del agente en el directorio `skills/` específico del agente (requiere `--ai`)                                                                      |

### Ejemplos

```bash
# Basic project initialization
specify init my-project

# Initialize with specific AI assistant
specify init my-project --ai claude

# Initialize with Cursor support
specify init my-project --ai cursor-agent

# Initialize with Qoder support
specify init my-project --ai qodercli

# Initialize with Windsurf support
specify init my-project --ai windsurf

# Initialize with Kiro CLI support
specify init my-project --ai kiro-cli

# Initialize with Amp support
specify init my-project --ai amp

# Initialize with SHAI support
specify init my-project --ai shai

# Initialize with Mistral Vibe support
specify init my-project --ai vibe

# Initialize with IBM Bob support
specify init my-project --ai bob

# Initialize with Pi Coding Agent support
specify init my-project --ai pi

# Initialize with Antigravity support
specify init my-project --ai agy --ai-skills

# Initialize with an unsupported agent (generic / bring your own agent)
specify init my-project --ai generic --ai-commands-dir .myagent/commands/

# Initialize with PowerShell scripts (Windows/cross-platform)
specify init my-project --ai copilot --script ps

# Initialize in current directory
specify init . --ai copilot
# or use the --here flag
specify init --here --ai copilot

# Force merge into current (non-empty) directory without confirmation
specify init . --force --ai copilot
# or
specify init --here --force --ai copilot

# Skip git initialization
specify init my-project --ai gemini --no-git

# Enable debug output for troubleshooting
specify init my-project --ai claude --debug

# Use GitHub token for API requests (helpful for corporate environments)
specify init my-project --ai claude --github-token ghp_your_token_here

# Install agent skills with the project
specify init my-project --ai claude --ai-skills

# Initialize in current directory with agent skills
specify init --here --ai gemini --ai-skills

# Check system requirements
specify check
```

### Slash Commands Disponibles

Después de ejecutar `specify init`, tu agente de codificación con IA tendrá acceso a estos slash commands para un desarrollo estructurado:

#### Comandos Principales

Comandos esenciales para el flujo de trabajo de Desarrollo Dirigido por Especificaciones:

| Comando                 | Descripción                                                              |
| ----------------------- | ------------------------------------------------------------------------ |
| `/speckit.constitution` | Crear o actualizar los principios rectores y directrices de desarrollo del proyecto |
| `/speckit.specify`      | Definir qué quieres construir (requisitos e historias de usuario)         |
| `/speckit.plan`         | Crear planes de implementación técnica con tu stack tecnológico elegido   |
| `/speckit.tasks`        | Generar listas de tareas accionables para la implementación               |
| `/speckit.implement`    | Ejecutar todas las tareas para construir la funcionalidad según el plan   |

#### Comandos Opcionales

Comandos adicionales para mejorar la calidad y validación:

| Comando              | Descripción                                                                                                                          |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `/speckit.clarify`   | Clarificar áreas poco especificadas (recomendado antes de `/speckit.plan`; anteriormente `/quizme`)                                  |
| `/speckit.analyze`   | Análisis de consistencia y cobertura entre artefactos (ejecutar después de `/speckit.tasks`, antes de `/speckit.implement`)           |
| `/speckit.checklist` | Generar listas de verificación de calidad personalizadas que validen la completitud, claridad y consistencia de los requisitos (como "pruebas unitarias para el lenguaje natural") |

### Variables de Entorno

| Variable          | Descripción                                                                                                                                                                                                                                                                                            |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `SPECIFY_FEATURE` | Sobrescribir la detección de funcionalidad para repositorios sin Git. Establécela con el nombre del directorio de la funcionalidad (ej., `001-photo-albums`) para trabajar en una funcionalidad específica cuando no se usa Git con branches.<br/>\*\*Debe establecerse en el contexto del agente con el que estás trabajando antes de usar `/speckit.plan` o comandos posteriores. |

## 📚 Filosofía Central

El Desarrollo Dirigido por Especificaciones es un proceso estructurado que enfatiza:

- **Desarrollo dirigido por intención** donde las especificaciones definen el "*qué*" antes del "*cómo*"
- **Creación de especificaciones enriquecidas** usando guardrails y principios organizacionales
- **Refinamiento en múltiples pasos** en lugar de generación de código de un solo intento a partir de prompts
- **Gran dependencia** de las capacidades avanzadas de modelos de IA para la interpretación de especificaciones

## 🌟 Fases de Desarrollo

| Fase                                          | Enfoque                      | Actividades Clave                                                                                                                                                               |
| --------------------------------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Desarrollo 0-a-1** ("Greenfield")           | Generar desde cero           | <ul><li>Comenzar con requisitos de alto nivel</li><li>Generar especificaciones</li><li>Planificar pasos de implementación</li><li>Construir aplicaciones listas para producción</li></ul> |
| **Exploración Creativa**                       | Implementaciones paralelas   | <ul><li>Explorar soluciones diversas</li><li>Soportar múltiples stacks tecnológicos y arquitecturas</li><li>Experimentar con patrones de UX</li></ul>                           |
| **Mejora Iterativa** ("Brownfield")            | Modernización brownfield     | <ul><li>Añadir funcionalidades iterativamente</li><li>Modernizar sistemas legados</li><li>Adaptar procesos</li></ul>                                                            |

## 🎯 Objetivos Experimentales

Nuestra investigación y experimentación se centra en:

### Independencia tecnológica

- Crear aplicaciones usando stacks tecnológicos diversos
- Validar la hipótesis de que el Desarrollo Dirigido por Especificaciones es un proceso no ligado a tecnologías, lenguajes de programación o frameworks específicos

### Restricciones empresariales

- Demostrar el desarrollo de aplicaciones de misión crítica
- Incorporar restricciones organizacionales (proveedores cloud, stacks tecnológicos, prácticas de ingeniería)
- Soportar sistemas de diseño empresariales y requisitos de cumplimiento normativo

### Desarrollo centrado en el usuario

- Construir aplicaciones para diferentes cohortes de usuarios y preferencias
- Soportar varios enfoques de desarrollo (desde vibe-coding hasta desarrollo AI-native)

### Procesos creativos e iterativos

- Validar el concepto de exploración de implementaciones paralelas
- Proveer flujos de trabajo robustos para el desarrollo iterativo de funcionalidades
- Extender los procesos para manejar tareas de actualización y modernización

## 🔧 Prerrequisitos

- **Linux/macOS/Windows**
- Agente de codificación con IA [soportado](#-agentes-de-ia-soportados).
- [uv](https://docs.astral.sh/uv/) para gestión de paquetes
- [Python 3.11+](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)

Si encuentras problemas con un agente, por favor abre un issue para que podamos mejorar la integración.

## 📖 Más Información

- **[Metodología Completa de Desarrollo Dirigido por Especificaciones](./spec-driven.md)** - Profundización en el proceso completo
- **[Guía Detallada](#-proceso-detallado)** - Guía de implementación paso a paso

---

## 📋 Proceso Detallado

<details>
<summary>Haz clic para expandir la guía detallada paso a paso</summary>

Puedes usar el CLI Specify para inicializar tu proyecto, lo cual traerá los artefactos necesarios a tu entorno. Ejecuta:

```bash
specify init <project_name>
```

O inicializa en el directorio actual:

```bash
specify init .
# or use the --here flag
specify init --here
# Skip confirmation when the directory already has files
specify init . --force
# or
specify init --here --force
```

![CLI Specify inicializando un nuevo proyecto en la terminal](./media/specify_cli.gif)

Se te pedirá que selecciones el agente de IA que estás usando. También puedes especificarlo directamente en la terminal de forma proactiva:

```bash
specify init <project_name> --ai claude
specify init <project_name> --ai gemini
specify init <project_name> --ai copilot

# Or in current directory:
specify init . --ai claude
specify init . --ai codex

# or use --here flag
specify init --here --ai claude
specify init --here --ai codex

# Force merge into a non-empty current directory
specify init . --force --ai claude

# or
specify init --here --force --ai claude
```

El CLI verificará si tienes Claude Code, Gemini CLI, Cursor CLI, Qwen CLI, opencode, Codex CLI, Qoder CLI, Tabnine CLI, Kiro CLI, Pi o Mistral Vibe instalados. Si no los tienes, o prefieres obtener las plantillas sin verificar las herramientas correctas, usa `--ignore-agent-tools` con tu comando:

```bash
specify init <project_name> --ai claude --ignore-agent-tools
```

### **PASO 1:** Establecer los principios del proyecto

Ve a la carpeta del proyecto y ejecuta tu agente de IA. En nuestro ejemplo, estamos usando `claude`.

![Inicializando el entorno de Claude Code](./media/bootstrap-claude-code.gif)

Sabrás que todo está configurado correctamente si ves los comandos `/speckit.constitution`, `/speckit.specify`, `/speckit.plan`, `/speckit.tasks` y `/speckit.implement` disponibles.

El primer paso debe ser establecer los principios rectores de tu proyecto usando el comando `/speckit.constitution`. Esto ayuda a garantizar una toma de decisiones consistente a lo largo de todas las fases de desarrollo posteriores:

```text
/speckit.constitution Create principles focused on code quality, testing standards, user experience consistency, and performance requirements. Include governance for how these principles should guide technical decisions and implementation choices.
```

Este paso crea o actualiza el archivo `.specify/memory/constitution.md` con las directrices fundamentales de tu proyecto que el agente de IA consultará durante las fases de especificación, planificación e implementación.

### **PASO 2:** Crear las especificaciones del proyecto

Con los principios del proyecto establecidos, ahora puedes crear las especificaciones funcionales. Usa el comando `/speckit.specify` y luego proporciona los requisitos concretos para el proyecto que quieres desarrollar.

> [!IMPORTANT]
> Sé lo más explícito posible sobre *qué* estás intentando construir y *por qué*. **No te enfoques en el stack tecnológico en este punto**.

Un ejemplo de prompt:

```text
Develop Taskify, a team productivity platform. It should allow users to create projects, add team members,
assign tasks, comment and move tasks between boards in Kanban style. In this initial phase for this feature,
let's call it "Create Taskify," let's have multiple users but the users will be declared ahead of time, predefined.
I want five users in two different categories, one product manager and four engineers. Let's create three
different sample projects. Let's have the standard Kanban columns for the status of each task, such as "To Do,"
"In Progress," "In Review," and "Done." There will be no login for this application as this is just the very
first testing thing to ensure that our basic features are set up. For each task in the UI for a task card,
you should be able to change the current status of the task between the different columns in the Kanban work board.
You should be able to leave an unlimited number of comments for a particular card. You should be able to, from that task
card, assign one of the valid users. When you first launch Taskify, it's going to give you a list of the five users to pick
from. There will be no password required. When you click on a user, you go into the main view, which displays the list of
projects. When you click on a project, you open the Kanban board for that project. You're going to see the columns.
You'll be able to drag and drop cards back and forth between different columns. You will see any cards that are
assigned to you, the currently logged in user, in a different color from all the other ones, so you can quickly
see yours. You can edit any comments that you make, but you can't edit comments that other people made. You can
delete any comments that you made, but you can't delete comments anybody else made.
```

Después de introducir este prompt, deberías ver que Claude Code inicia el proceso de planificación y redacción de especificaciones. Claude Code también activará algunos de los scripts integrados para configurar el repositorio.

Una vez completado este paso, deberías tener un nuevo branch creado (ej., `001-create-taskify`), así como una nueva especificación en el directorio `specs/001-create-taskify`.

La especificación producida debe contener un conjunto de historias de usuario y requisitos funcionales, según lo definido en la plantilla.

En esta etapa, el contenido de la carpeta de tu proyecto debería parecerse a lo siguiente:

```text
└── .specify
    ├── memory
    │  └── constitution.md
    ├── scripts
    │  ├── check-prerequisites.sh
    │  ├── common.sh
    │  ├── create-new-feature.sh
    │  ├── setup-plan.sh
    │  └── update-claude-md.sh
    ├── specs
    │  └── 001-create-taskify
    │      └── spec.md
    └── templates
        ├── plan-template.md
        ├── spec-template.md
        └── tasks-template.md
```

### **PASO 3:** Clarificación de la especificación funcional (requerido antes de planificar)

Con la especificación base creada, puedes proceder a clarificar cualquiera de los requisitos que no fueron capturados correctamente en el primer intento.

Deberías ejecutar el flujo de trabajo de clarificación estructurada **antes** de crear un plan técnico para reducir el retrabajo posterior.

Orden preferido:

1. Usa `/speckit.clarify` (estructurado) – cuestionamiento secuencial basado en cobertura que registra las respuestas en una sección de Clarificaciones.
2. Opcionalmente, continúa con un refinamiento libre ad-hoc si algo aún parece vago.

Si intencionalmente quieres omitir la clarificación (ej., spike o prototipo exploratorio), indícalo explícitamente para que el agente no se bloquee por clarificaciones faltantes.

Ejemplo de prompt de refinamiento libre (después de `/speckit.clarify` si aún es necesario):

```text
For each sample project or project that you create there should be a variable number of tasks between 5 and 15
tasks for each one randomly distributed into different states of completion. Make sure that there's at least
one task in each stage of completion.
```

También deberías pedirle a Claude Code que valide la **Lista de Verificación de Revisión y Aceptación**, marcando los elementos que están validados/cumplen los requisitos, y dejando sin marcar los que no. Se puede usar el siguiente prompt:

```text
Read the review and acceptance checklist, and check off each item in the checklist if the feature spec meets the criteria. Leave it empty if it does not.
```

Es importante usar la interacción con Claude Code como una oportunidad para clarificar y hacer preguntas sobre la especificación - **no trates su primer intento como definitivo**.

### **PASO 4:** Generar un plan

Ahora puedes ser específico sobre el stack tecnológico y otros requisitos técnicos. Puedes usar el comando `/speckit.plan` que está integrado en la plantilla del proyecto con un prompt como este:

```text
We are going to generate this using .NET Aspire, using Postgres as the database. The frontend should use
Blazor server with drag-and-drop task boards, real-time updates. There should be a REST API created with a projects API,
tasks API, and a notifications API.
```

El resultado de este paso incluirá varios documentos de detalle de implementación, con tu árbol de directorios parecido a esto:

```text
.
├── CLAUDE.md
├── memory
│  └── constitution.md
├── scripts
│  ├── check-prerequisites.sh
│  ├── common.sh
│  ├── create-new-feature.sh
│  ├── setup-plan.sh
│  └── update-claude-md.sh
├── specs
│  └── 001-create-taskify
│      ├── contracts
│      │  ├── api-spec.json
│      │  └── signalr-spec.md
│      ├── data-model.md
│      ├── plan.md
│      ├── quickstart.md
│      ├── research.md
│      └── spec.md
└── templates
    ├── CLAUDE-template.md
    ├── plan-template.md
    ├── spec-template.md
    └── tasks-template.md
```

Revisa el documento `research.md` para asegurarte de que se utiliza el stack tecnológico correcto, según tus instrucciones. Puedes pedirle a Claude Code que lo refine si alguno de los componentes destaca, o incluso hacer que verifique la versión instalada localmente de la plataforma/framework que quieres usar (ej., .NET).

Adicionalmente, podrías querer pedirle a Claude Code que investigue detalles sobre el stack tecnológico elegido si es algo que cambia rápidamente (ej., .NET Aspire, frameworks de JS), con un prompt como este:

```text
I want you to go through the implementation plan and implementation details, looking for areas that could
benefit from additional research as .NET Aspire is a rapidly changing library. For those areas that you identify that
require further research, I want you to update the research document with additional details about the specific
versions that we are going to be using in this Taskify application and spawn parallel research tasks to clarify
any details using research from the web.
```

Durante este proceso, podrías encontrar que Claude Code se queda atascado investigando algo incorrecto - puedes ayudarlo a redirigirse en la dirección correcta con un prompt como este:

```text
I think we need to break this down into a series of steps. First, identify a list of tasks
that you would need to do during implementation that you're not sure of or would benefit
from further research. Write down a list of those tasks. And then for each one of these tasks,
I want you to spin up a separate research task so that the net results is we are researching
all of those very specific tasks in parallel. What I saw you doing was it looks like you were
researching .NET Aspire in general and I don't think that's gonna do much for us in this case.
That's way too untargeted research. The research needs to help you solve a specific targeted question.
```

> [!NOTE]
> Claude Code podría ser demasiado entusiasta y añadir componentes que no solicitaste. Pídele que aclare la justificación y la fuente del cambio.

### **PASO 5:** Hacer que Claude Code valide el plan

Con el plan en su lugar, deberías hacer que Claude Code lo revise para asegurarse de que no faltan piezas. Puedes usar un prompt como este:

```text
Now I want you to go and audit the implementation plan and the implementation detail files.
Read through it with an eye on determining whether or not there is a sequence of tasks that you need
to be doing that are obvious from reading this. Because I don't know if there's enough here. For example,
when I look at the core implementation, it would be useful to reference the appropriate places in the implementation
details where it can find the information as it walks through each step in the core implementation or in the refinement.
```

Esto ayuda a refinar el plan de implementación y te ayuda a evitar posibles puntos ciegos que Claude Code pasó por alto en su ciclo de planificación. Una vez completada la pasada de refinamiento inicial, pídele a Claude Code que revise la lista de verificación una vez más antes de pasar a la implementación.

También puedes pedirle a Claude Code (si tienes el [GitHub CLI](https://docs.github.com/en/github-cli/github-cli) instalado) que cree un pull request desde tu branch actual hacia `main` con una descripción detallada, para asegurarte de que el esfuerzo se rastrea correctamente.

> [!NOTE]
> Antes de que el agente implemente, también vale la pena pedirle a Claude Code que verifique los detalles para ver si hay piezas sobredimensionadas (recuerda - puede ser demasiado entusiasta). Si existen componentes o decisiones sobredimensionados, puedes pedirle a Claude Code que los resuelva. Asegúrate de que Claude Code siga la [constitución](base/memory/constitution.md) como la pieza fundamental que debe respetar al establecer el plan.

### **PASO 6:** Generar el desglose de tareas con /speckit.tasks

Con el plan de implementación validado, ahora puedes desglosar el plan en tareas específicas y accionables que pueden ejecutarse en el orden correcto. Usa el comando `/speckit.tasks` para generar automáticamente un desglose detallado de tareas a partir de tu plan de implementación:

```text
/speckit.tasks
```

Este paso crea un archivo `tasks.md` en el directorio de especificación de tu funcionalidad que contiene:

- **Desglose de tareas organizado por historia de usuario** - Cada historia de usuario se convierte en una fase de implementación separada con su propio conjunto de tareas
- **Gestión de dependencias** - Las tareas están ordenadas para respetar las dependencias entre componentes (ej., modelos antes que servicios, servicios antes que endpoints)
- **Marcadores de ejecución paralela** - Las tareas que pueden ejecutarse en paralelo están marcadas con `[P]` para optimizar el flujo de trabajo de desarrollo
- **Especificaciones de rutas de archivos** - Cada tarea incluye las rutas exactas de archivos donde debe ocurrir la implementación
- **Estructura de desarrollo dirigido por pruebas** - Si se solicitan pruebas, las tareas de prueba se incluyen y ordenan para escribirse antes de la implementación
- **Validación por puntos de control** - Cada fase de historia de usuario incluye puntos de control para validar la funcionalidad independiente

El archivo tasks.md generado proporciona una hoja de ruta clara para el comando `/speckit.implement`, asegurando una implementación sistemática que mantiene la calidad del código y permite la entrega incremental de historias de usuario.

### **PASO 7:** Implementación

Una vez listo, usa el comando `/speckit.implement` para ejecutar tu plan de implementación:

```text
/speckit.implement
```

El comando `/speckit.implement`:

- Validará que todos los prerrequisitos estén en su lugar (constitución, especificación, plan y tareas)
- Analizará el desglose de tareas de `tasks.md`
- Ejecutará las tareas en el orden correcto, respetando las dependencias y los marcadores de ejecución paralela
- Seguirá el enfoque TDD definido en tu plan de tareas
- Proporcionará actualizaciones de progreso y manejará los errores apropiadamente

> [!IMPORTANT]
> El agente de IA ejecutará comandos CLI locales (como `dotnet`, `npm`, etc.) - asegúrate de tener las herramientas necesarias instaladas en tu máquina.

Una vez completada la implementación, prueba la aplicación y resuelve cualquier error en tiempo de ejecución que pueda no ser visible en los logs del CLI (ej., errores en la consola del navegador). Puedes copiar y pegar dichos errores de vuelta a tu agente de IA para su resolución.

</details>

---

## 🔍 Solución de Problemas

### Git Credential Manager en Linux

Si tienes problemas con la autenticación de Git en Linux, puedes instalar Git Credential Manager:

```bash
#!/usr/bin/env bash
set -e
echo "Downloading Git Credential Manager v2.6.1..."
wget https://github.com/git-ecosystem/git-credential-manager/releases/download/v2.6.1/gcm-linux_amd64.2.6.1.deb
echo "Installing Git Credential Manager..."
sudo dpkg -i gcm-linux_amd64.2.6.1.deb
echo "Configuring Git to use GCM..."
git config --global credential.helper manager
echo "Cleaning up..."
rm gcm-linux_amd64.2.6.1.deb
```

## 💬 Soporte

Para obtener soporte, por favor abre un [issue en GitHub](https://github.com/github/spec-kit/issues/new). Damos la bienvenida a reportes de errores, solicitudes de funcionalidades y preguntas sobre el uso del Desarrollo Dirigido por Especificaciones.

## 🙏 Agradecimientos

Este proyecto está fuertemente influenciado por y basado en el trabajo e investigación de [John Lam](https://github.com/jflam).

## 📄 Licencia

Este proyecto está licenciado bajo los términos de la licencia de código abierto MIT. Por favor consulta el archivo [LICENSE](./LICENSE) para los términos completos.
