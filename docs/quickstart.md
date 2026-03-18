# Guía de Inicio Rápido

Esta guía te ayudará a comenzar con el Desarrollo Dirigido por Especificaciones usando Spec Kit.

> [!NOTE]
> Todos los scripts de automatización ahora proporcionan variantes tanto en Bash (`.sh`) como en PowerShell (`.ps1`). El CLI `specify` selecciona automáticamente según el SO a menos que pases `--script sh|ps`.

## El Proceso de 6 Pasos

> [!TIP]
> **Reconocimiento de Contexto**: Los comandos de Spec Kit detectan automáticamente la funcionalidad activa basándose en tu rama actual de Git (por ejemplo, `001-feature-name`). Para cambiar entre diferentes especificaciones, simplemente cambia de rama en Git.

### Paso 1: Instalar Specify

**En tu terminal**, ejecuta el comando CLI `specify` para inicializar tu proyecto:

```bash
# Crear un nuevo directorio de proyecto
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>

# O inicializar en el directorio actual
uvx --from git+https://github.com/github/spec-kit.git specify init .
```

Elegir el tipo de script explícitamente (opcional):

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME> --script ps  # Force PowerShell
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME> --script sh  # Force POSIX shell
```

### Paso 2: Definir tu Constitución

**En la interfaz de chat de tu Agente de IA**, usa el comando slash `/speckit.constitution` para establecer las reglas y principios fundamentales de tu proyecto. Debes proporcionar los principios específicos de tu proyecto como argumentos.

```markdown
/speckit.constitution This project follows a "Library-First" approach. All features must be implemented as standalone libraries first. We use TDD strictly. We prefer functional programming patterns.
```

### Paso 3: Crear la Especificación

**En el chat**, usa el comando slash `/speckit.specify` para describir lo que quieres construir. Enfócate en el **qué** y el **por qué**, no en el stack tecnológico.

```markdown
/speckit.specify Build an application that can help me organize my photos in separate photo albums. Albums are grouped by date and can be re-organized by dragging and dropping on the main page. Albums are never in other nested albums. Within each album, photos are previewed in a tile-like interface.
```

### Paso 4: Refinar la Especificación

**En el chat**, usa el comando slash `/speckit.clarify` para identificar y resolver ambigüedades en tu especificación. Puedes proporcionar áreas de enfoque específicas como argumentos.

```bash
/speckit.clarify Focus on security and performance requirements.
```

### Paso 5: Crear un Plan de Implementación Técnica

**En el chat**, usa el comando slash `/speckit.plan` para proporcionar tu stack tecnológico y decisiones de arquitectura.

```markdown
/speckit.plan The application uses Vite with minimal number of libraries. Use vanilla HTML, CSS, and JavaScript as much as possible. Images are not uploaded anywhere and metadata is stored in a local SQLite database.
```

### Paso 6: Desglosar e Implementar

**En el chat**, usa el comando slash `/speckit.tasks` para crear una lista de tareas accionables.

```markdown
/speckit.tasks
```

Opcionalmente, valida el plan con `/speckit.analyze`:

```markdown
/speckit.analyze
```

Luego, usa el comando slash `/speckit.implement` para ejecutar el plan.

```markdown
/speckit.implement
```

> [!TIP]
> **Implementación por Fases**: Para proyectos complejos, implementa en fases para evitar saturar el contexto del agente. Comienza con la funcionalidad principal, valida que funcione y luego añade funcionalidades de forma incremental.

## Ejemplo Detallado: Construyendo Taskify

Aquí tienes un ejemplo completo de cómo construir una plataforma de productividad para equipos:

### Paso 1: Definir la Constitución

Inicializa la constitución del proyecto para establecer las reglas base:

```markdown
/speckit.constitution Taskify is a "Security-First" application. All user inputs must be validated. We use a microservices architecture. Code must be fully documented.
```

### Paso 2: Definir Requisitos con `/speckit.specify`

```text
Develop Taskify, a team productivity platform. It should allow users to create projects, add team members,
assign tasks, comment and move tasks between boards in Kanban style. In this initial phase for this feature,
let's call it "Create Taskify," let's have multiple users but the users will be declared ahead of time, predefined.
I want five users in two different categories, one product manager and four engineers. Let's create three
different sample projects. Let's have the standard Kanban columns for the status of each task, such as "To Do,"
"In Progress," "In Review," and "Done." There will be no login for this application as this is just the very
first testing thing to ensure that our basic features are set up.
```

### Paso 3: Refinar la Especificación

Usa el comando `/speckit.clarify` para resolver interactivamente cualquier ambigüedad en tu especificación. También puedes proporcionar detalles específicos que deseas asegurar que se incluyan.

```bash
/speckit.clarify I want to clarify the task card details. For each task in the UI for a task card, you should be able to change the current status of the task between the different columns in the Kanban work board. You should be able to leave an unlimited number of comments for a particular card. You should be able to, from that task card, assign one of the valid users.
```

Puedes continuar refinando la especificación con más detalles usando `/speckit.clarify`:

```bash
/speckit.clarify When you first launch Taskify, it's going to give you a list of the five users to pick from. There will be no password required. When you click on a user, you go into the main view, which displays the list of projects. When you click on a project, you open the Kanban board for that project. You're going to see the columns. You'll be able to drag and drop cards back and forth between different columns. You will see any cards that are assigned to you, the currently logged in user, in a different color from all the other ones, so you can quickly see yours. You can edit any comments that you make, but you can't edit comments that other people made. You can delete any comments that you made, but you can't delete comments anybody else made.
```

### Paso 4: Validar la Especificación

Valida la lista de verificación de la especificación usando el comando `/speckit.checklist`:

```bash
/speckit.checklist
```

### Paso 5: Generar el Plan Técnico con `/speckit.plan`

Sé específico sobre tu stack tecnológico y requisitos técnicos:

```bash
/speckit.plan We are going to generate this using .NET Aspire, using Postgres as the database. The frontend should use Blazor server with drag-and-drop task boards, real-time updates. There should be a REST API created with a projects API, tasks API, and a notifications API.
```

### Paso 6: Definir Tareas

Genera una lista de tareas accionables usando el comando `/speckit.tasks`:

```bash
/speckit.tasks
```

### Paso 7: Validar e Implementar

Haz que tu agente de IA audite el plan de implementación usando `/speckit.analyze`:

```bash
/speckit.analyze
```

Finalmente, implementa la solución:

```bash
/speckit.implement
```

> [!TIP]
> **Implementación por Fases**: Para proyectos grandes como Taskify, considera implementar en fases (por ejemplo, Fase 1: Estructura básica de proyectos/tareas, Fase 2: Funcionalidad Kanban, Fase 3: Comentarios y asignaciones). Esto previene la saturación del contexto y permite la validación en cada etapa.

## Principios Clave

- **Sé explícito** sobre lo que estás construyendo y por qué
- **No te enfoques en el stack tecnológico** durante la fase de especificación
- **Itera y refina** tus especificaciones antes de la implementación
- **Valida** el plan antes de comenzar a programar
- **Deja que el agente de IA se encargue** de los detalles de implementación

## Próximos Pasos

- Lee la [metodología completa](https://github.com/github/spec-kit/blob/main/spec-driven.md) para una guía en profundidad
- Consulta [más ejemplos](https://github.com/github/spec-kit/tree/main/templates) en el repositorio
- Explora el [código fuente en GitHub](https://github.com/github/spec-kit)
