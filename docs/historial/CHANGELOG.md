> **Revisión v2:** el usuario reportó un error de apertura TMDL en v1. Se corrigió la serialización de Ventas Netas Corregidas; ver CORRECCION-v2.md. Esta revisión aún no tiene apertura exitosa confirmada en Desktop.

# Registro de cambios

2026-11-06. Cambios aplicados exclusivamente a una copia.

- DAX: ventas netas aplica descuentos según LEEME; Ventas Netas usa la medida canónica; promedio por línea usa mismo universo confirmado. Formatos CLP enteros y porcentajes de dos decimales.
- Power Query: cinco rutas Excel apuntan al dataset incluido en esta entrega. Cambiar rutas al clonar el repositorio.
- Cuatro páginas: títulos con tildes, tipografía consistente, encabezados 28 pt y subtítulos 14 pt; tablas 11 pt y encabezados con ajuste de línea. Se conserva tema Frontier y todos los identificadores.
- Resumen: cuatro KPI con tendencia mensual sustituidos por tarjetas para mostrar el total del período seleccionado, no el último mes. Requiere comprobar representación en Desktop.
- Top 10 productos: se reemplaza orden por conteo de nombre por Ventas Netas Corregidas descendente; Top 10 clientes ya usaba ventas.
- Vendedores: valores 30 → 11 pt, título 25 → 14 pt; orden descendente por ventas.
- Slicer del resumen ajustado dentro de los 1920 px; se conservan filtros e interacciones existentes.

No se editó el PBIX ni el Excel; no se eliminaron páginas, tablas, medidas, relaciones ni recursos. La caché ABF se conserva sin manipular; refrescar en Desktop antes de conciliar.
