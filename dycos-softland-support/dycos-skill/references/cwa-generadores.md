# CWA — Generadores: Reportes, Procesos, Aplicaciones y Movimientos

> **Cuándo leer este archivo:** cuando el ticket involucra el generador de reportes, generador de procesos (wizard), generador de aplicaciones, generador de movimientos, o el asistente de parametrización

---

## [GeneradordeReportes.htm]

## Generador de Reportes 
## Alcance Funcional El generador de reportes es una
herramienta desarrollada íntegramente por CWA y forma parte del sistema de
gestión, como su nombre lo indica sirve como herramienta de creación de
listados y consultas. Todos los reportes que llegan en las
versiones de CWA han sido elaborados con dicha herramienta. La creación de Reportes consta de dos
etapas: Definición del Reporte : Se definen las tablas del reporte, campos asociados, relaciones,
cortes de control, parámetros, etc. Todo lo referente a la información, como ir
a buscarla y que datos recuperar. Presentación del Reporte : Se define el formato de los campos, como ser los tipos de
letras, colores, tamaños, fondos de página, etc. Todo lo referente a la
presentación. 
## Índice Generador de Reportes . 1 Alcance Funcional 1 Índice . 1 Definición del Reporte . 2 Generación de un
Reporte nuevo (Nueva Definición) 2 General 3 Diseño . 3 Diseño  Solapa
Campos (Especificaciones) 3 Grupos del reporte . 3 Saldos Iniciales . 3 Formularios . 4 Transportes: 4 CrossTab (Para
Formularios) 5 Diseño  Solapa
Grupos (Especificaciones) 6 Diseño  Solapa
Orden (Especificaciones) 6 Diseño  Solapa SQL
(Especificaciones) 7 SENTENCIAS SQL - Sintaxis . 7 Diseño  Solapa
Campos (Suplementos) 7 Suplemento
multimoneda . 7 Objeto Info . 7 Diseño  Solapa
Campos (Eventos) 7 Eventos . 8 Inicialización de Eventos (Initialize) 8 Comienzo de Eventos (Begin) 8 Fin de Eventos . 8 Terminación de Eventos . 8 Predefinición de Parámetros . 8 Diseño  Solapa
Campos (Relaciones) 8 Propiedades de la relación (Solapa General) 8 Propiedades de la relación (Solapa
Parámetros) 8 Parámetros . 9 Parámetros Libres . 9 Preview (vista preliminar) 9 Formato o Presentación de Reporte . 11 Macros . 11 Macros predefinidas
para Presentación de Reportes . 11 Macros del archivo
de control: 11 Símbolos
reservados: 11 Macros de Variables . 11 Tratamiento de imágenes . 13 Definición de
Reporte . 13 Campo Calculado . 13 Formato del
Reporte . 13 Campo Calculado . 13 Imagen . 13 VBScript Lenguage Reference . 13 Lista de palabras reservadas por CWA . 13 Funciones más habituales de VBScript. 14 Funciones de
Cadena . 14 Null 14 Abs Function . 14 Chr Function . 14 Int, Fix Functions . 14 Replace Function . 14 Filter Function . 15 InStr Function . 15 LTrim, RTrim, and
Trim Functions . 15 UCase Function . 15 LCase Function . 15 Mid Function . 16 String Function . 16 Space Function . 16 Len Function . 16 Funciones de
Fecha . 17 Now Function . 17 Weekday Function . 17 MonthName Function . 17 Month Function . 17 Day Function . 17 Funciones
Miscelaneas . 17 Dim Statement 17 Array Function . 17 If...Then...Else
Statement 18 Null 18 True . 18 False . 18 Empty . 18 Ejemplos de Campos Calculados . 19 Campos calculados
del lado de Cliente (VBScript) 19 Función: Recupera
el día en palabras. 19 Función: Recupera
el mes en palabras. 19 Función: Calculo de
saldo acumulado. 19 Función: Recupera
texto asociado en formulario de remito. 19 Campos calculados del lado del Servidor 20 Función: Recupera
la condición de pago desde un remito. 20 Función: Recupera
el transportista desde un remito. 20 Función: Recupera
los pendientes de ventas para análisis de Stock. 20 Importación y Exportación de Reportes . 21 Alcance funcional 21 Método de utilización (Exportación de
Reportes) 21 Tablas de Reportes (Internas) 21 
## Definición del Reporte En el menú, dentro de la carpeta
Administración del Sistema, se encuentra la opción Editor de Reportes. La acción Doble Click, ejecuta la opción
Nueva definición, mientras que con el botón derecho del Mouse, posicionado en
Editor de Reportes, aparecerán las opciones de: Nueva definición Editar Definición Editar formato Nuevo fondo de Página Editar fondo de Página Propiedades 
## Generación de un Reporte nuevo (Nueva Definición) Aparecerá una ventana con el contenido de
las tablas de sistema, para que el usuario seleccione la tabla base del
reporte. Tabla Base: es la tabla de inicio del reporte o la tabla principal del
mismo. Una vez elegida, el sistema mostrará los
campos de dicha tabla y el usuario deberá seleccionar los que considere
necesarios incorporar para la ejecución del reporte. 
## General En la
solapa General, el usuario deberá asignarle el nombre físico del reporte, la
descripción (la que aparecerá en el menú), a que módulo y área pertenece, y el
tipo de Reporte (reporte o formulario). 
## Diseño En la solapa de diseño veremos la tabla
base con los respectivos campos seleccionados, a su vez veremos en la sección
de abajo, los mismos campos, con la descripción asociada y las especificaciones
particulares. 
## Diseño  Solapa Campos (Especificaciones) Orden : orden en que aparecerá dicho campo Campo : nombre físico del campo en la tabla del sistema Descripción : descripción asociada al campo que el sistema trae desde el
diccionario de datos. Server
Side : si el mismo está seleccionado, corresponde
a que dicho campo se ejecute en el Servidor, caso contrario, se ejecuta en el
cliente. Expresión : es la expresión que se definirá para los campos calculados. La
misma puede ser definida para ser ejecutada del lado del cliente (Lenguaje
VBScript) o para ser ejecutada del lado del servidor (Standard ODBC). Agrupación : de ser seleccionado, indica que el reporte trabaja con
agrupación o grupos (GROUP BY en SQL). Todos los otros campos definidos para
ser ejecutados del lado del servidor se marcarán. Visible : corresponde en caso que dicho campo se quiera ver en el reporte
o no. Por defecto queda marcado en Sí. Parámetro : de ser seleccionado, aparecerá en la solapa de parámetros para
que se defina el tipo de parámetro a utilizar para dicho campo (rango,
requerido, valores). Tipo
de Dato : Opciones Õ Doble precisión, Caracter, Entero, etc. Se utiliza casi siempre
en los campos calculados, ya que el diccionario de datos no tiene información
sobre el mismo. Tamaño : define la cantidad de dígitos o caracteres. Decimales : define la cantidad de dígitos decimales. Saldo
Inicial : corresponde seleccionar en caso que se
pretenda calcular el saldo inicial (para un campo numérico) a una fecha. Separador
de Miles : corresponde seleccionar en caso que se
pretenda separar un campo tipo número con el caracter definido en el panel de
control para separador de miles. Ej: para el número 1200000.00, al seleccionar quedaría como 1,200,000.00 NOTA : El botón derecho del mouse
habilita la creación de alta o baja de campos calculados. Grupos del reporte Cuando el usuario define relaciones de tablas,
sobre la cual la información no podrá extraerse de una sola vez, el sistema
arma automáticamente grupos del reporte. Ejemplo: | Tabla Base: | Encabezado de movimientos de Venta
 (Cliente, Fecha emisión, Textos asociados, etc.) | Tabla relacionada I: | Items de movimientos de Venta (Producto,
 concepto, imputación Contable, Importe) | Tabla relacionada II: | Cuentas Corrientes de Venta (Cuota,
 Vencimiento, Importe) En el ejemplo, el sistema abrirá tres (3)
