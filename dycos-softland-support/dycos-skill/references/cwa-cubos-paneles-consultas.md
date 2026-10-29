# Softland Logic — Paneles, Cubos, Generador de Movimientos y Consultas Integradas

> **Cuándo leer este archivo:** cuando el ticket involucra Paneles del sistema de gestión, Cubos (análisis multidimensional sobre un reporte), el Generador de Movimientos (altas automáticas de Compras/Facturación/Producción a partir de un reporte), Consultas Integradas (buscador asociado a un campo de una registración), o la relación directa entre un reporte y una registración (volcado de datos).
>
> Fuente: Manual de Reportes II - Softland Logic (SAC, v1.0).

---

## Paneles

**Objetivo:** que "la información busque al usuario" en vez de que el usuario tenga que ir a buscarla, ejecutando reporte por reporte. Permite ver en una única pantalla varios paneles de información, vinculados o no entre sí.

- Se define un objeto **Administrador de Paneles** (ícono propio en el menú o en favoritos).
- A diferencia de un objeto tradicional, se puede marcar que se abra automáticamente al arrancar el sistema (solo un panel auto-ejecutable por usuario/empresa).
- La hoja de definición se divide en secciones vía drag&drop de opciones de reporte (Etapa I) desde el árbol de menú hacia la hoja en blanco.
- Cada sección admite un **timer de re-ejecución** (minutos, horas, días).
- Puede haber **nexo entre paneles**: al seleccionar un valor en un panel (ej. cliente), los otros paneles reaccionan mostrando información relacionada (deuda en cuenta corriente, remitos pendientes, valores en cartera, etc.).
- El contenido de los paneles se define para todos los usuarios; el espacio/tamaño de cada panel es personalizable por usuario.

**Al abrir un objeto tipo Panel**, el sistema muestra en el costado derecho todo el menú pero solo son arrastrables los objetos de tipo reporte. Dentro de cada panel, las opciones normales de un reporte (drill down, filtros, copiar/exportar) siguen disponibles.

---

## Cubos

### Conceptos generales

Un **Cubo** es una representación de un conjunto de datos con:
- Separación entre **Dimensiones** (personas, cosas, categorías o tiempo — ej. producto, cliente, año, mes; sirven para filtrar por valor único o por rango) y **Métricas** (magnitudes asociadas — cantidad, importe, valor unitario, costo, impuesto).
- Permite filtrar, ordenar, ranquear y pivotear información, "cortando" datos por distintos ejes.

### Cubos en Softland Logic

- Un cubo **siempre parte de un reporte**, que determina las dimensiones, las métricas y cómo se calculan.
- El reporte de origen debe tener **un único grupo de datos** (no admite reportes con múltiples grupos).
- Todos los campos del reporte que participan del cubo deben estar **visibles** y tener el **tipo de dato establecido explícitamente** (si queda en Default, para campos calculados no se puede inferir y se recupera como Variant).
- Selección automática dimensión/métrica: campos de tipo "punto flotante" (double/float) → **métrica**; el resto → **dimensión**.
- Los campos de tipo **fecha se expanden en 9 dimensiones**: año, semestre, cuatrimestre, trimestre, bimestre, mes, quincena, semana y día.
- Los datos generados se guardan en tablas asociadas al cubo, identificadas por un **Número de Lote** (una corrida = un lote; puede haber múltiples lotes por reporte; reprocesar un lote existente reemplaza sus datos).

### Generación de cubos

**Interactiva:** en la solapa "Formato e Impresión" del reporte generador, elegir el Formato **"Exportación a Tabla para Cubo"**. En "Exportar a Indicador" definir el **Número de lote** (propone el siguiente al último usado) y, si la estructura de datos no coincide con la del reporte, tildar **"Permitir rehacer la tabla en caso de incompatibilidad de su estructura"** (esto borra los datos existentes de la tabla del cubo).

Si el reporte generador cambia de definición (se agregan/modifican campos), la tabla del cubo debe regenerarse y se pierden los datos guardados. Recomendación: hacer "Guardar Como" del reporte, generar un cubo nuevo, migrar los datos del cubo viejo por Query SQL si hace falta, y luego eliminar el cubo desactualizado.

**Automática vía Administrador de Tareas** (VBScript, ObjectType=5 para reportes, OutputPrinter=5 para exportación a cubo):

```vbscript
Const CompanyName = "EMPRESA"
Const ReportName = "STR_MVK_PRO"
Const ObjectType = 5
Const OutputPrinter = 5
Dim oReport, oRenderer
Set oReport = oApplication.Companies(CompanyName).GetObject(ReportName, ObjectType, "")
Set oRenderer = oReport.GetRenderer(OutputPrinter)
oRenderer.BatchID = 1                    ' Número de lote
oRenderer.AllowRebuildTable = True        ' Permite rehacer tabla (pierde datos existentes)
oRenderer.Render
```

