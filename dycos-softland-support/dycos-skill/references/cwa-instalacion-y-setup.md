# CWA — Instalación, Setup del Servidor y Diccionario de Datos

> **Cuándo leer este archivo:** cuando el ticket involucra instalación del servidor, configuración inicial de SQL Server (7 o 2000), creación de bases de datos, habilitación del sistema, o el diccionario de datos (tablas de usuario, FillerUsr)

---

## [Setup_1Vez.htm]

## Instalación (Servidor - Primera Vez) 
## Contenido Configuración del Servidor SQL . 1 SQL Server 7 . 1 SQL Server 2000 . 4 Creación de las Bases de Datos . 8 Contenido del CD de la versión . 9 Instalación de SQL Servidor . 10 Carga de estructuras en las bases de empresas . 17 Definición de empresas . 17 
## Configuración del Servidor SQL Para el correcto funcionamiento del
sistema, SQL debe tener configurados algunos parámetros en la forma que se
indica seguidamente. Todos los parámetros o configuraciones que no figuran en
el siguiente detalle pueden ser configurados a gusto del instalador. 
## SQL Server 7 
## Durante la instalación Durante la instalación de SQL, los
parámetros Character Set , Sort Order y Unicode Collation deben mantenerse con los valores por defecto, en la siguiente pantalla se
muestra como quedarían: 
## Seguridad El tipo de seguridad debe ser SQL
Server and Windows NT, es la que se instala por defecto, por tal motivo no hay
que hacer cambios al respecto. Igualmente se puede verificar por la herramienta
Enterprise Manager, accediendo a las propiedades del servidor: 
## Usuario SA El usuario con el cual se va a
acceder a la base de datos (generalmente es el usuario SA) debe tener
definido el idioma Inglés. De acuerdo a la versión de SQL que se instaló puede
que este valor venga definido asi o no. La manera de verificarlo es accediendo
a las propiedades del usuario por la herramienta Enterprise Manager: Este usuario debe ser dbo de
todas las bases que se van a utilizar con nuestro sistema, por tal motivo
generalmente se utiliza el sa. 
## Service Pack Por último se debe tener instalado
Service Pack 3 o superior de SQL Server 7. 
## SQL Server 2000 
## Durante la instalación Durante la instalación de SQL, el
modo de autenticación debe definirse como Mixed Mode (Modo Mixto): El parámetro Server Collation debe
definirse como Dictionary Order, case-insensitive, for use with 1252 Character Set,
en la siguiente pantalla se muestra como quedarían: 
## 
## Seguridad El tipo de seguridad debe ser SQL
Server and Windows, si ya lo definimos así durante la instalación no hay que
hacer cambios al respecto. Igualmente se puede verificar por la herramienta
Enterprise Manager, accediendo a las propiedades del servidor: 
## Usuario SA El
usuario con el cual se va a acceder a la base de datos (generalmente es el
usuario SA) debe tener definido el idioma Inglés. De acuerdo a la versión de
SQL que se instaló puede que este valor venga definido así o no. La manera de
verificarlo es accediendo a las propiedades del usuario por la herramienta
Enterprise Manager: 
## Service Pack Por último se debe tener instalado
Service Pack 2 o superior de SQL Server 2000. 
## Aclaraciones El sistema actualmente no soporta
múltiples instancias de SQL Server 2000, por lo tanto la instalación debe
realizarse en un servidor con una única instancia. 
## Creación de las Bases de Datos Antes de
comenzar con la instalación, deben crearse las bases de datos en SQL Server de
la siguiente manera: | Bases
 de Datos | Archivo
 de Datos | Archivo
 de Log | CWSGCoreModel | CWSGCoreModel_Data | CWSGCoreModel_Log | CWSGModel | CWSGModel_Data | CWSGModel_Log | CWSGCore | CWSGCore_Data | CWSGCore_Log | Emp_Empresa | Emp_Empresa_Data | Emp_Empresa_Log En todas las