grupos, lo cual al momento de formatear o presentar el reporte, aparecerán tres
secciones con sus encabezados y pies. De esta forma, podremos presentar en un
solo reporte, la composición completa de una transacción, incluyendo relaciones
que de otra forma no podrían ser visualizadas en una sola vista. Saldos Iniciales Para poder utilizar saldos iniciales, el
sistema debe detectar que en diseño existe un campo tipo Fecha, que esté
definido como parámetro y del tipo Rango. En función de la combinación de los
estados anteriores, se habilitará en diseño las columna de Saldo Inicial. Valores
Posibles | Ninguno: | No tiene efecto en el Saldo Inicial | Fecha límite: | Debe ser un campo tipo fecha, el sistema
 tomará el desde, y calculará el saldo inicial a esta fecha para aquellos
 campos definidos como Calcular. | Calcular: | Son los campos en los que se calculará el
 saldo inicial a la fecha Desde Texto
Asociado La siguiente expresión sirve para incluir
el texto de Saldo Inicial o Saldo al Inicio, en aquellos reportes que utilicen
las funciones de Saldos Iniciales IF
CURRENTRECORD.INITIALBALANCE THEN RESULT = "SALDO INICIAL" ELSE RESULT = "" END IF NOTA: En éste campo calculado deberá seleccionarse
en la columna de Saldos Iniciales con la opción Calcular. Formularios Pasos a seguir para la creación de un
formulario: Definir en la sección General de
diseño, que el tipo de Reporte es FORMULARIO. Definir más de un grupo. Con dichos elementos, el sistema tratará
al reporte, como un formulario. Cada grupo puede tener definido área de
totales, y en el formato, se abrirá una sección de encabezado y pie. El sistema, automáticamente, no mostrará
la sección final de parámetros del reporte. El botón izquierdo sobre las secciones,
opción Propiedades: Altura máxima de la sección, tendrá efecto para la
definición de la cantidad máxima de filas por formulario. Ejemplo: Detalle de ítems, si defino que la altura
de la sección es de cinco (5), al definir que la Altura máxima de la sección es
de cuarenta (40), le estaría indicando al sistema que si imprime más de ocho
(8) filas (=40/5), salte automáticamente a otra página. El sistema en este caso
repetiría todas las secciones anteriores a la misma, y empezaría a imprimir
desde el ítem 41. Transportes: Para definir un transporte, hay que
definir un campo calculado cuyo resultado sea el total acumulado a ese
instante. Ejemplo: Si el total que el sistema deberá
imprimir es para el campo VTRMVC_IMPNAC (importe en moneda nacional de la
cuenta corriente), debo definir un campo calculado cuya expresión es: RESULT =
CURRENTRECORD(VTRMVC_IMPNAC).ACUM, este campo luego en el formato, se debería
de arrastrar hasta la sección transporte de la cuenta corriente (para el
Encabezado y/o Pie). NOTA I: No arrastrar el contenido de Detalle al
Encabezado para la primer sección, ya que sino el formulario saldrá bien para
la primer página y mal para el resto. NOTA
II: La opción de Preview o Vista previa del
formulario, únicamente muestra el contenido de la sección inicial o base. Para
verlo en forma completa, deberá de hacerlo recién en el formato o presentación. NOTA
III: En los grupos distintos del inicial (en
nuestro ejemplo: Items de movimientos de Venta y Cuentas Corrientes de Venta),
no se pueden definir campos calculados con SUBQUERYS, del lado del servidor, lo
que representa tener que escribirlas del lado del cliente, ya que el Driver
de ODBC no es capaz de administrar dicho pedido. Recomendamos en este caso, generar un
nuevo reporte con este grupo (probablemente sea una sola tabla), para poder
trabajarlo ON-LINE, ver el resultado de VBScript, y una vez finalizado, pasar
al reporte principal. CrossTab (Para Formularios) Para definir que una sección de ítems se
imprima toda en la misma fila, se utiliza la opción de CrossTab. Para poder realizarlo se deberá de marcar
la opción de CrossTab en el costado inferior Derecho de la pantalla,
posicionado sobre el grupo en cuestión. A continuación se deberá de definir
para cada campo, la columna de diseño llamada Crosstab, en la cual se
especifican 3 opciones: | Ninguna: | No tendrá tratamiento de CrossTab | Divide: | Es o son los campos que divide las columnas | Dividido: | Es o son los campos que quedarían
 divididos en columnas, en función de los campos que Dividen Una vez
seleccionados los campos, con el botón de VALORES (que se habilita
automáticamente cuando está seleccionado la marca de crosstab), se deben de
especificar los parámetros de Divide. Ejemplo: Items
de movimientos de Venta (Totales), el sistema graba un registro por cada
concepto e imputación contable. El requerimiento del formulario pre-impreso es: | SUBTOTAL | Descuentos y Recargos | I.V.A. | I.V.A. Adicional | Impuestos Internos | TOTAL | XXX.XX | XXX.XX | XXX.XX | XXX.XX | XXX.XX | XXX.XX El
campo de Importe, se debería definir para el ejemplo como Dividido, mientras que
el tipo y código de concepto, se deberían de definir como Divide. | Tipo de Concepto | Código de Concepto | Ejemplo | D | D01 | Descuento | I | I01 | IVA | I | I03 | IVA adicional | J | J01 | Impuestos Internos | T | T01 | TOTAL NOTA: Cuando
se agregue una nueva combinación, deberá de volver a agregar dichos valores en
los Valores Posibles. Es por esto recomendamos tener en cuenta en la
parametrización. Diseño  Solapa Grupos (Especificaciones) En
dicha solapa se definirán los filtros del reporte, si el reporte es de
agrupación, y se compone de dos secciones: Filtros
para campos (WHERE) Filtros
para resultados (HAVING) Diseño  Solapa Orden (Especificaciones) En
dicha solapa se definirá el ordenamiento del reporte. En la
primer sección aparecerá la lista de todos los campos que se ejecutan del lado
del servidor, el usuario deberá seleccionar los campos por los cuales se
ordenará el reporte y los mismos con la acción, Doble Click o con el Drag and
Drop, pasará los campos de una sección a la otra. El
botón de totales se activará en cuanto haya al menos un campo seleccionado en
el orden. Para
calcular totales, deberá existir al menos un campo numérico. Nota : si define ordenamiento, recuerde que el ordenamiento
de los campos de la solapa CAMPOS deberá ser el mismo, para que el reporte
funcione correctamente. Diseño  Solapa SQL (Especificaciones) En
dicha solapa aparecerá la sentencia que el sistema ejecutará para recuperar la
información. La misma es informativa, y sirve en algunos casos para copiarla y
pegarla en herramientas como el ISQL, y revisar el funcionamiento de la misma,
y detectar las causas por las cuales no funciona correctamente. Ej: relaciones,
campos calculados, etc. SENTENCIAS SQL - Sintaxis | SELECT select_list | Lista de campos | [FROM table_name] | Lista de tablas | [WHERE clause] | Condición de filtro para los campos | [GROUP BY clause] | Lista de campos | [HAVING clause] | Condición de filtro para los resultados | [ORDER BY clause] | Lista de campos 
## Diseño  Solapa Campos (Suplementos) Como
anexo a partir de la versión 1.9.7. se agregó el botón de Suplementos (abajo a
la derecha). Esta opción esta pensada
para agregar suplementos accesorios al generador de reportes y poder
utilizarlos en el mismo. En la misma versión se incluye la programación
orientada al tratamiento de múltiples monedas. Al
seleccionar la misma, le aparecerá en la ejecución del reporte, una nueva
solapa, luego del formato, y parámetros del reporte. Suplemento multimoneda | CURRECYOBJECTS.COUNT | Cantidad de monedas definidas en la
 empresa | CURRECYOBJECTS(N).SELECTED | Moneda seleccionada por el usuario, donde
 N es un número. | CURRECYOBJECTS(N).ID | Código de moneda, donde N es un número. | REPORTEDITOR.GROUPS(1).WHERE | Se agrega a la clausula del WHERE | CURRECYOBJECTS.CONVERTIONCURRENCY | Código de Moneda a la que se va a
 convertir, seleccionada por el usuario. | CURRECYOBJECTS.LOCALCURRENCY | Código de Moneda Nacional | CURRECYOBJECTS(Codigo).EXCHANGERATE | Cambio o paridad, donde Código es el
 código de moneda. Objeto Info | Info.UserId | Código de usuario (Sistema CWA) | Info.UserName | Nombre de usuario (Sistema CWA) | Info.CompanyDescription | Razón Social de Empresa (Sistema CWA) | Info.CompanyName | Código de Empresa (Sistema CWA) | Info.NTUserID | Nombre de usuario (NT) | Info.NTUserIDWithDomain | Nombre de dominio\usuario 
 (NT) Como anexo
