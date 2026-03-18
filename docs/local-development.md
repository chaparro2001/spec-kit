# Guía de Desarrollo Local

Esta guía muestra cómo iterar sobre el CLI `specify` de forma local sin publicar una versión ni hacer commit a `main` primero.

> Los scripts ahora tienen variantes tanto en Bash (`.sh`) como en PowerShell (`.ps1`). El CLI selecciona automáticamente según el SO a menos que pases `--script sh|ps`.

## 1. Clonar y Cambiar de Rama

```bash
git clone https://github.com/github/spec-kit.git
cd spec-kit
# Work on a feature branch
git checkout -b your-feature-branch
```

## 2. Ejecutar el CLI Directamente (Retroalimentación más Rápida)

Puedes ejecutar el CLI a través del punto de entrada del módulo sin instalar nada:

```bash
# From repo root
python -m src.specify_cli --help
python -m src.specify_cli init demo-project --ai claude --ignore-agent-tools --script sh
```

Si prefieres invocar el archivo de script directamente (usa shebang):

```bash
python src/specify_cli/__init__.py init demo-project --script ps
```

## 3. Usar Instalación Editable (Entorno Aislado)

Crea un entorno aislado usando `uv` para que las dependencias se resuelvan exactamente como las obtienen los usuarios finales:

```bash
# Create & activate virtual env (uv auto-manages .venv)
uv venv
source .venv/bin/activate  # or on Windows PowerShell: .venv\Scripts\Activate.ps1

# Install project in editable mode
uv pip install -e .

# Now 'specify' entrypoint is available
specify --help
```

Volver a ejecutar después de editar el código no requiere reinstalación gracias al modo editable.

## 4. Invocar con uvx Directamente Desde Git (Rama Actual)

`uvx` puede ejecutarse desde una ruta local (o una referencia de Git) para simular flujos de usuario:

```bash
uvx --from . specify init demo-uvx --ai copilot --ignore-agent-tools --script sh
```

También puedes apuntar uvx a una rama específica sin hacer merge:

```bash
# Push your working branch first
git push origin your-feature-branch
uvx --from git+https://github.com/github/spec-kit.git@your-feature-branch specify init demo-branch-test --script ps
```

### 4a. uvx con Ruta Absoluta (Ejecutar Desde Cualquier Lugar)

Si estás en otro directorio, usa una ruta absoluta en lugar de `.`:

```bash
uvx --from /mnt/c/GitHub/spec-kit specify --help
uvx --from /mnt/c/GitHub/spec-kit specify init demo-anywhere --ai copilot --ignore-agent-tools --script sh
```

Establece una variable de entorno por conveniencia:

```bash
export SPEC_KIT_SRC=/mnt/c/GitHub/spec-kit
uvx --from "$SPEC_KIT_SRC" specify init demo-env --ai copilot --ignore-agent-tools --script ps
```

(Opcional) Define una función de shell:

```bash
specify-dev() { uvx --from /mnt/c/GitHub/spec-kit specify "$@"; }
# Then
specify-dev --help
```

## 5. Probar la Lógica de Permisos de Scripts

Después de ejecutar un `init`, verifica que los scripts de shell sean ejecutables en sistemas POSIX:

```bash
ls -l scripts | grep .sh
# Expect owner execute bit (e.g. -rwxr-xr-x)
```

En Windows usarás los scripts `.ps1` en su lugar (no se necesita chmod).

## 6. Ejecutar Lint / Verificaciones Básicas (Añade las Tuyas)

Actualmente no se incluye una configuración de lint obligatoria, pero puedes hacer una verificación rápida de importabilidad:

```bash
python -c "import specify_cli; print('Import OK')"
```

## 7. Construir un Wheel Localmente (Opcional)

Valida el empaquetado antes de publicar:

```bash
uv build
ls dist/
```

Instala el artefacto construido en un entorno temporal limpio si es necesario.

## 8. Usar un Workspace Temporal

Al probar `init --here` en un directorio con archivos, crea un workspace temporal:

```bash
mkdir /tmp/spec-test && cd /tmp/spec-test
python -m src.specify_cli init --here --ai claude --ignore-agent-tools --script sh  # if repo copied here
```

O copia solo la parte modificada del CLI si deseas un sandbox más ligero.

## 9. Depurar Problemas de Red / Omisiones de TLS

Si necesitas omitir la validación TLS mientras experimentas:

```bash
specify check --skip-tls
specify init demo --skip-tls --ai gemini --ignore-agent-tools --script ps
```

(Usar solo para experimentación local.)

## 10. Resumen del Ciclo Rápido de Edición

| Acción | Comando |
|--------|---------|
| Ejecutar CLI directamente | `python -m src.specify_cli --help` |
| Instalación editable | `uv pip install -e .` luego `specify ...` |
| Ejecución local con uvx (raíz del repo) | `uvx --from . specify ...` |
| Ejecución local con uvx (ruta absoluta) | `uvx --from /mnt/c/GitHub/spec-kit specify ...` |
| uvx desde rama de Git | `uvx --from git+URL@branch specify ...` |
| Construir wheel | `uv build` |

## 11. Limpieza

Elimina artefactos de compilación / entorno virtual rápidamente:

```bash
rm -rf .venv dist build *.egg-info
```

## 12. Problemas Comunes

| Síntoma | Solución |
|---------|----------|
| `ModuleNotFoundError: typer` | Ejecutar `uv pip install -e .` |
| Scripts no ejecutables (Linux) | Volver a ejecutar init o `chmod +x scripts/*.sh` |
| Paso de Git omitido | Pasaste `--no-git` o Git no está instalado |
| Tipo de script incorrecto descargado | Pasar `--script sh` o `--script ps` explícitamente |
| Errores de TLS en red corporativa | Probar `--skip-tls` (no para producción) |

## 13. Próximos Pasos

- Actualiza la documentación y sigue el Inicio Rápido usando tu CLI modificado
- Abre un PR cuando estés satisfecho
- (Opcional) Etiqueta una versión una vez que los cambios lleguen a `main`
