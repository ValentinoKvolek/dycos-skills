# CWA — Interfaces de Entrada, Salida, Importación y Exportación

> **Cuándo leer este archivo:** cuando el ticket involucra importación o exportación de datos, interfaces de entrada desde archivos de texto o SQL, interfaces de salida, o transferencia de reportes/tablas/diccionario entre ambientes

---

## [InterfacesDeEntrada.htm]

## Intefases de Entrada 
## Objetivo Posibilidad de
importar a las bases del Sistema de Gestión, desde Archivos de texto o bases de
datos SQL, cualquier tipo de dato o transacción. 
## Alcance
Funcional El módulo de Interfases,
estará dividido en dos tipos de componentes. Normalización
de tablas A partir de una
definición de parte del cliente/usuario/consultor, el sistema incorporará
archivos en cualquier formato a unas tablas normalizadas. Registraciones A partir de las
tablas normalizadas, el sistema brindará la posibilidad de incorporar en forma
automática, dicho contenido de tablas al sistema de Gestión, instanciando a los
programas estándares del propio sistema como ser: Facturación, Maestro de
clientes, Maestro de productos, Datos impositivos, regionales, Etc. 
## Ficha
Técnica La
parametrización consta básicamente de 3 tablas (a/b/m) y un Proceso. · Transacciones Externas · Composición de transacciones · Objetos · Definición de parámetros de interfaces 
## Transacciones
externas Código: De la transacción Descripción: De la transacción Graba a
tablas normalizadas: La transacción importará los
datos a tablas generadas por cliente/usuario/consultor, en caso de no estar seleccionado este ítem,
los datos se procesaran a través de la aplicación asociada al objeto
(posteriormente definido (Código Objeto)) y se grabarán en las tablas del
sistema. Permite
actualizaciones: En caso de existencia del
movimiento en las bases destino, permitir actualizarlas con los nuevos datos importados. Código
Objeto: Objeto a utilizar por la transacción (Ver
a/b/m de objetos) Wizard: En caso de no utilizar Tablas Normalizadas, sino que los datos se
incorporarán al Sistema de Gestión a través de una aplicación estándar, se debe
definir cual es el Wizard a utilizar si así lo requiere la aplicación. Ubicación: Se indica donde se encuentra el archivo a importar. Nombre: Del archivo a importar. Tipo: Fijo : Si el archivo viene sin separadores y los datos se encuentran
siempre en la misma posición Variable : Si el archivo viene con separadores, en este caso, se debe definir
cual es el separador Tipo de
registro: Aquí se identifica el dato (dentro de
cada línea del archivo) en donde se encuentra que clase de registro se esta
procesando (Posición desde y Longitud); este dato es de utilidad al momento de
definir la composición de la transacción, ya que forma parte de la clave
identificatoria de la misma (ver A/b/m de composiciones). Cada línea del archivo la denominaremos de ahora en adelante como Registro Archivos de
log: Ubicación: Donde se grabarán los archivos de log Log de
errores: Nombre del log de errores Log de
transacciones: Nombre de log de transacciones En caso de no
definir los nombres, los mismos tomarán los nombres de: Log de errores:
<Nombre de la transacción>_Err.log Log de
transacciones: <Nombre de la transacción>_Tra.log Tiempos de
log: Totales: Se grabará en el log de transacciones el tiempo total de la
transacción. Parciales: Se grabará en el log de transacciones los tiempos de cada
movimiento registrado. Ambos: Se grabará en el log de transacciones tanto los tiempos de cada
movimiento registrado como también el tiempo total de la transacción. Graba en
tablas del sistema: En caso de querer grabar los
Logs en una tabla de logs del sistema. Vbscript: Aquí nos encontramos con 2 funciones: Function On_Initialization_Transaction (sErrorMessage) Function On_Finish_Transaction (sErrorMessage) On_Initialization_Transaction Todo código
escrito aquí, se ejecutará justo antes de iniciar la transacción On_Finish_Transaction Todo código
escrito aquí, se ejecutará justo después de finalizar la transacción El parámetro
sErrorMessage se debe utilizar en caso de detectar algún error (a través del código
VBscript); si dicho parámetro posee algún valor, se cortará la transacción
mostrándose el valor de dicho parámetro. 
## Composición
de transacciones 
## Composición de transacciones
(Encabezado) Código: Aquí se debe indicar alguna transacción existente (ya dada de alta
en el A/b/m de transacciones) Tipo de
transacción: El valor ingresado acá, se validará de
la siguiente manera (recordar que tanto este campo como el de Código son la
clave de la composición) : Con el código
de transacción ingresado, se irá a buscar la posición desde y la
Longitud definida para el tipo de
registro de la transacción, una vez obtenidos estos datos se buscará en el
archivo a importar la existencia del registro ingresado (la ubicación y el
nombre del mismo fueron definidos en la transacción), en caso de existir, se
permitirá continuar con la parametrización de la composición. Corte de
transacción: Este check es para indicar que este
registro se utiliza como corte, es decir, una vez identificado este tipo de
registro, se procede a grabar en las tablas del sistema todo lo anteriormente
procesado. (a este conjunto de datos a grabar lo identificaremos de ahora en
adelante como movimiento) VBScript: Aquí nos encontramos con 2 Funciones: Function On_Initialization_Record_<Tipo de Registro>(sErrorMessage) Function On_Finish_Record_<Tipo de Registro> (sErrorMessage) Se ejecutará
antes de procesar el registro, en caso de la variable sErrorMessage poseer
algún valor, no se procesará el registro y se continuará con el siguiente. Se ejecutará
después de procesar el registro. Objeto: Lo indicado en este recuadro es a modo informativo, son datos
recuperados de la transacción Factor
Multilineal: Nos facilita el tratamiento de aquellos
registros en los cuales vienen varios ítems por bloques, uno al lado de otro,
en lugar de venir uno abajo de otro. Digamos que vienen pequeños registros
dentro de un gran registro. Aplica : Define si se
aplica el factor multilineal Posición y
Longitud : La posición en la cual está informada la cantidad de bloques que
vienen en forma horizontal. Cantidad fija : Si no viene
informada en el archivo, la cantidad de bloques en forma horizontal Longitud del bloque : La
longitud total del bloque que se repite horizontalmente 
## Composición de transacciones
(Ítems) A nivel de
ítem, encontramos 4 solapas: · Campos · Ítems · Pasos de Wizard · Campos calculados 
## Campos Aquí se
desplegarán todos los campos del objeto definido en el A/b/m de transacciones Se definen los
siguientes datos: Campo-Tabla Base : Nombre
del campo Descripción : Del campo Nombre : Nombre que le
quiere dar el Usuario al Campo Posición : Del campo en el
registro Longitud : Del campo en el
registro Cantidad de decimales : En
caso de ser numérico, la cantidad de decimales del campo Valor tentativo : Al
complementar los datos anteriores, en este campo aparecerá un valor extraído
del archivo a modo de ayuda (respetando lo definido anteriormente). Valor fijo : En caso de no
querer obtener datos del archivo, sino que siempre se desea que este campo
tenga el mismo valor. Orden de lectura : El orden
en que se desea que se procesen los datos. Compone bloque multilineal :
Se indica si el campo es parte del bloque multilineal (en caso del registro ser
de este tipo) .Recordar Factor Multilineal definido a nivel de Header. Ejecuta VBScript : Al
seleccionar este ítem, se le indica que dicho campo posee código VBScript
asociado. VBScript : Aquí aparecerá
una función llamada: Function
<Nombre del Campo>_On_Change_<Tipo de registro>(sErrorMessage) El código que
se escriba en esta función se ejecutará luego de procesar el campo. En caso que se
le asigne algún valor al sErrorMessage, dará un error, el registro no será
procesado y se continuará con el siguiente. Corte de transacción : En
caso que el tipo de registro no defina Corte de Transacción, se puede utilizar
un campo para que cumpla esa función, es decir, al cambiar el valor del campo
(de un registro a otro) se tomara como que hasta ahí es un movimiento y se procederá
a grabar. Graba en log : Si
anteriormente en el A/b/m de transacciones se definió que los tiempos de log
que se registrarán son Parciales o Ambos, entre el tiempo de inicio y el tiempo
de fin del movimiento, aparecerá este campo. En caso de definir varios campos,
los mismos aparecerán separados por comas. Orden de escritura de log :
El orden en que aparecerán los campos en el Log No actualiza : Esta opción
permite no actualizar aquellos campos que no se deseen en caso de haber
definido en el A/b/m de transacciones que Permite actualizaciones 
## Ítems Aquí se
encuentran todas las tablas dependientes del objeto definido anteriormente. Se definen
los siguientes datos: Tabla base: Tabla
relacionada Descripción : De
la tabla Campos: Si se
abre esta opción, se verán todos los campos de la tabla base con las opciones
anteriormente mencionadas para los campos de la tabla madre (Nombre, posición,
longitud, etc..) Tabla dependiente: En caso de tener tabla relacionadas, se despliegan las mismas (así
sucesivamente hasta un 4to nivel). Agrega ítem : En
caso que el movimiento este compuesto por un Encabezado y Varios Ítems, a la
tabla que sea utilizada como ítem del movimiento, habrá que seleccionarle esta
opción. 
## Campos de Wizard Si se define en la transacción que no se trabaja con tablas
normalizadas, queda habilitado el campo Wizard, en el mismo se define el
Wizard a utilizar por la aplicación (en caso que posea). En esta solapa
se definen los siguientes datos: Paso del
Wizard: Nombre de la tabla del paso del Wizard Nombre del
campo: Nombre de la tabla Descripción: Del campo Los demás datos
son idénticos a los descriptos en anteriormente para la tabla madre. 
## Campos calculados Son campos que se crean al momento de ejecutar la transacción y los
mismos se suelen utilizar como campos para cálculos intermedios de los demás
campos ya que el valor de los mismos puede ser utilizados por otros campos de
las tablas. Su definición es igual a los campos de la tabla madre . 
## Objetos Los objetos se
definen para aquellas transacciones que no graban a tablas normalizadas, estos
objetos son la relación entre esas tablas normalizadas y las tablas del
sistema, es acá donde se relacionan los campos de ambas tablas (Normalizadas 
Sistema de Gestión). 
## Encabezado Código: De la transacción, recordar que la misma no debe tener definida que
Graba en tablas normalizadas Código: Del objeto, el mismo debe ser un objeto del Sistema de Gestión
(Como por ejemplo: VT3MVH (Registración de movimientos ventas)) Wizard: En caso que la aplicación utilice Wizard, indicar el nombre del
mismo (en el caso del VT3MVH seria VT3WIZ, como ejemplo) VBScript: Cumple la misma función que la definida anteriormente para la
composición de transacciones. De
normalización: Se encuentra dentro del recuadro de
Tabla Encabezado. En el mismo se define la tabla normalizada de donde se
obtendrán los datos para importarlos a las tablas del Sistema de Gestión. 
## Items A nivel de ítems, encontramos 4 solapas: · Encabezados
de objetos · Items · Pasos de
Wizard · Campos
calculados 
## Encabezados de
objetos Campos - Tabla base : Campos del objeto Descripción : De los campos Campos : Este largavista
trae todos aquellos campos de la tabla normalizada definida en el header. Una
vez que se selecciona, el mismo, es puesto en la columna Campos  Tabla.
Recordar que tanto el campo de la tabla normalizada como el de la tabla del
sistema deben ser del mismo tipo. El resto de las
columnas tienen el mismo concepto que los explicados anteriormente para los
ítems de la Composición de Transacciones. 
## Items Tabla base: Tabla relacionada con el objeto definido en el header Descripción: De la tabla relacionada Tablas: Este largavista trae todas las tablas del sistema. Una vez
seleccionada la tabla, la misma se coloca en la columna Tabla de
normalización. Descripción: De la tabla seleccionada en el ítem anterior. Campos: Aquí se aperturan todos los campos de la Tabla Base. Las
columnas que allí se deben definir son las mismas que en los ítems de la
composición de Transacciones con la diferencia de la columna Campos , el
cual es un largavista que trae todos aquellos campos de la tabla definida en la
columna Tabla de normalización . Recordar que deben ser del mismo tipo,
ya que los datos en el campo de la tabla normalizada serán importados al de la
tabla base. Tabla
dependiente: Se despliegan todas aquellas tablas
que dependen de la Tabla Base. 
## Pasos de Wizard La definición de
esta solapa es la misma que la definida en este documento en la parte de
Composición de Transacción con la única diferencia de 2 columnas: Tablas: Este largavista trae todas las tablas del sistema y la seleccionada
la coloca en la columna Tabla de normalización. Campos: Este largavista trae todos los campos de la tabla seleccionada en la
columna de Tabla de normalización. Cuando se corre
el proceso de importación, el valor del campo anteriormente nombrado se coloca
en el campo indicado en la columna Campos Tabla Base. 
## Campos calculados Mismo
tratamiento que el explicado en la Composición de transacciones. 
## Definición de parámetros Aquí encontramos
un solo parámetro el cual nos indica si deseamos que se visualice mientras se procesan
los datos la barra de progreso. La utilidad de no mostrar dicha barra radica en
la performance del proceso como así también, el mostrarla nos ayuda a ver cual
es el grado de avance del mismo. 
## Proceso de importación de
transacciones externas Este proceso
llevará a cabo la importación de los datos a las bases del Sistema de Gestión
según lo parametrizado anteriormente en los A/b/m. 
## Datos solicitados al proceso Código: De transacción que se utilizará para la importación de los datos.
(definido anteriormente en el A/b/m de Transacciones). Ubicación y
Nombre: Del archivo desde donde se importarán los
datos al Sistema de Gestión. Estos datos aparecerán completos en caso de
haberlos definidos en el A/b/m de transacciones, pero se le da la opción al usuario
de modificarlos. Tipo: En caso que la transacción tenga asociado algún objeto (dado de alta
en el A/b/m de objetos) se habilitará este combo en donde se le debe indicar al
proceso, si los archivos a importar vendrán desde un archivo o desde una base SQL. Una vez
terminado el ingreso de los datos solicitados, se debe presionar el botón de
terminar para que comience la importación.

