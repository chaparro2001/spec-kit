# Guía de Instalación

## Requisitos Previos

- **Linux/macOS** (o Windows; los scripts de PowerShell ahora son compatibles sin WSL)
- Agente de programación con IA: [Claude Code](https://www.anthropic.com/claude-code), [GitHub Copilot](https://code.visualstudio.com/), [Codebuddy CLI](https://www.codebuddy.ai/cli), [Gemini CLI](https://github.com/google-gemini/gemini-cli) o [Pi Coding Agent](https://pi.dev)
- [uv](https://docs.astral.sh/uv/) para la gestión de paquetes
- [Python 3.11+](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)

## Instalación

### Inicializar un Nuevo Proyecto

La forma más sencilla de comenzar es inicializar un nuevo proyecto:

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>
```

O inicializar en el directorio actual:

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init .
# o usar la bandera --here
uvx --from git+https://github.com/github/spec-kit.git specify init --here
```

### Especificar el Agente de IA

Puedes especificar proactivamente tu agente de IA durante la inicialización:

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai claude
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai gemini
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai copilot
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai codebuddy
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai pi
```

### Especificar el Tipo de Script (Shell vs PowerShell)

Todos los scripts de automatización ahora tienen variantes tanto en Bash (`.sh`) como en PowerShell (`.ps1`).

Comportamiento automático:

- Windows por defecto: `ps`
- Otros SO por defecto: `sh`
- Modo interactivo: se te preguntará a menos que pases `--script`

Forzar un tipo de script específico:

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --script sh
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --script ps
```

### Ignorar la Verificación de Herramientas del Agente

Si prefieres obtener las plantillas sin verificar que tengas las herramientas correctas:

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai claude --ignore-agent-tools
```

## Verificación

Después de la inicialización, deberías ver los siguientes comandos disponibles en tu agente de IA:

- `/speckit.specify` - Crear especificaciones
- `/speckit.plan` - Generar planes de implementación
- `/speckit.tasks` - Desglosar en tareas accionables

El directorio `.specify/scripts` contendrá tanto scripts `.sh` como `.ps1`.

## Solución de Problemas

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
