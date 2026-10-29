# CWA — Administrador de Tareas (Automatización vbScript)

> **Cuándo leer este archivo:** cuando el ticket involucra automatización de tareas, ejecución programada, scripts vbScript, clases del sistema (SWizard, STable, SRows, SField, renderers de reportes, File System Helper, Application, Company), o el servicio de Administrador de Tareas

---

## [AdministradorDeTareas.htm]

## Administrador de tareas 
## Objetivo El Administrador de Tareas es un módulo que
permite automatizar la ejecución de tareas. Se entiende por tareas, la emisión
de reportes, la ejecución de procesos, guardar información en tablas, etc. Todo esto se logra mediante la programación
de las actividades en un entorno que combina vbScript con objetos del Sistema
de Gestión, lo que permite realizar todas las operaciones prácticamente como si
se estuviera trabajando normalmente con el Sistema de Gestión. Una vez que la tarea ha sido
diseñada y programada, puede establecerse su ejecución basado en un esquema de
ocurrencia temporal, es decir que se ejecutará en un día y a una hora
especificada, o bien puede establecerse que se ejecutará cuando se produzcan
cambios en un directorio específico. 
## 
## Indice Administrador
de tareas . 1 Objetivo . 1 Indice . 1 Instalación . 4 Instalación del
módulo de administrador de Tareas 4 Instalación 4 Iniciar el
servicio 4 Desinstalación 4 Planificación de la tarea . 5 Nuevo 5 Editar 5 Eliminar 5 Suspender la
ejecución de esta tarea 5 Edición de las
propiedades de la Planificación 5 Nombre 5 Descripción 5 Ejecutar la Tarea
cuando ocurra el evento temporal 5 Ejecutar la Tarea
cuando se produzcan cambios en el directorio 5 Ejecución por
evento temporal 5 Ocurrencia . 6 Diaria . 6 Semanal 6 Mensual 6 Frecuencia Diaria . 6 Duración . 6 Ejecutar la Tarea cuando se
produzcan cambios en el directorio . 6 Permitir la ejecución
inmediata de la Tarea . 6 Propiedades de la tarea . 7 Nombre de la Tarea 7 Descripción de la
Tarea 7 Escribir al
registro de aplicación 7 Eliminar la tarea
una vez ejecutada 7 Permitir la
ejecución simultánea de esta Tarea 7 Iniciar sesión en
el Sistema de Gestión 7 Nombre 7 Password 7 Referencia . 7 Ficha Técnica . 8 Clase Application 8 Application.Companies 8 Clase Company 8 Company.GetObject 8 Company.Name 9 Clase USER 9 USER.ID 9 USER.NAME 9 Ejemplos . 10 ¿Cómo averiguar el código y nombre del usuario del
sistema? 10 Propiedades de la conexión de base de datos 10 Manipulación de registry 10 Administrador de procesos para tareas . 11 Clase SField 11 SField.Caption 12 SField.DataType 12 SField.Description 12 SField.Enabled 12 SField.HasDescription 13 SField.Name 13 SField.Size 13 SField.Value 13 Clase SFields 14 SFields.Item 14 SFields.Count 14 Clase SRow 15 SRow.Fields 15 SRow.Number 15 Clase SRows 15 SRows.Remove 15 SRows.Add 16 SRows.Item 16 SRows.Test 16 SRows.Count 17 SRows.MaxRows 17 Clase SStep 17 SStep.Class 17 SStep.Description 18 SStep.Index 18 SStep.Table 18 Clase SSteps 18 SSteps.Item 19 SSteps.Count 19 Clase STable 19 STable.Fields 19 STable.Rows 20 STable.Description 20 STable.Name 20 Clase StableDef 20 STableDef.FieldDefs 21 STableDef.Frames 21 STableDef.Name 21 Case SWizard 21 SWizard.Cancel 21 SWizard.Finish 22 SWizard.MoveBack 22 SWizard.MoveNext 22 SWizard.CurrentStep 23 SWizard.Description 23 SWizard.Name 23 SWizard.State 24 SWizard.Steps 24 Ejemplo: Como ejecutar un proceso desde una
tarea. 24 Administrador de Tareas para Reportes . 25 Clase DBFRenderer 25 DBFRenderer.Render 26 DBFRenderer.AutoStart 26 DBFRenderer.FileName 26 DBFRenderer.SendMail 26 Clase GridRenderer 26 GridRenderer.DirectRender 27 GridRenderer.Render 27 Clase HtmlRenderer 27 HtmlRenderer.Render 27 HtmlRenderer.AutoStart 27 HtmlRenderer.FileName 27 HtmlRenderer.SendMail 27 Clase TableRenderer 28 TableRenderer.Render 28 TableRenderer.GetLastBatchID 28 TableRenderer.GetLastBatchIDForNewTables 28 TableRenderer.VerifyBatchIDExists 28 TableRenderer.AllowRebuildTable 29 TableRenderer.BatchID 29 Clase TextRenderer 29 TextRenderer.Render 29 TextRenderer.AutoStart 30 TextRenderer.ColumnSeparator 30 TextRenderer.FileName 30 TextRenderer.PrintTitles 30 TextRenderer.SendMail 30 Clase
Win32Renderer 31 Win32Renderer.Render 31 Win32Renderer.GetRandomKeyForReportName 31 Win32Renderer.CompressFile 31 Win32Renderer.Copies 31 Win32Renderer.GoToLastPageOnly 32 Win32Renderer.OutputPath 32 Win32Renderer.PageFrom 32 Win32Renderer.PageTo 32 Win32Renderer.PrinterName 32 Win32Renderer.PrintToFile 33 Ejemplos . 33 Impresión de un
reporte sencillo. 33 Impresión de un
reporte con parámetros. 33 Impresión de un
reporte a impresora, modificando parámetros 34 Impresión de un
reporte a archivo de texto 35 Impresión de un
reporte a archivo de HTML 36 Impresión de un
reporte a archivo de dBaseIII 36 Generación de
cubos a partir de reportes 37 Impresión de un
reporte a archivo de texto y envío del mismo 37 File System Helper 39 Referencia 39 Clase File 39 File.Delete 39 File.Move 40 File.Rename 41 File.Copy 41 File.GetCRC 42 File.CanOpenExclusive 42 File.Extension 42 File.FullName 43 File.Name 43 File.Path 43 Clase Files 44 Files.Count 44 Files.Item 44 Clase
FileSystemHelper 45 FileSystemHelper.FileDelete 45 FileSystemHelper.FileMove 46 FileSystemHelper.FileRename 46 FileSystemHelper.FolderDelete 47 FileSystemHelper.CreateFolder 47 FileSystemHelper.FileCanOpenExclusive 48 FileSystemHelper.FileCopy 48 FileSystemHelper.FileExists 49 FileSystemHelper.FileGetCRC 49 FileSystemHelper.FolderExists 50 FileSystemHelper.FolderGetCRC 50 FileSystemHelper.FolderMake 51 FileSystemHelper.GetFile 51 FileSystemHelper.GetFiles 52 FileSystemHelper.GetFolder 52 FileSystemHelper.GetSubFolders 53 FileSystemHelper.NormalizePath 54 Clase Folder 54 Folder.Delete 54 Folder.Move 55 Folder.Rename 55 Folder.Copy 56 Folder.GetCRC 56 Folder.GetFiles 57 Folder.GetSubFolders 58 Folder.Files 58 Folder.FullName 59 Folder.Name 59 Folder.Path 60 Folder.SubFolders 60 Clase Folders 60 Folders.Count 61 Folders.Item 61 
## Instalación 
## Instalación del módulo de
administrador de Tareas Instalación del servicio de Tareas La instalación del servicio debe ser
realizada por un administrador local, o un usuario con derechos suficientes
para agregar servicios. Esta operación se realiza por única vez y
no requiere repetirse salvo que se cambie la ubicación de los archivos del
módulo del Tareas. 
## Instalación Abrir una sesión de Command Prompt. Posicionarse en el directorio de
instalación del sistema de gestión \JM Ej:"C:\Program Files\CWA\Sistema de
Gestión\JM" Ejecutar la siguiente sentencia para
instalar el servicio cwjmagnt.exe -install dom\usr pass Donde: install : Es el comando que le indica al
programa que debe correr en modo instalación. dom : Es el dominio al que pertenece el
servidor. Si el servidor no perteneciera a ningún dominio o fuese el mismo el
controlador del dominio, este parámetro corresponde al nombre de la máquina. usr : Es el nombre de usuario que será
utilizado para correr el servicio. Este usuario debe tener atributos de
administrador local, de lo contrario el servicio no funcionará. pass : Es la password del usuario nombrado
en el punto anterior. Debe tenerse en cuenta que cuando se escriba la password,
ésta será visible en la pantalla, y no aparecerá enmascarada, es decir que
aparecerán los caracteres en pantalla. Luego de unos segundos el control vuelve al
prompt sin dar indicios de que la operación se haya concretado. Para verificar que el servicio ha sido
instalado correctamente deberá verificarse en el service manager que se
encuentre la entrada del servicio en la lista de servicios instalados. Para verificar esto deben seguirse los
siguientes pasos. Windows NT 4 En el panel de control seleccionar el ítem
de Services (o Servicios) Windows 2000 Hacer click derecho al icono "My
Computer", elegir "Manage". Aparecerá la ventana "Computer
Management". El el árbol jerárquico de la izquierda
expandir el ítem "Services and Applications". En ambos casos verificar en la lista que se
muestra que exista un ítem "CWA - SG32 - Job Manager (agent)" 
## Iniciar el servicio Presionar el boton Start (o iniciar) El estado del servicio deberá decir
"Started" en la columna de estado. Si se presentan errores intentando
iniciar el servicio deberá verificarse la existencia en el directorio Shared
del sistema de gestión del archivo "Sistema de Gestión.log", ahí se
mostrará el código de error de lo que puede estar fallando. 
## Desinstalación Abrir el service manager Windows NT 4 En el panel de control seleccionar el ítem
de Services (o Servicios). Windows 2000 Hacer click derecho al icono "My
Computer", elegir "Manage". Aparecerá la ventana "Computer
Management". El el árbol jerárquico de la izquierda
expandir el ítem "Services and Applications". Seleccionar de la lista el servicio
"CWA - SG32 - Job Manager (agent)" Presionar el botón "Stop" (o
Detener) Abrir una sesión de Command Prompt. Posicionarse en el directorio de
instalación del sistema de gestión \JM Ej:"C:\Program Files\CWA\Sistema de
Gestión\JM" Ejecutar la siguiente sentencia cwjmagnt.exe -uninstall 
## 
## Planificación
de la tarea Permite establecer una o más
planificaciones para la Tarea asociada. Muestra una lista de planificaciones
definidas en la parte superior de la ventana, mientras que abajo muestra la
descripción de la planificación. 
## Nuevo Muestra la ventana de edición de
planificación y agrega una nueva planificación a la lista. 
## Editar Permite editar la planificación
seleccionada. 
## Eliminar Borra la planificación seleccionada. 
## Suspender la ejecución de esta
tarea Ignora la Tarea, por lo que ninguna de las
planificaciones de ésta es tenida en cuenta para ejecución. 
## Edición de las propiedades de la
Planificación Permite definir los parámetros temporales o
de escucha de directorio que hará que la Tarea a la que pertenece se ejecute. 
## Nombre Nombre de la planificación, este debe ser
único dentro de una misma Tarea. 
## Descripción Es la descripción de la planificación, como
"Planificación de los jueves" 
## Ejecutar la Tarea cuando ocurra el
evento temporal Habilita la ejecución de la Tarea en el
momento que se especifica por fecha y hora. 
## Ejecutar la Tarea cuando se
produzcan cambios en el directorio Habilita la ejecución de la Tarea cuando
sea detectado un cambio en un directorio especifico. 
## Ejecución por evento temporal 
## Ocurrencia Permite determinar el día que se ejecutará
la Tarea. Diaria La Tarea se ejecutará todos los días en el
horario especificado. Semanal La Tarea se ejecutará una vez cada n
semanas, todos los día que se establezca. Ej "todos los martes" Ej "todos los lunes cada 2
semanas" Mensual Esta modalidad de ejecución tiene 2 sub
modalidades: De día fijo cada N meses : Ejecutará la
Tarea todos los días n cada m meses Ej: Todos los días 4 cada 3 meses De día variablesemanal : El n día de la
semana indicada cada m meses Ej: El primer lunes de cada semana, cada 2
meses Ej: El ultimo viernes de cada semana, cada
1 meses Ej: El ultimo día no laborable de cada 2
meses Para esta modalidad también pueden
seleccionarse los meses en la que deberá ejecutarse o ignorarse la ejecución. 
## Frecuencia
Diaria Permite establecer, una vez que se ha
determinado que el día de ejecución es hoy, en que momento del día se ejecutará
la Tarea. Las opciones son : Ocurre una vez a las: Permite especificar a que hora se ejecutará
la Tarea especificada. Ej 10:00:00 AM Cada n Horas Permite establecer que la Tarea se
ejecutará cada una hora dentro de una franja horaria establecida por
"comenzando" y "terminando". 
## Duración Permite establecer el rango de fechas en
que la Tarea será considerado para ejecución automática. Comienzo Establece la fecha a partir de la que se
considera la Tarea para ejecución. Finalización Establece la fecha hasta la que se
considerará la Tarea para ejecución. Sin fecha de finalización No establece una fecha tope de finalización
para la Tarea. 
## Ejecutar
la Tarea cuando se produzcan cambios en el directorio Establece el path que será monitoreado para
detectar cambios de cualquier índole en los archivos. No
considera cambio en la estructura de subdirectorios. Monitorea el estado de los archivos en los subdirectorios del
directorio indicado. 
## Permitir
la ejecución inmediata de la Tarea Permite que la ejecución de la Tarea se
produzca apenas se guarda la nueva configuración, de inmediato, sin importar lo
que diga la planificación. De no marcarse esta opción no se producirá
la ejecución de la Tarea hasta que se den las condiciones temporales indicadas. No tiene ningún efecto sobre la ejecución
por escucha de directorio. 
## Propiedades de la tarea 
## Nombre de la Tarea Identifica la Tarea. Debe ser único. 
## Descripción de la Tarea Permite describir brevemente la Tarea. 
## Escribir al registro de aplicación Establece cuando se dejará registro de la
actividad de la Tarea en el servicio de eventos de Windows NT/2000/XP: Nunca Cuando sea exitoso Cuando no sea exitoso Cuando termine 
## Eliminar la tarea una vez ejecutada Borra la Tarea cuando este termine la
ejecución: Nunca Cuando sea exitoso Cuando no sea exitoso Cuando termine 
## Permitir la ejecución simultánea de
esta Tarea Permite establecer si la Tarea correrá más
una instancia a la vez, esto es, suponga que una tarea se ejecuta cada 1 hora, y
cada una de sus ejecuciones demora 4 horas. En un momento puede darse que la misma tarea esté
corriendo 3 instancias simultáneas, con la consecuente caída de los recursos
del equipo y los problemas de sincronización. Para evitar esta situación, esta
opción debe dejarse en blanco. Cuando se permite la ejecución simultánea,
comenzará una nueva instancia de la tarea cada vez que se produzca el evento
temporal o de escucha de directorio. 
## Iniciar sesión en el Sistema de
Gestión Especifica si debe iniciarse una sesión en
el sistema de gestión. Si no va a utilizarse nada relacionado con reportes,
registraciones, wizards o tablas, puede blanquear esta opción, hará que la
tarea se inicie más rápidamente y consuma menos recursos. Además cada vez que
se ejecuta una tarea, se consume una licencia del Sistema de Gestión y de la
base de datos SQL Server. 
## Nombre Nombre de usuario del sistema de gestión
con el que se ejecutará la tarea. Este debe tener derechos, para la operación
que realice, tal como si fuera un usuario utilizando normalmente el sistema de
gestión. 
## Password Contraseña del usuario nombrado en el punto
anterior. 
## Referencia Clases, interfaces y enumeraciones Application cwLWOE.ApplicationTopic Company cwLWOE.CompanyTopic USER cwLWOE.USERTopic Ejemplos Propiedades de la conexión de base de datos CWJMDBPROPERTIESTopic Manipulación de registry CwJMREGOPERATIONTopic Otras referencias File System
Helper CWFSHELPTopic Administrador de reportes para tareas CWRMINTTopic Administrador de procesos para tareas CWTMANBZTopic 
## 
## Ficha
Técnica 
## Clase Application Propiedades Companies cwLWOE.Application.CompaniesTopic 
## Application.Companies Colección de empresas del sistema. Public Property
Companies( _ ByVal sName As String
_ ) As cwLWOE.Company Parámetros sName Nombre de la empresa que desea accederse Valor de
retorno cwLWOE.Company 
## Clase Company Métodos GetObject cwLWOE.Company.GetObjectTopic Propiedades Name cwLWOE.Company.NameTopic 
## Company.GetObject Devuelve un
objeto del tipo solicitado. Public Function
GetObject( _ ByRef sObjectName As
String, _ ByRef eClass As
ObjectManager.ObjectClasses, _ ByRef sOperation As
String _ ) As Object Parámetros sObjectName Nombre del objeto que se solicita, tal como
aparece en las propiedades del arbol del sistema de gestión eClass Clase del objeto que se está solicitando : 5 para obtener un objeto de tipo reporte 6 para obtener un objeto de tipo wizard sOperation No utilizado por ahora, enviar string nulo
"" Valor de
retorno Object 
## Company.Name Nombre de la empresa. Public Property
Name( _ ) As String Valor de
retorno String 
## Clase USER Ofrece las características del usuario
activo en la Company Propiedades ID cwLWOE.USER.IDTopic NAME cwLWOE.USER.NAMETopic Ejemplos ¿Cómo averiguar el código y nombre del
usuario del sistema? JM09ASKFORUSERIDANDNAMETopic 
## USER.ID Devuelve el Código del usuario Actual Public Property ID (_ ) As String. Valor de retorno String. Ejemplos ¿Cómo averiguar el código y nombre del
usuario del sistema? JM09ASKFORUSERIDANDNAMETopic 
## USER.NAME Devuelve el Nombre del usuario actual Public Property NAME(
_ ) As String. Valor de retorno String. Ejemplos ¿Cómo averiguar el código y nombre del
usuario del sistema? 
## Ejemplos 
## ¿Cómo averiguar el código y nombre del
usuario del sistema? El siguiente código muestra como es posible
desde la tarea acceder al objeto User del objeto Company, la cual se obtiene
solicitandolo al objeto Application Option Explicit 'Creación del Objeto Reporte Const cTipoObjeto = 5 'Tipo del objeto que
se intenta crear. A un Reporte le corresponde un 5 Dim oCompany Dim oReport Set oCompany =
oApplication.Companies("EMPRESA") With oCompany Msgbox .User.Id Msgbox .User.Name End With 'Luego se puede
seguir utilizando la company normalmente Set oReport =
oCompany..GetObject(Nombre_Reporte, cTipoObjeto, "") ........... 'Otra opción es MsgBox
oApplication.Companies("EMPRESA").User.ID MsgBox
oApplication.Companies("EMPRESA").User.Name 
## Propiedades de la conexión de base de
datos Este ejemplo muestra como acceder a las
propiedades de la conexión a la base de datos para permitir al usuario
establecer una conexión propia a la base de datos de la empresa. Option Explicit Dim sUser Dim sPassWord Dim Server Dim sDriver Dim
sDatabase 'Siempre asignar el nombre de la empresa
antes de cualquier otra cosa DBProperties.CompanyName =
"EMPRESA" sUser = DBProperties.User 'Devuelve el usuario de la base
de datos sPassWord = DBProperties.PassWord 'Devuelve la password de la base de
datos sDatabase = DBProperties.Database 'Devuelve el nombre de la base de datos sServer = DBProperties.Server 'Devuelve el nombre del servidor de
base de datos sDriver = DBProperties.Driver 'Devuelve el nombre del driver del
servidor de base d e datos 
## Manipulación de
registry Este ejemplo muestra como acceder a
información guardada en la registry local. Option Explicit Dim sPath Dim sValueName Dim sValue Dim sNewValue sPath =
"HKEY_CURRENT_USER\Software\CWA" sKeyValueName =
"CustomValue" sValue =
"SaveMe" 'Guarda el contenido
de sValue RegEdit.SaveRegistrySettings
sPath, sKeyValueName, sValue 'Recupera el contenido
en sNewValue sNewValue = RegEdit.LoadRegistrySettings(sPath,
sKeyValueName, "Default Value") 'sValue vale
"SaveMe" '****************************************************************************** ' Para valores
numéricos '****************************************************************************** Dim lValue Dim lNewValue lValue = 9657 'Guarda el
contenido de lValue RegEdit.SaveRegistrySettings
sPath, sKeyValueName, lValue 'Recupera el contenido
en lNewValue lNewValue = RegEdit.LoadRegistrySettings(sPath,
sKeyValueName, 123) 'lNewValue vale
9567 
## Administrador de procesos para tareas Ofrece clases y métodos que modelan tablas
y procesos. A través de estos objetos es posible
ejecutar procesos del Sistema, Clases, interfaces y enumeraciones SField cwTManBZ.SFieldTopic SFields cwTManBZ.SFieldsTopic SRow cwTManBZ.SRowTopic SRows cwTManBZ.SRowsTopic SStep cwTManBZ.SStepTopic SSteps cwTManBZ.SStepsTopic STable cwTManBZ.STableTopic STableDef cwTManBZ.STableDefTopic SWizard cwTManBZ.SWizardTopic Ejemplos Como ejecutar un proceso desde una tarea. WMJM01Topic Otras referencias File System Helper CWFSHELPTopic CWLWOETopic Administrador de
reportes para tareas CWRMINTTopic 
## Clase SField Clase que representa un campo. Propiedades Caption cwTManBZ.SField.CaptionTopic DataType cwTManBZ.SField.DataTypeTopic Description cwTManBZ.SField.DescriptionTopic Enabled cwTManBZ.SField.EnabledTopic HasDescription cwTManBZ.SField.HasDescriptionTopic Name cwTManBZ.SField.NameTopic Size cwTManBZ.SField.SizeTopic Value cwTManBZ.SField.ValueTopic 
## SField.Caption Titulo del campo. Public Property
Caption( _ ) As String Valor de retorno String 
## SField.DataType Tipo de dato del
campo. Public Property
DataType( _ ) As cwDBHelp.dtDataTypes Valor de
retorno cwDBHelp.dtDataTypes 
## SField.Description Si el campo esta relacionado con otra
tabla, y se le asigno un campo descripción, se puede consultar su valor vía
este método. Public Property
Description( _ ) As String Valor de retorno String Notas Si el campo no esta relacionado con otra
tabla, o si la propiedad HasDescription cwTManBZ.SField.HasDescriptionTopic vale False, se genera un error. 
## SField.Enabled Devuelve si el campo puede o no recibir
datos. Public Property
Enabled( _ ) As Boolean Valor de retorno Boolean Notas Si Enabled vale False, y se intenta asignar
un valor a la propiedad Value cwTManBZ.SField.ValueTopic ,
se produce un error. 
## SField.HasDescription Devuelve si un campo admite o no
descripcion. Public Property
HasDescription( _ ) As Boolean Valor de retorno Boolean 
## SField.Name Devuelve el nombre del campo. Public Property Name(
_ ) As String Valor de retorno String 
## SField.Size Devuelve la longitud que admite el campo. Public
Property Size( _ ) As Integer Valor de
retorno Integer 
## SField.Value Devuelve o asigna el valor de un campo. Este valor debe ser del tipo de dato adecuado
(es decir, no se le puede asignar el valor "AAA" a un campo numerico,
por ejemplo) Cuando se asigna el valor a un campo, el
Sistema verifica que sea del tipo de dato adecuado, y que cumpla con lo
requisitos basicos (longitud, formato). Asimismo, si el campo esta relacionado
con otra tabla, verifica qiue el valor exista. Si alguna de estas condiciones
no se cumple, se produce un error. Public
Property Value( _ ) As Variant Valor de
retorno Variant 
## Clase SFields Lista de campos que componen una fila. Métodos Item cwTManBZ.SFields.ItemTopic Propiedades Count cwTManBZ.SFields.CountTopic 
## SFields.Item Devuelve el campo solicitado. Public Function Item(
_ ByRef vIndexKey As
Variant _ ) As cwTManBZ.SField Parámetros vIndexKey Nombre o indice del
campo. Valor de retorno cwTManBZ.SField 
## SFields.Count Cantidad de campos. Public Property
Count( _ ) As Integer Valor de retorno Integer 
## Clase SRow Clase que representa una fila de una tabla. Métodos Fields cwTManBZ.SRow.FieldsTopic Propiedades Number cwTManBZ.SRow.NumberTopic 
## SRow.Fields Lista de campos que componen la fila. Public Function
Fields( _ ) As cwTManBZ.SFields Valor de
retorno cwTManBZ.Sfields 
## SRow.Number Indice de
la fila. Public
Property Number( _ ) As Integer Valor de
retorno Integer 
## Clase SRows Lista de
filas que componen una tabla. Métodos Remove cwTManBZ.SRows.RemoveTopic Add cwTManBZ.SRows.AddTopic Item cwTManBZ.SRows.ItemTopic Test cwTManBZ.SRows.TestTopic Propiedades Count cwTManBZ.SRows.CountTopic MaxRows cwTManBZ.SRows.MaxRowsTopic 
## SRows.Remove Elimina una fila de la tabla. Public Sub Remove( _ ByRef iIndex As
Integer _ ) Parámetros iIndex Indice de la fila a eliminar. Notas Este metodo solo puede ser usado en tablas
de tipo tcItem. 
## SRows.Add Agrega una fila a la tabla. Public Function Add( _ ByRef iIndex As
Integer _ ) As cwTManBZ.SRow Parámetros iIndex Indice de la fila a
agregar. Valor de retorno cwTManBZ.SRow Notas Este metodo solo
puede ser usado en tablas de tipo tcItem. 
## SRows.Item Devuelve la fila solicitada. Public Function Item(
_ ByRef iIndex As
Integer _ ) As cwTManBZ.SRow Parámetros iIndex Indice de la fila. Valor de retorno cwTManBZ.SRow 
## SRows.Test Devuelve la fila
solicitada, si existe. Es similar a Item, solo que no
genera un error si la fila solicitada no existe. Public Function Test(
_ ByRef iIndex As
Integer _ ) As cwTManBZ.SRow Parámetros iIndex Valor de
retorno cwTManBZ.SRow 
## SRows.Count Indica cuantas filas existen actualmente en
la tabla. Public Property
Count( _ ) As Integer Valor de retorno Integer 
## SRows.MaxRows Indica cual es el maximo numero de filas
que se puede agregar a la tabla. Public
Property MaxRows( _ ) As Integer Valor de
retorno Integer 
## Clase SStep Clase que representa un paso del proceso. Propiedades Class cwTManBZ.SStep.ClassTopic Description cwTManBZ.SStep.DescriptionTopic Index cwTManBZ.SStep.IndexTopic Table cwTManBZ.SStep.TableTopic 
## SStep.Class Tipo de tabla. Los valores posibles son tcHeader (0) y
tcItem (1). Public Property Class(
_ ) As cwTMEnum.TableClasses Valor de retorno cwTMEnum.TableClasses 
## SStep.Description Descripción del paso. Public Property
Description( _ ) As String Valor de retorno String Notas Es la misma que aparece en la ventana de
proceso, cuando se ejecuta en modo interactivo. 
## SStep.Index Indice del paso. Indica la posicion que ocupa en la lista de
pasos del proceso. Public
Property Index( _ ) As Integer Valor de
retorno Integer 
## SStep.Table Tabla que agrupa los datos del paso. Public Property Table(
_ ) As cwTManBZ.STable Valor de retorno cwTManBZ.STable 
## Clase SSteps Lista de pasos que componen el proceso. Métodos Item cwTManBZ.SSteps.ItemTopic Propiedades Count cwTManBZ. SSteps.CountTopic 
## SSteps.Item Devuelve el paso solicitado. Public Function Item(
_ ByRef iIndex As
Integer _ ) As cwTManBZ.SStep Parámetros iIndex Indice del paso. Valor de
retorno cwTManBZ.SStep 
## SSteps.Count Cantidad de pasos que componen el proceso. Public Property
Count( _ ) As Integer Valor de retorno Integer 
## Clase STable Clase que representa una tabla. Las tablas pueden ser tipo tcHeader o
tcItem. Las tablas tipo tcHeader admiten una sola fila de datos. En cambio, las
tipo tcItem admiten multiples filas. La cantidad exacta de estas filas depende
del proceso. Métodos Fields cwTManBZ.STable.FieldsTopic Rows cwTManBZ.STable.RowsTopic Propiedades Description cwTManBZ.STable.DescriptionTopic Name cwTManBZ.STable.NameTopic 
## STable.Fields Acceso directo a la coleccion de campos de
la primera fila. Public Function
Fields( _ ) As cwTManBZ.SFields Valor de retorno cwTManBZ.SFields Notas Solo es valido en tablas de tipo tcHeader. 
## STable.Rows Lista de filas que componen la tabla. En una tabla de tipo tcHeader, esta lista contiene
una sola fila. Public Function Rows(
_ ) As cwTManBZ.SRows Valor de retorno cwTManBZ.SRows 
## STable.Description Descripcion de la tabla. Public Property
Description( _ ) As String Valor de retorno String 
## STable.Name Nombre de la tabla. Public Property Name(
_ ) As String Valor de retorno String 
## Clase StableDef Propiedades FieldDefs cwTManBZ.STableDef.FieldDefsTopic Frames cwTManBZ.STableDef.FramesTopic Name cwTManBZ.STableDef.NameTopic 
## STableDef.FieldDefs Public Property
FieldDefs( _ ) As cwTManBZ.SFieldDefs Valor de
retorno cwTManBZ.SFieldDefs 
## STableDef.Frames Public
Property Frames( _ ) As cwTManBZ.SFrames Valor de
retorno cwTManBZ.SFrames 
## STableDef.Name Public Property Name(
_ ) As String Valor de retorno String 
## Case SWizard Clase que representa un proceso. A partir de un SWizard es posible acceder a
los SSteps que lo componen, y realizar operaciones básicas de navegación. Métodos Cancel cwTManBZ.SWizard.CancelTopic Finish cwTManBZ.SWizard.FinishTopic MoveBack cwTManBZ.SWizard.MoveBackTopic MoveNext cwTManBZ.SWizard.MoveNextTopic Propiedades CurrentStep cwTManBZ.SWizard.CurrentStepTopic Description cwTManBZ.SWizard.DescriptionTopic Name cwTManBZ.SWizard.NameTopic State cwTManBZ.SWizard.StateTopic Steps cwTManBZ.SWizard.StepsTopic 
## SWizard.Cancel Cancela el proceso. Public Sub
Cancel( _ ) Notas Luego de ejecutar este metodo, se debe
destruir la referencia al objeto SWizard. Ejemplo 'crear un proceso Set oWizard =
oApplication.Companies("NombreDeLaEmpresa").GetObject("NombreDelProceso",
6, "") 'cancelar su ejecución oWizard.Cancel 'destruirlo Set oWizard = Nothing 
## SWizard.Finish Termina el
proceso. Public Sub
Finish( _ ) Notas Solo puede ser llamado cuando el paso
actual es el ultimo. Ejemplo Set oWizard =
oApplication.Companies("NombreDeLaEmpresa").GetObject("NombreDelProceso",
6, "") oWizard.CurrentStep.Table.Fields("Campo1").Value
= "A" oWizard.MoveNext oWizard.CurrentStep.Table.Fields("Campo2").Value
= "19760611" oWizard.Finish Set oWizard = Nothing 
## SWizard.MoveBack Navega al paso anterior, si es posible. Public Sub
MoveBack( _ ) Notas Solo puede ser llamado cuando el paso
actual no es el primero. 
## SWizard.MoveNext Navega al proximo paso. Para que esta navegacion sea exitosa, todos
los campos requeridos deben estar completos, y sus valores deben ser validos. Public Sub
MoveNext( _ ) Notas No puede ejecutarse cuando el paso actual
es el ultimo. En tal caso, use el metodo Finish. 
## SWizard.CurrentStep Indica cual es el paso actual del proceso. Public Property
CurrentStep( _ ) As cwTManBZ.SStep Valor de retorno cwTManBZ.SStep Objeto de tipos SStep que representa el paso
actual del proceso. Ejemplo Set oWizard =
oApplication.Companies("NombreDeLaEmpresa").GetObject("NombreDelProceso",
6, "") i =
oWizard.CurrentStep.Index ' i vale 1 oWizard.MoveNext i =
oWizard.CurrentStep.Index ' i ahora vale 2 oWizard.Cancel Set oWizard = Nothing 
## SWizard.Description Descripción del proceso. Public Property
Description( _ ) As String Valor de retorno String Notas Esta descripción es la misma que aparece en
el árbol del Sistema. 
## SWizard.Name Nombre del proceso. Public Property Name(
_ ) As String Valor de retorno String 
## SWizard.State Indica cual es el estado actual del
proceso. Los estados posibles son S_NEW, S_IDLE y
S_DEAD.: S_NEW: El proceso esta funcionando, o listo
para funcionar. S_IDLE: El proceso termino correctamente. S_DEAD: Se produjo un error. Public Property State(
_ ) As cwTMEnum.stStates Valor de retorno cwTMEnum.stStates 
## SWizard.Steps Lista de los pasos que componen el proceso. Public Property Steps(
_ ) As cwTManBZ.SSteps Valor de retorno cwTManBZ.SSteps 
## 
## 
## Ejemplo: Como ejecutar
un proceso desde una tarea . Para ejecutar un proceso desde una tarea es
necesario cumplir varios pasos. Primero se debe crear el objeto SWizard.
Para esto, se debe usar el metodo GetObject cwLWOE.Company.GetObjectTopic del objeto Company cwLWOE.CompanyTopic . A
continuación, se muestra un ejemplo con un proceso ficticio. Se asignan valores
a varios campos, se avanza de paso, se agregan dos filas, se modifican sus
valores, y se termina el proceso. ' Se crea un proceso Set oWizard =
oApplication.Companies("NombreDeLaEmpresa").GetObject("NombreDelProceso",
6, "") ' Se asignan valores a dos campos. Notese
que la tabla es de tipo tcHeader oWizard.CurrentStep.Table.Fields("Campo1").Value
= "A" oWizard.CurrentStep.Table.Fields("Campo2").Value
= "19760611" ' Se avanza al paso siguiente. oWizard.MoveNext ' En este caso, la tabla es de tipo tcItem,
por lo que es necesario agregarle filas antes de poder usarlas. With oWizard.CurrentStep.Table ' Se agrega una fila... Set oRow = .Rows.Add(1) ' y se asignan valores a sus campos. oRow.Fields("Campo1").Value = 10.59 oRow.Fields("Campo2").Value = "CODFOR" Set oRow = .Rows.Add(2) oRow.Fields("Campo1").Value = 9.95 oRow.Fields("Campo2").Value
= "MODFOR" End UIT ' Se avanza al paso siguiente. oWizard.MoveNext ' En este paso hay una tabla de tipo
tcItem. El siguiente codigo le asigna el valor ' "S" a el campo
"CampoN", en todas las filas en las cuales el campo esta habilitado. For Each oRow in
oWizard.CurrentStep.Table.Rows If
oRow.Fields("CampoN").Enabled Then oRow.Fields("CampoN").Value = "S" End If Next ' Al ejecutar el metodo finish, el proceso
propiamente dicho se inicia. oWizard.Finish ' Al terminar, se debe destruir el proceso. Set oWizard =
Nothing 
## Administrador de Tareas para Reportes Clases, interfaces y enumeraciones DBFRenderer cwRMInt.DBFRendererTopic GridRenderer cwRMInt.GridRendererTopic HtmlRenderer cwRMInt.HtmlRendererTopic TableRenderer cwRMInt.TableRendererTopic TextRenderer cwRMInt.TextRendererTopic Win32Renderer cwRMInt.Win32RendererTopic Ejemplos Impresión de un reporte sencillo. JM01PRINTREPORTTopic Impresión de un reporte con parámetros. JM02PRINTREPORTPARAMTopic Impresión de un reporte a impresora,
modificando parámetros JM03PRINTOUTPUTPRINTERTopic Impresión de un reporte a archivo de texto JM04PRINTOUTPUTTEXTTopic Impresión de un reporte a archivo de HTML JM05PRINTOUTPUTHTMTopic Impresión de un reporte a archivo de
dBaseIII JM06PRINTOUTPUTdBaseIIITopic Generación de cubos a partir de reportes JM07PRINTOUTPUTCUBETopic Impresión de un reporte a archivo de texto
y envío del mismo JM08PRINTOUTPUTTEXTMAILTopic Otras referencias File System Helper CWFSHELPTopic CWLWOETopic CWTMANBZTopic 
## Clase DBFRenderer Administrador de
exportación de reportes a formato DBF. Métodos Render cwRMInt.DBFRenderer.RenderTopic Propiedades AutoStart cwRMInt.DBFRenderer.AutoStartTopic FileName cwRMInt.DBFRenderer.FileNameTopic SendMail cwRMInt.DBFRenderer.SendMailTopic 
## DBFRenderer.Render Realizar la exportación del reporte. Public Sub
Render( _ ) 
## DBFRenderer.AutoStart Abrir el archivo luego de exportar (no
aplicable al ). Public Property AutoStart( _ ) As Boolean Valor de retorno Boolean 
## DBFRenderer.FileName Path y nombre del archivo dBaseIII a
generar. Public Property FileName( _ ) As String Valor de
retorno String 
## DBFRenderer.SendMail Enviar un mail al terminar (no aplicable al
). Public Property
SendMail( _ ) As Boolean Valor de retorno Boolean 
## Clase GridRenderer Administrador de
exportación de reportes a formato planilla. Métodos DirectRender cwRMInt.GridRenderer.DirectRenderTopic Render cwRMInt.GridRenderer.RenderTopic 
## GridRenderer.DirectRender Public Sub
DirectRender( _ ) 
## GridRenderer.Render Realizar la exportación del reporte. Public Sub Render( _ ) 
## Clase HtmlRenderer Administrador de exportación de reportes a
formato HTML. Métodos Render cwRMInt.HtmlRenderer.RenderTopic Propiedades AutoStart cwRMInt.HtmlRenderer.AutoStartTopic FileName cwRMInt.HtmlRenderer.FileNameTopic SendMail cwRMInt.HtmlRenderer.SendMailTopic 
## HtmlRenderer.Render Realizar la exportación del reporte. Public Sub
Render( _ ) 
## HtmlRenderer.AutoStart Abrir el archivo luego de exportar (no
aplicable al ). Public Property
AutoStart( _ ) As Boolean Valor de retorno Boolean 
## HtmlRenderer.FileName Path y nombre del
archivo HTML a generar. Public Property
FileName( _ ) As String Valor de
retorno String 
## HtmlRenderer.SendMail Enviar un mail con el archivo una vez
finalizado (no aplicable al ). Public Property
SendMail( _ ) As Boolean Valor de retorno Boolean 
## Clase TableRenderer Administrador de exportación de reportes a
tablas de Cubos. Métodos Render cwRMInt.TableRenderer.RenderTopic GetLastBatchID cwRMInt.TableRenderer.GetLastBatchIDTopic GetLastBatchIDForNewTables cwRMInt.TableRenderer.GetLastBatchIDForNewTablesTopic VerifyBatchIDExists cwRMInt.TableRenderer.VerifyBatchIDExistsTopic Propiedades AllowRebuildTable cwRMInt.TableRenderer.AllowRebuildTableTopic BatchID cwRMInt.TableRenderer.BatchIDTopic 
## TableRenderer.Render Realizar la exportación del reporte. Public Sub
Render( _ ) 
## TableRenderer.GetLastBatchID Devuelve el último número de lote utilizado
para tablas generadas en la versión anterior a la 224. Public Function
GetLastBatchID( _ ) As Long Valor de retorno Long 
## TableRenderer.GetLastBatchIDForNewTables Devuelve el último número de lote utilizado
para tablas generadas en la versión posterior a la 224. Public Function
GetLastBatchIDForNewTables( _ ) As Long Valor de retorno Long 
## TableRenderer.VerifyBatchIDExists Verifica la existencia de un lote de
proceso. Public Function
VerifyBatchIDExists( _ ByRef lBatchID As Long
_ ) As Boolean Parámetros lBatchID Valor de retorno Boolean 
## TableRenderer.AllowRebuildTable Indica si Permitirá rehacer la tabla en
caso que la estructura de datos existente no coincida con la del reporte que se
está intentando exportar. Public Property
AllowRebuildTable( _ ) As Boolean Valor de retorno Boolean 
## TableRenderer.BatchID Especifica el número de lote de proceso del
cubo. Public Property BatchID( _ ) As Variant Valor de retorno Variant 
## Clase TextRenderer Administrador de exportación de reportes a
formato texto. Métodos Render cwRMInt.TextRenderer.RenderTopic Propiedades AutoStart cwRMInt.TextRenderer.AutoStartTopic ColumnSeparator cwRMInt.TextRenderer.ColumnSeparatorTopic FileName cwRMInt.TextRenderer.FileNameTopic PrintTitles cwRMInt.TextRenderer.PrintTitlesTopic SendMail cwRMInt.TextRenderer.SendMailTopic 
## TextRenderer.Render Realizar la exportación del reporte. Public Sub
Render( _ ) 
## TextRenderer.AutoStart Abrir el archivo luego de exportar (no
aplicable al ). Public Property AutoStart( _ ) As Boolean Valor de retorno Boolean 
## TextRenderer.ColumnSeparator Indica el caracter delimitador de las
columnas. En forma pre determinada se utiliza el caracter AscII 9 (tab). Public Property ColumnSeparator( _ ) As String Valor de retorno String 
## TextRenderer.FileName Path y nombre del archivo de Texto a
generar. Public Property
FileName( _ ) As String Valor de retorno String 
## TextRenderer.PrintTitles Indica si se deben escribir los títulos de
las columnas. Public Property
PrintTitles( _ ) As Boolean Valor de retorno Boolean 
## TextRenderer.SendMail Enviar un mail con el archivo una vez
finalizado. Public Property
SendMail( _ ) As Boolean Valor de retorno Boolean 
## Clase Win32Renderer Administrador de
impresión de reportes a impresora. Métodos Render cwRMInt.Win32Renderer.RenderTopic GetRandomKeyForReportName cwRMInt.Win32Renderer.GetRandomKeyForReportNameTopic Propiedades CompressFile cwRMInt.Win32Renderer.CompressFileTopic Copies cwRMInt.Win32Renderer.CopiesTopic GoToLastPageOnly cwRMInt.Win32Renderer.GoToLastPageOnlyTopic OutputPath cwRMInt.Win32Renderer.OutputPathTopic PageFrom cwRMInt.Win32Renderer.PageFromTopic PageTo cwRMInt.Win32Renderer.PageToTopic PrinterName cwRMInt.Win32Renderer.PrinterNameTopic PrintToFile cwRMInt.Win32Renderer.PrintToFileTopic 
## Win32Renderer.Render Imprime el
reporte. Public Sub
Render( _ ) 
## Win32Renderer.GetRandomKeyForReportName Devuelve un string aleatorio compuesto de
números y letras. Public Function
GetRandomKeyForReportName( _ ByRef Number As
Integer _ ) As String Parámetros Number Valor de
retorno String 
## Win32Renderer.CompressFile Indica que el archivo debe ser comprimido
luego de impreso. En este caso debe tenerse en cuenta cambiar la extensión de
archivo del OutputPath. Public Property CompressFile(
_ ) As Boolean Valor de retorno Boolean 
## Win32Renderer.Copies Establece la cantidad de copias que se
imprimirán de cada página. Public Property Copies( _ ) As Integer Valor de retorno Integer 
## Win32Renderer.GoToLastPageOnly Establece que del reporte se imprimirá
solamente la última página. Public Property
GoToLastPageOnly( _ ) As Boolean Valor de retorno Boolean 
## Win32Renderer.OutputPath Indica el archivo y camino que se utilizará
para la Impresión a archivo. Public Property
OutputPath( _ ) As String Valor de retorno String 
## Win32Renderer.PageFrom Establece la página inicial a partir de la
cual se imprimirá el reporte. Public
Property PageFrom( _ ) As Integer Valor de
retorno Integer 
## Win32Renderer.PageTo Establece la página final hasta la que se
imprimirá el reporte. Public
Property PageTo( _ ) As Integer Valor de
retorno Integer 
## Win32Renderer.PrinterName Indica la impresora que debe ser utilizada
para imprimir el reporte. En caso que se omita esta configuración, el reporte
será impreso en la impresora que tiene asignada. Si no tuviera impresora
asignada, será impreso en la impresora pre determinada de Windows. En caso de impresoras de red, éstas deben
ser nombradas según la convención de nombres UNC Ej:
"\\HOST\PrinterName" Public Property PrinterName( _ ) As String Valor de retorno String 
## Win32Renderer.PrintToFile Establece que se imprimirá a archivo en
lugar del port de impresora pre determinado para la misma. Public Property
PrintToFile( _ ) As Boolean Valor de retorno Boolean 
## 
## Ejemplos 
## Impresión de un reporte sencillo. Este ejemplo muestra los pasos necesarios
para lograr la impresión de un reporte, en forma directa y sencilla. Option Explicit Const CompanyName =
"EMPRESA" 'Constante
que contendrá el nombre de la empresa. Debe ser reemplazado por el nombre de
empresa 'tal como figura en el ABM
de Empresas. Const ReportName =
"STR_MVK_PRO" 'Constante
que contendrá el nombre del reporte tal como figura en las propiedades del
reporte. Const ObjectType = 5 'Constante que indica el
tipo de objeto. Este vale 5 para los reportes Const OutputPrinter = 1 'Constante que indica el tipo
de salida, esta es 1 para impresora. Dim oReport 'Variable Objeto que contendrá el
Reporte en si. Dim oRenderer 'Variable Objeto que contendrá el
componente de pintado del reporte. 'Creación del Objeto Reporte. Set oReport =
oApplication.Companies(CompanyName).GetObject(ReportName, ObjectType,
"") Set oRenderer =
oReport.GetRenderer(OutputPrinter) 'Obtiene un objeto Renderer que maneja las opciones de impresora oRenderer.Render 'Emite el reporte 
## Impresión de un reporte con parámetros. Este ejemplo muestra como ejecutar un
reporte y darle valores a sus parámetros. Option Explicit Const CompanyName = "DESASP" 'Constante que contendrá el nombre
de la empresa. Debe ser reemplazado por el nombre de empresa 'tal como figura en
el ABM de Empresas. Const ReportName =
"SPR_MVH_EST" 'Constante que contendrá el nombre del reporte tal como figura en las
propiedades del reporte. Const ObjectType = 5 'Constante que indica el
tipo de objeto. Este vale 5 para los reportes Const OutputPrinter = 1 'Constante que indica el tipo
de salida, esta es 1 para impresora. Const ParameterName =
"SPRMVI_CODFOR" 'Constante
que contiene el nombre del parámetro. Dim oReport 'Variable Objeto que contendrá el
Reporte en si. Dim oRenderer 'Variable Objeto que contendrá el
componente de pintado del reporte. Dim oParameter 'Variable Objeto que contendrá el
parámetro del reporte. 'Creación del Objeto Reporte Set oReport =
oApplication.Companies(CompanyName).GetObject(ReportName, ObjectType,
"") '*************************************************************************************** '* Parámetros '*************************************************************************************** 'Parámetro Simple 'Forma de asignar
valor a los parámetros oReport.Parameters(ParameterName).Value
= "PE" 'Asigna el valor
"AAAA" al parámetro indicado. 'Forma de asignar
valor a los parámetros de valores múltiples oReport.Parameters(ParameterName).Value(2)
= "BBBB" 'Asigna el valor
"BBBB" a la segunda instancia del parámetro indicado. oReport.Parameters(ParameterName).Value(3)
= "CCCC" 'Asigna el valor
"CCCC" a la tercera instancia del parámetro indicado. 'Forma de asignar valores a rango de
parámetros oReport.Parameters(ParameterName).ValueFrom
= "PE" 'Asigna el valor
"AAAA" al valor desde del parámetro indicado. oReport.Parameters(ParameterName).ValueTo =
"PE" 'Asigna el valor
"ZZZZ" al valor hasta del parámetro indicado. 'Forma de asignar valores a rango de
parámetros con múltiples valores oReport.Parameters(ParameterName).ValueFrom(2)
= "AAAA" 'Asigna el valor "AAAA" al la segunda instancia
del "valor desde" del parámetro indicado. oReport.Parameters(ParameterName).ValueTo(2)
= "ZZZZ" 'Asigna el valor
"ZZZZ" al la segunda instancia del "valor hasta" del
parámetro indicado. 'Parámetros de tipo de dato numérico oReport.Parameters(ParameterName).Value =
325 'Parámetros de tipo de fecha oReport.Parameters(ParameterName).Value
= CVDate("17/01/02") 'Para evitar confusiones con los formatos
de fecha es recomendable utilizar la siguiente forma oReport.Parameters(ParameterName).Value =
DateSerial(2002, 01, 17) 'o en su defecto oReport.Parameters(ParameterName).Value =
20020717 'Es de tipo numérico Set oRenderer = oReport.GetRenderer(OutputPrinter) 'Obtiene un objeto Renderer que maneja
las opciones de impresora oRenderer.PrinterName =
"Impresora" 'Impresora a la que se dirige el reporte oRenderer.Render 'Emite el reporte 
## Impresión de un reporte a impresora, modificando
parámetros Este ejemplo muestra las opciones
disponibles, para los parámetros de impresión de un reporte. Option Explicit Const CompanyName =
"EMPRESA" 'Constante
que contendrá el nombre de la empresa. Debe ser reemplazado por el nombre de
empresa 'tal como figura en el ABM
de Empresas. Const ReportName =
"STR_MVK_PRO" 'Constante que contendrá el nombre del reporte tal como figura en las
propiedades del reporte. Const ObjectType = 5 'Constante que indica el
tipo de objeto. Este vale 5 para los reportes Const OutputPrinter = 1 'Constante que indica el tipo
de salida, esta es 1 para impresora. Dim oReport 'Variable Objeto que contendrá el
Reporte en si. Dim oRenderer 'Variable Objeto que contendrá el
componente de pintado del reporte. 'Creación del Objeto Reporte. Set oReport =
oApplication.Companies(CompanyName).GetObject(ReportName, ObjectType,
"") Set oRenderer =
oReport.GetRenderer(OutputPrinter) 'Obtiene un objeto Renderer que maneja las opciones de impresora 'PrinterName : Indica la impresora que debe
ser utilizada para imprimir el reporte. En caso que se omita esta
configuración, el reporte 'será impreso en la impresora que tiene
asignada. Si no tuviera impresora asignada, será impreso en la impresora pre
determinada de windows. 'En caso de impresoras de Red, estas deben
ser nombradas según la convención de nombres UNC Ej: \\HOST\PrinterName oRenderer.PrinterName = "HP LaserJet
6P" 'Página desde : Establece la página inicial
a partir de la cual se imprimirá el reporte. oRenderer.PageFrom = 1 'Página hasta : Establece la página final
hasta la que se imprimirá el reporte. oRenderer.PageTo = 10 'Cantidad de Copias : Establece la cantidad
de copias que se imprimirán de cada página oRenderer.Copies = 3 'Ir a ultima página : Establece que del
reporte se imprimirá solamente la última página oRenderer.GoToLastPageOnly = True 'Imprimir a archivo : Establece que se
imprimirá a archivo en lugar del port de impresora pre determinado para la
misma. oRenderer.PrintToFile = True 'Path de la impresión a archivo : Indica el
archivo y camino que se utilizará para la Impresión a archivo. oRenderer.OutputPath =
"C:\Test.prn" 'Compresión del archivo : Indica que el
archivo debe ser comprimido luego de impreso. En este caso debe tenerse en
cuenta cambiar la extensión de archivo del OutputPath oRenderer.CompressFile = True 'Obtener clave aleatoria : Devuelve una cadena
con la cantidad de caracteres establecida por el parámetro. Esta cadena se
compone de letras y números. 'Se recomienda su uso para complementar al
nombre de archivo en caso que desee evitarse las repeticiones Dim sKey sKey = oRenderer.GetRandomKeyForReportName(4) 'Devuelve un string compuesto de números y
letras aleatorio. 'Imprime el reporte oRenderer.Render 
## Impresión de un reporte a archivo de texto Este ejemplo muestra las opciones
disponibles que modifican la salida del archivo de texto. Option Explicit Const CompanyName =
"EMPRESA" 'Constante
que contendrá el nombre de la empresa. Debe ser reemplazado por el nombre de
empresa 'tal como figura en el ABM
de Empresas. Const ReportName = "STR_MVK_PRO" 'Constante que contendrá el nombre del
reporte tal como figura en las propiedades del reporte. Const ObjectType = 5 'Constante que indica el
tipo de objeto. Este vale 5 para los reportes Const OutputPrinter = 2 'Constante que indica el tipo de salida, esta es 2 para
archivo de texto. Dim oReport 'Variable Objeto que contendrá el
Reporte en si. Dim oRenderer 'Variable Objeto que contendrá el
componente de pintado del reporte. 'Creación del Objeto Reporte. Set oReport =
oApplication.Companies(CompanyName).GetObject(ReportName, ObjectType,
"") Set oRenderer =
oReport.GetRenderer(OutputPrinter) 'Obtiene un objeto Renderer que maneja las opciones de impresora 'Nombre de Archivo : Path y nombre del
archivo de texto generado oRenderer.FileName =
"C:\Test.txt" 'Impresión de títulos : Indica si se deben
escribir los títulos de las columnas. oRenderer.PrintTitles = Trae 'Separador de columnas : Indica el caracter
delimitador de las columnas. oRenderer.ColumnSeparator = Chr(9) 'En forma pre determinada se separa con
caracter AscII 9 (tab) 'Imprime al archivo de texto oRenderer.Render 
## Impresión de un reporte a archivo de HTML Este ejemplo muestra como exportar un
reporte a un archivo HTML respetando el formato del reporte. Option Explicit Const CompanyName =
"EMPRESA" 'Constante
que contendrá el nombre de la empresa. Debe ser reemplazado por el nombre de
empresa 'tal
como figura en el ABM de Empresas. Const ReportName =
"STR_MVK_PRO" 'Constante que contendrá el nombre del reporte tal como figura en las
propiedades del reporte. Const ObjectType = 5 'Constante que indica el
tipo de objeto. Este vale 5 para los reportes Const OutputPrinter = 3 'Constante que indica el tipo
de salida, esta es 3 para archivo de HTML. Dim oReport 'Variable Objeto que contendrá el
Reporte en si. Dim oRenderer 'Variable Objeto que contendrá el
componente de pintado del reporte. 'Creación del Objeto Reporte. Set oReport =
oApplication.Companies(CompanyName).GetObject(ReportName, ObjectType,
"") Set oRenderer =
oReport.GetRenderer(OutputPrinter) 'Obtiene un objeto Renderer que maneja las opciones de impresora 'Nombre de Archivo : Path y nombre del
archivo HTML generado oRenderer.FileName =
"C:\Test.html" 'Imprime al archivo HTML oRenderer.Render 
## Impresión de un reporte a archivo de dBaseIII Este ejemplo muestra como exportar un
reporte a un archivo HTML respetando el formato del reporte. Option Explicit Const CompanyName =
"EMPRESA" 'Constante
que contendrá el nombre de la empresa. Debe ser reemplazado por el nombre de
empresa 'tal como figura en el ABM
de Empresas. Const ReportName =
"STR_MVK_PRO" 'Constante que contendrá el nombre del reporte tal como figura en las
propiedades del reporte. Const ObjectType = 5 'Constante que indica el
tipo de objeto. Este vale 5 para los reportes Const OutputPrinter = 4 'Constante que indica el tipo
de salida, esta es 4 para archivo de dBaseIII. Dim oReport 'Variable Objeto que contendrá el
Reporte en si. Dim oRenderer 'Variable Objeto que contendrá el
componente de pintado del reporte. 'Creación del Objeto Reporte. Set oReport =
oApplication.Companies(CompanyName).GetObject(ReportName, ObjectType,
"") Set oRenderer =
oReport.GetRenderer(OutputPrinter) 'Obtiene un objeto Renderer que maneja las opciones de impresora 'Nombre de Archivo : Path y nombre del
archivo dBaseIII generado oRenderer.FileName =
"C:\Test.dbf" 'Imprime al archivo dBaseIII oRenderer.Render 
## Generación de cubos a partir de reportes Este ejemplo muestra cómo crear un cubo a
partir de un reporte desde un Job. Option Explicit Const CompanyName =
"EMPRESA" 'Constante
que contendrá el nombre de la empresa. Debe ser reemplazado por el nombre de
empresa 'tal como figura en el ABM
de Empresas. Const ReportName =
"STR_MVK_PRO" 'Constante
que contendrá el nombre del reporte tal como figura en las propiedades del
reporte. Const ObjectType = 5 'Constante que indica el
tipo de objeto. Este vale 5 para los reportes Const OutputPrinter = 5 'Constante que indica el tipo
de salida, esta es 5 para exportación a cubos. Dim oReport 'Variable Objeto que contendrá el
Reporte en si. Dim oRenderer 'Variable Objeto que contendrá el
componente de pintado del reporte. 'Creación del Objeto Reporte. Set oReport =
oApplication.Companies(CompanyName).GetObject(ReportName, ObjectType,
"") Set oRenderer =
oReport.GetRenderer(OutputPrinter) 'Obtiene un objeto Renderer que maneja las opciones de impresora 'Número de lote : Especifica el número de
lote de proceso del cubo oRenderer.BatchID = 1 'Rehacer tabla : Indica si Permitirá
rehacer la tabla en caso que la estructura de datos existente no coincida con
la del reporte que se está intentando exportar. 'Tener en cuenta que rehacer la tabla
implica la perdida de la información contenida hasta el momento por la misma. oRenderer.AllowRebuildTable = True 'Exporta el archivo a Cubo oRenderer.Render 
## Impresión de un reporte a archivo de texto y
envío del mismo Este ejemplo muestra las opciones
disponibles que modifican la salida del archivo de texto. Option Explicit Const CompanyName =
"EMPRESA" 'Constante
que contendrá el nombre de la empresa. Debe ser reemplazado por el nombre de
empresa 'tal
como figura en el ABM de Empresas. Const ReportName =
"STR_MVK_PRO" 'Constante que contendrá el nombre del reporte tal como figura en las
propiedades del reporte. Const ObjectType = 5 'Constante que indica el
tipo de objeto. Este vale 5 para los reportes Const OutputPrinter = 2 'Constante que indica el tipo
de salida, esta es 2 para archivo de texto. Dim oReport 'Variable Objeto que contendrá el
Reporte en si. Dim oRenderer 'Variable Objeto que contendrá el
componente de pintado del reporte. 'Creación del Objeto Reporte. Set oReport =
oApplication.Companies(CompanyName).GetObject(ReportName, ObjectType,
"") Set oRenderer =
oReport.GetRenderer(OutputPrinter) 'Obtiene un objeto Renderer que maneja las opciones de impresora 'Nombre de Archivo : Path y nombre del
archivo de texto generado oRenderer.FileName =
"C:\Test.txt" 'Imprime al archivo de texto oRenderer.Render '****************************************************************************** '* Envío por mail '****************************************************************************** Dim oMapi 'Crea el objeto de mail Set oMapi =
CreateObject("CWMAPI.MAPIOBJECT") 'Se loguea en el servicio de mail con un
usuario y password específicos. Esto es necesario cuando existe más de un
profile configurado o la situación lo requiera, puede variar con los clientes de
mail que se utilicen u otras circunstancias. Normalmente no es necesario incluirla oMapi.LoginSpecificProfile
"USER", "PASSWORD" 'Componer y enviar mail 'Function
ComposeMessage(sRecipAdress, sRecipNames, sMessageSubject, sMessageText,
sCCRecipAdress, sCCRecipNames, sAttachedFiles, NotShowDialog) As Bolean 'Parámetros 'sRecipAdress : Es la dirección de correo
del destinatario. Puede especificarse más de una dirección separándose éstas
por punto y coma (;) 'sRecipNames : Es el nombre del destinatario
tal cual se mostrará en el mensaje cuando llegue a destino. Puede especificarse
más de una nombre separándolos por punto y coma (;) 'sMessageSubject : Es el tema del mensaje 'sMessageText : Es el texto del mensaje 'sCCRecipAdress : Es la dirección de correo del destinatario copiado. Puede
especificarse más de una dirección separándose éstas por punto y coma (;) sCCRecipNames : Es el nombre del
destinatario copiado tal cual se mostrará en el mensaje cuando llegue a
destino. Puede especificarse más de una nombre separándolos por punto y coma
(;) 'sAttachedFiles : Es el path local del o
los archivos adjuntados. En caso de tratarse de más de un archivo, sus paths
deben ser separados por punto y coma (;) 'NotShowDialog : Especifica si debe
mostrarse o no la ventana del mensaje. Mostrar la ventana del mensaje permite
que el usuario lo modifique antes de enviarlo. En Jobs nunca debe mostrarse la
ventana ya que no habrá un usuario para presionar el botón "enviar".
Por lo tanto debe ponerse siempre en "true" 'Ejemplo oMapi.ComposeMessage
"pe@cwanet.com", "Pablo Etcheverry", "Tema del
mensaje", "Cuerpo del mensaje", "pe@cwanet.com",
"Pablo Etcheverry", "C:\test.txt", Trae oMapi.Logoff 'Nota: En caso que las direcciones no estén
bien formadas o no se puedan resolver los nombres se mostrará la ventana de
envío del mensaje para que el usuario tenga oportunidad de corregirlas. En el
caso de Jobs debe tenerse especial cuidado en suministrar las direcciones
correctas. Set oMapi = Nothing 
## File System Helper 
## Referencia Ofrece clases y métodos para trabajar con
archivos y directorios en el módulo de Jobs. En un Job la funcionalidad puede utilizarse
usando los métodos públicos de FileSystemHelper o creando objetos de tipo File cwFSHelp.FileTopic o Folder cwFSHelp.FolderTopic . Clases, interfaces y enumeraciones File cwFSHelp.FileTopic Files cwFSHelp.FilesTopic FileSystemHelper cwFSHelp.FileSystemHelperTopic Folder cwFSHelp.FolderTopic Folders cwFSHelp.FoldersTopic 
## Clase File Clase que permite crear objetos a partir de
un archivo y poder hacer uso de las funcionalidades de ese archivo utilizando
el objeto. Métodos Delete cwFSHelp.File.DeleteTopic Move cwFSHelp.File.MoveTopic Rename cwFSHelp.File.RenameTopic Copy cwFSHelp.File.CopyTopic GetCRC cwFSHelp.File.GetCRCTopic Propiedades CanOpenExclusive cwFSHelp.File.CanOpenExclusiveTopic Extension cwFSHelp.File.ExtensionTopic FullName cwFSHelp.File.FullNameTopic Name cwFSHelp.File.NameTopic Path cwFSHelp.File.PathTopic 
## File.Delete Elimina el archivo asociado al objeto File cwFSHelp.FileTopic . Public Sub Delete( _ ByVal bUseRecycleBin As Boolean _ ) 
## Parámetros bUseRecycleBin Indica de qué manera será eliminado el
archivo. Si el parámetro es Verdadero (True), el archivo es enviado a la
Papelera de Reciclaje (Recycle Bin). Si es Falso (False), es eliminado
definitivamente. 
## 
## Notas Debería eliminarse la referencia del objeto
File o cambiarla a un archivo existente luego de ejecutar este método. Ejemplo Dim oFile 'As File 'Se crea el objeto File relacionándolo con
el archivo Ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Ejemplo.txt") 'Envía el archivo a la Papelera de
Reciclaje (Recycle Bin). oFile.Delete Trae 'Se reusa el objeto File relacionándolo con
el archivo Otro ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Otro ejemplo.txt") 'Elimina el archivo definitivamente, sin
posibilidades de recuperación. oFile.Delete False 
## File.Move Mueve el archivo asociado al objeto File cwFSHelp.FileTopic al nuevo directorio
especificado. Public Sub Move( _ ByVal sNewPath As String _ ) Parámetros sNewPath Nombre del directorio al que será movido el
archivo. Ejemplo Dim oFile 'As File 'Se crea el objeto File relacionándolo con el
archivo Ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Ejemplo.txt") 'Mueve el archivo al directorio Gastos. oFile.Move "C:\Gastos" MsgBox oFile.Path 'Muestra
"C:\Gastos\". 
## File.Rename Renombra el archivo asociado al objeto File cwFSHelp.FileTopic con el nombre
especificado. Public Sub Rename( _ ByVal sNewName As
String _ ) Parámetros sNewName Nuevo nombre que se le asignará al archivo. Ejemplo Dim oFile 'As File 'Se crea el objeto File relacionándolo con el
archivo Ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Ejemplo.txt") 'Se lo renombra como Renombrado.txt. oFile.Rename "Renombrado.txt" MsgBox oFile.FullName 'Muestra
"C:\Renombrado.txt". 
## File.Copy Copia el archivo asociado al objeto File cwFSHelp.FileTopic al nuevo directorio
y nombre especificados. Public Function Copy(
_ ByVal sNewFile As
String _ ) As cwFileSystemHelper.File Parámetros sNewFile Ubicación y nombre del archivo de destino. Valor de retorno cwFileSystemHelper.File Devuelve una referencia a un objeto File cwFSHelp.FileTopic relacionado con el
archivo de destino. Ejemplo Dim oFile1
'As File Dim oFile2
'As File 'Se crea el objeto File relacionándolo con
el archivo Ejemplo.txt Set oFile1 = FileSystemHelper.GetFile("C:\Ejemplo.txt") MsgBox
oFile1.FullName 'Muestra "C:\Ejemplo.txt". 'Copia el archivo al directorio Gastos y
devuelve una referencia a un objeto File relacionado con Copia.txt. Set oFile2 =
oFile1.Copy("C:\Gastos\Copia.txt") MsgBox oFile2.FullName 'Muestra
"C:\Gastos\Copia.txt". 
## 
## File.GetCRC Devuelve una cadena única que identifica al
contenido del archivo asociado al objeto File cwFSHelp.FileTopic . Public Function
GetCRC( _ ) As String Valor de retorno String Ejemplo Dim oFile 'As File 'Se crea el objeto File relacionándolo con
el archivo Ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Ejemplo.txt") MsgBox oFile.GetCRC 'Muestra una cadena
similar a la siguiente: D41D8CD98F00B204E9800998ECF8427E 
## 
## File.CanOpenExclusive Indica si el archivo asociado al objeto File cwFSHelp.FileTopic puede abrirse de
manera exclusiva. Public Property
CanOpenExclusive( _ ) As Boolean Valor de retorno Boolean Ejemplo Dim oFile 'As File 'Se crea el objeto File relacionándolo con
el archivo Ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Ejemplo.txt") MsgBox
oFile.CanOpenExclusive 'Muestra Verdadero (True) o Falso (False). 
## File.Extension Extensión del archivo
asociado al objeto File cwFSHelp.FileTopic . Public Property
Extension( _ ) As String Valor de
retorno String Ejemplo Dim oFile
'As File 'Se crea el objeto File relacionándolo con
el archivo Ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Ejemplo.txt") MsgBox
oFile.Extension 'Muestra "txt". 
## 
## File.FullName Ubicación y nombre del archivo asociado al
objeto File cwFSHelp.FileTopic . Public Property
FullName( _ ) As String Valor de retorno String Ejemplo Dim oFile 'As File 'Se crea el objeto File relacionándolo con
el archivo Ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Ejemplo.txt") MsgBox oFile.FullName 'Muestra
"C:\Ejemplo.txt". 
## File.Name Nombre del archivo asociado al objeto File cwFSHelp.FileTopic . Public Property Name(
_ ) As String Valor de retorno String Ejemplo Dim oFile 'As File 'Se crea el objeto File relacionándolo con
el archivo Ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Ejemplo.txt") MsgBox oFile.Name 'Muestra "Ejemplo.txt". 
## File.Path Directorio en el que se ubica el archivo
asociado al objeto File cwFSHelp.FileTopic . Public Property Path(
_ ) As String Valor de retorno String Ejemplo Dim oFile 'As File 'Se crea el objeto File relacionándolo con
el archivo Ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Ejemplo.txt") MsgBox oFile.Path
'Muestra "C:\". 
## Clase Files Colección de objetos File cwFSHelp.FileTopic . Propiedades Count cwFSHelp.Files.CountTopic Item cwFSHelp.Files.ItemTopic 
## Files.Count Cantidad de objetos File cwFSHelp.FileTopic que se encuentran
en la colección. Public Property Count(
_ ) As Long Valor de retorno Long Ejemplo Dim oFolder 'As Folder Dim oFiles 'As
Files 'Obtiene un
objeto Folder relacionado con el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Informes") Set oFiles =
oFolder.GetFiles("*.*") MsgBox oFiles.Count 'Muestra la cantidad de
objetos File en la colección. 
## Files.Item Objeto File cwFSHelp.FileTopic que se corresponde
con el nombre especificado. Public
Property Item( _ ByRef
sFileName As String _ ) As cwFileSystemHelper.File Parámetros sFileName Nombre del archivo asociado al objeto File cwFSHelp.FileTopic . Valor de retorno cwFileSystemHelper.File Notas La propiedad Item es la propiedad por
defecto del objeto Files, por lo que no es obligatorio escribirla. Ejemplo Dim oFolder
'As Fólder Dim oFiles
'As Files 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Informes") Set oFiles =
oFolder.GetFiles("*.*") MsgBox
oFiles("cwObjMan.sta").FullName '"Muestra
"C:\Informes\cwObjMan.sta". 
## Clase FileSystemHelper Clase global que permite usar todas las
funciones de archivos y directorios sin tener que crear objetos File cwFSHelp.FileTopic o Folder cwFSHelp.FolderTopic . Métodos FileDelete cwFSHelp.FileSystemHelper.FileDeleteTopic FileMove cwFSHelp.FileSystemHelper.FileMoveTopic FileRename cwFSHelp.FileSystemHelper.FileRenameTopic FolderDelete cwFSHelp.FileSystemHelper.FolderDeleteTopic CreateFolder cwFSHelp.FileSystemHelper.CreateFolderTopic FileCanOpenExclusive cwFSHelp.FileSystemHelper.FileCanOpenExclusiveTopic FileCopy cwFSHelp.FileSystemHelper.FileCopyTopic FileExists cwFSHelp.FileSystemHelper.FileExistsTopic FileGetCRC cwFSHelp.FileSystemHelper.FileGetCRCTopic FolderExists cwFSHelp.FileSystemHelper.FolderExistsTopic FolderGetCRC cwFSHelp.FileSystemHelper.FolderGetCRCTopic FolderMake cwFSHelp.FileSystemHelper.FolderMakeTopic GetFile cwFSHelp.FileSystemHelper.GetFileTopic GetFiles cwFSHelp.FileSystemHelper.GetFilesTopic GetFolder cwFSHelp.FileSystemHelper.GetFolderTopic GetSubFolders cwFSHelp.FileSystemHelper.GetSubFoldersTopic NormalizePath cwFSHelp.FileSystemHelper.NormalizePathTopic 
## 
## FileSystemHelper.FileDelete Elimina el archivo especificado pudiendo
enviarlo a la Papelera de Reciclaje o eliminarlo definitivamente. Public Sub FileDelete( _ ByVal sFileName As String, _ ByVal
bUseRecycleBin As Boolean _ ) Parámetros sFileName Nombre del archivo a eliminar. bUseRecycleBin Indica de qué manera será eliminado el archivo.
Si el parámetro es Verdadero (True), el archivo es enviado a la Papelera de
Reciclaje (Recycle Bin). Si es Falso (False), es eliminado definitivamente. Ejemplo 'Envía el archivo Ejemplo.txt a la Papelera
de Reciclaje. FileSystemHelper.FileDelete
"C:\Ejemplo.txt", True 'Elimina Copia.txt
definitivamente. FileSystemHelper.FileDelete
"C:\Copia.txt", True 
## FileSystemHelper.FileMove Mueve el archivo de origen al archivo de
destino. Public Sub FileMove( _ ByVal sFileName As
String, _ ByVal sNewPath As
String _ ) Parámetros sFileName Nombre y ubicación del archivo de origen. sNewPath Nombre del directorio al que será movido el
archivo. Ejemplo 'Mueve el archivo Ejemplo.txt al directorio
Gastos. FileSystemHelper.FileMove
"C:\Ejemplo.txt", "C:\Gastos" 
## FileSystemHelper.FileRename Renombra el archivo de origen con el nombre
especificado. Public Sub FileRename(
_ ByVal sFileName As
String, _ ByVal sNewName As
String _ ) Parámetros sFileName Nombre y ubicación del archivo de origen. sNewName Nuevo nombre que se le asignará al archivo. Ejemplo 'Renombra el archivo Ejemplo.txt como
Renombrado.txt. FileSystemHelper.FileRename
"C:\Ejemplo.txt", "Renombrado.txt" 
## FileSystemHelper.FolderDelete Elimina el directorio especificado pudiendo
enviarlo a la Papelera de Reciclaje o eliminarlo definitivamente. Public Sub FolderDelete( _ ByVal sFullName As String, _ ByVal
bUseRecycleBin As Boolean _ ) Parámetros sFullName Nombre y ubicación del directorio a
eliminar. bUseRecycleBin Indica de qué manera será eliminado el
directorio. Si el parámetro es Verdadero (True), el directorio es enviado a la
Papelera de Reciclaje (Recycle Bin). Si es Falso (False), es eliminado
definitivamente. Ejemplo 'Envía la carpeta Gastos a la Papelera de
Reciclaje (Recycle Bin). FileSystemHelper.FolderDelete
"C:\Gastos", Trae 'Elimina la carpeta Saldos definitivamente. FileSystemHelper.FolderDelete
"C:\Saldos", False 
## FileSystemHelper.CreateFolder Crea un directorio en la ruta especificada. Public Function
CreateFolder( _ ByVal sFullName As
String _ ) As cwFileSystemHelper.Folder Parámetros sFullName Nombre y ubicación del dierctorio a crear. Valor de retorno cwFileSystemHelper.Folder Notas Este método es igual al método FolderMake. Ejemplo Dim oFolder 'As Fólder 'Crea el directorio Ingresos y devuelve una
referencia a un objeto Folder relacionado con el directorio. Set oFolder = FileSystemHelper.CreateFolder("C:\Ingresos") MsgBox
oFolder.FullName 'Muestra "C:\Ingresos". 
## FileSystemHelper.FileCanOpenExclusive Devuelve si un archivo puede ser abierto de
modo exclusivo por alguna aplicación. Public Function
FileCanOpenExclusive( _ ByVal sFileName As
String _ ) As Boolean Parámetros sFileName Nombre del archivo del que se quiere
averiguar si se puede abrir de modo exclusivo. Valor de retorno Boolean Ejemplo 'Muestra Verdadero (True) o Falso (False) indicando
si el archivo puede ser abierto en modo exclusivo. MsgBox
FileSystemHelper.FileCanOpenExclusive("C:\Ejemplo.txt") 
## FileSystemHelper.FileCopy Copia el archivo de origen a la ruta de
destino. Public Function
FileCopy( _ ByVal sFileName As String,
_ ByVal sNewFile As
String _ ) As cwFileSystemHelper.File Parámetros sFileName Nombre y ubicación del archivo de origen. sNewFile Ubicación de la copia del archivo. Valor de retorno cwFileSystemHelper.File Devuelve un objeto File asociado al archivo
recientemente copiado. Ejemplo Dim oFile 'As File 'Copia el archivo Ejemplo.txt a Copia.txt. Set oFile =
FileSystemHelper.FileCopy("C:\Ejemplo.txt", "C:\Copia.txt") MsgBox oFile.FullName 'Muestra
"C:\Copia.txt". 
## FileSystemHelper.FileExists Indica si el archivo
especificado existe. Public Function
FileExists( _ ByVal sFullName As
String _ ) As Boolean Parámetros sFullName Nombre del
archivo a averiguar si existe. Valor de retorno Boolean Ejemplo 'Muestra
Verdadero (True) o Falso (False) indicando si el archivo Ejemplo.txt existe. MsgBox
FileSystemHelper.FileExists("C:\Ejemplo.txt") 
## FileSystemHelper.FileGetCRC Devuelve una
cadena única identificativa del archivo. Public Function FileGetCRC(
_ ByVal sFileName As
String _ ) As String Parámetros sFileName Nombre del archivo a obtener el CRC. Valor de retorno String Ejemplo 'Muestra una cadena de texto similar a la
siguiente: "D41D8CD98F00B204E9800998ECF8427E". MsgBox
FileSystemHelper.FileGetCRC("C:\Ejemplo.txt") 
## 
## FileSystemHelper.FolderExists Indica si el
directorio especificado existe. Public Function
FolderExists( _ ByVal sFullName As
String _ ) As Boolean Parámetros sFullName Nombre del directorio
a averiguar si existe. Valor de retorno Boolean Ejemplo 'Muestra Verdadero
(True) o Falso (False) indicando si la carpeta existe. MsgBox
FileSystemHelper.FolderExists("C:\Saldos") 
## FileSystemHelper.FolderGetCRC Devuelve una cadena única identificativa
del directorio. Public Function
FolderGetCRC( _ ByVal sFullName As
String _ ) As String Parámetros sFullName Nombre del directorio del que se quiere
obtener el CRC. Valor de retorno String Ejemplo 'Muestra una cadena de texto similar a la
siguiente: "D41D8CD98F00B204E9800998ECF8427E". MsgBox
FileSystemHelper.FolderGetCRC("C:\Gastos") 
## FileSystemHelper.FolderMake Crea un directorio en la ruta especificada. Public Function
FolderMake( _ ByVal sFullName As
String _ ) As cwFileSystemHelper.Folder Parámetros sFullName Nombre y ubicación del dierctorio a crear. Valor de retorno cwFileSystemHelper.Folder Notas Este método es igual al método
CreateFolder. Ejemplo Dim oFolder 'As Fólder 'Crea el directorio Ingresos y devuelve una
referencia a un objeto Folder relacionado con el directorio. Set oFolder =
FileSystemHelper.FolderMake("C:\Ingresos") MsgBox
oFolder.FullName 'Muestra "C:\Ingresos". 
## FileSystemHelper.GetFile Devuleve un objeto File cwFSHelp.FileTopic a partir del nombre
de un archivo. Public Function
GetFile( _ ByVal sFullName As
String _ ) As cwFileSystemHelper.File Parámetros sFullName Nombre del archivo al que se quiere enlazar
un objeto File cwFSHelp.FileTopic Valor de retorno cwFileSystemHelper.File Ejemplo Dim oFile 'As File 'Obtiene un archivo File relacionando con
el archivo Ejemplo.txt. Set oFile =
FileSystemHelper.GetFile("C:\Ejemplo.txt") MsgBox oFile.FullName 'Muestra
"C:\Ejemplo.txt". 
## FileSystemHelper.GetFiles Devuelve una colección Files cwFSHelp.FilesTopic a partir de los
archivos de una carpeta. Public Function
GetFiles( _ ByVal sPath As String,
_ Optional ByRef sFilter
As String = *.* _ ) As cwFileSystemHelper.Files Parámetros sPath Nombre del directorio del que se quieren
obtener los archivos. sFilter Filtro a aplicar a los archivos. Valor de retorno cwFileSystemHelper.Files Notas El uso del filtro puede generar resultados
inesperados, porque la búsqueda se realiza tanto en los nombres largos de los
archivos como en los alias (nombre que tiene el formato de DOS, de ocho
caracteres para el nombre y tres para la extensión). Si en el directorio en que se busca existe
un archivo llamado "Nombre largo de archivo.txt", el archivo será
tenido en cuenta cuando el filtro sea "*1.txt" si el alias es
"NOMBRE~1.TXT". Ejemplo Dim oFiles 'As Files 'Devuelve una colección Files con objetos File
asociados a los archivos que cumplen el filtro. Set oFiles =
FileSystemHelper.GetFiles("C:\Gastos", "*.*") MsgBox oFiles.Count 'Muestra la cantidad de
objetos File en la colección. 
## FileSystemHelper.GetFolder Devuleve un objeto Folder cwFSHelp.FolderTopic a partir del
nombre de un directorio. Public Function
GetFolder( _ ByVal sFullName As
String _ ) As cwFileSystemHelper.Folder Parámetros sFullName Nombre del directorio al que se quiere
enlazar un objeto Folder cwFSHelp.FolderTopic Valor de retorno cwFileSystemHelper.Folder Ejemplo Dim oFolder 'As Fólder Devuelve una objeto Folder relacionado con
el directorio Inmuebles. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos\Inmuebles") MsgBox oFolder.Name 'Muestra
"Inmuebles". 
## FileSystemHelper.GetSubFolders Devuelve una colección Folders cwFSHelp.FoldersTopic a partir de los
subdirectorios de una carpeta. Public Function
GetSubFolders( _ ByVal sPath As String,
_ Optional ByRef sFilter
As String = *.* _ ) As
cwFileSystemHelper.Folders Parámetros sPath Nombre del directorio del que se quieren
obtener los subdirectorios. sFilter Filtro a aplicar a los subdirectorios. Valor de retorno cwFileSystemHelper.Folders Notas El uso del filtro puede generar resultados
inesperados, porque la búsqueda se realiza tanto en los nombres largos de los
archivos como en los alias (nombre que tiene el formato de DOS, de ocho
caracteres para el nombre y tres para la extensión). Si en el directorio en que se busca existe
un directorio llamado "Nombre largo de directorio", el archivo será
tenido en cuenta cuando el filtro sea "*1" si el alias es
"NOMBRE~1". Ejemplo Dim oFolders 'As Folders 'Devuelve una colección Folders con objetos
Folder asociados a los directorios que cumplen el filtro. Set oFolders =
FileSystemHelper.GetSubFolders("C:\Gastos") MsgBox oFolders.Count 'Muestra la cantidad
de objetos Folder en la colección. 
## FileSystemHelper.NormalizePath Agrega una barra invertida al final del
nombre de una archivo de texto si no tiene uno. Public Function
NormalizePath( _ ByVal sPath As String
_ ) As String Parámetros sPath Nombre del directorio al que se desea
agregar la barra invertida. Valor de retorno String Ejemplo 'Muestra "C:\Gastos\". MsgBox
FileSystemHelper.NormalizePath("C:\Gastos") 
## Clase Folder Clase que permite crear objetos a partir de
un directorio y poder hacer uso de las funcionalidades de ese directorio
utilizando el objeto. Métodos Delete cwFSHelp.Folder.DeleteTopic Move cwFSHelp.Folder.MoveTopic Rename cwFSHelp.Folder.RenameTopic Copy cwFSHelp.Folder.CopyTopic GetCRC cwFSHelp.Folder.GetCRCTopic GetFiles cwFSHelp.Folder.GetFilesTopic GetSubFolders cwFSHelp.Folder.GetSubFoldersTopic Propiedades Files cwFSHelp.Folder.FilesTopic FullName cwFSHelp.Folder.FullNameTopic Name cwFSHelp.Folder.NameTopic Path cwFSHelp.Folder.PathTopic SubFolders cwFSHelp.Folder.SubFoldersTopic 
## Folder.Delete Elimina el directorio asociado al objeto Folder cwFSHelp.FolderTopic . Public Sub Delete( _ ByVal bUseRecycleBin As Boolean _ ) Parámetros bUseRecycleBin Indica de qué manera será eliminado el
directorio. Si el parámetro es Verdadero (True), el directorio es enviado a la
Papelera de Reciclaje (Recycle Bin). Si es Falso (False), es eliminado
definitivamente. Notas Debería eliminarse la referencia del objeto
Folder o cambiarla a un directorio existente luego de ejecutar este método. Ejemplo Dim oFolder 'As Fólder 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos") 'Envia el directorio a la Papelera de
Reciclaje. oFolder.Delete True Set oFolder =
FileSystemHelper.GetFolder("C:\New Folder\Gastos") 'Elimina el directorio
definitivamente. oFolder.Delete False 
## Folder.Move Mueve el directorio asociado al objeto Folder cwFSHelp.FolderTopic al nuevo
directorio especificado. Public Sub Move( _ ByVal sNewPath As
String _ ) Parámetros sNewPath Nueva ubicación del directorio. Ejemplo Dim oFolder 'As Fólder 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos") oFolder.Move
"C:\Informes" MsgBox oFolder.FullName
'Muestra "C:\Informes\Gastos" 
## Folder.Rename Renombra el directorio asociado al objeto Folder cwFSHelp.FolderTopic con el nombre
especificado. Public Sub Rename( _ ByVal sNewName As
String _ ) Parámetros sNewName Nuevo nombre de la carpeta. Ejemplo Dim oFolder 'As Fólder 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos\Mudanza") oFolder.Rename "Inmuebles" MsgBox oFolder.Name 'Muestra "Inmuebles". 
## Folder.Copy Copia el directorio asociado al objeto Folder cwFSHelp.FolderTopic al nuevo
directorio especificado. Public Function Copy(
_ ByVal sNewFile As
String _ ) As cwFileSystemHelper.File Parámetros sNewFile Ubicación del directorio de destino. Valor de retorno cwFileSystemHelper.File Ejemplo Dim oFolder1 'As Fólder Dim oFolder2 'As Fólder 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder1 =
FileSystemHelper.GetFolder("C:\New Folder\Gastos") 'Realiza la copia del directorio Gastos al
directorio raíz y devuelve un objeto relacionado con el directorio. Set oFolder2 =
oFolder1.Copy("C:\") MsgBox
oFolder1.FullName 'Muestra "C:\New Folder\Gastos". MsgBox oFolder2.FullName 'Muestra
"C:\Gastos". 
## Folder.GetCRC Devuelve una cadena única que identifica al
contenido del directorio asociado al objeto Folder cwFSHelp.FolderTopic . Public Function
GetCRC( _ ) As String Valor de retorno String Ejemplo Dim oFolder 'As Fólder 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos") MsgBox oFolder.GetCRC 'Muestra una cadena
de texto similar a la siguiente: "533D8241CDAC2686C84215F56349E229". 
## Folder.GetFiles Devuelve una colección de tipo Files cwFSHelp.FilesTopic con todos los
archivos que cumplen con el filtro. Public Function
GetFiles( _ ByVal sFilter As
String _ ) As cwFileSystemHelper.Files Parámetros sFilter Filtro a aplicar a los
archivos del directorio para devolver los que únicamente lo cumplan. Valor de retorno cwFileSystemHelper.Files Notas El uso del filtro puede generar resultados
inesperados, porque la búsqueda se realiza tanto en los nombres largos de los
archivos como en los alias (nombre que tiene el formato de DOS, de ocho
caracteres para el nombre y tres para la extensión). Si en el directorio en que se busca existe
un archivo llamado "Nombre largo de archivo.txt", el archivo será
tenido en cuenta cuando el filtro sea "*1.txt" si el alias es
"NOMBRE~1.TXT". Ejemplo Dim oFolder 'As Fólder Dim oFiles 'As Files 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos") 'Devuelve un objeto Files con la cantidad
de archivos que responden al filtro. Set oFiles =
oFolder.GetFiles("*.txt") MsgBox oFiles.Count 'Muestra la cantidad de
objetos File en la colección. 
## Folder.GetSubFolders Devuelve una colección de tipo Folders cwFSHelp.FoldersTopic con todos los
directorios que cumplen con el filtro. Public Function
GetSubFolders( _ ByVal sFilter As
String _ ) As cwFileSystemHelper.Folders Parámetros sFilter Filtro a aplicar a los
subdirectorios del directorio para devolver los que únicamente lo cumplan. Valor de retorno cwFileSystemHelper.Folders Notas El uso del filtro puede generar resultados
inesperados, porque la búsqueda se realiza tanto en los nombres largos de los
archivos como en los alias (nombre que tiene el formato de DOS, de ocho
caracteres para el nombre y tres para la extensión). Si en el directorio en que se busca existe
un directorio llamado "Nombre largo de directorio", el archivo será
tenido en cuenta cuando el filtro sea "*1" si el alias es
"NOMBRE~1". Ejemplo Dim oFolder 'As Fólder Dim oFolders 'As Folders 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos") 'Devuelve un objeto Folders con la cantidad
de directorios que responden al filtro. Set oFolders =
oFolder.GetSubFolders("*.*") MsgBox oFolders.Count 'Muestra la cantidad
de objetos Folder en la colección. 
## Folder.Files Colección de tipo Files cwFSHelp.FilesTopic que contiene un
objeto File cwFSHelp.FileTopic por cada archivo dentro del directorio asociado al objeto Folder cwFSHelp.FolderTopic . Public Property Files(
_ ) As cwFileSystemHelper.Files Valor de retorno cwFileSystemHelper.Files Ejemplo Dim oFolder 'As
Fólder Dim oFiles 'As
Files 'Obtiene un
objeto Folder relacionado con el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos") 'Devuelve una colección Files con la
cantidad correspondiente al filtro aplicado. Set oFiles =
oFolder.GetFiles("*.*") MsgBox oFiles.Count 'Muestra la cantidad de
objetos File que hay. 
## Folder.FullName Ubicación y nombre del directorio asociado
al objeto Folder cwFSHelp.FolderTopic . Public Property
FullName( _ ) As String Valor de retorno String Ejemplo Dim oFolder 'As Fólder 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos") MsgBox
oFolder.FullName 'Muestra C:\Gastos 
## Folder.Name Nombre del directorio asociado al objeto Folder cwFSHelp.FolderTopic . Public Property Name(
_ ) As String Valor de retorno String Ejemplo Dim oFolder 'As Fólder 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos") MsgBox oFolder.Name
'Muestra "Gastos" 
## Folder.Path Directorio en el que se ubica el directorio
asociado al objeto Folder cwFSHelp.FolderTopic . Public Property Path(
_ ) As String Valor de retorno String Ejemplo Dim oFolder 'As Fólder 'Obtiene un objeto Folder relacionado con
el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos") MsgBox oFolder.Path
'Muestra "C:\" 
## 
## Folder.SubFolders Colección de objetos Folder cwFSHelp.FolderTopic enlazados con los
subdirectorios que se encuentran dentro del directorio del objeto Folder cwFSHelp.FolderTopic . Public Property
SubFolders( _ ) As cwFileSystemHelper.Folders Valor de retorno cwFileSystemHelper.Folders Ejemplo Dim oFolder 'As
Fólder Dim oFolders 'As Folders 'Obtiene un
objeto Folder relacionado con el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Gastos") 'Devuelve una colección Folders asociados a
los archivos que cumplen el filtro. Set oFolders =
oFolder.GetSubFolders("*.*") MsgBox oFolders.Count 'Muestra la cantidad
de objetos Folder en la colección. 
## Clase Folders Colección de objetos Folder cwFSHelp.FolderTopic . Propiedades Count cwFSHelp.Folders.CountTopic Item cwFSHelp.Folders.ItemTopic 
## Folders.Count Cantidad de objetos Folder cwFSHelp.FolderTopic que se encuentran
en la colección. Public Property Count(
_ ) As Long Valor de retorno Long Ejemplo Dim oFolder 'As Folder Dim oFolders 'As
Folders 'Obtiene un objeto
Folder relacionado con el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Informes") Set oFolders =
oFolder.GetSubFolders("*.*") MsgBox oFolders.Count 'Muestra la cantidad
de objetos File en la colección. 
## Folders.Item Objeto Folder cwFSHelp.FolderTopic que se corresponde con el nombre
especificado. Public Property Item( _ ByRef sName As String _ ) As cwFileSystemHelper.Folder Parámetros sName Nombre del directorio asociado al objeto Folder cwFSHelp.FolderTopic . Valor de retorno cwFileSystemHelper.Folder Notas La propiedad Item es la propiedad por
defecto del objeto Folders, por lo que no es obligatorio escribirla. Ejemplo Dim oFolder 'As Folder Dim oFolders 'As
Folders 'Obtiene un
objeto Folder relacionado con el directorio Gastos. Set oFolder =
FileSystemHelper.GetFolder("C:\Informes") Set oFolders =
oFolder.GetSubFolders("*.*") MsgBox
oFolders("Gastos").FullName '"Muestra
"C:\Informes\Gastos".

---

