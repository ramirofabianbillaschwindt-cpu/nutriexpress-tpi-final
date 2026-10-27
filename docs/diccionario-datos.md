# Diccionario de datos de NutriExpress

Modelo preliminar del módulo de inventario y planificación de demanda.

## Insumo

| Campo | Tipo de dato | Descripción funcional |
|---|---|---|
| id_insumo | Integer PK | Identificador único del insumo. |
| nombre | String(100) | Denominación del ingrediente o envase. |
| unidad_medida | String(10) | Unidad base: kg, l o un; se usa en todas las operaciones. |
| stock_minimo | Decimal(12,3) | Umbral que activa una alerta de reposición. |
| activo | Boolean | Permite usar el insumo en nuevas operaciones. |

## Lote

| Campo | Tipo de dato | Descripción funcional |
|---|---|---|
| id_lote | Integer PK | Identificador único de la partida recibida. |
| id_insumo | Integer FK | Insumo al que pertenece el lote. |
| codigo_lote | String(50) | Código de trazabilidad de la partida. |
| fecha_ingreso | Date | Fecha de recepción en depósito. |
| fecha_vencimiento | Date | Fecha límite de utilización del lote. |
| costo_unitario | Decimal(12,2) | Costo por unidad base, expresado en pesos. |

## MovimientoStock

| Campo | Tipo de dato | Descripción funcional |
|---|---|---|
| id_movimiento | Integer PK | Identificador único de la operación. |
| id_lote | Integer FK | Lote afectado por la operación. |
| fecha_hora | DateTime | Momento en que se registra el movimiento. |
| tipo | String(20) | Ingreso, consumo, merma, ajuste positivo o negativo. |
| cantidad | Decimal(12,3) | Magnitud positiva expresada en la unidad base. |
| responsable | String(80) | Identificador del usuario que registra la operación. |

## Menu

| Campo | Tipo de dato | Descripción funcional |
|---|---|---|
| id_menu | Integer PK | Identificador de la variedad de vianda. |
| nombre | String(100) | Nombre comercial del menú. |
| descripcion | String(250) | Composición general de la preparación. |
| activo | Boolean | Indica si puede recibir nuevos pedidos. |

## DetalleReceta

| Campo | Tipo de dato | Descripción funcional |
|---|---|---|
| id_detalle_receta | Integer PK | Identificador del componente de una receta. |
| id_menu | Integer FK | Menú al que corresponde el componente. |
| id_insumo | Integer FK | Ingrediente o envase requerido. |
| cantidad_por_vianda | Decimal(12,3) | Cantidad necesaria para una vianda, en unidad base. |

## Pedido

| Campo | Tipo de dato | Descripción funcional |
|---|---|---|
| id_pedido | Integer PK | Identificador único del pedido. |
| referencia_cliente | String(80) | Código interno del cliente que solicita las viandas. |
| fecha_pedido | DateTime | Momento de ingreso de la solicitud. |
| fecha_entrega | Date | Día previsto para entregar las viandas. |
| estado | String(20) | Pendiente, confirmado, en producción, entregado o cancelado. |

## DetallePedido

| Campo | Tipo de dato | Descripción funcional |
|---|---|---|
| id_detalle_pedido | Integer PK | Identificador del renglón del pedido. |
| id_pedido | Integer FK | Pedido al que pertenece el renglón. |
| id_menu | Integer FK | Variedad de vianda solicitada. |
| cantidad_viandas | Integer | Número de viandas de esa variedad; mayor que cero. |

## Reglas

Las PK son únicas y las FK referencian registros existentes. Las cantidades de receta y movimiento son positivas. El saldo se obtiene de movimientos por lote; se excluyen vencidos de la disponibilidad y se prioriza FEFO. Las correcciones conservan el original y generan movimientos compensatorios. La confirmación de producción debe registrar consumos atómicos e idempotentes.

La gestión completa de proveedores, usuarios y la entidad de confirmación de producción se detallarán en el diseño de implementación; este diccionario es preliminar.
