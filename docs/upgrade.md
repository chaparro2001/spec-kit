# Guía de Actualización

> Ya tienes Spec Kit instalado y deseas actualizar a la última versión para obtener nuevas funcionalidades, correcciones de errores o comandos slash actualizados. Esta guía cubre tanto la actualización de la herramienta CLI como la actualización de los archivos de tu proyecto.

---

## Referencia Rápida

| Qué Actualizar | Comando | Cuándo Usar |
|----------------|---------|-------------|
| **Solo la Herramienta CLI** | `uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git` | Obtener las últimas funcionalidades del CLI sin tocar los archivos del proyecto |
| **Archivos del Proyecto** | `specify init --here --force --ai <your-agent>` | Actualizar comandos slash, plantillas y scripts en tu proyecto |
| **Ambos** | Ejecutar la actualización del CLI y luego la del proyecto | Recomendado para actualizaciones de versiones mayores |

---

## Parte 1: Actualizar la Herramienta CLI

La herramienta CLI (`specify`) es independiente de los archivos de tu proyecto. Actualízala para obtener las últimas funcionalidades y correcciones de errores.

### Si instalaste con `uv tool install`

```bash
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
```

### Si usas comandos `uvx` de un solo uso

No se necesita actualización: `uvx` siempre obtiene la última versión. Simplemente ejecuta tus comandos como de costumbre:

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init --here --ai copilot
```

### Verificar la actualización

```bash
specify check
```

Esto muestra las herramientas instaladas y confirma que el CLI está funcionando.

---

## Parte 2: Actualizar los Archivos del Proyecto

Cuando Spec Kit publica nuevas funcionalidades (como nuevos comandos slash o plantillas actualizadas), necesitas actualizar los archivos de Spec Kit en tu proyecto.

### ¿Qué se actualiza?

Ejecutar `specify init --here --force` actualizará:

- ✅ **Archivos de comandos slash** (`.claude/commands/`, `.github/prompts/`, etc.)
- ✅ **Archivos de scripts** (`.specify/scripts/`)
- ✅ **Archivos de plantillas** (`.specify/templates/`)
- ✅ **Archivos de memoria compartida** (`.specify/memory/`) - **⚠️ Ver advertencias abajo**

### ¿Qué permanece seguro?

Estos archivos **nunca son modificados** por la actualización; los paquetes de plantillas ni siquiera los contienen:

- ✅ **Tus especificaciones** (`specs/001-my-feature/spec.md`, etc.) - **CONFIRMADO SEGURO**
- ✅ **Tus planes de implementación** (`specs/001-my-feature/plan.md`, `tasks.md`, etc.) - **CONFIRMADO SEGURO**
- ✅ **Tu código fuente** - **CONFIRMADO SEGURO**
- ✅ **Tu historial de git** - **CONFIRMADO SEGURO**

El directorio `specs/` está completamente excluido de los paquetes de plantillas y nunca será modificado durante las actualizaciones.

### Comando de actualización

Ejecuta esto dentro del directorio de tu proyecto:

```bash
specify init --here --force --ai <your-agent>
```

Reemplaza `<your-agent>` con tu asistente de IA. Consulta esta lista de [Agentes de IA Soportados](../README.md#-supported-ai-agents)

**Ejemplo:**

```bash
specify init --here --force --ai copilot
```

### Entendiendo la bandera `--force`

Sin `--force`, el CLI te advierte y pide confirmación:

```text
Warning: Current directory is not empty (25 items)
Template files will be merged with existing content and may overwrite existing files
Proceed? [y/N]
```

Con `--force`, omite la confirmación y procede inmediatamente.

**Importante: Tu directorio `specs/` siempre está seguro.** La bandera `--force` solo afecta a los archivos de plantillas (comandos, scripts, plantillas, memoria). Tus especificaciones de funcionalidades, planes y tareas en `specs/` nunca están incluidos en los paquetes de actualización y no pueden ser sobrescritos.

---

## ⚠️ Advertencias Importantes

### 1. El archivo de constitución será sobrescrito

**Problema conocido:** `specify init --here --force` actualmente sobrescribe `.specify/memory/constitution.md` con la plantilla por defecto, borrando cualquier personalización que hayas realizado.

**Solución alternativa:**

```bash
# 1. Back up your constitution before upgrading
cp .specify/memory/constitution.md .specify/memory/constitution-backup.md

# 2. Run the upgrade
specify init --here --force --ai copilot

# 3. Restore your customized constitution
mv .specify/memory/constitution-backup.md .specify/memory/constitution.md
```

O usa git para restaurarlo:

```bash
# After upgrade, restore from git history
git restore .specify/memory/constitution.md
```

### 2. Modificaciones personalizadas en plantillas

Si personalizaste alguna plantilla en `.specify/templates/`, la actualización las sobrescribirá. Haz una copia de seguridad primero:

```bash
# Back up custom templates
cp -r .specify/templates .specify/templates-backup