a partir de la versión 2.0.2 se agregó la posibilidad de referenciar al Objeto
Info. Esto puede llegar a ser utilizado generalmente en los eventos,
especialmente en el Inicialize, como para poder filtrar las operaciones por
usuario. Ejemplo: ReportEditor.GROUPS(1).WHERE = "VTRMVH_NROCTA = '" & Info.userid
& "'" Diseño  Solapa Campos (Eventos) Como
anexo a partir de la versión 1.9.7. se agregó el botón de Eventos (abajo a la
derecha). Esta opción esta pensada para
poder utilizar eventos en la inicialización, el comienzo, el final y la salida
del reporte. Para
citar algunos ejemplos: Grabación
de tabla temporaria tipo TXT/XLS en la inicialización del reporte y grabar en
la misma durante la ejecución, formateo de planilla XLS, utilización de parámetros
de multimonedas, creación e inicialización de variables globales del reporte. Eventos Inicialización de Eventos
(Initialize) En el
ejemplo se crean variables globales a efectos de utilizarlas en campos calculados
del reporte. La inicialización de eventos se ejecuta antes que el pedido de
parámetros. Variables.DeclareVariable(Moneda_Selección) Variables.DeclareVariable(Moneda_Nacional) Variables.DeclareVariable(Valor_Moneda_Selección) Comienzo de Eventos (Begin) ReportEditor.Groups(1).Where
= VTRMVH_COFLIS =  & Variables(Moneda_Selección) & En el
ejemplo se crea la cláusula del WHERE y se utilizan las variables globales
definidas previamente. NOTA:
El reporte se ejecuta luego del pedido de parámetros. Fin de Eventos Se
ejecuta luego de terminar el reporte Terminación de Eventos Se
ejecuta luego de salir del reporte Predefinición de Parámetros Como
agregado funcional a partir de la versión 2.0.2, en los eventos se podrá
predefinir valores a los parámetros de los reportes, sean libres o no. Esto es
posible en el evento Initialize del reporte, en el que se puede acceder a la
colección de parámetros y consultar o fijar valores. Ahora
existen dos nuevas funciones que facilitan el manejo de parámetros del tipo
fecha. Estos manejan un formato numérico invertido de modo que el valor de
fecha 28/03/2001 aparece como entero largo de valor 20010328, lo que dificulta
operar estos valores. InternalDateToDate(lNumber
As Long) DateToInternalDate(vDate
As Date) Diseño  Solapa Campos (Relaciones) Botón
de Relaciones (abajo a la derecha). Esta
opción esta pensada para poder relacionar reportes. Propiedades de la relación (Solapa General) Descripción
Identificatoria: Define el título que aparecerá luego en el momento de su
visualización. Reporte
de Destino de la relación: Es el reporte que se ejecutará. Campo a
partir del cual se puede relacionar: Es el lugar donde el usuario visualizará
la relación para la posterior ejecución del reporte de destino. Propiedades de la relación (Solapa Parámetros) Se
deberán definir los parámetros que se pasan de un reporte a otro. De origen a
Destino. NOTA:
los campos que se pasan como parámetro deben estar visibles en el reporte
formateado, ya que de lo contrario causará un error en la aplicación. 
## Parámetros En la
solapa de parámetros veremos los campos que han sido seleccionados en la
columna de parámetros de la sección CAMPOS y podremos definir: Ordenamiento : el orden de aparición de los mismos. Campo : No lo define el usuario, si está marcado corresponde a un
parámetro sobre los campos de la sección CAMPOS, caso contrario es un parámetro
libre. Nombre : Se habilita para los parámetros libres. Es el nombre físico,
por el cual el usuario va a acceder al mismo. Título : Se habilita para los parámetros libres. Es el nombre lógico,
que verá el usuario en la ejecución. Tipo
de dato : Se habilita para los parámetros libres.
Idem definición de solapa CAMPOS Tamaño : Se habilita para los parámetros libres. Es la cantidad de
dígitos o caracteres. Rango : Define si el parámetro es desde - hasta o no. Requerido : Define si permite o no completar dicho parámetro. EL no completarlo en el HASTA implica TODOS. Valores : Define la cantidad de veces que se pedirá dicho parámetros.
MULTI-RANGO. Botón
de Defaults (Valores por defecto) : El sistema
permite grabar los valores por defecto para cada parámetro a fin de facilitarle
la operatoria al usuario del reporte. Parámetros Libres Los
parámetros libres sirven para filtrar datos, que con la manera habitual
(columna de parámetro en los campos de diseño), no se podría lograr porque
dicho campo no está. Expresión "
& parameters("Parámetro_Libre").values(1).fromvaluesql &
" Donde | Parámetro_Libre | Es el nombre físico del parámetro libre | (1) | Es el parámetro número 1, el cual se
 deberá de incrementar ante múltiples parámetros | Fromvalue | Es el Desde del parámetro libre o el único
 en caso de no definir sea del tipo Rango | Tovalue | Es el Hasta del parámetro libre | Sql | a) SQL = Formato para SQL Standard. Ej:
 Texto y Fecha entre comillas simples, Número normal. b) TEXT = valor formateado. Ej: Fecha con
 /, Texto sin comilla. c) VARIANT = valor sin formato. |  & y &  | Sirven para concatenar Strings, ya que
 todo la expresión se pasa a VBScript, y este lo convierte a los valores
 definidos por el usuario. NOTA: estos caracteres se deben de utilizar en los filtros o en los campos
 calculados del lado del servidor. En los campos calculados del lado del
 cliente NO deben de utilizarse. NOTA: Los
parámetros libres definidos como tipo: | Strings (Cadena) | se convertirán asociándoles el símbolo ' antes
 y después del dato. | Date (fecha) | se convertirán asociádoles {d y } antes y
 después del dato. | Number (Números) | no se convertirán Como
agregado funcional a partir de la versión 2.0.2, a los parámetros libres se les
podrá asociar un Alias de Tipo de dato Combo de valores posibles. 
## Preview (vista preliminar) En la
solapa de preview, veremos la salida del reporte en modo planilla a fines de
controlar la información a incluir en el reporte. 
## Formato o Presentación de Reporte Seleccionando
el campo deseado y oprimiendo el botón derecho del mouse podremos cambiar las
propiedades de este campo (color, tipo de letra, alineación, etc.) . No
seleccionando ningún campo, oprimiendo el botón derecho del mouse, podremos
agregar nuevos campos u objetos al reporte 
## Macros Macros predefinidas para Presentación de Reportes | &NumeroPagina (&PageNumber): | número de página | &Fecha (&Date): | fecha en el formato corto de la máquina | &Horas (&Hours): | hora | &Hora (&Hour): | hora completa (horas, minutos, etc.) en
 el formato corto de la máquina | &Minutos (&Minutes): | minutos | &Segundos (&Seconds): | segundos | &NombreEmpresa (&CompanyName): | nombre de la empresa | &NombreUsuario (&UserName): | nombre del usuario | &CodigoUsuario (UserID): | código del usuario | &NombreReporte (&ReportName): | nombre del reporte | &NombreCopia (&CopyName): | nombre de la copia Entre paréntesis
