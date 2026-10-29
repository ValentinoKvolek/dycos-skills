# CWA — Seguridad, Usuarios y Administración de Menú

> **Cuándo leer este archivo:** cuando el ticket involucra usuarios, permisos, grupos, derechos, niveles de acceso (1-9), tipos de seguridad (estándar/mixta/integrada), autenticación Windows/SQL, o el usuario ADMIN

---

## [AdministracionDeMenu.htm]

## Administración de Menú 
## Objetivo Este documento explica las
distintas configuraciones de seguridad utilizadas por el Sistema de Gestión, y
los distintos conceptos en la asignación de derechos. 
## Tipos
de usuario Existen
tres tipos de usuario: administrador, usuario normal y usuario con acceso a la
empresa de administración. 
## Usuario
Administrador Los
usuarios de tipos Administrador poseen el control total sobre el Sistema. Que
usuarios cuentan con este derecho depende del tipo de autenticación usado.
Cuando se usa autenticación estándar, solo el usuario ADMIN posee este
derecho. Este usuario no puede ser editado. En cambio, cuando se usa
autenticación mixta o integrada, este derecho puede darse a cualquier usuario. 
## Usuario Normal La mayoría
de los usuarios entran en esta categoría. Los usuarios de este tipo no tienen
derechos intrínsecos, sino que dependen de los derechos asignados. Los usuarios
comunes no pueden acceder a la empresa de Administración. 
## Usuario
con acceso a la empresa de Administración Un usuario
con acceso a la empresa de Administración tiene un acceso prácticamente
irrestricto a la empresa de Administración, y solo a ella. Cuando un usuario
cuenta con este derecho, no puede acceder a otras empresas. Dentro de la propia
empresa de Administración, su única restricción es que no puede modificarse a
si mismo. Este tipo de usuario es práctico si se quiere dar a alguien la
posibilidad de administrar usuarios, grupos, etc., sin permitirle acceder a las
otras empresas. 
## Derechos Existen
dos tipos de derechos: los que se asignan a un objeto, o grupo de objetos
(área) en particular, y los que se refieren a operaciones sobre alguna empresa. 
## Áreas Las áreas
son una forma de agrupar objetos funcionalmente relacionados. Por ejemplo,
todos aquellos objetos que tiene alguna relación con mantenimiento del módulo
de tesorería pertenecen al área
"CJM". Esto simplifica la asignación de derechos. Los
objetos originales del Sistema tienen un área predefinida. Sin embargo, a los
objetos creados por el usuario (tablas, reportes) se les debe asignar un área
en el momento de su creación. 
## Derechos
a un objeto Que un
usuario acceda o no a un objeto, y las operaciones que puede realizar sobre el
depende de los derechos que tenga asignados. Los
derechos pueden asignarse directamente al objeto o al área al que pertenece. Los
derechos se expresan mediante el concepto de "nivel". Este nivel es
un número del 1 al 9. El significado de este número depende del tipo de objeto,
según la tabla a continuación. | Nivel | Tipo de Objeto | Derechos | 1 | Tabla
 (Registración) | Abrir | 2 | Tabla
 (Registración) | Alta | 3 | Tabla
 (Registración) | Modificar | 4 | Tabla
 (Registración) | Borrar | 5 | Tabla
 (Registración) | Alta y
 Modificación | 6 | Tabla
 (Registración) | Alta y Borrado | 7 | Tabla
 (Registración) | Modificación y
 Borrado | 8 | Tabla
 (Registración) | Alta,
 Modificación y Borrado | 1 | Reporte | Ejecutar | 1 | Proceso | Ejecutar | 1 | Cubo | Ejecutar | 9 | Todos | Denegar El caso