# After upgrade, merge your changes back manually
```

### 3. Comandos slash duplicados (agentes basados en IDE)

Algunos agentes basados en IDE (como Kilo Code, Windsurf) pueden mostrar **comandos slash duplicados** después de actualizar: aparecen tanto las versiones antiguas como las nuevas.

**Solución:** Elimina manualmente los archivos de comandos antiguos de la carpeta de tu agente.

**Ejemplo para Kilo Code:**

```bash
# Navigate to the agent's commands folder
cd .kilocode/rules/

# List files and identify duplicates
ls -la

# Delete old versions (example filenames - yours may differ)
rm speckit.specify-old.md
rm speckit.plan-v1.md
```

Reinicia tu IDE para actualizar la lista de comandos.

---

## Escenarios Comunes

### Escenario 1: "Solo quiero los nuevos comandos slash"

```bash
# Upgrade CLI (if using persistent install)
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git

# Update project files to get new commands
specify init --here --force --ai copilot

# Restore your constitution if customized
git restore .specify/memory/constitution.md
```

### Escenario 2: "Personalicé plantillas y la constitución"

```bash
# 1. Back up customizations
cp .specify/memory/constitution.md /tmp/constitution-backup.md
cp -r .specify/templates /tmp/templates-backup

# 2. Upgrade CLI
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git

# 3. Update project
specify init --here --force --ai copilot

# 4. Restore customizations
mv /tmp/constitution-backup.md .specify/memory/constitution.md
# Manually merge template changes if needed
```

### Escenario 3: "Veo comandos slash duplicados en mi IDE"

Esto sucede con agentes basados en IDE (Kilo Code, Windsurf, Roo Code, etc.).

```bash
# Find the agent folder (example: .kilocode/rules/)
cd .kilocode/rules/

# List all files
ls -la

# Delete old command files
rm speckit.old-command-name.md

# Restart your IDE
```

### Escenario 4: "Estoy trabajando en un proyecto sin Git"

Si inicializaste tu proyecto con `--no-git`, aún puedes actualizar:

```bash
# Manually back up files you customized
cp .specify/memory/constitution.md /tmp/constitution-backup.md

# Run upgrade
specify init --here --force --ai copilot --no-git

# Restore customizations
mv /tmp/constitution-backup.md .specify/memory/constitution.md
```

La bandera `--no-git` omite la inicialización de git pero no afecta las actualizaciones de archivos.

---

## Uso de la Bandera `--no-git`

La bandera `--no-git` le indica a Spec Kit que **omita la inicialización del repositorio git**. Esto es útil cuando:

- Gestionas el control de versiones de otra manera (Mercurial, SVN, etc.)
- Tu proyecto es parte de un monorepo más grande con una configuración de git existente
- Estás experimentando y aún no quieres control de versiones

**Durante la configuración inicial:**

```bash
specify init my-project --ai copilot --no-git
```

**Durante la actualización:**

```bash
specify init --here --force --ai copilot --no-git
```

### Lo que `--no-git` NO hace

❌ NO previene las actualizaciones de archivos
❌ NO omite la instalación de comandos slash
❌ NO afecta la fusión de plantillas

**Solo** omite la ejecución de `git init` y la creación del commit inicial.

### Trabajar sin Git

Si usas `--no-git`, necesitarás gestionar los directorios de funcionalidades manualmente:

**Establece la variable de entorno `SPECIFY_FEATURE`** antes de usar los comandos de planificación:

```bash
# Bash/Zsh
export SPECIFY_FEATURE="001-my-feature"

# PowerShell
$env:SPECIFY_FEATURE = "001-my-feature"
```

Esto le indica a Spec Kit qué directorio de funcionalidad usar al crear especificaciones, planes y tareas.

**Por qué esto importa:** Sin git, Spec Kit no puede detectar el nombre de tu rama actual para determinar la funcionalidad activa. La variable de entorno proporciona ese contexto manualmente.

---

## Solución de Problemas

### "Los comandos slash no aparecen después de la actualización"

**Causa:** El agente no recargó los archivos de comandos.

**Solución:**

1. **Reinicia tu IDE/editor completamente** (no solo recargar la ventana)
2. **Para agentes basados en CLI**, verifica que los archivos existan:

   ```bash
   ls -la .claude/commands/      # Claude Code
   ls -la .gemini/commands/      # Gemini
   ls -la .cursor/commands/      # Cursor
   ls -la .pi/prompts/           # Pi Coding Agent
   ```

3. **Verifica la configuración específica del agente:**
   - Codex requiere la variable de entorno `CODEX_HOME`
   - Algunos agentes necesitan reiniciar el workspace o limpiar la caché

### "Perdí mis personalizaciones de la constitución"

**Solución:** Restaurar desde git o una copia de seguridad:

```bash
# If you committed before upgrading
git restore .specify/memory/constitution.md

