# Indicadores y estándares propuestos

Las metas provienen de la entrega 2. No se presentan resultados de pruebas ni mejoras operativas que todavía no se hayan medido.

| Indicador | Cálculo o criterio | Meta | Frecuencia y responsable |
| --- | --- | --- | --- |
| Tiempo de respuesta | Percentil 95 de duración de consultas de stock con 20 usuarios concurrentes | Hasta 2 segundos | En pruebas y ante cambios; Calidad |
| Capacidad | Operaciones correctas con un conjunto controlado de registros | 50.000 movimientos y 10.000 pedidos | Antes de aceptación; Desarrollo y Datos |
| Exactitud de inventario | Registros de saldo que coinciden con conteo físico, dentro de tolerancia documentada, / registros auditados × 100 | Al menos 98 % al tercer mes | Mensual; Depósito y Administración |
| Reducción de merma | (Merma base - merma posterior) / merma base × 100, usando períodos comparables | 20 % durante los primeros cuatro meses | Mensual; Administración |
| Disponibilidad | (Tiempo operativo previsto - indisponibilidad no programada) / tiempo operativo previsto × 100 | Al menos 99 % mensual | Mensual; Sistemas |

## Reglas de medición
La línea base de merma debe ser mayor que cero y usar el mismo criterio de valoración para evitar confundir inflación con mejora. Si no existe una base comparable, el resultado queda pendiente. La exactitud requiere unidades y tolerancias homogéneas. La disponibilidad excluye mantenimiento previamente programado, tal como se definió en la entrega 2.

Ante un desvío se registra evidencia, se identifica la causa, se asigna una acción y se verifica nuevamente. Ninguna meta se considera cumplida solo por haber sido redactada.