del nivel 9 (denegar) es especial. Un objeto con nivel 9 no puede ser accedido
jamás por el usuario. 
## Derechos
a operaciones Existen
dos operaciones que requieren un derecho especial: edición de reportes y
edición de diccionario de datos. Estos derechos se asignan por empresa. Un
usuario Administrador los posee en todas las empresas, y un usuario con acceso
a la empresa de Administración los posee solo en la empresa de Administración. Cuando un
usuario posee derechos de edición de reportes en una empresa, puede modificar
todo reporte, además de crear nuevos y borrar los existentes (siempre y cuando
sean reportes de usuario). Asimismo puede ejecutar todo reporte en la empresa,
sin importar si se le asignaron derechos específicos. El derecho
de edición de diccionario de datos habilita a un usuario a crear tablas,
modificar las existentes y borrar las tablas de usuario. Las tablas que cree
serán accesibles a los demás usuarios, siempre y cuando se les asigne derechos
a ellas. 
## Grupos Los grupos
son una forma de simplificar la asignación de derechos a múltiples usuarios.
Típicamente, en una empresa varios empleados realizan labores similares, y por
lo tanto requieren el mismo nivel de acceso a los mismos objetos en el Sistema.
Si estos usuarios pertenecen todos al mismo grupo, la asignación de derechos se
puede realizar una sola vez, y automáticamente es heredada. Un usuario puede
pertenecer a más de un grupo, con lo que los derechos equivalen a la sumatoria
de todos ellos. 
## Prioridades La
asignación de derechos permite que distintos niveles de acceso a un mismo
objeto existan para determinado usuario. Esta situación se puede dar cuando un
usuario posee derechos un objeto, al área al cual pertenece el objeto, y
pertenece a un grupo que asigna derechos a los mismos. En estos
casos, se toma el derecho más particular. Es decir, tiene más prioridad el
nivel asignado a un objeto que el asignado al área al que pertenece, y tiene
más prioridad los derechos asignados directamente al usuario que los que hereda
por pertenecer a un grupo. En el caso de que un usuario pertenezca a más de un
grupo, y estos grupos asignen distintos niveles a un mismo objeto o área, se
toma el mayor. La única
excepción a esta regla es con el nivel 9 (denegar). Si un objeto recibe un
"denegar" en cualquier nivel no puede ser accedido, por mas que se le
asigne otro nivel de forma más particular. 
## Tipos
de seguridad El Sistema
admite tres tipos de seguridad: estándar, mixta e integrada. 
## Seguridad
estándar Cuando se
utiliza seguridad estándar, el manejo de usuarios es exclusiva responsabilidad
del Sistema. Este se ocupa de almacenar y verificar passwords. Es el método de
seguridad por defecto. Su principal ventaja es la simplicidad. En este
modelo, el único usuario que tiene derechos de administración es el usuario
"ADMIN", que no puede ser removido. 
## Seguridad
mixta Cuando se
utiliza seguridad mixta, el manejo de usuarios es compartido entre el Sistema y
Windows. De esta forma, pueden existir usuarios manejados por el Sistema de
forma similar a cuando se utiliza la seguridad estándar, y además pueden
existir usuarios manejados por Windows. Estos usuarios son usuarios del dominio
que se "mapean" a usuarios del Sistema. A discreción del
Administrador, estos usuarios de Windows pueden autenticarse al Sistema siempre
como usuarios de Windows, siempre como usuarios del Sistema o de ambas formas.
Si un usuario de Windows no existe para el Sistema, se le presenta la opción de
identificarse como un usuario estándar. Para
asignar derechos a un usuario de Windows, se lo debe importar en el Sistema, y
a continuación asignarle derechos de forma similar a la usada con seguridad
estándar. En este
modo de seguridad, cualquier usuario de Windows puede ser promovido a
Administrador. Asimismo, se mantiene la figura del usuario "ADMIN". 
## Seguridad
integrada Cuando se
utiliza la seguridad integrada, la responsabilidad de la verificación de
passwords es exclusivamente de Windows. El Sistema no valida los passwords,
sino que confía en la identificación de los usuarios realizada por el sistema
operativo. En este
modo de seguridad, desaparece el usuario "ADMIN". Los administradores
del Sistema son aquellos a los que se les otorgó específicamente el derecho. 
## Modo
de acceso a la base de datos El Sistema
esta pensado para utilizar seguridad mixta de SQL Server. Para ello, se
almacena información de login en dos lugares: el archivo ObjectManager.ini y en
la base de datos de Administración. En los dos lugares la información se
encuentra encriptada. En el
archivo ObjectManager.ini se guarda la cadena de conexión para acceder a la
empresa de Administración. Esto permite a las terminales verificar passwords,
derechos, y recuperar datos centralizados como la lista de empresas. En la base
de Administración, en cambio, se guarda la información de acceso a cada
empresa. Esta es recuperada por el Sistema al acceder por primera vez a una
empresa en cada sesión. El usuario
de SQL Server que se utiliza para acceder a las bases desde el Sistema debe ser
el usuario "sa" (system administrator) o en su defecto un usuario que
tenga el rol de db_owner sobre las bases a las que accede. De esta forma el
Sistema puede cumplir con todas sus tareas, que en algunos casos (edición del
diccionario de datos, creación de tablas temporarias por razones de
performance, etc.) requieren este derecho.

---