---

## [InterfacesDeSalida.htm]

## Interfases de Salida 
## Objetivo Posibilidad de
exportar archivos en cualquier formato desde el Stradivarius Sistema de
Gestión. 
## 
## Alcance Funcional A partir de una definición de parte del cliente/usuario/consultor, el sistema
recuperará información, grabando internamente una tabla propia del sistema
(INRMSH/I), y luego exportando dicha información a un Archivo en formato
predeterminado. La
parametrización consta básicamente de 2 tablas (a/b/m) y un Proceso: ABM de Transacciones
de salida, ABM de Composición de transacciones de salida y Proceso de
exportación de transacciones. 
## Ficha Técnica 
## Definición de parámetros Se deberá
definir si se desea visualizar la barra de proceso durante el proceso de
exportación o no. La utilidad de mostrar dicha barra, mejora la velocidad
(performance) del proceso, como así también, nos ayuda a ver cual es el grado
de avance del mismo. 
## Transacciones de
salida 
## Objetivo Posibilidad de definir una nueva interfase de salida, especificando el
directorio y archivo de salida, que el sistema deberá proponer por defecto. 
## Alcance
funcional A continuación, se detalla el contenido de dicha aplicación, y sus tablas
(solapas) dependientes: 
## Encabezado
(INMTRS) | Campo | Descripción | Código de transacción | Código o identificación que se le va a
 dar a la transacción. | Descripción de la transacción | Descripción detallada de la misma. | Rango | Determina si se usa el Tipo de Período. | Tipo de Período | El tipo de período puede ser: Diario,
 Mensual o Anual. Se utiliza en el proceso de Exportación de Transacciones para definir el
 rango de fechas a procesar. Por ejemplo: Si se define la transacción
 del tipo Mensual, en el proceso, al completar el código, traerá de forma
 automática las fechas en el rango Mensual. | Carpeta donde se grabarán los archivos | Define la dirección en donde se generará
 el archivo. | Nombre de archivo | Define el nombre del archivo. | Tipo | Puede ser de dos tipos: Fijo : Si el
 archivo ha generar viene sin separadores y los datos se encuentran siempre en
 la misma posición. Variable :
 Si el archivo ha generar viene con separadores, en este caso, se debe definir
 cual es el separador. | Separado
 por | Si el
 campo tipo es Variable, habrá que definir el caracter de separación. | Carpeta donde se grabarán los archivos de
 Log | Define la dirección en donde se grabará
 el archivo de seguimiento (log). | Nombre
 del log de Errores | Define
 el nombre del archivo de seguimiento (log) de errores. | Nombre
 del log de Transacciones | Define
 el nombre del archivo de seguimiento (log) de
 transacciones. En caso
 de no definir los nombres, los mismos tomarán los nombres de: Log de
 errores: <Nombre de la transacción>_Err.log Log de
 transacciones: <Nombre de la transacción>_Tra.log | Tiempos
 de log | Totales: Se grabará en
 el log de transacciones el tiempo total de la transacción. Parciales: Se grabará en el log de
 transacciones los tiempos de cada movimiento registrado. Ambos: Se grabará en el log de
 transacciones tanto los tiempos de cada movimiento registrado como también el
 tiempo total de la transacción. | VBScript | Aquí nos encontramos con 3 funciones: Function
 On_Initialization_Transaction(sErrorMessage) Function On_Finish_Transaction(sErrorMessage) Function
 On_Finish_Insert(sErrorMessage) On_Initialization_Transaction Dicho código, se ejecutará justo antes de
 iniciar la transacción. On_Finish_Transaction Dicho código, se ejecutará justo después
 de finalizar la transacción. On_Finish_Insert Dicho código, se ejecutará justo después
 de insertar los datos en las tablas INRMSH, INRMSI. El parámetro sErrorMessage se debe
 utilizar en caso de detectar algún error (a través del código VBscript); si
 dicho parámetro posee algún valor, se cortará la transacción mostrándose el
 valor de dicho parámetro. 