bases creadas se deberá setear la opción:  Select
Into Bulk/Copy  si el servidor es
SQL Server 7. Si el servidor es SQL 2000, las bases deben tener el collation name SQL_Latin1_General_CP1_CI_AS , por defecto tendrán
este collation si se siguieron las indicaciones de instalación anteriormente
descriptas. La información que guardará cada base de datos
es la siguiente: CWSGCore: guarda la
información de los usuarios, grupos de usuarios y empresas. Dentro del sistema
esta base se encuentra con el nombre de empresa Administración. CWSGCoreModel: la utiliza el proceso de conversión
de base de datos que veremos mas adelante. CWSGModel: la utiliza el proceso de conversión
de base de datos que veremos mas adelante. Emp_Empresa: es la base que va a guardar toda la
información generada desde el sistema y dentro del mismo se encontrará definido
con el nombre indicado por el usuario. Por cada empresa que se va a utilizar se
necesita crear una base de este tipo. Importante: Al momento de resguardar la información es
indispensable hacer los backups de las bases CWSGCore y Emp_Empresa. 
## 
## Contenido del CD de la versión El CD en el cual se entrega la
versión posee tres carpetas principales: Html :
contiene la presentación del CD. La cual se abre automáticamente al insertar el
mismo. Install : contiene todos los archivos necesarios para la instalación en el
servidor y en las terminales. ServicePack : contiene las últimas actualizaciones del sistema operativo y de
SQL Importante!! No instale desde el CD, es recomendable que
copie el contenido completo de la carpeta Install desde el CD al disco rígido
del servidor, dentro de una carpeta llamada Install y luego renombrarla por el
número de la versión que se está instalando (ej: al renombrar la carpeta Install
por 2.3.00, me quedará en el servidor la siguiente estructura C:\Install\2.3.0) Una vez realizado este
procedimiento, abrir una ventana de DOS, buscar la carpeta Install, entrar en
ella, y ejecutar el siguiente comando para eliminar el atributo de Solo Lectura
a todos los archivos copiados desde el CD: ATTRIB *.* -r /s 
## Instalación de SQL Servidor Para comenzar la instalación del
Servidor, se debe ejecutar el archivo Setup.exe , que se encuentra en el
directorio StradSetup que viene con la versión. De acuerdo al ejemplo que vimos
anteriormente la ruta completa será: C:\Install\2.3.00\StradSetup\Setup.exe Para que la instalación se ejecute
sin problemas debemos estar logueados en el servidor con un usuario
Administrador o en su defecto con un usuario que tenga permisos de
administración local en el servidor. Seleccionar Siguiente. Seleccionar la opción Servidor, y
Siguiente, con este tipo de instalación se instalaran las utilidades necesarias
para el funcionamiento del Servidor del sistema. Los componentes se instalan en dos
carpetas, es recomendable mantener estos valores como vienen por defecto (no
modificar los nombres de estas carpetas, mantener las dos carpetas en la misma unidad
y sobre el directorio raiz ). Se puede modificar la unidad
destino si el servidor tuviera varias. A continuación comenzara la copia
de las utilidades del Servidor, seleccionar Siguiente. El instalador informa que está
descomprimiendo y copiando los archivos necesarios para el resto de la
instalación. El sistema informa que generará la
Carpeta maestra donde las terminales se conectarán para actualizar las
librerías. Nota :
Para mayor información consulte el documento de Actualización Automática de
Librerías. Ingrese el código de cliente y la
sucursal, ambos datos deben ser suministrados por la habilitación. Seleccione Siguiente En esta pantalla debe ingresar un
usuario para que el sistema de licencias del sistema pueda iniciarse en el
servidor. Si el Servidor en donde se esta instalando el sistema de licencias es
un PDC (Controlador de Dominio Primario), o un BDC (Controlador de Domino
Secundario); se debe elegir un usuario del dominio. Si es un Servidor STAND
ALONE, se puede elegir un usuario local del servidor. En ambos casos recuerde que debe
elegir un usuario que pertenezca al grupo de Administradores, y que posea el
derecho de iniciar sesión como servicio. IMPORTANTE !!! Este proceso instala un servicio en Windows y configura un
servidor DCOM, para que este proceso pueda realizarse es necesario desactivar
la política de seguridad Recordar N Contraseñas al momento de la instalación,
si esto no se realiza la aplicación generara un mensaje indicando que no se
puede verificar el par usuario/password. Si la política esta a nivel de
dominio, se debe deshabilitar desde un controlador de dominio y forzar la
propagación de políticas al servidor donde se esta instalando. Recomendamos
esperar aproximadamente 5 minutos a que la política se propague automáticamente
o reiniciar el servidor donde se está instalando el sistema. Es recomendado crear un usuario
independiente. Una vez instalado el sistema de licencias, bajo ninguna
circunstancia cambie el password del usuario que el sistema de licencias
utiliza para iniciarse en el servidor desde el panel de servicios de windows,
si así lo hiciera, puede no volverse a iniciar el servicio de licencias. Para
realizar el cambio de usuario o contraseña configurados para este servicio existe
una opción de menú especialmente creada Software de Gestión Servidor ->
Configuración del Software de Gestión, en la opción de Servicio se puede
modificar el usuario y/o la contraseña de este servicio y se reinstalara con
todos sus valores correctos. Ahora, deberá elegir el tipo de
motor sobre el cual esta instalado el sistema de gestión, el usuario
administrador de SQL, (por lo general SA), y la password si la tuviese. La opción Microsoft SQL Server 7 se
utiliza tanto para los servidores SQL Server 7.0 como también para los
servidores SQL Server 2000. En esta pantalla se realizan las
modificaciones a las bases propias del sistema (CWSGCore, CWSGCoreModel,
CWSGModel). Seleccionar los 3 checks y con el
botón buscar, busque la carpeta SQL Server 7. Este subdirectorio esta dentro de
la versión en el directorio Databases. Para nuestro ejemplo será: C:\Install\2.3.00\Databases\SQL
Server 7 El sistema permite elegir entre 3
distintas formas de seguridad Seguridad Estándar : se mantendrá la figura del ADMIN, como máximo usuario del sistema. Seguridad Mixta : se pede utilizar tanto la seguridad del sistema, como también la
seguridad de NT. Seguridad Integrada : desaparece la figura del ADMIN, y solo se utilizan para entrar al
sistema, los usuarios creados en NT. Si elige seguridad mixta, no puede
volver a seguridad estándar. Y si elige seguridad integrada, no puede volver a
seguridad mixta, ni a seguridad estándar. SE RECOMIENDA INSTALAR SEGURIDAD
ESTANDAR INICIALMENTE!! y luego
consultar con el líder de cuenta sobre el proceso de migración. Este es un
proceso que modifica la estructura de todas las tablas del sistema, que demora
varias horas y que no se puede deshacer automáticamente. Con el botón EXPORTAR, se genera un
archivo, el cual debe ser enviado por mail. Dicho mail será respondido con otro
adjuntando un archivo similar al enviado el cual deberá ser ingresado mas tarde
al sistema. Una vez que se recibió el mail de
respuesta El archivo recibido debe colocarse en
el sistema; con el botón BUSCAR busque el archivo cuyo nombre seguramente es
LICENSE.CWH .Para mas información acerca de la habilitación del sistema,
consulte la documentación habilitación del Sistema de Gestión. Una vez seleccionado, pulse sobre
el botón TERMINAR. Finalizo la instalación del
Servidor, debe reinicializar el sistema. 
## 
## Carga de estructuras en las bases de
empresas A esta altura de la instalación las bases CWSGCore, CWSGCoreModel y
CWSGModel ya tienen sus datos y estructura cargados. Por lo tanto nos quedaría cargar la base Emp_Empresa para poder ser
utilizada desde el sistema. Este procedimiento se realiza mediante la
herramienta Enterprise Manager de SQL. Lo que tenemos que hacer es backupear la
base CWSGModel y restaurarla sobre la base Emp_Empresa (este procedimiento lo
haremos por cada base de empresa creada). Una vez finalizado el restore de la base, tendremos una base sin
movimientos lista para ser utilizada, lo único que nos queda es definirla en
nuestro sistema para poder accederla. 
## Definición
de empresas Ingresar con el usuario ADMIN
(sin contraseña) y seleccionar la empresa llamada ADMINISTRACIÓN Haciendo doble click del mouse sobre la opción de Empresas del sistema se define una
empresa nueva donde debe completar los siguientes datos: · Código de la empresa. · Descripción: nombre de la
empresa. · Servidor: nombre del servidor
SQL donde se encuentra la base de empresa. · Base de datos: nombre de la
base de datos en SQL (ej: Emp_Empresa). · Nombre de usuario: nombre del
usuario SQL con el cual se accederá a la base de empresa. Debe ser dbo de la
base, por tal motivo generalmente se utiliza el SA. · Password: password del
usuario SQL. En esta opción debe dar de alta las empresas creadas. Según
nuestro ejemplo debe crear una empresa cuya base de datos SQL se llama
Emp_Empresa.