se indica el nombre de la macro en inglés, que también puede utilizarse. Como
agregado funcional a partir de la versión 2.0.2, en el formato, se podrán
incluir las siguientes macros: | Descripción | Español | Portugués | Inglés | Nombre de Usuario Logueado | &ntnombreusuario | &ntnomeusuario | &ntusername | Nombre de Dominio y usuario Logeado | &ntdominioynombreusuario | &ntdominioenomeusuario | &ntdomainusername | Fecha de Creación del Reporte | &fechadealtadereporte | &datadacriasaoreporte | &reportcreationdate | Fecha de Modificación del Reporte | &fechademodificaciondelreporte | &datadamodificasaoreporte | &reportlastupdateddate Macros del archivo de control: También
pueden utilizarse macros tomadas del archivo de control. Para ello se antepone
&P: al nombre de la macro. Por ejemplo, &P: Tel será reemplazada por la
variable Tel del archivo de control. Símbolos reservados: Los
símbolos & y &P: se utilizan para indicar un reemplazo por una macro
predefinida y del archivo de control respectivamente. Para incluir estos
símbolos en el texto debe duplicarse el caracter &, es decir que &&
quedará como & y &&P: quedará como &P: en el texto final. Macros
que no se encuentren: Si se
especifica una macro y la misma no puede ser encontrada para su reemplazo, la
misma no tendrá efecto en el texto final. Macros de Variables Como
agregado funcional a partir de la versión 2.0.2, en el formato de cualquier reporte
se podrán incluir macros a variables del reporte. Esto es
a las variables definidas en los eventos vía vbscript. Ejemplo Variables.DeclareVariable
("Texto") Variables(Texto)
= Texto para revisión y prueba en Formato Luego,
en el formato, al incluir un campo del estilo Texto, asociarle al mismo ->
&V:TEXTO, y probar que en el formato aparecerá dicha leyenda. Esta
funcionalidad tiene como objetivo, poder incluir textos variables o sea,
dependientes, NO Fijos. 
## Tratamiento de imágenes 
## Definición de Reporte Campo Calculado Se debe crear un campo calculado que
retorne como resultado la ruta hacia la imagen deseada. NOTA:
solo soporta archivos de imágenes BMP. Ejemplo
de Campo Calculado | Nombre | Usr_Iconos | Expresión | sImagen =CurrentRecord("VTRMVH_CODCOM") Result = "F:\Pictures\Comprobantes\" & sImagen & ".BMP" 
## Formato del Reporte Campo Calculado Se debe
agregar el campo calculado (ref. párrafo anterior), en la solapa Texto y
asociar el mismo al campo Texto. Es conveniente
que NO se imprima, NI se vea, el contenido del mismo, ya que solo se usa, para
que el formato lo vea en línea, y no a efectos de impresión de la ruta de
acceso al gráfico. Por
eso, recomendamos, ponerle color blanco tanto al frente como al fondo. Imagen Se debe
agregar un nuevo campo tipo IMAGEN, esto se activa, con botón derecho, agregar
objeto, imagen. Luego
completar la solapa correspondiente a Imagen, en el campo Archivo, con el
nombre del campo calculado mencionado anteriormente, pero agregarle el símbolo
# al principio. 
## VBScript Lenguage Reference Para
utilizar dicho lenguaje de programación, se deberá de conocer procedimientos de
CWA para su funcionamiento. Ejemplo
de demostración Fecha_calculada
es un campo calculado cuya expresión es: RESULT
= NOW Cuando
la ejecute RESULT = el sistema asignará
a Fecha_calculada, la expresión NOW que equivale a la fecha actual. 
## Lista de palabras reservadas por CWA | RESULT | Objeto | Ver ejemplo anterior | NUMBERTOTEXT | Función | Sirve para convertir un número a letras RESULT = NUMBERTOTEXT(importe1) | ACUM | Función | Sirve para ir acumulando el resultado. RESULT = campo1.ACUM | CURRENTRECORD | Objeto | Recupera campo actual RESULT = CURRENTRECORD(CGRMVH_FCHMOV) | PARAMETER | Objeto | Recupera parámetros RESULT = " &
 parameters("Fecha").values(1).fromvaluesql & " Donde Fecha es el parámetro libre, y (1)
 es el desde en caso de ser rango o en caso de no serlo. 
## Funciones más habituales de VBScript. 
## Funciones de Cadena Null Description The Null keyword is used to indicate
that a variable contains no valid data. This is not the same thing as Empty . Abs Function Description Returns the absolute
value of a number. Syntax Abs( number ) The number argument can be any valid numeric
expression . If number contains Null , Null is returned; if it is an uninitialized variable, zero is
returned. Remarks The
absolute value of a number is its unsigned magnitude. For example, Abs( -1 ) and Abs( 1 ) both return 1. Chr Function Description Returns
the character associated with the specified ANSI character code. Syntax Chr( charcode ) The charcode argument is a number that
identifies a character . Remarks Numbers
from 0 to 31 are the same as standard, nonprintable ASCII codes. For example, Chr(10) returns a
linefeed character. Int, Fix Functions Description Returns
the integer portion of a number. Syntax Int( number ) Fix( number ) The number argument can be any valid numeric
expression . If number contains Null , Null is returned. Remarks Both Int and Fix remove the fractional part of number and return the resulting integer value. The difference
between Int and Fix is that if number is
negative, Int returns the first
negative integer less than or equal to number, whereas Fix returns the first
negative integer greater than or equal to number. For example, Int converts -8.4 to
-9, and Fix converts -8.4 to -8. Fix( number ) is equivalent to: Sgn( number ) *
Int(Abs( number )Int) Replace Function Description Returns
a string in which a specified substring has been replaced with another
substring a specified number of times. Syntax Replace( expression , find , replacewith [ , start [ , count [ , compare ]]] ) The Replace function syntax has these parts: Remarks The
return value of the Replace function
is a string, with substitutions made, that begins at the position specified by start and and concludes at the end of
the expression string. It is not a
copy of the original string from start to finish. Filter Function Description Returns
a zero-based array containing subset of a string array based on a specified
filter criteria. Syntax Filter( InputStrings , Value [ , Include [ , Compare ]] ) The Filter function syntax has these parts: Remarks If
no matches of Value are found within InputStrings , Filter returns an empty array. An error occurs if InputStrings is Null or is not a one-dimensional array. The array returned by the Filter function contains only enough
elements to contain the number of matched items. InStr Function Description Returns
the position of the first occurrence of one string within another. Syntax InStr( [ start , ] string1 , string2 [ , compare ] ) The InStr function syntax has these arguments: Return Values The InStr function returns the following
values: LTrim, RTrim, and Trim Functions Description Returns
a copy of a string without leading spaces ( LTrim ),
trailing spaces ( RTrim ), or both
leading and trailing spaces ( Trim ). Syntax LTrim( string ) RTrim( string ) Trim( string ) The string argument is any valid string
expression . If string contains Null , Null is returned. UCase Function Description Returns
a string that has been converted to uppercase. Syntax UCase( string ) The string argument is any valid string
expression . If string contains Null , Null is returned. Remarks Only
lowercase letters are converted to uppercase; all uppercase letters and
nonletter characters remain unchanged. LCase Function Description Returns
a string that has been converted to lowercase. Syntax LCase( string ) The string argument is any valid string
expression . If string contains Null , Null is returned. Remarks Only
uppercase letters are converted to lowercase; all lowercase letters and
nonletter characters remain unchanged. Mid Function Description Returns
a specified number of characters from a string. Syntax Mid( string , start [ , length ] ) The Mid function syntax has these arguments: Remarks To
determine the number of characters in string ,
use the Len function. Note The MidB function is
used with byte data contained in a string. Instead of specifying the number of
characters, the arguments specify numbers of bytes. String Function Description Returns
a repeating character string of the length specified. Syntax String( number , character ) The String function syntax has these arguments: Remarks If
you specify a number for character greater than 255, String converts
the number to a valid character code using the formula: character Mod 256 Space Function Description Returns
a string consisting of the specified number of spaces. Syntax Space( number ) The number argument is the number of spaces
you want in the string. Len Function Description Returns
the number of characters in a string or the number of bytes required to store a
variable. Syntax Len( string | varname ) The Len function syntax has these parts: 
## Funciones de Fecha Now Function Description Returns
the current date and time according to the setting of your computer's system
date and time. Syntax Now Weekday Function Description Returns
a whole number representing the day of the week. Syntax Weekday( date, [ firstdayofweek ] ) The Weekday function syntax has these
arguments: MonthName Function Description Returns
a string indicating the specified month. Syntax MonthName( month [ , abbreviate ] ) The MonthName function syntax has these parts: Month Function Description Returns
a whole number between 1 and 12, inclusive, representing the month of the year. Syntax Month( date ) The date argument is any expression that can
represent a date. If date contains Null , Null is returned. Day Function Description Returns
a whole number between 1 and 31, inclusive, representing the day of the month. Syntax Day(date) 
## Funciones Miscelaneas Dim Statement Description Declares
variables and allocates storage space. Syntax Dim varname [ ( [ subscripts ] ) ][ , varname [ ( [ subscripts ] ) ]] . . . The Dim statement
syntax has these parts: Array Function vbstoc.htm Description Returns a Variant containing an array . Syntax Array( arglist ) The
required arglist argument is a
comma-delimited list of values that are assigned to the elements of an array
contained with the Variant . If no
arguments are specified, an array of zero length is created. Dim AA = Array(10,20,20)B = A(2) Note A variable that is not declared as an array can still contain an
array. Although a Variant variable
containing an array is conceptually different from an array variable containing Variant elements, the array elements
are accessed in the same way. If...Then...Else Statement Description Conditionally
executes a group of statements, depending on the value of an expression. Syntax If condition Then statements [ Else elsestatements ] Or, you can use the block form syntax: If condition Then [ statements ] [ ElseIf condition-n Then [ elseifstatements ]] . . . [ Else [ elsestatements ]] End If The If...Then...Else statement syntax has these parts: Remarks You
can use the single-line form (first syntax) for short, simple tests. However,
the block form (second syntax) provides more structure and flexibility than the
single-line form and is usually easier to read, maintain, and debug. Null Description The Null keyword is used to indicate
that a variable contains no valid data. This is not the same thing as Empty . True Description The True keyword has a value equal to
-1. False Description The False keyword has a value equal to
0. Empty Description The Empty keyword is used to indicate an
uninitialized variable value. This is not the same thing as Null . Si
desea más información puede consultar la siguiente página de Microsoft:1 http://msdn.microsoft.com/scripting/default.htm?/scripting/VBScript/doc/VBSTOC.htm 
## 
## Ejemplos de Campos Calculados 
## Campos calculados del lado de Cliente (VBScript) Función: Recupera el día en palabras. A
partir de una fecha grabada en el sistema, y luego pasarlo a Mayúscula para el
primer carácter y minúscula para los próximos. | DIM D | D=CURRENTRECORD("VTRMVH_FCHMOV") | | DIM A,B | A =
 ARRAY("SABADO","DOMINGO","LUNES","MARTES","MIERCOLES","JUEVES","VIERNES") | B = A(WEEKDAY(D)-1) | | RESULT = UCASE(MID(B,1,1)) &
 LCASE(MID(B,2,19)) Función: Recupera el mes en palabras. A partir de una fecha grabada en