## Orden de Campos (INMTRI) | Campo | Descripción | Número de Campo | Tomará el
 ordenamiento de todas las composiciones definidas para esta transacción. | Nombre de Campo | Muestra la
 descripción del número de campo 
## Composición de
transacciones de salida 
## Objetivo En función del código de transacción, definido en la tabla (ABM) anterior,
se deberá de especificar un código de Tipo de Registro, permitiendo de esta
forma, ilimitados niveles de recuperación de la información. Cada tipo de registro equivale a una sentencia tipo SQL, a efectos de
recuperación de datos. 
## Alcance
funcional A continuación, se detalla el contenido de dicha aplicación, y sus tablas
(solapas) dependientes: 
## Encabezado (INTTSH) | Campo | Descripción | Código de transacción | Código o
 identificación que se definió en la transacción. | Tipo de
 registro | Se
 identificará el tipo de registro para cada composición | Tipo de
 Proceso | Se puede
 definir dos tipos de proceso: Manual o Automático. Manual:
 Solamente se habilitara la tabla de formatos, pudiendo definir los campos y
 formatos ha utilizar en la sentencia final. Al
 elegir esta opción, la sentencia la define el usuario y no la define el
 sistema. En la
 solapa de Formatos, se cargará automáticamente el campo "Campo de Tabla
 Normalizada" con el rango 1 a 99. Automático:
 Se debe definir las tablas ha utilizar en la solapa de Tablas. Las
 tablas tienen que tener un vínculo en común de lo contrario no se armara la
 sentencia de condición en el campo de Sentencia Final. En la
 solapa de campos, se definirán los campos que se quieren utilizar, estos
 campos deben ser campos pertenecientes a tablas definidas en la solapa de
 tablas. El campo
 "Filtro de Fechas" se habilitara únicamente cuando el campo sea de
 tipo fecha, este campo se usa para la condición de Where en la sentencia
 final, al usarlo se generará un filtro con campos tipo macro que después en
 el proceso estos campos se cambiarán a valores reales. En la
 solapa de campos calculados, se debe definir los campos: tipo de dato,
 expresión, filtro de fechas (actúa de la misma forma que el de la solapa de
 campos), y el agrupa que se habilitara cuando el Tipo de Transacción sea de
 tipo Totales (al tener valor S se agregara la expresión al group by de la
 sentencia final). A medida
 que se van definiendo los campos y campos calculados, se irán generando los
 formatos correspondientes a estos campos, para poder definir el número
 correspondiente en el campo de tabla normalizada y poder generar el formato
 de una manera más ágil. | Tipo de
 Transacción | Especifica
 si la sentencia usará agrupación o no (Detalle o totales) | Generar
 sentencia | Generará
 la sentencia tipo SQL a efectos de su posterior revisión. | Filtro Sql (Where) | El
 usuario podrá agregar filtros para la condición de Where | Filtro Sql (Having) | El
 usuario podrá agregar una condición para el Having | Sentencia
 Final | Depende
 del Tipo de Proceso a utilizar. Por
 ejemplo si se utiliza: Manual:
 Se deberá definir la sentencia que se quiere ejecutar. Automático:
 La composición generara la sentencia. | VB
 Script | Se pueden escribir dos (2) tipos de Funciones: Function On_Initialization_Record_<Tipo de
 Registro>(sErrorMessage). Se
 ejecutará antes de procesar el registro, en caso de que la variable
 sErrorMessage posee algún valor, no se procesará el registro y se continuará
 con el siguiente. Function On_Finish_Record_<Tipo de Registro> (sErrorMessage) Se ejecutará después de procesar el registro. 
