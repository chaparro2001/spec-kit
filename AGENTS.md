# AGENTS.md

## Acerca de Spec Kit y Specify

**GitHub Spec Kit** es un toolkit completo para implementar el Desarrollo Dirigido por Especificaciones (SDD) - una metodología que enfatiza la creación de especificaciones claras antes de la implementación. El toolkit incluye plantillas, scripts y flujos de trabajo que guían a los equipos de desarrollo a través de un enfoque estructurado para construir software.

**Specify CLI** es la interfaz de línea de comandos que inicializa proyectos con el framework de Spec Kit. Configura las estructuras de directorios, plantillas e integraciones de agentes de IA necesarias para soportar el flujo de trabajo del Desarrollo Dirigido por Especificaciones.

El toolkit soporta múltiples asistentes de codificación con IA, permitiendo que los equipos usen sus herramientas preferidas mientras mantienen una estructura de proyecto y prácticas de desarrollo consistentes.

---

## Añadir Soporte para Nuevos Agentes

Esta sección explica cómo añadir soporte para nuevos agentes/asistentes de IA al CLI Specify. Usa esta guía como referencia al integrar nuevas herramientas de IA en el flujo de trabajo del Desarrollo Dirigido por Especificaciones.

### Descripción General

Specify soporta múltiples agentes de IA generando archivos de comandos y estructuras de directorios específicos para cada agente al inicializar proyectos. Cada agente tiene sus propias convenciones para:

- **Formatos de archivos de comandos** (Markdown, TOML, etc.)
- **Estructuras de directorios** (`.claude/commands/`, `.windsurf/workflows/`, etc.)
- **Patrones de invocación de comandos** (slash commands, herramientas CLI, etc.)
- **Convenciones de paso de argumentos** (`$ARGUMENTS`, `{{args}}`, etc.)

### Agentes Actualmente Soportados

| Agente                     | Directorio             | Formato  | Herramienta CLI | Descripción                 |
| -------------------------- | ---------------------- | -------- | --------------- | --------------------------- |
| **Claude Code**            | `.claude/commands/`    | Markdown | `claude`        | CLI Claude Code de Anthropic |
| **Gemini CLI**             | `.gemini/commands/`    | TOML     | `gemini`        | CLI Gemini de Google         |
| **GitHub Copilot**         | `.github/agents/`      | Markdown | N/A (basado en IDE) | GitHub Copilot en VS Code   |
| **Cursor**                 | `.cursor/commands/`    | Markdown | `cursor-agent`  | CLI de Cursor                |
| **Qwen Code**              | `.qwen/commands/`      | Markdown | `qwen`          | CLI Qwen Code de Alibaba     |
| **opencode**               | `.opencode/command/`   | Markdown | `opencode`      | CLI de opencode              |
| **Codex CLI**              | `.codex/prompts/`      | Markdown | `codex`         | CLI de Codex                 |
| **Windsurf**               | `.windsurf/workflows/` | Markdown | N/A (basado en IDE) | Flujos de trabajo del IDE Windsurf |
| **Kilo Code**              | `.kilocode/workflows/` | Markdown | N/A (basado en IDE) | IDE Kilo Code               |
| **Auggie CLI**             | `.augment/commands/`   | Markdown | `auggie`        | CLI de Auggie                |
| **Roo Code**               | `.roo/commands/`       | Markdown | N/A (basado en IDE) | IDE Roo Code                |
| **CodeBuddy CLI**          | `.codebuddy/commands/` | Markdown | `codebuddy`     | CLI de CodeBuddy             |
| **Qoder CLI**              | `.qoder/commands/`     | Markdown | `qodercli`      | CLI de Qoder                 |
| **Kiro CLI**               | `.kiro/prompts/`       | Markdown | `kiro-cli`      | CLI de Kiro                  |
| **Amp**                    | `.agents/commands/`    | Markdown | `amp`           | CLI de Amp                   |
| **SHAI**                   | `.shai/commands/`      | Markdown | `shai`          | CLI de SHAI                  |
| **Tabnine CLI**            | `.tabnine/agent/commands/` | TOML | `tabnine`       | CLI de Tabnine               |
| **Kimi Code**              | `.kimi/skills/`        | Markdown | `kimi`          | CLI de Kimi Code (Moonshot AI) |
| **Pi Coding Agent**        | `.pi/prompts/`         | Markdown | `pi`            | Agente de codificación Pi en terminal |
| **IBM Bob**                | `.bob/commands/`       | Markdown | N/A (basado en IDE) | IDE IBM Bob                 |
| **Trae**                   | `.trae/rules/`         | Markdown | N/A (basado en IDE) | IDE Trae                    |
| **Genérico**               | Especificado por el usuario via `--ai-commands-dir` | Markdown | N/A | Trae tu propio agente       |