---

## [Habilitacion.htm]

## Habilitación del Sistema 
## Objetivo Este documento tiene por objetivo
especificar la forma de instalar CWA SQL Windows en la parte del servidor
(Nueva versión). Para realizar los
pasos de este instructivo es recomendable poseer conocimientos del Sistema de
Gestión. 
## Alcance
Funcional Una vez instalado
el sistema de licencias en el Servidor, si se necesitan agregar mas licencias,
ya sea porque se compraron otros módulos o porque se agregaron mas puestos de
trabajos, se debe volver a habilitar el sistema. Para ello contamos
con un panel de control del sistema de licencia. Para ejecutar este panel de
controles se debe ejecutar el programa que se encuentra en INICIO\ PROGRAMAS\
SISTEMA DE GESTION SERVIDOR\ CONFIGURACIÓN DEL SISTEMA DE GESTION. El panel de
controles posee 4 operaciones diferentes: 1 - Monitor: En
este panel se pueden ver la cantidad de licencias de las que se dispone y la
cantidad de usuarios activos. (Imagen
anterior) 2 - Habilitación:
Desde este panel se puede volver a habilitar el sistema, y para hacerlo es
necesario copiar el código de referencia para luego utilizarlo en nuestra
pagina de habilitaciones (suppot.cwa.com.ar). El proceso en la pagina solicita
código de cliente, clave, sucursal(en general ADMI), y luego el código de
referencia antes copiado. Una vez culminado el proceso en la pagina Web, recibirá un mail en el cual estará adjunto
un archivo, LICENSE.CWH. (Es importante mantener la extensión CWH de este
archivo, de otro modo no será reconocido como un archivo valido por el sistema
de licencias!!) Una vez obtenido el
mail con el correspondiente archivo adjunto LICENSE.CWH; deberá guardar este
archivo en alguna carpeta en el servidor, (Recuerde siempre mantener la extensión del archivo). Luego, con el botón
buscar, selecciones el archivo recibido, y apriete el botón Aceptar. No recibirá ningún mensaje, solo
volverá a ver el panel de control de las licencias. Hecho esto los cambios se
habrán registrado, pudiendo salir del panel de control. 3 - Seguridad: Con
esta opción usted puede cambiar el tipo de seguridad del Sistema de gestión.
Con Seguridad Estándar, la seguridad es manejada exclusivamente por CWA; con
Seguridad Mixta, se puede usar tanto la seguridad proporcionada por CWA, como
la proporcionada por Windows NT; con Seguridad Integrada, la seguridad será
manejada exclusivamente por Windows NT. Importante ¡! Los cambios en la seguridad no son
reversibles, si usted elige Seguridad Mixta, no podrá volver a
seguridad Estándar; y si elige Seguridad Integrada con Windows NT, no
podrá volver a Seguridad Mixta, ni tampoco a Seguridad
Estándar. 4 - Servicio: Esta
opción solo esta disponible a partir de la versión 2.0.0 del Sistema de
Gestión. En este panel, usted puede
cambiar el usuario que es utilizado por el sistema de licencias para funcionar.
No es recomendable hacer modificaciones en este campo, ya que es fundamental
para el funcionamiento de las licencias. Para realizar algún cambio, consulte
primeramente con CWA S.A.

