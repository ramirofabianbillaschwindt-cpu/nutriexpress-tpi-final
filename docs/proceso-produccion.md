# Especificación del proceso de planificación de producción

## Participantes
Pool NutriExpress con lanes Ventas, Sistema, Compras y Depósito, y Cocina y Producción. Pool externo Proveedor, representado sin su proceso interno. El flujo de secuencia permanece dentro de cada pool; los mensajes cruzan entre NutriExpress y Proveedor.

## Flujo propuesto
1. Ventas inicia la planificación diaria y selecciona pedidos confirmados para una fecha de entrega.
2. Sistema calcula requerimientos desde Pedido, DetallePedido, Menu, DetalleReceta e Insumo.
3. Sistema consulta saldos por Lote y MovimientoStock y excluye lotes vencidos.
4. Una compuerta exclusiva pregunta si el stock utilizable alcanza.
5. Si alcanza, Cocina revisa y confirma la orden de producción.
6. Si falta, Compras solicita provisión al Proveedor mediante mensaje y espera su respuesta.
7. Una compuerta exclusiva evalúa si existe provisión compatible con el plazo.
8. Si la provisión es viable, Compras recibe los insumos, verifica cantidad y vencimiento y registra los lotes y sus movimientos de ingreso. Luego se vuelve a verificar disponibilidad.
9. Si no es viable, Ventas acuerda reprogramación o cancelación del pedido. Sistema actualiza su estado y finaliza esa planificación sin descontar consumos.
10. Antes de confirmar producción, Sistema valida nuevamente disponibilidad. Si cambió, vuelve a la gestión de faltantes.
11. Al confirmar, Sistema registra el consumo por lote una sola vez, en una operación consistente; Cocina elabora las viandas.
12. Sistema actualiza existencias y alertas. El evento final indica producción registrada.

## Excepciones y reglas
- No descontar stock por pedidos cancelados antes de producción.
- No utilizar lotes vencidos ni permitir saldos negativos.
- Priorizar lotes por vencimiento más próximo.
- Rechazar una confirmación duplicada.
- Si falla el registro, no dejar consumos parciales; informar el incidente y permitir una repetición segura.
- Mantener estable la receta aplicada a una producción confirmada.

## Situación
La especificación se representa en [dos vistas BPMN](../diagramas/Diagrama_BPMN_NutriExpress.pdf): proceso principal y detalle de abastecimiento. El [modelo editable](../diagramas/nutriexpress-produccion.bpmn) conserva ambos procesos y sus conexiones. Es un diseño descriptivo; no acredita software implementado.