### Guía de Integración Paso a Paso

Sigue estos pasos para añadir un nuevo agente (usando un agente hipotético como ejemplo):

#### 1. Añadir a AGENT_CONFIG

**IMPORTANTE**: Usa el nombre real de la herramienta CLI como clave, no una versión abreviada.

Añade el nuevo agente al diccionario `AGENT_CONFIG` en `src/specify_cli/__init__.py`. Esta es la **fuente única de verdad** para todos los metadatos de agentes:

```python
AGENT_CONFIG = {
    # ... existing agents ...
    "new-agent-cli": {  # Use the ACTUAL CLI tool name (what users type in terminal)
        "name": "New Agent Display Name",
        "folder": ".newagent/",  # Directory for agent files
        "commands_subdir": "commands",  # Subdirectory name for command files (default: "commands")
        "install_url": "https://example.com/install",  # URL for installation docs (or None if IDE-based)
        "requires_cli": True,  # True if CLI tool required, False for IDE-based agents
    },
}
```

**Principio de Diseño Clave**: La clave del diccionario debe coincidir con el nombre real del ejecutable que los usuarios instalan. Por ejemplo:

- Use `"cursor-agent"` porque la herramienta CLI se llama literalmente `cursor-agent`
- No use `"cursor"` como atajo si la herramienta es `cursor-agent`

Esto elimina la necesidad de mapeos de casos especiales a lo largo del código.

**Explicación de los Campos**:

- `name`: Nombre legible para mostrar a los usuarios
- `folder`: Directorio donde se almacenan los archivos específicos del agente (relativo a la raíz del proyecto)
- `commands_subdir`: Nombre del subdirectorio dentro de la carpeta del agente donde se almacenan los archivos de comandos/prompts (por defecto: `"commands"`)
  - La mayoría de los agentes usan `"commands"` (ej., `.claude/commands/`)
  - Algunos agentes usan nombres alternativos: `"agents"` (copilot), `"workflows"` (windsurf, kilocode), `"prompts"` (codex, kiro-cli, pi), `"command"` (opencode - singular)
  - Este campo permite que `--ai-skills` localice correctamente las plantillas de comandos para la generación de skills
- `install_url`: URL de la documentación de instalación (establecer como `None` para agentes basados en IDE)
- `requires_cli`: Si el agente requiere una verificación de herramienta CLI durante la inicialización

#### 2. Actualizar el Texto de Ayuda del CLI

Actualiza el texto de ayuda del parámetro `--ai` en el comando `init()` para incluir el nuevo agente:

```python
ai_assistant: str = typer.Option(None, "--ai", help="AI assistant to use: claude, gemini, copilot, cursor-agent, qwen, opencode, codex, windsurf, kilocode, auggie, codebuddy, new-agent-cli, or kiro-cli"),
```

También actualiza cualquier docstring de funciones, ejemplos y mensajes de error que listen los agentes disponibles.

#### 3. Actualizar la Documentación del README

