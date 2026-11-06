# Corrección v2 — error TMDL de apertura

El intento de apertura del usuario en Power BI Desktop October 2026, versión 2.159.1231.0, falló con InvalidLineType en FactVentas, línea 98. La expresión de Ventas Netas Corregidas empezaba en la declaración y continuaba en líneas posteriores. Esa mezcla no es válida para una expresión multilínea TMDL.

Se movió CALCULATE a la línea siguiente al signo igual, con tres tabulaciones de sangría. No se cambió ningún token del cálculo, medida, dato ni identificador. También se actualizaron las cinco rutas del Excel para apuntar a la carpeta Data de la entrega v2.

Se comprobó que el cambio de la medida solo altera espacios y saltos de línea. Se revisaron las medidas de todas las tablas para detectar declaraciones con expresión en línea seguidas de una continuación multilínea: sin incidencias. Esta comprobación específica no sustituye al deserializador oficial ni valida todo TMDL.

El intento anterior queda registrado como FALLIDO, no como validación aprobada. Esta revisión v2 todavía requiere apertura, actualización y comprobación de las cuatro páginas en Desktop. Las verificaciones estáticas anteriores siguen siendo históricas de v1; el archivo validacion-v2.json registra lo comprobado en esta revisión.

Fuente: https://learn.microsoft.com/en-us/analysis-services/tmdl/tmdl-overview

Abrir PowerBI/Retail_Sales_Intelligence.pbip de esta carpeta v2. No reemplazar el original. Si se extrae el ZIP en otra ubicación, actualizar las rutas Excel antes de refrescar.