## Tablas (INTTST) | Campo | Descripción | Nombre | Se
 deberá definir el nombre de la tabla a utilizar. En la
 primera fila irá siempre la tabla de tipo encabezado Ej: VTRMVH. | Descripción | Descripción
 de la tabla | Seleccionar Tabla | El
 largavistas mostrará las tablas del sistema que se pueden elegir 
## Campos (INTTSE) | Campo | Descripción | Nombre de Tabla | Se deberá definir la tabla a utilizar, siendo la misma validable con
 respecto a la solapa anterior (que exista). | Descripción | Muestra la descripción de la tabla. | Campo - Tabla base | Se deberá definir el campo a utilizar. | Descripción | Muestra de descripción del campo. | Filtro de Fechas | S e habilitará
 únicamente cuando el campo sea de tipo fecha, este campo se usa para la condición
 de Where en la sentencia final, al usarlo se generará un filtro con campos
 tipo macro que después en el proceso se cambiarán a valores reales. Solamente se puede elegir un solo filtro para todos los campos definidos. | Seleccionar campos | El largavistas
 recupera los campos de las tablas que se definieron en la solapa de tablas, a
 efectos de facilitar el ingreso al usuario. 
## Campos Calculados (INTTSC) | Campo | Descripción | Código | Código de campo calculado. | Expresión | Se
 define la expresión (SQL) a utilizar. | Agrupa | Se
 habilitará cuando el Tipo de Transacción sea de tipo Totales (al tener valor
 S se agregará la expresión al group by de la sentencia final). | Tipo de dato | Se debe definir
 que tipo de dato se va a usar para ese campo calculado, las opciones son:
 Caracter, Numérico y Fecha. | Filtro de Fechas | S e habilitará
 únicamente cuando el campo sea de tipo fecha, este campo se usa para la
 condición de Where en la sentencia final, al usarlo se generará un filtro con
 campos tipo macro que después en el proceso se cambiaran a valores reales. Solamente se puede elegir un solo filtro para todos los campos que se
 definieron. 