el sistema y luego pasarlo a Mayúscula para el primer carácter y minúscula para
los próximos. | DIM D | D=CURRENTRECORD("VTRMVH_FCHMOV") | | DIM A,B | A = ARRAY("ENERO",
 "FEBRERO", "MARZO", "ABRIL", "MAYO",
 "JUNIO", "JULIO", "AGOSTO",
 "SETIEMBRE", "OCTUBRE", "NOVIEMBRE"
 ,"DICIEMBRE") | B = A(MONTH(D)-1) | | RESULT = UCASE(MID(B,1,1))&LCASE(MID(B,2,19)) Función: Calculo de saldo acumulado. Para un
campo calculado anterior llamado SALDO. | RESULT =
 CURRENTRECORD("SALDO").ACUM Función: Recupera texto asociado en formulario de remito. Se
encuentra posicionado en la tabla STRMVI (Items del remito), el texto asociado
se encuentra en FCRMVI (Items de movimientos de ventas [Notas de venta,
Remitos, Facturas, etc.]), se escribe un nuevo campo calculado con la siguiente
expresión: DIM
SSQL SMOD =
ACTUALREG("STRMVI_MODFOR") SCOD =
ACTUALREG("STRMVI_CODFOR") SNRO =
ACTUALREG("STRMVI_NROFOR") SITM =
ACTUALREG("STRMVI_NROITM") SSQL =
"" SSQL =
"SELECT FCRMVI_TEXTOS FROM FCRMVI WHERE FCRMVI_MODFOR= '" SSQL =
SSQL & SMOD & "' AND FCRMVI_CODFOR= '" SSQL =
SSQL & SCOD & "' AND FCRMVI_NROFOR= " SSQL =
SSQL & SNRO & " AND
FCRMVI_NROITM= " SSQL =
SSQL & SITM & " AND
FCRMVI_CODFOR=FCRMVI_CODAPL" S_RES=
QUERYEXEC(CSTR(SSQL)) IF
S_RES & VBNULLSTRING = VBNULLSTRING THEN RESULT = VBNULLSTRING ELSE RESULT = S_RES END IF 
## Campos calculados del lado del Servidor Función: Recupera la condición de pago desde un remito. Se
encuentra posicionado en la tabla STRMVH (encabezado del remito), el código de
condición de pago se encuentra en FCRMVH (encabezado de movimientos de ventas
[Notas de venta, Remitos, Facturas, etc.]), se escribe un nuevo campo calculado
con la siguiente expresión: SELECT VTTCPH_DESCRP FROM VTTCPH,FCRMVH WHERE VTTCPH_CNDPAG
= FCRMVH_CNDPAG AND FCRMVH_MODFOR
= STRMVH_MODFOR AND FCRMVH_CODFOR
= STRMVH_CODFOR AND FCRMVH_NROFOR
= STRMVH_NROFOR ) Función: Recupera el transportista desde un remito. Se
encuentra posicionado en la tabla STRMVH (encabezado del remito), el código de
transportista se encuentra en FCRMVH (encabezado de movimientos de ventas [Notas
de venta, Remitos, Facturas, etc.]), se escribe un nuevo campo calculado con la
siguiente expresión: SELECT
FCRMVH_TRANSP FROM FCRMVH WHERE FCRMVH_MODFOR
= STRMVH_MODFOR AND FCRMVH_CODFOR
= STRMVH_CODFOR AND FCRMVH_NROFOR
= STRMVH_NROFOR Función: Recupera los pendientes de ventas para análisis de Stock. Se
encuentra posicionado en la tabla STMPDH (Maestro de productos), los pendientes
de ventas se encuentran en FCRMVI (Items de movimientos de ventas [Notas de
venta, Remitos, Facturas, etc.]), se escribe un nuevo campo calculado con la
siguiente expresión: SELECT
ISNULL(SUM(FCRMVI_CANTID),0) FROM FCRMVI WHERE FCRMVI_TIPPRO
= STMPDH_TIPPRO AND FCRMVI_ARTCOD
= STMPDH_ARTCOD AND FCRMVI_MODAPL
= FC AND FCRMVI_CODAPL = " &
parameters("Fecha_Libre").values(1).fromvaluesql & " 
## Importación y Exportación de Reportes 
## Alcance funcional Esta herramienta sirve para importar y/o
exportar reportes. Puede transferir desde una empresa a otra
o bien hacia un archivo tipo Access (MDB), para luego llevarlo (vía medio
magnético hacia otra instalación como ser sucursales o bien CWA. Además de dicha funcionalidad, el
import-export, puede importar y/o exportar datos de tablas y diccionario de
datos, solo que en esta ocasión nos detendremos a analizarlo para reportes. 
## Método de utilización (Exportación de Reportes) La herramienta se instala con la llegada
de cualquier versión de nuestro producto, y se ubica en el mismo directorio que
el menú. El nombre técnico de la aplicación es cwIMPEXP.exe Tipo de
proceso: Reportes Diccionario Tablas Seleccionaremos
Reportes Tipo de
base: MDB SQL Se
deberá seleccionar MDB para exportar reportes a Access, o SQL para exportar
reportes a otra empresa. Origen Se
deberá seleccionar la empresa del Origen de la exportación Destino Se
deberá seleccionar la empresa del Destino de la exportación para el caso SQL o
el archivo ACCESS en caso MDB. Archivo Nuevo: Al
oprimir los tres puntos, aparecerá el explorador, para que indique en que
subdirectorio generará el archivo. Luego
completar el nombre del archivo a generar. Al
oprimir el botón de CREAR, se mostrará una ventana, con las estructuras de las tablas de reportes, generadas
para el archivo en cuestión. A
continuación el usuario deberá seleccionar él o los reportes a exportar. NOTA:
sacar el seleccionar TRANFERIR TODOS Al
aceptar, luego del proceso de exportación aparecerá el siguiente mensaje El proceso
termino con éxito. Si el mismo no aparece la exportación no se realizó. 
## Tablas de Reportes (Internas) Descripción de las tablas y su contenido. | CWRMDEFINITIONS | Encabezado de los reportes (1 registro
 por grupo de reporte) | Name | Description_ARG | BaseTable | BaseTableID | BaseGroupID | GRTPOS | GR - Códigos postales | GRTPAC | GRTPAC | 1 | | | | | | | CWRMGROUPS | Grupos de los reportes (1 registro por
 grupo de reporte) | ReportName | GroupID | DistinctClause | WhereClause | HavingClause | GRTPOS | 1 | 0 | | | | | | | | | CWRMFIELDS | Campos de los reportes (1 registro por
 campo del reporte) | Name | RealField | Expression | Visible | ServerSide | OrderBy | GroupBy | Cant_items | 0 | 1 | 1 | 1 | 0 | -1 | GRTPAC_CODPAI | 1 | | 1 | 1 | 1 | -1 | GRTPAC_CODPOS | 1 | | 1 | 1 | 2 | -1 | GRTPAC_CODPRO | 1 | | 1 | 1 | 0 | -1 | GRTPAC_DESCRP | 1 | | 1 | 1 | 0 | -1 | GRTPAC_PAIPRO | 1 | | 0 | 1 | 0 | -1 | GRTPAH_CODPAI | 1 | | 0 | 1 | 0 | -1 | GRTPAH_DESCRP | 1 | | 1 | 1 | 0 | -1 | GRTPAI_CAPFED | 1 | | 1 | 1 | 0 | -1 | GRTPAI_CODPAI | 1 | | 0 | 1 | 0 | -1 | GRTPAI_CODPRO | 1 | | 0 | 1 | 0 | -1 | GRTPAI_DESCRP | 1 | | 1 | 1 | 0 | -1 | | | | | | | | | CWRMFORMATS | Formato de los reportes (1 registro por
 reporte) | CWRMFORMATFIELDS | Formato de los campos de reportes | CWRMPARAMETERS | Parámetros libres del reporte