# If you backed up manually
cp /tmp/constitution-backup.md .specify/memory/constitution.md
```

**Prevención:** Siempre haz commit o copia de seguridad de `constitution.md` antes de actualizar.

### "Advertencia: El directorio actual no está vacío"

**Mensaje de advertencia completo:**

```text
Warning: Current directory is not empty (25 items)
Template files will be merged with existing content and may overwrite existing files
Do you want to continue? [y/N]
```

**Qué significa esto:**

Esta advertencia aparece cuando ejecutas `specify init --here` (o `specify init .`) en un directorio que ya tiene archivos. Te está indicando:

1. **El directorio tiene contenido existente** - En el ejemplo, 25 archivos/carpetas
2. **Los archivos se fusionarán** - Los nuevos archivos de plantilla se añadirán junto a tus archivos existentes
3. **Algunos archivos podrían ser sobrescritos** - Si ya tienes archivos de Spec Kit (`.claude/`, `.specify/`, etc.), serán reemplazados con las nuevas versiones

**Qué se sobrescribe:**

Solo los archivos de infraestructura de Spec Kit:

- Archivos de comandos del agente (`.claude/commands/`, `.github/prompts/`, etc.)
- Scripts en `.specify/scripts/`
- Plantillas en `.specify/templates/`
- Archivos de memoria en `.specify/memory/` (incluyendo la constitución)

**Qué no se toca:**

- Tu directorio `specs/` (especificaciones, planes, tareas)
- Tus archivos de código fuente
- Tu directorio `.git/` e historial de git
- Cualquier otro archivo que no sea parte de las plantillas de Spec Kit

**Cómo responder:**

- **Escribe `y` y presiona Enter** - Proceder con la fusión (recomendado si estás actualizando)
- **Escribe `n` y presiona Enter** - Cancelar la operación
- **Usa la bandera `--force`** - Omitir esta confirmación por completo:

  ```bash
  specify init --here --force --ai copilot
  ```

**Cuándo ves esta advertencia:**

- ✅ **Esperado** al actualizar un proyecto existente de Spec Kit
- ✅ **Esperado** al añadir Spec Kit a un código base existente
- ⚠️ **Inesperado** si pensabas que estabas creando un nuevo proyecto en un directorio vacío

**Consejo de prevención:** Antes de actualizar, haz commit o copia de seguridad de tu `.specify/memory/constitution.md` si lo personalizaste.

### "La actualización del CLI no parece funcionar"

Verifica la instalación:

```bash
# Check installed tools
uv tool list

# Should show specify-cli

# Verify path
which specify

# Should point to the uv tool installation directory
```

Si no se encuentra, reinstala:

```bash
uv tool uninstall specify-cli
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

### "¿Necesito ejecutar specify cada vez que abro mi proyecto?"

**Respuesta corta:** No, solo ejecutas `specify init` una vez por proyecto (o al actualizar).

**Explicación:**

La herramienta CLI `specify` se usa para:

- **Configuración inicial:** `specify init` para inicializar Spec Kit en tu proyecto
- **Actualizaciones:** `specify init --here --force` para actualizar plantillas y comandos
- **Diagnósticos:** `specify check` para verificar la instalación de herramientas

Una vez que hayas ejecutado `specify init`, los comandos slash (como `/speckit.specify`, `/speckit.plan`, etc.) quedan **instalados permanentemente** en la carpeta del agente de tu proyecto (`.claude/`, `.github/prompts/`, `.pi/prompts/`, etc.). Tu asistente de IA lee estos archivos de comandos directamente, sin necesidad de ejecutar `specify` de nuevo.

**Si tu agente no reconoce los comandos slash:**

1. **Verifica que los archivos de comandos existan:**

   ```bash
   # For GitHub Copilot
   ls -la .github/prompts/

   # For Claude
   ls -la .claude/commands/

   # For Pi
   ls -la .pi/prompts/
   ```

2. **Reinicia tu IDE/editor completamente** (no solo recargar la ventana)

3. **Verifica que estés en el directorio correcto** donde ejecutaste `specify init`

4. **Para algunos agentes**, puede ser necesario recargar el workspace o limpiar la caché

**Problema relacionado:** Si Copilot no puede abrir archivos locales o usa comandos de PowerShell inesperadamente, esto es típicamente un problema de contexto del IDE, no relacionado con `specify`. Intenta:

- Reiniciar VS Code
- Verificar los permisos de archivos
- Asegurarte de que la carpeta del workspace esté correctamente abierta

---

## Compatibilidad de Versiones

Spec Kit sigue versionado semántico para las versiones mayores. El CLI y los archivos del proyecto están diseñados para ser compatibles dentro de la misma versión mayor.

**Buena práctica:** Mantén tanto el CLI como los archivos del proyecto sincronizados actualizando ambos juntos durante los cambios de versiones mayores.

---

## Próximos Pasos

Después de actualizar:

- **Prueba los nuevos comandos slash:** Ejecuta `/speckit.constitution` u otro comando para verificar que todo funcione
- **Revisa las notas de la versión:** Consulta las [Publicaciones en GitHub](https://github.com/github/spec-kit/releases) para nuevas funcionalidades y cambios importantes
- **Actualiza los flujos de trabajo:** Si se añadieron nuevos comandos, actualiza los flujos de trabajo de desarrollo de tu equipo
- **Consulta la documentación:** Visita [github.io/spec-kit](https://github.github.io/spec-kit/) para las guías actualizadas