## Formato (INTTSF) | Campo | Descripción | Campo de Tabla Normalizada | Se debe
 definir el número de campo que se desea utilizar, este número internamente se
 guardara con la notación FLD00. Ejemplo: si se define el número 1 la notación
 será FLD001 y si se define el número 23 la notación será FLD023. Cuando
 se utiliza el tipo de proceso automático, este campo habilitará el resto de
 los campos, en cambio si se usa el tipo de proceso manual, el campo que
 habilita al resto de los campos es la descripción. | Nombre de Tabla | Se
 utiliza únicamente en los procesos automáticos, cuando se definen los campos
 en la solapa de campos, cargándose el nombre de la tabla que se utilizo | Campo - Tabla base | Se
 utiliza únicamente en los procesos automáticos, y el valor que tomará será de
 los campos definidos en la solapa de campos y campos calculados. | Descripción | Cuando
 se utiliza tipo de proceso automático, se guardará la expresión o descripción
 del campo, y si se utiliza tipo de proceso manual, se definirá el nombre identificatorio
 para cada campo del formato. | Posición desde | Posición
 que se debe definir por cada campo que se graba en el archivo | Longitud | Longitud
 del campo. Si no se especifica longitud, este campo NO se incluirá en el formato. | Ejecuta VB Script | Al
 seleccionar este campo, se le indica que dicho campo posee código VBScript
 asociado | VB Script | Aquí
 aparecerá una función llamada: Function
 <Nombre del Campo>_On_Change_<Tipo de registro>(sErrorMessage) El código
 que se escriba en esta función se ejecutará luego de procesar el campo. En caso
 de que se le asigne algún valor al sErrorMessage, dará un error, el
 registro no será procesado y se continuará con el siguiente | Cantidad de decimales | Si el
 campo es numérico, se habilitará y se podrá definir la cantidad de decimales
 que posee. | Punto decimal | Si el
 campo es numérico, se puede definir si trabaja con punto decimal. | Selecciona decimal | Si el valor
 del campo Punto decimal esta en Si, entonces se debe elegir que separador
 de decimales se utilizará. Las opciones son: punto (.) o coma (,). | Completa con ceros | Si el
 campo es numérico, se puede definir si se completa con ceros | Completa a | Si el
 valor del campo Completa con ceros esta en S, entonces se deberá definir
 si se completa con ceros a la izquierda o a la derecha. | Graba en log | Se
 define si se graba en el archivo de seguimiento (Log). 