Actualiza la sección de **Agentes de IA Soportados** en `README.md` para incluir el nuevo agente:

- Añade el nuevo agente a la tabla con el nivel de soporte apropiado (Completo/Parcial)
- Incluye el enlace al sitio web oficial del agente
- Añade cualquier nota relevante sobre la implementación del agente
- Asegúrate de que el formato de la tabla permanezca alineado y consistente

#### 4. Actualizar el Script de Paquetes de Release

Modifica `.github/workflows/scripts/create-release-packages.sh`:

##### Añadir al array ALL_AGENTS

```bash
ALL_AGENTS=(claude gemini copilot cursor-agent qwen opencode windsurf kiro-cli)
```

##### Añadir sentencia case para la estructura de directorios

```bash
case $agent in
  # ... existing cases ...
  windsurf)
    mkdir -p "$base_dir/.windsurf/workflows"
    generate_commands windsurf md "\$ARGUMENTS" "$base_dir/.windsurf/workflows" "$script" ;;
esac
```

#### 4. Actualizar el Script de Release de GitHub

Modifica `.github/workflows/scripts/create-github-release.sh` para incluir los paquetes del nuevo agente:

```bash
gh release create "$VERSION" \
  # ... existing packages ...
  .genreleases/spec-kit-template-windsurf-sh-"$VERSION".zip \
  .genreleases/spec-kit-template-windsurf-ps-"$VERSION".zip \
  # Add new agent packages here
```

#### 5. Actualizar los Scripts de Contexto del Agente

##### Script Bash (`scripts/bash/update-agent-context.sh`)

Añadir variable de archivo:

```bash
WINDSURF_FILE="$REPO_ROOT/.windsurf/rules/specify-rules.md"
```

Añadir a la sentencia case:

```bash
case "$AGENT_TYPE" in
  # ... existing cases ...
  windsurf) update_agent_file "$WINDSURF_FILE" "Windsurf" ;;
  "")
    # ... existing checks ...
    [ -f "$WINDSURF_FILE" ] && update_agent_file "$WINDSURF_FILE" "Windsurf";
    # Update default creation condition
    ;;
esac
```

##### Script PowerShell (`scripts/powershell/update-agent-context.ps1`)

Añadir variable de archivo:

```powershell
$windsurfFile = Join-Path $repoRoot '.windsurf/rules/specify-rules.md'
```

Añadir a la sentencia switch:

```powershell
switch ($AgentType) {
    # ... existing cases ...
    'windsurf' { Update-AgentFile $windsurfFile 'Windsurf' }
    '' {
        foreach ($pair in @(
            # ... existing pairs ...
            @{file=$windsurfFile; name='Windsurf'}
        )) {
            if (Test-Path $pair.file) { Update-AgentFile $pair.file $pair.name }
        }
        # Update default creation condition
    }
}
```

#### 6. Actualizar las Verificaciones de Herramientas CLI (Opcional)

Para agentes que requieren herramientas CLI, añade verificaciones en el comando `check()` y la validación del agente:

```python
# In check() command
tracker.add("windsurf", "Windsurf IDE (optional)")
windsurf_ok = check_tool_for_tracker("windsurf", "https://windsurf.com/", tracker)

# In init validation (only if CLI tool required)
elif selected_ai == "windsurf":
    if not check_tool("windsurf", "Install from: https://windsurf.com/"):
        console.print("[red]Error:[/red] Windsurf CLI is required for Windsurf projects")
        agent_tool_missing = True
```

**Nota**: Las verificaciones de herramientas CLI ahora se manejan automáticamente basándose en el campo `requires_cli` en AGENT_CONFIG. No se necesitan cambios de código adicionales en los comandos `check()` o `init()` - automáticamente recorren AGENT_CONFIG y verifican las herramientas según sea necesario.

## Decisiones de Diseño Importantes

### Usar Nombres Reales de Herramientas CLI como Claves