---

## [FillerUsr.htm]

## Diccionario
de Datos 
## Objetivo Posibilidad de
definir nuevos Objetos en el Sistema de gestión. La aplicación
permite: a) Administración
de tablas 1. Creación
de tablas de usuario a. Tablas
independientes Estas tablas son posibles ABMs de usuario. No tienen relación de dependencia contra tablas del sistema sean de usuario o
nativos del sistema. b. Tablas
dependientes (Hijas de...) Estas tablas son hijas de otras tablas (solapas dentro de un ABM), sean de
usuario o nativos del sistema. 2. Agregado
de campos de usuario a una tabla existente Estos campos pueden tener relación de dependencia contra campos de usuario o
campos nativos del sistema. b) Administración
de Procesos 1. Creación
de Procesos (Wizard) de Usuario c) Operaciones
Secundarias 1. Creación
de Tipos de Dato 2. Posicionamiento
de Tablas 3. Regeneración
de Procedimientos almacenados (Stored Procedures) 
## Alcance Funcional El
alcance está dividido en tres opciones principales: 
## Administración de Tablas Creación
de Tablas de Usuario Elementos a definir: · Nombre : debe comenzar con el Prefijo USR_. · Tipo : consta de tres opciones, la principal es
Tabla Física, indica que la tabla que se está creando tiene persistencia en
la base de datos; le segunda opción es Tablas Alias, indica que la nueva
tabla parte de una tabla física existente; la última opción es Tabla virtual,
indica que la tabla no tiene persistencia en la basa de datos · Tabla
Base : se habilita sólo si
la tabla es de tipo Tabla Alias. · Descripción . · Descripción
compacta. · Tabla hija,
indica si tabla depende en jerarquía de otra tabla existente (Tabla de items). · Hija falsa,
se habilita sólo si es Tabla hija, indica que no hereda la clave de su tabla
padre · Tabla, se
habilita sólo si es Tabla hija, indica la tabla de la que depende (Tabla
Padre). · Árbol de la
empresa, si es Tabla hija no se encuentra habilitado ya que hereda esta
propiedad de la tabla padre; indica si se muestra en el menú del sistema de
gestión. · Generador de
reportes, Indica si se puede crear un reporte de esta tabla. · Módulo y
Área, si es Tabla hija no se encuentra habilitado ya que hereda esta
propiedad de la tabla padre; indica la posición de partida de la nueva tabla. o Clase
controladora, El nombre de la clase controladora de Tablas de usuario es
GRWUsrScr.ControllerGRUSCR. · Versión, los
valores posibles son, 3 para recibir un evento de grabación por todas las
tablas del ABM y 4 para recibir un evento de grabación por cada tabla del
ABM. Agregar
campos de usuario a una tabla existente El procedimiento de agregado de
campos en una tabla es el mismo independientemente del tipo de tabla. Elementos a definir: · Nombre, debe
comenzar con el Prefijo USR_; se define directamente en la creación del
campo. · Encabezado,
indica la descripción del campo. · Tipo de
Campo, se define directamente en la creación del campo; Consta de cuatro
opciones, la principal es Normal, indica que el campo tiene persistencia en
base de datos y se muestra en el ABM; la segunda opción es Se graba pero no se
muestra, indica que tiene persistencia y no aparece en el ABM; la tercer
opción es Se muestra pero no se graba, indica que no tiene persistencia pero
aparece en el ABM; la última opción es No se graba ni se muestra, indica que
no tiene persistencia ni se muestra en el ABM. Nota: Las opciones dependen del tipo de tabla. · Tipo de
dato, en este campo se carga el Alias de tipo de dato del campo. · Clave,
indica si es parte de la clave primaria de la tabla, fuerza el campo
Requerido. · Requerido,
Indica si es obligatorio completar este campo. · Sólo
lectura, indica si el campo es editable. · Validable,
sólo se habilita si la tabla tiene Clase controladora asociada; indica si la
modificación de este campo genera un evento de validación para la clase. · Clave
Foránea, indica a con qué tabla y campo, tiene relación. · Descripción,
indica a qué tabla y campo, ilustra. · Normal,
indica que valor por omisión tendrá el campo para el nuevo registro. · Conversión,
indica con que valor se actualizará el campo cuando se convierte la empresa. · Reglas de
validación, la regla de validación está compuesta por un Operador y tanto un
Valor cómo un Campo para hacer la comparación en función del operador
elegido. · Filtro para las
relaciones, en caso de definir que el campo tiene Clave foránea, se puede
extender el filtro para la relación acotando el resultado de la unión. · Máscara,
Indica la tabla y el campo del que se recupera la máscara para el campo. · Se compara
contra otros campos, indica si el filtro para recuperar la máscara se hace
igualando la clave de la tabla de máscaras con campos del mismo registro. · Se compara
contra valores constantes, indica si el filtro para recuperar la máscara se
hace igualando la clave de la tabla de máscaras con valores fijos. · Filtro para
hallar la máscara. 
## Administración de Procesos (Wizard) La
creación de un Wizard consta de los siguientes pasos: Creación
de Wizard La creación de un wizard implica que se agrega un
objeto en el menú del sistema de gestión. Elementos a definir: · Nombre, debe
comenzar con el Prefijo USR_. · Descripción,
es la que aparece en el menú para referenciar al Wizard. · Clase
controladora, El nombre de la clase controladora de Wizards de usuario es
GRWUsrScr.ControllerGRUWIZ · Versión,
debe ser igual a cero (0) · Mostrar
mensajes, indica si al terminar, se muestran mensajes sobre el proceso que se
está realizando o mensajes de error. · Visible,
indica si es visible en el menú, se define que no es visible cuando el wizard
termina volcando datos en un ABM. · Pasos,
haciendo Click derecho sobre la lista de pasos, se despliega un menú contextual
con las opciones Add Step y Delete Step. Add Step, agrega un nuevo paso al
Wizard, haciendo Click sobre el mismo se puede editar el nombre (debe comenzar
con el Prefijo USR_). Delete Step, elimina el campo seleccionado. · Descripción
del Step, en este campo se modifica la descripción del paso seleccionado en la
lista de pasos. Creación
de Tablas de Wizard La creación de Tablas de usuario es
igual a la de tablas normales con las siguientes diferencias: · Nombre. · Wizard,
indica a qué Wizard pertenece la nueva tabla. · Descripción. · Descripción
compacta. · Paso, Indica
qué paso del Wizard ilustra la tabla. 
## Operaciones secundarias Creación
de Tipos de dato Elementos a definir: · Data Type,
debe comenzar con el Prefijo USR_. · Tipo de dato
base, Indica el tipo de dato equivalente en la base de datos. · Cantidad de
caracteres. · Decimales,
sólo se habilita si el Tipo de dato base es de tipo numérico. · Máscara. · Reglas,
indica las reglas de validación; la carga es igual a la que se define en un
campo, con la salvedad de que sólo maneja valores fijos. · Lista de
datos, para definir si el tipo de datos es de tipo lista, se debe presionar el
botón Editar lista y en la nueva ventana definir las claves y sus
descripciones. Posicionamiento
de Tablas El posisionamiento permite indicar el orden de los
campos de una tabla, la posición en referencia a otro campo y ubicar al campo
dentro de un marco (frame). Nota: sólo se pueden posicionar las tablas de tipo
usuario. Regeneración
de Procedimientos almacenados (Stored Procedure) Para regenerar un Stored Procedure, ir a la última
opción del menú Herramientas, la misma despliega un ventana en la que se
puede escoger cual o cuales procedimientos regenerar.

---