---

## [SuplementoReportesI-RelacionesVariablesYCodigosDeBarra.htm]

> Fuente: Manual de Reportes I - Softland Logic (SAC, v1.3). Complementa la sección "Generador de Reportes" de este archivo con temas que no estaban documentados: niveles de relación entre tablas, tipos de relación (Join), variables especiales de la ventana de formato/exportación (`RM_UI_*`), y códigos de barra.

## Relación entre tablas — Niveles

Un reporte parte de una tabla base y se le pueden agregar tablas relacionadas siempre que exista un vínculo (ForeignKey o MappedKey) en el diccionario de datos, directo o transitando por una tabla intermedia:

- **Relación de Nivel 1:** la tabla agregada tiene relación directa con la tabla base (comparten un campo, ej. `CategoriaID` entre Categorías y Productos).
- **Relación de Nivel 2 (o superior):** no hay relación directa; se llega a la tabla destino atravesando una tabla intermedia (ej. desde Categorías se llega a Proveedores pasando por Productos).

Para relacionar tablas: botón derecho sobre la tabla de origen → **Relacionar tablas** → elegir la tabla destino → **Seleccionar campos** a incorporar.

## Propiedades de relaciones (tipo de Join)

Botón derecho sobre la tabla de origen → **Propiedades de las relaciones**. Tipos disponibles:

- **Por defecto:** recupera los valores según lo definido en el Diccionario de datos.
- **Requerida:** solo muestra registros que existen en ambas tablas (equivalente a INNER JOIN).
- **No Requerida:** muestra todos los valores de la tabla A y solo los de B que coincidan con A; lo inexistente se completa con nulos (equivalente a LEFT JOIN).
- **Inversa no requerida:** muestra todos los valores de la tabla B y solo los de A que coincidan con B; lo inexistente se completa con nulos (equivalente a RIGHT JOIN).

Diagnóstico típico: si un reporte "pierde" registros que sí existen en la tabla base, revisar si la relación con una tabla agregada quedó como **Requerida** en vez de **No Requerida** — eso descarta silenciosamente los registros sin contraparte.

## Atajos de alineación de objetos (edición de formato)

`Ctrl+T` alinea al margen superior, `Ctrl+B` al margen inferior, `Ctrl+L` a la izquierda, `Ctrl+R` a la derecha. Requieren 2 o más objetos seleccionados.

## Variables especiales de la ventana de Formato/Exportación (`RM_UI_*`)

Se declaran e inicializan igual que cualquier variable (`Variables.DeclareVariable("...")` / `Variables("...") = valor`), típicamente en el evento **Initialize**, y controlan los controles de la ventana de parámetros/exportación del reporte (habilitar/deshabilitar un control, o fijar su valor por defecto):

| Variable | Controla |
|---|---|
| `RM_UI_PrintToFile_Enabled` / `_Value` | Habilita y valor por defecto del check "Imprimir a archivo" |
| `RM_UI_OutputPath_Enabled` / `_Value` | Habilita y valor por defecto del path de salida del archivo |
| `RM_UI_CompressFile_Enabled` / `_Value` | Habilita y valor por defecto del check "Comprimir archivo" |
| `RM_UI_ExportFile_Enabled` / `_Value` | Habilita y valor por defecto de la exportación del archivo |
| `RM_UI_OUTPUT_TEXT_SEPARATOR_ENABLED` / `_VALUE` | Habilita y texto del separador de columnas (exportación a texto, hasta 3 caracteres) |
| `RM_UI_OUTPUT_TEXT_COLUMN_HEADERS_ENABLED` / `_VALUE` | Habilita y valor de "mostrar nombres de columna" (exportación a texto) |
| `RM_UI_OUTPUT_GRID_SHOW_GRAND_TOTAL_ENABLED` / `_VALUE` | Habilita y valor de "Total Gral." en formato grilla |
| `RM_UI_OUTPUT_GRID_SHOW_SUB_TOTAL_ENABLED` / `_VALUE` | Habilita y valor de "Subtotales" en formato grilla |
| `RM_UI_OUTPUT_TEXT_SHOW_GRAND_TOTAL_ENABLED` / `_VALUE` | Habilita y valor de "Total Gral." en exportación a texto |
| `RM_UI_OUTPUT_TEXT_SHOW_SUB_TOTAL_ENABLED` / `_VALUE` | Habilita y valor de "Subtotales" en exportación a texto |
| `RM_UI_OUTPUT_TEXT_TERMINATE_WITH_ENTER_ENABLED` / `_VALUE` | Habilita y valor de "terminar con enter final" en exportación a texto |