**CRITICO**: Al añadir un nuevo agente a AGENT_CONFIG, siempre usa el **nombre real del ejecutable** como clave del diccionario, no una versión abreviada o conveniente.

**Por qué esto importa:**

- La función `check_tool()` usa `shutil.which(tool)` para encontrar ejecutables en el PATH del sistema
- Si la clave no coincide con el nombre real de la herramienta CLI, necesitarás mapeos de casos especiales a lo largo del código
- Esto crea complejidad innecesaria y carga de mantenimiento

**Ejemplo - La Lección de Cursor:**

**Enfoque incorrecto** (requiere mapeo de caso especial):

```python
AGENT_CONFIG = {
    "cursor": {  # Shorthand that doesn't match the actual tool
        "name": "Cursor",
        # ...
    }
}

# Then you need special cases everywhere:
cli_tool = agent_key
if agent_key == "cursor":
    cli_tool = "cursor-agent"  # Map to the real tool name
```

**Enfoque correcto** (no necesita mapeo):

```python
AGENT_CONFIG = {
    "cursor-agent": {  # Matches the actual executable name
        "name": "Cursor",
        # ...
    }
}

# No special cases needed - just use agent_key directly!
```

**Beneficios de este enfoque:**

- Elimina la lógica de casos especiales dispersa por el código
- Hace el código más mantenible y fácil de entender
- Reduce la probabilidad de errores al añadir nuevos agentes
- La verificación de herramientas "simplemente funciona" sin mapeos adicionales

#### 7. Actualizar los Archivos de Devcontainer (Opcional)

Para agentes que tienen extensiones de VS Code o requieren instalación de CLI, actualiza los archivos de configuración de devcontainer:

##### Agentes Basados en Extensiones de VS Code

Para agentes disponibles como extensiones de VS Code, añádelos a `.devcontainer/devcontainer.json`:

```json
{
  "customizations": {
    "vscode": {
      "extensions": [
        // ... existing extensions ...
        // [New Agent Name]
        "[New Agent Extension ID]"
      ]
    }
  }
}
```

##### Agentes Basados en CLI

Para agentes que requieren herramientas CLI, añade comandos de instalación a `.devcontainer/post-create.sh`:

```bash
#!/bin/bash

# Existing installations...

echo -e "\n🤖 Installing [New Agent Name] CLI..."
# run_command "npm install -g [agent-cli-package]@latest" # Example for node-based CLI
# or other installation instructions (must be non-interactive and compatible with Linux Debian "Trixie" or later)...
echo "✅ Done"

```

**Consejos Rápidos:**

- **Agentes basados en extensiones**: Añadir al array `extensions` en `devcontainer.json`
- **Agentes basados en CLI**: Añadir scripts de instalación a `post-create.sh`
- **Agentes híbridos**: Pueden requerir tanto extensión como instalación CLI
- **Probar a fondo**: Asegurarse de que las instalaciones funcionan en el entorno devcontainer

## Categorías de Agentes

### Agentes Basados en CLI

Requieren una herramienta de línea de comandos instalada:

- **Claude Code**: CLI `claude`
- **Gemini CLI**: CLI `gemini`
- **Cursor**: CLI `cursor-agent`
- **Qwen Code**: CLI `qwen`
- **opencode**: CLI `opencode`
- **Kiro CLI**: CLI `kiro-cli`
- **CodeBuddy CLI**: CLI `codebuddy`
- **Qoder CLI**: CLI `qodercli`
- **Amp**: CLI `amp`
- **SHAI**: CLI `shai`
- **Tabnine CLI**: CLI `tabnine`
- **Kimi Code**: CLI `kimi`
- **Pi Coding Agent**: CLI `pi`

### Agentes Basados en IDE

Funcionan dentro de entornos de desarrollo integrados:

- **GitHub Copilot**: Integrado en VS Code/editores compatibles
- **Windsurf**: Integrado en el IDE Windsurf
- **IBM Bob**: Integrado en el IDE IBM Bob