## Proceso de Exportación de
transacciones 
## Objetivo Este proceso exportará a un archivo definido por el usuario, en función de las definiciones previamente realizadas tanto en el
A/b/m de "Transacciones de Salida" como en el de "Composición de
transacciones de salida", a un archivo. 
## Alcance
funcional Dicho proceso
contará con un campo "Código", en el cual se le deberá de indicar el
código de transacción a procesar, una vez ingresado, se completarán los campos: Lote : Aquí se mostrará el número de lote que le será asignado al proceso;
el manejo de lotes se realizará a
través de la aplicación "Administración de aplicaciones por lotes o
períodos" Fecha Desde: Se propondrá la fecha en que se está corriendo el proceso. Fecha Hasta : Dependiendo de lo definido en el A/b/m de
"transacciones de Salida" con respecto al tipo de período, aquí se
podrá ver una fecha la cual se conformará con la fecha desde, más el período
definido. Ambas fechas se podrán modificar, pero se debe tener en cuenta, que
al modificar una, la otra automáticamente cambiará su valor dependiendo del
tipo de período que se esté utilizando. Ubicación : Aquí aparecerá la ubicación del Archivo que se generará, la misma
se puede modificar, pero se debe tener en cuenta, que la nueva ubicación deberá
existir. Nombre : Nombre del archivo que se generará. El mismo es modificable. Una vez
terminado el ingreso de los datos solicitados, se debe presionar el botón de
terminar para que comience la exportación.