Todos toman `TRUE`/`FALSE`. Útiles cuando un ticket pide que un reporte específico salga siempre con una configuración fija de exportación (por ejemplo, forzar separador de columnas o suprimir el total general) sin que el usuario tenga que tildarlo cada vez.

## Códigos de barra soportados

El generador soporta 4 tipos, cada uno vía una función de conversión (usada en un campo calculado) + una fuente incluida en el sistema que se aplica al campo en el formato:

| Tipo | Función de conversión | Fuente a aplicar |
|---|---|---|
| Bar Cod 25 | `NumberToBarCode25I` | alguna de las 5 variantes `Font Bar 25i` |
| EAN 13 | `NumberToBarCodeEAN13` | `EAN a` |
| QR | `StringToQR` | `MRV QRCode` |
| DataMatrix | `StringToDataMatrix` | `MRV DataMatrix5` |

Patrón típico del campo calculado (ejemplo con QR, mismo patrón para los otros tres):

```vbscript
sCodigo = CurrentRecord("STMPDH_INDCOD")
If IsNumeric(sCodigo) Then Result = stringtoqr(sCodigo) Else Result = 0 End If
```

En la edición del formato, al campo de texto que muestra el código convertido hay que asignarle la fuente correspondiente de la tabla y, en Propiedades → solapa Estilo, tildar **Múltiples líneas** (los códigos QR/DataMatrix se renderizan como texto multilínea con esa fuente).

---

## [GeneradordeProcesos.htm]

## Generador de Procesos 
## Objetivo Posibilidad de generar nuevos
procesos No Standard del tipo Wizard (Paso a Paso) en forma ágil y dinámica. 
## Alcance Funcional A partir de la
generación de un reporte, el sistema generará 3 pasos de Wizard, donde: Pedirá los
parámetros del reporte Mostrará en una
nueva ventana, los registros del reporte, con todos sus columnas, permitiendo
al usuario la posibilidad de selección total o parcial. Al terminar,
procesará altas o modificaciones sobre cualquier tabla o tablas del sistema. 
## Ficha Técnica 
## Ubicación en el menú Administración
del Sistema, Generales, Instalación. Opción: Generador de Wizards. 
## Generación del Reporte Se deberá definir un nuevo reporte
desde el cual se recuperarán los datos y las sentencias de actualización a
utilizar por el proceso. En el reporte se deberán de
utilizar los siguientes campos calculados: | CWA_MENSAJE | Al Terminar, mostrará dicho mensaje para cada
 registro procesado. | CWA_SI | Al Terminar, mostrará dicho texto únicamente para
 los registros seleccionados | CWA_NO | Al Terminar, mostrará dicho texto únicamente para
 los registros NO seleccionados | CWA_SENTENCIA | Sentencia (Query) - La misma se ejecutará únicamente para los registros
 seleccionados. | CWA_NOSENTENCIA | Sentencia (Query) - La misma se ejecutará únicamente para los registros NO seleccionados. | CWA_MAILTO | Dirección de mail  En caso de estar completa, el
 sistema disparará un mail para cada uno de los registros seleccionados, en
 forma automática, a esta casilla de correo. NOTA: Estos campos deberán estar
visibles. 
## Generación de Wizard Seleccionar la opción de menú Generador
de Wizard, botón derecho, Crear Link, asociar nombre al nuevo objeto del
menú. Ejecutar el nuevo objeto de menú. 1º Paso: Menú descolgable, opción
Grabar Macro. 2º Paso: Ingresar el código de
reporte a utilizar. 3º Paso: Completar los parámetros
que NO desea sean visibles o editables por el usuario. 4º Paso: Menú descolgable, opción
Grabar Macro. Salir de la aplicación. Para probar la aplicación,
ejecutar dicha opción de menú, seleccionar uno o más registros, terminar y
revisar las tablas actualizadas, por reportes del sistema o por SQL. NOTA: si se desean ejecutar más de una sentencia, separar las mismas por medio
de ;.

---

## [GeneradordeAplicaciones.htm]

## Generador de Aplicaciones 
## Objetivo Posibilidad de
generar nuevas aplicaciones en forma ágil y dinámica. Estas
aplicaciones tienen carácter de "A medida del Cliente". 
## Alcance Funcional A partir de la generación de un reporte,
el sistema recuperará la información del mismo, bajando a un ABM, previa
selección, con la posibilidad de editar cualquier campo y luego grabarlo. Este tipo de
aplicaciones, trabajan con un modelo tipo VBScript, asociando código de
programación simple a: a) Edición o cambio de valor de cualquier campo b) Inicialización de la aplicación c) Previo a la grabación (Validaciones) d) Grabación (Insertar, modificar o borrar) 
## Ficha Técnica 
## Configuración de
aplicaciones En la
Configuración de Aplicaciones, se dará de alta la aplicación propiamente dicha,
que se invocará desde el Generador de Aplicaciones. Para ello se deberá definir
el reporte desde el cual se recuperarán los datos para dicha aplicación y el
código VBScript que se ejecutará en la misma. El código de aplicación, según el
UpGrade instalado en el cliente (ver cuadro de UpGrades), deberá ser
"APL01", "APL02", etc., salvo que haya instalado las
aplicaciones libres, en cuyo caso el código no tiene ningún tipo de
restricción. 
## Generador
de aplicaciones Se deberá
ingresar el código de la aplicación, previamente dada de alta a través del ABM
de Configuración de Aplicaciones, luego se pasa a la ejecución del reporte,
previo pedido de parámetros (si es que el reporte los requiere); el resultado
de la ejecución del reporte se mostrará en una grilla desde la cual el usuario
seleccionará los ítems a procesar. Una vez seleccionados los ítems y al dar
"Terminar" en el Wizard, entra a ejecutarse el Vbscript asociado a la
aplicación, y paralelamente la bajada al spread de los ítems seleccionados.
Cuando se da "Guardar" en el ABM, se grabará en las tablas del
Generador (GRRMDH y GRRMDI), la aplicación en cuestión. 
## Creación
de Links y Personalización de pantallas El Generador de Aplicaciones
fue desarrollado pensando para utilizarse a través de links, para lo cual el
usuario deberá crear los links pensando en cada uno como una aplicación por
separado, personalizando los pasos del Wizard y la pantalla del AMB en los
mismos, y no en el Generador de Aplicaciones mismo. 
## UpGrades | Código | Cantidad de
 Aplicaciones | | GA01 | 1 | (Una) | GA02 | 2 | (Dos) | GA01 | 3 | (Tres) | GA01 | 5 | (Cinco) | GA01 | 10 | (Diez) | GANN | n | (Libre)

---

## [GeneradorDeMovimientos.htm]

## Generador de Movimientos 
## Objetivo Posibilidad de generar movimientos en forma automatica
partiendo de un reporte generado por el usuario. 
## Alcance
Funcional Se permitirá realizar movimientos
aplicables a las registraciones de Compras, Facturación y Producción en forma
automatica recuperando los datos necesarios sobre la base de un reporte. 
## Ficha
Técnica La
aplicación permite definir en forma automatica circuitos que apliquen sobre si
mismos, como ser la orden de compra, y circuitos que aplique sobre otros como
ser un vale de consumo. Para los
circuitos que aplican sobre sí mismo es necesario tener definido la siguiente
lista de campos en el reporte asociado: TIPORI ARTORI CANTID FCHENT MODULO NROCTA FORMUL DEPOSI SECTOR Para los
circuitos que aplican sobre otros circuitos es necesario tener definido 2
reportes uno de grupo y otro reporte de detalle. En el reporte de grupo es
requerida la siguiente lista de campos en el reporte MODULO, NROCTA. En el
reporte de detalle es requerida la siguiente lista de campos: MODAPL,
CODAPL NROAPL,
ITMAPL TIPORI,
ARTORI CANTID,
DEPOSI SECTOR MODULO La
aplicación en todos los casos genera un log con la lista de errores detectados

