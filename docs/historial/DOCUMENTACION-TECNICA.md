# Documentación técnica

## Alcance y preservación

Se revisaron todos los archivos de definición del informe, tablas TMDL, relaciones, recursos de tema y las seis hojas del Excel. Se conservaron cuatro páginas, 34 visuales (cuatro KPI convertidos a tarjetas), nueve tablas del modelo incluyendo auxiliares de fecha, seis relaciones incluyendo dos de fecha automática, nombres y lineageTags. No se modificó la estructura binaria del PBIX, la caché ABF ni el Excel.

La copia modificada se entrega separada del proyecto abierto. El respaldo contiene la carpeta PowerBI tal como se recibió; el dataset incluido conserva su contenido original. Cambios externos al proyecto abierto pueden requerir recarga en Desktop; usar la copia entregada evita sobrescribir trabajo no guardado en el original.

## Modelo

FactVentas: 3.000 líneas. DimProducto: 30 productos; DimCliente: 100 clientes; DimVendedor: cinco vendedores; DimFecha: 365 fechas de 2025. No hay claves comerciales duplicadas, nombres comerciales duplicados ni huérfanos; tampoco fechas huérfanas. Las relaciones comerciales apuntan desde la tabla de hechos a las claves de dimensión. Se preserva la configuración original (muchos a uno y filtro simple por defecto); confirmar su interpretación efectiva en el motor Desktop. Dos relaciones adicionales soportan jerarquías de fecha automáticas.

No se eliminaron tablas automáticas, no se cambió la tabla calendario ni se reconfiguraron relaciones para evitar efectos colaterales. Mes ya tiene sortByColumn MesNumero. La condición de tabla de fechas y el orden de las jerarquías se deben verificar en Desktop.

## DAX revisado

| Familia | Decisión |
|---|---|
| Ventas Netas Corregidas | Aplicar Cantidad × PrecioUnitarioCLP × (1 − DescuentoPct) en Estado Confirmada, según LEEME |
| Ventas Netas | Alias a Ventas Netas Corregidas, para unificar las cuatro páginas |
| Ventas Promedio por linea | Numerador neto y denominador de líneas confirmadas; incluye líneas de devolución |
| Costo Total | Fórmula preservada: cantidades confirmadas × costo relacionado; devoluciones descuentan costo |
| Utilidad Bruta | Preservada como ventas corregidas menos costo; cambia por el nuevo ingreso neto |
| Margen Bruto %, Margen Producto %, Margen Vendedor % | Fórmulas preservadas; porcentajes con dos decimales |
| Participaciones | Fórmulas preservadas; formato porcentual, denominador sin filtros de toda la dimensión correspondiente |
| Rankings | RANKX / ALLSELECTED / DESC / DENSE preservado; nombres únicos en datos actuales |
| Clientes Activos, Vendedores Activos | Preservan definición de ventas netas positivas, no mero conteo de transacciones |
| Diagnósticos y Ventas Anuladas | Conservan base antes de descuentos para trazabilidad; no confundir con venta neta |
| Medida | Medida vacía heredada sin referencias en visuales; conservada para evitar eliminar contenido sin necesidad |

No se agregaron medidas. `DIVIDE(..., 0)` se conserva: ante denominador cero devuelve cero, una decisión heredada que conviene revisar si se requieren blancos. `CALCULATE` sobre Estado reemplaza filtros previos de esa misma columna; no se añadió KEEPFILTERS sin una definición comercial que lo justifique. `REMOVEFILTERS(DimProducto/DimCliente/DimVendedor)` también quita filtros de categoría, segmento o equipo pertenecientes a esa dimensión: la participación no equivale al porcentaje del subconjunto seleccionado. Los rankings sí respetan ALLSELECTED; esas semánticas son distintas y se mantienen documentadas.

## Conciliación