---

## [Import_Export.htm]

## Importación y Exportación 
## Objetivo Posibilidad de transferir datos (importando o
exportando), como ser: Reportes, Tablas del Diccionario de datos, Fondos de
Página, etc. 
## Alcance
Funcional La interfase cuenta con un archivo tipo Ini, en el
cual se muestra la siguiente información: El campo UserID define el
usuario del Sistema de Gestión, se puede definir por defecto en el cwImpExp.ini
o se ingresa al abrir un Import-Export. El campo Password define la password del Sistema de Gestión, se puede
definir por defecto en el cwImpExp.ini o se ingresa al abrir un Import-Export. El campo Transferir se define con el valor M cuando se quiere ejecutar en
forma Manual, en cambio con el valor A cuando se quiere ejecutar en forma
automática (No se muestran las ventanas). El campo AllowSystemTables permite mostrar las tablas del sistema (cw) Las demás definiciones del Ini no
se modifican ya que se usan dentro de la aplicación. 
## Exportación Tipo de Proceso: Las opciones que
se contemplan son: Reportes : Se exportarán los reportes elegidos en la empresa origen. Tablas del Diccio : Se exportarán las tablas del diccionario de datos, estas
 tablas también incluyen las tablas de los procesos. Pasaje de Datos : Se exportarán los datos de las tablas definidas en la empresa
 origen. Wizard : Se exportarán los wizards donde se encuentran los pasos de
 los procesos. Fondos de Página : Se exportarán los fondos de página de los reportes. Jobs : Se exportarán los jobs elegidos en la empresa origen. Interfase de
 Entrada/Salida : Se exportarán las tablas de IN
 elegidas en la empresa origen. Tipo de Base: MDB o SQL Elegir la opción de Exportar Elegir la empresa de Origen Si el Tipo de Base es MDB: Elegir