La tarea corre en el contexto de seguridad del usuario configurado en el servicio de ejecución de tareas del Panel de Control.

### Consulta y manipulación de un cubo

- Al abrir se pide el **Número de Lote** y la **Vista** (vistas de usuario / vistas comunes / ninguna), y opcionalmente **parámetros de apertura** (filtrado inicial, análogo a parámetros de reporte).
- **Planilla (grilla) dinámica** — pivot table con 5 áreas:
  - **Página:** dimensión que no genera subtotales/totales (se "ignora" para el corte).
  - **Fila / Columna:** generan detalle, subtotales y totales, en el eje Y / X respectivamente.
  - **Datos:** métricas, en la intersección de filas y columnas.
  - **Ocultos:** dimensión que se comporta como Página pero sin mostrarse en la interfaz.
- **Pívot de dimensiones:** mover dimensiones entre áreas (o su orden dentro de un área) vía el "Administrador de Dimensiones y Métricas" o drag&drop directo sobre la planilla.
- **Propiedades de dimensión:** modo de visualización — Claves / Claves+Descripciones / Descripciones / Descripciones+Claves (no aplica a campos fecha ni calculados).
- **Propiedades de métrica:** función sumaria (para lectura SQL), factor desmultiplicador (miles/millones/etc.) y decimales.
- **Ranking y agrupamiento:** desde Propiedades de la Planilla se puede rankear una dimensión en función de una métrica, y definir criterios de agrupación/totales por métrica al colapsar valores.

### Gráfico de negocios

Muestra la misma información que la planilla en formato gráfico (barras, tortas, líneas, 2D o 3D). Limitación: máximo **3 dimensiones** (una se usa para las magnitudes/métricas). Si hay varias métricas, una de las 2 dimensiones restantes se ocupa con la serie de métricas, quedando solo 1 dimensión disponible para graficar; con una sola métrica se pueden graficar 2 dimensiones. El sistema envía automáticamente las dimensiones "sobrantes" a Página.

### Filtros, Drill Down y Vistas

- **Filtro modo rápido:** una solapa por dimensión filtrable, tildando valores u ordenando por texto tipeado. Ícono de embudo indica dimensión filtrada. Los filtros se pueden guardar con nombre por vista.
- **Filtro avanzado:** permite rangos fuera de los valores posibles, valores relativos de fecha (Hoy, mañana, mes pasado, próxima quincena...), condiciones complejas con grupos/paréntesis/operadores lógicos, filtrar sobre métricas, y usar partes del filtro como parámetro de apertura. Los filtros pueden activarse/desactivarse sin borrar su definición (menú Navegación → Filtros Activos).
- **Drill Down:** doble click sobre una celda de datos filtra por esa combinación y agrega una nueva dimensión de análisis (reversible con "Nivel Anterior"). No funciona sobre totales. El **orden de drill down** es configurable ("Cambiar Orden de Drill Down"); puede haber dependencias entre dimensiones (ej. no se puede seleccionar Producto sin antes seleccionar Tipo de producto).
- **Vistas:** guardan personalización de planilla/gráfico/filtros/drill down aplicado (no los datos ni la posición de celda/nivel de apertura). Se guardan por usuario o en el área común "Modelos Predefinidos"; un administrador puede guardar vistas de cualquier usuario. Check "Establecer como Predeterminada" para que se aplique al abrir el cubo.
- **Enviar cubo por mail:** requiere cliente de mail compatible con HTML + ActiveX embebido en ambos extremos (remitente y destinatario), y permisos de seguridad para instalar el componente ActiveX la primera vez.
- **Borrar:** al eliminar un cubo se borran todas sus vistas y todos los lotes de datos procesados — no se puede recuperar.

---

## Generador de Movimientos

**Objetivo:** generar movimientos (altas) en forma automática partiendo de un reporte armado por el usuario, aplicable a registraciones de **Compras, Facturación y Producción**.

- Se definen **circuitos** que aplican sobre sí mismos (ej. orden de compra) o circuitos que aplican sobre otro comprobante (ej. factura sobre nota de venta, parte de producción). Depende del/los Upgrade instalados en el cliente.
- Se da de alta el **Tipo de movimiento** (código + descripción) y se asocian los circuitos y los reportes a utilizar.
- **Ejecución (Wizard):** código de Tipo de movimiento → parámetros (ej. fecha de registración) → ejecución del reporte (con sus propios parámetros si los pide) → grilla de resultados donde el usuario selecciona los ítems a procesar → "Terminar" dispara el proceso según los circuitos del tipo seleccionado → al finalizar, opción de imprimir los formularios generados.

### Campos requeridos en el reporte según tipo de circuito

