---
name: conectar-zenci
description: Ayuda a conectar una cuenta de Zenci, iniciar sesión, reconectar una sesión vencida o diagnosticar por qué no aparecen las herramientas del comercio en Claude. Úsala al configurar Zenci, al elegir las preferencias de venta o cuando el usuario no pueda acceder a su cuenta desde el conector.
---

# Conectar Zenci

Ayuda al usuario a conectar su cuenta y comprobar el comercio autorizado. Responde en español, salvo que solicite otro idioma. Instalar el plugin y conectar la cuenta son pasos distintos: el plugin trae estas instrucciones y el conector trae las herramientas.

## Comprobar la conexión

1. Si la herramienta `zenci_connection` está disponible, llámala: es una consulta de identidad y permisos, no una venta.
2. Si responde correctamente, informa el usuario y el comercio que realmente devuelve. No interpretes los ámbitos OAuth como permisos adicionales. Si el usuario está configurando Zenci, sigue con [Preferencias](#preferencias); si pidió otra cosa, continúa con ella usando [Operar Zenci](../operate-zenci-pos/SKILL.md).
3. Si pide autenticación o devuelve `401`, indica al usuario que conecte o reconecte el conector de Zenci desde Claude. Iniciará sesión en la página de Zenci, elegirá su comercio y autorizará. No pidas su contraseña en el chat, no construyas una URL de autorización y no uses un token del POS como sustituto.
4. Si las herramientas no están disponibles, no afirmes que la contraseña sea incorrecta o que la sesión haya expirado. Lee [la guía de conexión](references/conexion.md) y da los pasos concretos del lugar donde está el usuario.

## Preferencias

Al configurar Zenci, ayuda al usuario a elegir cómo quiere operar. Llama a `zenci_settings_read` con `{}` para leer los valores actuales y las opciones disponibles.

Pregunta una cosa a la vez, partiendo de lo que el usuario ya haya dicho:

1. «¿En qué sucursal vendes normalmente?» Usa exactamente uno de los valores de `defaultBranch` que ofrece el esquema.
2. «¿Con qué método de pago cobras más seguido?» Usa uno de los valores de `defaultPaymentMethod`.
3. «¿Quieres revisar cada venta antes de que Zenci la registre?» Responde con `confirmSales` (recomendado: sí).

El usuario puede dejar los valores actuales u omitir este paso. Después llama a `zenci_settings_update` con un objeto `set` que contenga solo lo que cambió, por ejemplo `{"set":{"defaultBranch":"Casa Matriz","confirmSales":true}}`. Si no cambia nada, no lo llames. Confirma lo guardado con los valores que devuelve la herramienta; si falla, no digas que se guardó.

Para terminar, muestra el panel del comercio con `zenci_show_dashboard` y `{}`. Si el usuario estaba en medio de otra tarea, sigue con ella en la misma conversación.

## Cuentas y comercios

Cada conexión es de una persona y un comercio. Para cambiar de comercio, desconecta y vuelve a conectar el conector de Zenci y elige el otro comercio en la página de Zenci; no cambies un identificador en las llamadas.

Confirma que la conexión funciona solo después de obtener una respuesta real de `zenci_connection`. No confirmes acceso al inventario sin consultarlo ni hagas escrituras para probar la sesión.
