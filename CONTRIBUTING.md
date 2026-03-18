# Contribuir a Spec Kit

¡Hola! Estamos encantados de que quieras contribuir a Spec Kit. Las contribuciones a este proyecto se [publican](https://help.github.com/articles/github-terms-of-service/#6-contributions-under-repository-license) al público bajo la [licencia de código abierto del proyecto](LICENSE).

Por favor ten en cuenta que este proyecto se publica con un [Código de Conducta del Contribuidor](CODE_OF_CONDUCT.md). Al participar en este proyecto aceptas cumplir con sus términos.

## Prerrequisitos para ejecutar y probar código

Estas son instalaciones únicas necesarias para poder probar tus cambios localmente como parte del proceso de envío de pull requests (PR).

1. Instalar [Python 3.11+](https://www.python.org/downloads/)
1. Instalar [uv](https://docs.astral.sh/uv/) para gestión de paquetes
1. Instalar [Git](https://git-scm.com/downloads)
1. Tener un [agente de codificación con IA disponible](README.md#-agentes-de-ia-soportados)

<details>
<summary><b>💡 Consejo si estás usando <code>VSCode</code> o <code>GitHub Codespaces</code> como tu IDE</b></summary>

<br>

Siempre que tengas [Docker](https://docker.com) instalado en tu máquina, puedes aprovechar los [Dev Containers](https://containers.dev) a través de esta [extensión de VSCode](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers), para configurar fácilmente tu entorno de desarrollo, con las herramientas mencionadas ya instaladas y configuradas, gracias al archivo `.devcontainer/devcontainer.json` (ubicado en la raíz del proyecto).

Para hacerlo, simplemente:

- Clona el repositorio
- Ábrelo con VSCode
- Abre la [Paleta de Comandos](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette) y selecciona "Dev Containers: Open Folder in Container..."

En [GitHub Codespaces](https://github.com/features/codespaces) es aún más sencillo, ya que aprovecha el `.devcontainer/devcontainer.json` automáticamente al abrir el codespace.

</details>

## Enviar un pull request

> [!NOTE]
> Si tu pull request introduce un cambio grande que impacta materialmente el trabajo del CLI o del resto del repositorio (ej., estás introduciendo nuevas plantillas, argumentos u otros cambios importantes), asegúrate de que fue **discutido y acordado** por los mantenedores del proyecto. Los pull requests con cambios grandes que no tuvieron una conversación y acuerdo previo serán cerrados.

1. Haz fork y clona el repositorio
1. Configura e instala las dependencias: `uv sync`
1. Asegúrate de que el CLI funciona en tu máquina: `uv run specify --help`
1. Crea un nuevo branch: `git checkout -b my-branch-name`
1. Realiza tu cambio, añade pruebas y asegúrate de que todo sigue funcionando
1. Prueba la funcionalidad del CLI con un proyecto de ejemplo si es relevante
1. Haz push a tu fork y envía un pull request
1. Espera a que tu pull request sea revisado y fusionado con merge.

Aquí hay algunas cosas que puedes hacer para aumentar la probabilidad de que tu pull request sea aceptado:

- Sigue las convenciones de codificación del proyecto.
- Escribe pruebas para la nueva funcionalidad.
- Actualiza la documentación (`README.md`, `spec-driven.md`) si tus cambios afectan funcionalidades de cara al usuario.
- Mantén tu cambio lo más enfocado posible. Si hay múltiples cambios que te gustaría hacer que no dependen entre sí, considera enviarlos como pull requests separados.
- Escribe un [buen mensaje de commit](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html).
- Prueba tus cambios con el flujo de trabajo de Desarrollo Dirigido por Especificaciones para asegurar la compatibilidad.

## Flujo de trabajo de desarrollo

Al trabajar en spec-kit:

1. Prueba los cambios con los comandos del CLI `specify` (`/speckit.specify`, `/speckit.plan`, `/speckit.tasks`) en tu agente de codificación preferido
2. Verifica que las plantillas funcionan correctamente en el directorio `templates/`
3. Prueba la funcionalidad de los scripts en el directorio `scripts/`
4. Asegúrate de que los archivos de memoria (`memory/constitution.md`) se actualicen si se realizan cambios importantes en el proceso

### Probar cambios de plantillas y comandos localmente

Ejecutar `uv run specify init` descarga los paquetes publicados, que no incluirán tus cambios locales.
Para probar tus plantillas, comandos y otros cambios localmente, sigue estos pasos:

1. **Crear paquetes de release**

   Ejecuta el siguiente comando para generar los paquetes locales:

   ```bash
   ./.github/workflows/scripts/create-release-packages.sh v1.0.0
   ```

2. **Copiar el paquete relevante a tu proyecto de prueba**

   ```bash
   cp -r .genreleases/sdd-copilot-package-sh/. <path-to-test-project>/
   ```

3. **Abrir y probar el agente**

   Navega a la carpeta de tu proyecto de prueba y abre el agente para verificar tu implementación.

## Contribuciones con IA en Spec Kit

> [!IMPORTANT]
>
> Si estás usando **cualquier tipo de asistencia de IA** para contribuir a Spec Kit,
> debe ser revelado en el pull request o issue.

¡Damos la bienvenida y fomentamos el uso de herramientas de IA para ayudar a mejorar Spec Kit! Muchas contribuciones valiosas han sido mejoradas con asistencia de IA para generación de código, detección de problemas y definición de funcionalidades.

Dicho esto, si estás usando cualquier tipo de asistencia de IA (ej., agentes, ChatGPT) mientras contribuyes a Spec Kit,
**esto debe ser revelado en el pull request o issue**, junto con el grado en que se usó la asistencia de IA (ej., comentarios de documentación vs. generación de código).

Si las respuestas o comentarios de tu PR están siendo generados por una IA, revela eso también.

Como excepción, las correcciones triviales de espaciado o errores tipográficos no necesitan ser reveladas, siempre que los cambios se limiten a pequeñas partes del código o frases cortas.

Un ejemplo de revelación:

> Este PR fue escrito principalmente por GitHub Copilot.

O una revelación más detallada:

> Consulté ChatGPT para entender el código base pero la solución
> fue completamente escrita manualmente por mí.

No revelar esto es ante todo una falta de respeto hacia los operadores humanos al otro lado del pull request, pero también dificulta determinar cuánto escrutinio aplicar a la contribución.

En un mundo perfecto, la asistencia de IA produciría trabajo de igual o mayor calidad que cualquier humano. Ese no es el mundo en el que vivimos hoy, y en la mayoría de los casos donde la supervisión o experiencia humana no está presente, se genera código que no puede ser razonablemente mantenido o evolucionado.

### Lo que buscamos

Al enviar contribuciones asistidas por IA, por favor asegúrate de que incluyan:

- **Revelación clara del uso de IA** - Eres transparente sobre el uso de IA y el grado en que la estás usando para la contribución
- **Comprensión y pruebas humanas** - Has probado personalmente los cambios y entiendes lo que hacen
- **Justificación clara** - Puedes explicar por qué el cambio es necesario y cómo encaja dentro de los objetivos de Spec Kit
- **Evidencia concreta** - Incluye casos de prueba, escenarios o ejemplos que demuestren la mejora
- **Tu propio análisis** - Comparte tus pensamientos sobre la experiencia del desarrollador de extremo a extremo

### Lo que cerraremos

Nos reservamos el derecho de cerrar contribuciones que parezcan ser:

- Cambios no probados enviados sin verificación
- Sugerencias genéricas que no abordan necesidades específicas de Spec Kit
- Envíos masivos que no muestran revisión o comprensión humana

### Pautas para el éxito

La clave es demostrar que entiendes y has validado los cambios que propones. Si un mantenedor puede determinar fácilmente que una contribución fue generada completamente por IA sin intervención o pruebas humanas, probablemente necesita más trabajo antes de ser enviada.

Los contribuidores que envíen consistentemente cambios generados por IA de bajo esfuerzo pueden ser restringidos de hacer más contribuciones a discreción de los mantenedores.

Por favor sé respetuoso con los mantenedores y revela la asistencia de IA.

## Recursos

- [Metodología de Desarrollo Dirigido por Especificaciones](./spec-driven.md)
- [Cómo Contribuir al Código Abierto](https://opensource.guide/how-to-contribute/)
- [Usando Pull Requests](https://help.github.com/articles/about-pull-requests/)
- [Ayuda de GitHub](https://help.github.com)