> **Ver también:** `references/cwa-cubos-paneles-consultas.md` tiene la versión más completa y actualizada de este tema (Manual de Reportes II), con la lista completa de campos requeridos (incluye `MODINI`, `CODINI`, `NROINI`, `NIVINI`, `EXPINI`), la tabla de Upgrades habilitantes (`GMFC`/`GMCO`/`GMPD`/`GMNN`) y el detalle de comportamiento por tipo de registración (Facturación, Compras, Tesorería, Cobranzas/Pagos, Inventario, Movimientos de Ventas/Proveedores).

---

## [AsistentedeParametrizacion.htm]

## Asistente de Parametrización 
## Objetivo Estandarización
de las implementaciones en curso y nuevas. Reducción del
costo de implementación y parametrización. Acelerar las
tareas de: · Selección de los reportes a utilizar. · Personalización de pantallas. · Creación de circuitos, estructuras de
cálculo, comprobantes, etc. · Creación de links, y su posterior
posicionamiento. 
## Alcance Funcional Posibilidad de
importar Reportes : · Se tendrá la opción de importar uno o más reportes. · Se podrá cambiar el nombre del reporte a elección. · Se generará el reporte en el árbol del menú de la
empresa de destino. · MultiEmpresa. Posibilidad de importar Empresa pre-parametrizada parcialmente : · Posibilidad de importar
Circuitos, Comprobantes, Etc. (Con inteligencia tipo IMPORT-TRANSACTION). · Posibilidad
de renombrar el código del campo a generar. · MultiEmpresa. Posibilidad de
importar Empresa pre-parametrizada totalmente: · Idem parametrización parcial pero de cada tabla a
seleccionar se pasaran todos sus datos. Posibilidad de importar Pantallas (Links, Save to DB,
Registry): · Posibilidad de copiar links
dentro de la misma empresa o en otra. · MultiEmpresa. 
## DETALLE 
## Paso 1 En este paso, se
define el usuario y password del Sistema de Gestión, al haberlos cargado, se
procederá a cargar las empresas que están definidas para este usuario. (El
usuario debe ser administrador, ya que para los reportes y links, se graban en
el árbol del sistema y si no son administradores, los usuarios no tienen acceso
a todas las carpetas). Se deberá elegir
la empresa de Origen, esta al momento de salir de la aplicación se tomará por
default para la próxima vez que se utilice la aplicación, junto con el nombre
del usuario (Grabación en un INI). 
## Paso
2 Se deberán elegir
la/s empresas de destino. 
## Paso
3 
## Se deberá
definir el tipo de proceso a realizar: Parametrización Parcial, Parametrización
Total, Links o Reportes. Parametrización Parcial y Total: Se deshabilitaran
los filtros ya que las tablas de la parametrización se definen en la tabla
GRTLIN y de acuerdo al módulo se cargarán las tablas correspondientes en el
siguiente paso. Links y Reportes: Se habilitaran los
filtros, para que se pueda hacer una búsqueda más rápida de lo que se quiere
encontrar. 
## Filtros Código desde/hasta: En
estas opciones, se buscara a través del filtro >= y <= Ejemplo: Si
quiero buscar un rango de reportes que se encuentre entre CJCCBH y CJTCTA Se deberá poner
en el código desde: CJCCBH y en el código hasta: CJTCTA Código (Máscara: ?): Esta
opción trabaja igual que un wildcard. Ejemplo: Si
quiero traer todos los reportes o links, que tengan _ como tercer letra, lo
que puedo hacer es ??_, de esta manera los ?, podrá ser cualquier tipo de dato. Descripción: Este campo trabaja como un like
de SQL, no hace falta definir los % ya que lo hace la aplicación internamente,
buscara por la descripción del campo. Fecha Alta Desde/Hasta: Esta fecha se usa
para los reportes solamente y esta haciendo referencia al campo FECALT de la
tabla cwRmDefinitions. Fecha Modificación Desde/Hasta : Esta fecha
se usa para los reportes solamente y esta haciendo referencia al campo FECMOD
de la tabla cwRmDefinitions . 
## SobreEscribe Si esta opción esta
chequeada, al momento de correr el proceso, si se eligió la Parametrización
Parcial y se definió pasar un comprobante de facturación, si ese comprobante ya
existía lo pisara. Para el caso de
Parametrización Parcial y Total, se habilitaran dos opciones: Todo y Original. Si los datos no
existen en el destino se agregaran y si ya existen, se trabajara de esta forma: · Con la opción de Todo, se pisaran los
datos tanto de la tabla principal (Nivel 1), como las relacionadas a ella. · Con la opción de Original, solo se
pisara los datos de la tabla principal. Si la opción de
sobreescribe, no esta seleccionada y también se define pasar un comprobante de
facturación, existiendo el mismo en la empresa de destino, se generara un
error, mostrando todos los campos con sus respectivos valores, para el registro
que tuvo problemas. 
## Seleccionar
Módulo En esta opción
se verán todos los módulos que se pueden usar, se notará que si selecciona la
opción de Reportes, el primer módulo que aparecerá será el de (Todos), con esta
opción se cargaran todos los reportes de todos los módulos. En cambio si se
elige cualquier otro tipo de proceso esta opción no va a aparecer, ya que si o
si se necesita definir un módulo. 
## Paso
4 En este paso, la
visualización cambiara, envase al tipo de proceso que se elija. Parametrización Parcial :
Aparecerá una lista con las tablas que se definieron en la GRTLIN. Al elegir
una de las tablas, se cargara los campos claves existentes para dicha tabla.
Solamente se podrá elegir una sola tabla. Se pueden elegir
varios datos a procesar y se podrá renombrar el valor de destino. Parametrización Total : Se
elegirá la tabla/s, a procesar. Al hacer click derecho se podrá elegir todas
las tablas o borrar toda la selección. Links : Para Facturación,
Compras y Producción, se trabajara por circuito. Para Stock se
trabajara por formulario y para Tesorería se trabajara por comprobante. Se podrá elegir
varios links y se grabara en la registry. Reportes : Se podrá elegir
varios reportes. Opción de
renombrarlos: · Si estoy como Developer, se podrá
renombrar cualquier reporte · Si estoy como user, se podrá
renombrar, solamente los campos de usuario. 
## Paso
5 Se mostrará un
preview de los parámetros que se fueron eligiendo, a medida que fueron
avanzando en los pasos. 
## Operaciones Generales Este ejecutable,
cuenta con un archivo asociado tipo ini que se generará la primera vez que se
ejecute el programa. El archivo tipo
ini tiene cuatro campos: · La empresa de origen(EMPRESA) : Es el
código de la empresa de origen que se da de alta en el Sistema de Gestión. · El usuario(USER) : Usuario que se loguea en el
Asistente. · La habilitación de
queries(HABILITARQUERIES) : Las opciones son S o N, y sirve para generar un log con todas las sentencias
de INSERT que se generaron en la empresa de Destino, cuando se usa la
Parametrización parcial o Total. · El borrado del mdb(BORRARMDB) : Las opciones son S o N, al
hacer la Parametrización Parcial o Total, se genera un MDB en el directorio C:\
con los datos que se van a generar en la empresa de destino. También cuenta con una tabla de
parametrización que se llama GRTLIN, en esta tabla se definirá las tablas que
se deberán traer para la parametrización. Detalle de cada campo de la tabla: | GRTLIN_MODULO | Módulo
 de la tabla | GRTLIN_NOMTAB | Nombre
 de la tabla | GRTLIN_NOMCAM | Nombre
 de campo | GRTLIN_TABORD | Orden
 en que se toman los campos | GRTLIN_DEFAUL | Valores
 por default que se le dan a los campos, ejemplo: el módulo para el MODCOM. | GRTLIN_DESTAB | Descripción
 de la tabla | GRTLIN_SELECT | Select
 que se ejecuta en el paso 4, para recuperar los valores de una tabla determinada.
 (Se debe respetar el nombre de los campos, ejemplo: COD1, DES1).

---