**Circuitos que aplican sobre sí mismos** — el reporte debe incluir: `TIPORI`, `ARTORI`, `CANTID`, `FCHENT`, `MODULO`, `NROCTA`, `FORMUL`, `DEPOSI`, `SECTOR`, `MODINI`, `CODINI`, `NROINI`, `NIVINI`, `EXPINI`.

**Circuitos que aplican sobre otro circuito** — requieren **2 reportes** (uno de grupo, uno de detalle):
- Reporte de **grupo**: `MODULO`, `NROCTA`.
- Reporte de **detalle**: `MODAPL`, `CODAPL`, `NROAPL`, `ITMAPL`, `TIPORI`, `ARTORI`, `CANTID`, `DEPOSI`, `SECTOR`, `MODULO`.

La aplicación genera siempre un **histórico de errores**.

### Upgrades habilitantes

| Código | Habilita |
|---|---|
| GMFC | Circuitos de facturación |
| GMCO | Circuitos de Compras |
| GMPD | Circuitos de producción |
| GMNN | Circuitos de Facturación, Compras y producción |

---

## Consultas Integradas

**Objetivo:** usar un reporte como buscador dentro de una registración del sistema, con posibilidad de volcar los valores encontrados a los campos de la registración.

**Implementación** (herramienta "Diccionario de datos", `DE32.exe`, menú Herramientas → Consultas):

1. **Tipo de objeto:** `Tabla` (objeto estándar, ej. `VTRRCH` Registración de cobranzas) o `Alias de tabla` (objeto de usuario, prefijo `USR_`).
2. **Objeto:** opción de menú del sistema donde se va a visualizar la consulta (depende del Tipo de objeto elegido).
3. **Tabla:** tabla del objeto donde se va a mostrar la consulta y permitir el volcado de datos.
4. Alta/edición de la relación ("Relaciones a Reportes" → Nuevo/Editar/Eliminar):
   - **Descripción de la relación:** nombre visible en el menú "Consultas" de la registración.
   - **Objeto destino:** el reporte que se asocia (actúa como buscador).
   - **Campos de la relación:** en qué campo(s) de la registración se habilita la consulta — "parte desde cualquier campo" o solo desde un campo específico elegido.
   - Solapa **Parámetros:** mapeo `Campo/Parámetro origen` (campo de la registración) → `Parámetro destino` (parámetro del reporte que hereda ese valor).
   - Solapa **Opciones:** tipo de apertura — `Formateado` (solo visualización) o `Buscar Valores` (permite volcar valores a la registración); check `Permitir selección múltiple` para solapas de ítems (volcar varios registros a la vez).
   - Solapa **Retorno de datos:** mapeo `Campo destino` (campo de la registración) ← `Toma valor de` (campo del reporte).

**Uso:** posicionarse en el campo de la registración habilitado y abrir el menú "Consultas" — muestra todas las consultas implementadas para ese campo/cursor.

---

## Relación entre reportes y registraciones (alta directa desde un reporte)

**Objetivo:** generar una registración completa a partir de la ejecución de un reporte (no solo buscar y volcar un valor puntual, como en Consultas Integradas).

- Registraciones soportadas: Compras, Facturación, Inventario, Cobranzas, Pagos, Tesorería, Movimientos de Ventas y Movimientos de Proveedores.
- La carga de campos es **por coincidencia de nombre**: si el nombre del campo recuperado por el reporte coincide con el nombre del campo de la registración (incluyendo campos de usuario `USR_`), se asigna automáticamente. Deben incluirse al menos los campos primarios que identifican la registración a relacionar.

**Particularidades por tipo de registración:**
- **Inventario:** carga automática de encabezado y detalle de ítems, sin restricciones de valores.
- **Cobranzas y Pagos:** equivalente a carga manual (ej. en pagos no se recalculan retenciones); requiere recuperar en el reporte la clave del movimiento a aplicar o el comprobante de anticipo a generar.
- **Tesorería:** asigna campos de encabezado; si el comprobante define recuperación de conceptos, asigna valores del reporte a ese concepto; si no, agrega el concepto a la solapa de ítems según la columna debe/haber del reporte.
- **Movimientos de Ventas y Proveedores:** recupera encabezado + detalle de ítems; igual lógica de conceptos por comprobante que Tesorería.
- **Facturación y Compras:** asigna encabezado + solapa de ítems. En **circuitos directos** la asignación es automática. En **circuitos que aplican sobre otro comprobante**, se necesitan los campos `CO/FCRMVI_MODAPL`, `CO/FCRMVI_CODAPL`, `CO/FCRMVI_NROAPL`, `CO/FCRMVI_ITMAPL` y `CO/FCRMVI_EMPAPL` (este último en modelo multisociedad) en el reporte, para asignar en función del comprobante que se aplica.
