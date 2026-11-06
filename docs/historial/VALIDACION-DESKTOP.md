> **Revisión v2:** el usuario reportó un error de apertura TMDL en v1. Se corrigió la serialización de Ventas Netas Corregidas; ver CORRECCION-v2.md. Esta revisión aún no tiene apertura exitosa confirmada en Desktop.

# Pruebas pendientes en Power BI Desktop

Estado inicial: TODAS las pruebas siguientes están pendientes. Registrar versión exacta, fecha, resultado y evidencia. La versión objetivo es octubre de 2026; no se ha probado en ella.

1. Abrir el PBIP de esta entrega sin errores de TMDL o PBIR. Si Desktop identifica una propiedad incompatible, registrar archivo y mensaje antes de editar. No abrir el PBIX histórico como prueba de esta entrega.
2. Verificar que las cinco consultas Excel apuntan al archivo incluido. Actualizar y comprobar 3.000 líneas, 30 productos, 100 clientes, cinco vendedores y 365 fechas. Revisar errores de tipo y privacidad del origen.
3. En vista Modelo, comprobar relaciones comerciales activas muchos a uno, dirección simple dimensión → hechos y claves únicas. Confirmar calendario y orden enero–diciembre.
4. Sin filtros, conciliar tarjetas: ventas netas $314.176.084, utilidad $91.417.664 y margen 29,10 %. Costo exacto $222.758.420; precisión no redondeada en auditoria-metricas.json. Confirmar unidades netas contra Excel.
5. Confirmar que las tarjetas muestran el total anual y cambian correctamente al seleccionar meses. Comparar la suma de meses con el año completo; no aceptar solo el último mes.
6. Abrir las cuatro páginas a Ajustar a página y al 100 %. Comprobar títulos completos, encabezados, ancho de columnas, filas, decimales, totales y barras de desplazamiento. Revisar especialmente tabla de vendedores y tabla de productos. Ajustar anchos en Desktop si hace falta.
7. Comparar Top 10 productos y clientes con los CSV sin filtros. Comprobar vendedor líder y orden descendente de tabla. Probar filtros por mes, categoría, canal y vendedor según los slicers existentes. Bajo filtros, recalcular comparación usando el mismo contexto, no el CSV anual.
8. Probar participaciones y explicar su denominador: quitar filtros de toda la dimensión; conservar tiempo y otras dimensiones. Probar selección múltiple, contexto vacío, devolución y anulación.
9. Verificar filtros cruzados entre gráficos y tablas, botón Atrás y navegación por las cuatro pestañas. Revisar posibles selecciones persistentes provenientes de configuración local.
10. Guardar como una nueva copia PBIP desde Desktop, cerrar, volver a abrir y repetir la conciliación principal. Confirmar que el proyecto sigue abriendo sin errores.
11. Registrar versión, resultados y capturas de las cuatro páginas. Actualizar README con evidencia y estado aprobado solo si todas las pruebas pasan. Exportar PDF si se desea para el portafolio.

No se ha publicado ni sobrescrito contenido en Power BI Service. La publicación y acceso de una demo pública deben decidirse por separado.