## Formatos de Archivos de Comandos

### Formato Markdown

Usado por: Claude, Cursor, opencode, Windsurf, Kiro CLI, Amp, SHAI, IBM Bob, Kimi Code, Qwen, Pi

**Formato estándar:**

```markdown
---
description: "Command description"
---

Command content with {SCRIPT} and $ARGUMENTS placeholders.
```

**Formato de Chat Mode de GitHub Copilot:**

```markdown
---
description: "Command description"
mode: speckit.command-name
---

Command content with {SCRIPT} and $ARGUMENTS placeholders.
```

### Formato TOML

Usado por: Gemini, Tabnine

```toml
description = "Command description"

prompt = """
Command content with {SCRIPT} and {{args}} placeholders.
"""
```

## Convenciones de Directorios

- **Agentes CLI**: Generalmente `.<agent-name>/commands/`
- **Excepciones comunes basadas en prompts**:
  - Codex: `.codex/prompts/`
  - Kiro CLI: `.kiro/prompts/`
  - Pi: `.pi/prompts/`
- **Agentes IDE**: Siguen patrones específicos del IDE:
  - Copilot: `.github/agents/`
  - Cursor: `.cursor/commands/`
  - Windsurf: `.windsurf/workflows/`

## Patrones de Argumentos

Diferentes agentes usan diferentes placeholders de argumentos:

- **Basados en Markdown/prompt**: `$ARGUMENTS`
- **Basados en TOML**: `{{args}}`
- **Placeholders de script**: `{SCRIPT}` (reemplazado con la ruta real del script)
- **Placeholders de agente**: `__AGENT__` (reemplazado con el nombre del agente)

## Probando la Integración de un Nuevo Agente

1. **Prueba de build**: Ejecutar el script de creación de paquetes localmente
2. **Prueba de CLI**: Probar el comando `specify init --ai <agent>`
3. **Generación de archivos**: Verificar la estructura de directorios y archivos correcta
4. **Validación de comandos**: Asegurar que los comandos generados funcionan con el agente
5. **Actualización de contexto**: Probar los scripts de actualización de contexto del agente

## Errores Comunes

1. **Usar claves abreviadas en lugar de nombres reales de herramientas CLI**: Siempre usa el nombre real del ejecutable como clave de AGENT_CONFIG (ej., `"cursor-agent"` no `"cursor"`). Esto previene la necesidad de mapeos de casos especiales a lo largo del código.
2. **Olvidar los scripts de actualización**: Tanto los scripts de bash como los de PowerShell deben actualizarse al añadir nuevos agentes.
3. **Valor incorrecto de `requires_cli`**: Establecer como `True` solo para agentes que realmente tienen herramientas CLI para verificar; establecer como `False` para agentes basados en IDE.
4. **Formato de argumentos incorrecto**: Usar el formato de placeholder correcto para cada tipo de agente (`$ARGUMENTS` para Markdown, `{{args}}` para TOML).
5. **Nombres de directorios**: Seguir las convenciones específicas de cada agente exactamente (verificar los agentes existentes como referencia).
6. **Inconsistencia en texto de ayuda**: Actualizar todos los textos de cara al usuario de manera consistente (cadenas de ayuda, docstrings, README, mensajes de error).

## Consideraciones Futuras

Al añadir nuevos agentes:

- Considera los patrones nativos de comandos/flujos de trabajo del agente
- Asegura la compatibilidad con el proceso de Desarrollo Dirigido por Especificaciones
- Documenta cualquier requisito o limitación especial
- Actualiza esta guía con las lecciones aprendidas
- Verifica el nombre real de la herramienta CLI antes de añadirlo a AGENT_CONFIG

---

*Esta documentación debe actualizarse cada vez que se añadan nuevos agentes para mantener la precisión y completitud.*
