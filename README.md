# Zenci para Claude

Zenci es un punto de venta con inventario y facturación electrónica. Este plugin
conecta Claude con tu comercio en Zenci para que puedas pedir en lenguaje natural
lo que harías en la caja o en el panel.

## Qué puedes hacer

- Consultar existencias, productos, clientes, cotizaciones y reportes de ventas.
- Registrar ventas con sus pagos y emitir la factura electrónica, verificando el CUFE.
- Ver los resultados en tarjetas interactivas: venta con recibo y factura en PDF,
  panel del comercio, reportes con gráficas, existencias y cierres de caja.
- Revisar cada venta antes de registrarla, si activas «Revisar cada venta».

## Cómo usarlo

1. Instala el plugin y conecta el conector **Zenci** desde la pestaña Conectores
   del plugin (en Claude Code, con `/mcp`).
2. Inicia sesión en Zenci, elige tu comercio y autoriza.
3. Pide, por ejemplo: «¿Cuánto vendí esta semana?», «¿Cuántas camisetas negras
   talla M me quedan?» o «Factura dos cafés a Juan Pérez con tarjeta».

El plugin trae dos skills: `conectar-zenci` (conexión y preferencias) y
`operate-zenci-pos` (ventas, facturación, inventario y reportes).

## Datos y seguridad

- El plugin solo contiene instrucciones; no ejecuta programas en tu equipo.
- Claude envía las solicitudes al servidor de Zenci en `https://api.zenci.app/mcp`,
  con OAuth y PKCE. Cada llamada usa tu usuario, tu comercio y tus permisos
  actuales en Zenci; un cajero no puede hacer lo que su rol no le permite.
- Zenci recibe los datos de las operaciones que pidas (productos, clientes,
  ventas, pagos) y devuelve los del comercio conectado. No recibe el resto de la
  conversación ni tus archivos.
- Las ventas, pagos y facturas usan una clave de idempotencia: un reintento no
  duplica una venta.
- Puedes revocar el acceso en cualquier momento desconectando el conector.

Soporte: https://zenci.app