el MDB de destino o generar uno nuevo en el caso de que no se haya generado
anteriormente. Si el Tipo de Base es SQL: Elegir
la empresa de Destino. Entrar al botón de Cuales y
elegir las transacciones que se quieren exportar o se pueden elegir todas las
transacciones con el botón de Transferir Todo. Apretar el botón de
Transferir. 
## Importación Tipo de
Proceso: Las opciones que se contemplan son: Reportes : Se exportarán los reportes elegidos en la empresa origen. Tablas del Diccio : Se exportarán las tablas del diccionario de datos, estas
 tablas también incluyen las tablas de los procesos. Pasaje de Datos : Se exportarán los datos de las tablas definidas en la empresa
 origen. Wizard : Se exportarán los wizards donde se encuentran los pasos de
 los procesos. Fondos de Página : Se exportarán los fondos de página de los reportes. Jobs : Se exportarán los jobs elegidos en la empresa origen. Interfase de
 Entrada/Salida : Se exportarán las tablas de IN
 elegidas en la empresa origen. Tipo de
Base: MDB o SQL Elegir la
opción de Importar Si el
Tipo de Base es MDB: Elegir el MDB de Origen Si el
Tipo de Base es SQL: Elegir la Empresa de Origen Elegir
la Empresa de Destino Entrar
al botón de Cuales y elegir las transacciones que se quieren importar o se
pueden elegir todas las transacciones con el botón de Transferir Todo. Apretar
el botón de Transferir. 
## Características Generales Al
ingresar a la opción de Cuales, se cuenta con la opción de Filtros en la misma
se podrán ingresar determinadas características para buscar un determinado
reporte, tabla, etc.

---

