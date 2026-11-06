> **Revisión v2:** el usuario reportó un error de apertura TMDL en v1. Se corrigió la serialización de Ventas Netas Corregidas; ver CORRECCION-v2.md. Esta revisión aún no tiene apertura exitosa confirmada en Desktop.

# Retail Sales Intelligence — Distribuidora San Pedro

Proyecto demostrativo de Business Intelligence para una distribuidora ficticia del Gran Concepción, Chile. Explora ventas, rentabilidad, productos, clientes y desempeño comercial con 3.000 líneas de ventas sintéticas de 2025.

**Estado:** definiciones PBIP/PBIR corregidas y auditoría estática realizada. Pendiente apertura, actualización y revisión visual en Power BI Desktop de octubre de 2026. No se declara compatibilidad completamente probada.

## Preguntas de negocio

- ¿Cómo evolucionan las ventas netas y la utilidad bruta durante el año?
- ¿Qué productos concentran ventas y cuáles presentan menor margen?
- ¿Cómo se distribuyen las ventas por cliente, comuna y segmento?
- ¿Qué vendedores aportan más ventas y rentabilidad?

## Páginas

| Página | Contenido |
|---|---|
| Resumen Comercial | Tarjetas del período seleccionado, evolución mensual, ventas y utilidad por dimensiones comerciales y filtros |
| Análisis de Productos | Top 10 por ventas netas, participación, rentabilidad y detalle |
| Análisis de Clientes | Top 10, distribución territorial y por segmento, detalle comercial |
| Análisis de Vendedores | Ventas, utilidad, margen y tabla de desempeño |

## Resultados auditados

Cálculo independiente sobre el Excel incluido, sin filtros: 2.961 líneas confirmadas y 39 anuladas. Las devoluciones confirmadas usan cantidades negativas; no se invierte su signo de nuevo.

| Métrica | CLP / porcentaje |
|---|---:|
| Importe de todos los estados antes de descuentos | $327.635.194 |
| Importe confirmado antes de descuentos | $322.985.909 |
| Descuentos netos sobre líneas confirmadas | $8.809.824,68 |
| Ventas netas después de descuentos | $314.176.084,32 |
| Costo de ventas confirmado | $222.758.420 |
| Utilidad bruta | $91.417.664,32 |
| Margen bruto | 29,10 % |

El informe presenta CLP sin decimales, pero las medidas conservan precisión interna. La cifra histórica de $322.985.909 y el margen de 31,03 % omitían los descuentos. La corrección sigue la definición de la hoja LEEME del dataset. No existe IVA explícito: no se afirma que las cifras incluyan o excluyan impuestos.

## Abrir el proyecto

1. Mantener juntas las carpetas `PowerBI` y `Data` de esta entrega.
2. Abrir `PowerBI/Retail_Sales_Intelligence.pbip` desde esta copia. El PBIX del respaldo es histórico y no contiene estas correcciones.
3. En este equipo, las cinco consultas ya apuntan al Excel incluido en la ubicación de entrega. Si se mueve o clona el proyecto, cambiar las rutas `File.Contents` de FactVentas, DimProducto, DimCliente, DimVendedor y DimFecha mediante Configuración del origen de datos o Power Query.
4. Actualizar el modelo y verificar los resultados sin filtros. No confiar en la caché anterior para conciliar.
5. Seguir `VALIDACION-DESKTOP.md` y registrar la versión exacta de Desktop antes de publicar capturas o presentar el caso como terminado.

No sobrescribir el proyecto original abierto con esta copia. Las modificaciones se realizaron en archivos editables; el original y el respaldo permanecen intactos.

## Modelo y metodología

Modelo estrella con FactVentas al grano de línea de venta y dimensiones Producto, Cliente, Vendedor y Fecha. Las cuatro relaciones comerciales existentes se conservan. Se mantienen las tablas automáticas de fecha y las variaciones utilizadas por el proyecto para evitar romper referencias. Cultura `es-CL`, moneda CLP.

Ventas netas = suma de Cantidad × PrecioUnitarioCLP × (1 − DescuentoPct), solo Estado Confirmada. Costo = Cantidad × costo unitario de producto en líneas confirmadas. Utilidad = ventas netas − costo; margen = utilidad / ventas netas. Los rankings usan RANKX, ALLSELECTED, orden descendente y empates densos. Las participaciones conservan REMOVEFILTERS sobre toda la dimensión: representan participación contra el total de esa dimensión, manteniendo filtros de las otras tablas.

## Calidad y límites

No hay claves duplicadas ni huérfanas en las dimensiones comerciales; las fechas de venta tienen correspondencia en DimFecha. Hay 77 devoluciones confirmadas, todas con cantidad negativa. Existen 1.135 líneas con fecha de venta anterior al alta del cliente; se documentan y no se alteran los datos sintéticos para ocultarlas. Los nombres de producto, cliente y vendedor son únicos en este dataset; si se repiten en datos futuros, conviene revisar agrupación y rankings por identificador.

Los cálculos se reprodujeron fuera del motor DAX. La compilación DAX/TMDL, los filtros interactivos y el renderizado no están verificados en Desktop. El esquema de visuales 2.14.0 y el de configuración local del modelo 1.2.0 no estuvieron disponibles en el repositorio oficial; no se rebajaron versiones. No hay capturas finales verificadas.

## Estructura

- `PowerBI/`: proyecto editable, recursos y caché original sin manipular.
- `Data/`: Excel sintético original, preservado byte a byte.
- `CHANGELOG.md`: cambios y justificaciones.
- `DOCUMENTACION-TECNICA.md`: modelo, medidas y riesgos.
- `VALIDACION-DESKTOP.md`: pruebas de aceptación pendientes.
- `auditoria-metricas.json`, `Dim*-ranking.csv`: conciliación y rankings independientes.
- `validacion.json`: resultados y archivos modificados.
- `COMERCIALIZACION.md`: propuesta de servicios y uso del caso.

## Competencias demostradas

Modelado dimensional, Power Query, DAX, conciliación de indicadores, rankings y análisis comercial. La separación de definiciones PBIP/PBIR permite revisar cambios con Git. Los límites de validación se documentan de forma explícita.

## Uso y publicación

Todos los registros son ficticios y este proyecto no debe usarse para decisiones reales. Antes de publicar el repositorio, revisar la información local y las rutas de Power Query; `.gitignore` excluye cachés, configuraciones locales y PBIX. Publicar capturas de las cuatro páginas solo después de completar la validación en Desktop. No se publicó en Power BI Service ni en GitHub durante esta revisión.

## Referencias técnicas

- [Proyectos Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-overview)
- [Formato de informe PBIR](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-report)
- [Esquemas oficiales Microsoft](https://github.com/microsoft/json-schemas/tree/main/fabric/item/report)