327.635.194 de todas las líneas antes de descuentos menos 4.649.285 de anuladas = 322.985.909 confirmado antes de descuentos. Menos 8.809.824,68 de descuentos netos = 314.176.084,32 de ventas netas. Menos 222.758.420 de costo = 91.417.664,32 de utilidad. Margen = 29,0975885443 %. No se redondea cada línea: se conserva la precisión y se formatea CLP entero para presentación.

Los CSV de ranking incluyen todos los miembros y ventas con decimales; representan el año completo sin filtros. No equivalen a ejecutar RANKX bajo todos los contextos de filtro. Las sumas por producto, cliente y vendedor deben conciliar con el mismo total. Los empates pueden ampliar un Top N en Power BI.

## Diseño

Se conserva el tema Frontier. Encabezados principales 28 pt, subtítulos 14 pt, títulos de visuales 14 pt y tablas 11 pt. La tabla de vendedores tenía valores de 30 pt; se redujeron a 11. Se habilitó el ajuste de texto en encabezados y se acortaron etiquetas visibles de medidas de tablas sin renombrar las medidas. Se ajustó un slicer que excedía el ancho del lienzo.

Los KPI del resumen tenían DimFecha[Mes] como tendencia y podían mostrar el último punto, en vez del total del período. Se sustituyeron por tarjetas clásicas conservando visual IDs y medidas. Comprobar en Desktop que la versión instalada admite estas tarjetas y sus propiedades de formato.

El Top 10 productos tenía un ORDER BY por agregación del nombre de producto (Function 3, conteo), no por importe. Se corrigió usando el mismo patrón serializado de medida del Top 10 clientes, con FactVentas[Ventas Netas Corregidas]. El orden visual y el Top N deben verificarse juntos en Desktop. La tabla de vendedores queda ordenada por ventas netas descendentes.

## Validación realizada y límites

52 archivos JSON y equivalentes se pudieron parsear; 99 referencias serializadas a campos se resolvieron; 12 extremos de relaciones resueltos; nombres de páginas/visuales coinciden con carpetas; orden y página activa válidos; visuales dentro de límites geométricos. Se preservaron todos los lineageTags de FactVentas. Excel y PBIX original comprobados con SHA-256.

14 archivos pasaron sus esquemas oficiales versionados. No se pudo descargar el esquema visualContainer 2.14.0 ni semanticModel/localSettings 1.2.0 (404); se conservaron los valores originales. El detalle está en validacion.json. Parsear JSON no demuestra cumplimiento semántico de las propiedades específicas de cada visual.

TMDL: revisión estática de referencias y conservación de metadatos, sin deserializador oficial disponible. DAX: revisión lógica y cálculo independiente con Decimal sobre Excel; no se ejecutó el motor DAX. No se probó apertura, actualización, caché, interacciones ni renderizado. No se certifica compatibilidad con octubre de 2026. Las pruebas de Desktop son obligatorias antes de usar el proyecto como versión final de portafolio.

## Calidad de datos

1.135 líneas preceden la FechaAlta de su cliente. Se conservan porque corregirlas requeriría una regla de generación o una fecha de alta autorizada. Las 77 devoluciones confirmadas tienen cantidades negativas. Los únicos estados observados son Confirmada y Anulada; si aparecen pendientes o despachadas, revisar la política de reconocimiento de ventas. No hay IVA explícito ni historial de costos; el costo usa el valor actual de DimProducto, válido para la demostración pero insuficiente para costos históricos reales.

## Portabilidad y Git

Las cinco consultas apuntan al archivo entregado mediante rutas absolutas; al moverlo, actualizar las rutas. No se añadió una expresión M de parámetro sin poder validar su carga en Desktop. Para una fase posterior, parametrizar RutaDatos desde Power Query y volver a guardar en Desktop. Excluir `.pbi`, ABF, PBIX y rutas/credenciales locales del repositorio. El PBIX conservado en el respaldo no contiene los cambios; abrir exclusivamente el PBIP de la entrega.
