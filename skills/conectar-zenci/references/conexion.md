# Cuenta de Zenci en Claude

## Datos de la conexión

| Campo | Valor |
| --- | --- |
| URL del conector | `https://api.zenci.app/mcp` |
| Autenticación | OAuth con PKCE S256. Claude se identifica solo (CIMD): no hace falta Client ID ni Client Secret |
| Ámbitos | `zenci:read zenci:write`, o solo `zenci:read` para lectura |

## Conectar desde claude.ai, el escritorio o Cowork

1. Con el plugin instalado, abre **Personalizar → Plugins → Zenci** y entra en la pestaña **Conectores**. Pulsa **Conectar** en Zenci. Si no usas el plugin, añade el conector desde **Personalizar → Conectores**.
2. Se abre la página de Zenci: inicia sesión, elige el comercio y pulsa **Permitir**. La pantalla debe decir que quien pide acceso es **Claude** (`claude.ai`).
3. Vuelve a la conversación y activa Zenci en el menú de herramientas del chat si no está activo.

En los planes Team y Enterprise, una persona propietaria de la organización añade primero el conector y cada miembro conecta después su propia cuenta.

## Conectar desde Claude Code

El plugin declara el servidor en `.mcp.json`. En `/mcp`, elige `zenci` y autentica: Claude Code abre la página de Zenci, que debe decir **Claude Code**, y vuelve a un puerto local de tu equipo al terminar.

## Si no aparecen las herramientas

- Comprueba que el conector figure como conectado y que Zenci esté activado en esa conversación.
- Si la conexión expiró o se revocó desde Zenci, desconéctalo y vuelve a conectarlo.
- Si la página de Zenci muestra «Cliente o callback no registrado», copia el mensaje exacto: es un problema de configuración del servidor, no de la contraseña.
- Las tarjetas interactivas se ven en claude.ai, el escritorio y el móvil. Claude Code muestra los mismos datos como texto.

Fuentes: [conectores en Claude](https://claude.com/docs/connectors/building/authentication) y [plugins](https://claude.com/docs/plugins/build).
