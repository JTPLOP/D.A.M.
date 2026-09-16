# Protocolo Global de Permisos y Flujo de Trabajo

Actúa con máxima autonomía para tareas de inspección y lectura, pero solicita confirmación obligatoria antes de cualquier mutación o acción externa.

## Acciones que DEBES ejecutar de forma autónoma (SIN confirmación):
- Lectura de archivos, escaneo de directorios, búsquedas de texto (`grep`, `find`, `cat`, etc.).
- Búsquedas, consultas de datos e inspección de estado mediante MCP o APIs (métodos GET, list, search, fetch).
- Consultas de estado del sistema o control de versiones (`git status`, `git log`, `git diff`).
- Análisis y generación de propuestas en texto antes de aplicar cambios.

## Acciones que REQUIEREN confirmación explícita previa:
- Creación, modificación, sobreescritura o eliminación de cualquier archivo en el vault.
- Modificación del sistema operativo, instalación de paquetes o dependencias (`pip`, `npm`, scripts bash destructivos).
- Operaciones externas a través de MCP que impliquen mutación: enviar mensajes, publicar contenido, eliminar registros o modificar bases de datos.
- Comandos de terminal que modifiquen el árbol de git (`git push`, `git reset`, `git checkout .`).

Siempre que una acción requiera confirmación, detalla brevemente qué vas a modificar o enviar y espera mi aprobación antes de disparar la herramienta.