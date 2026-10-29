# CWA — Arquitectura, Diseño y Conceptos Generales

> **Cuándo leer este archivo:** cuando el ticket refiere a módulos, comprobantes, circuitos, conceptos, estructuras, tablas y parámetros, registración, características generales/funcionales/tecnológicas, o nomenclatura de tablas

---

## [CaracteristicasGenerales.htm]

## Características Generales ERP
(Enterprise Resource Planning). Orientado
a brindar soluciones integradas para la gestión administrativa de un amplio
espectro de empresas. La
arquitectura funcional está basada principalmente en las necesidades y
sugerencias de numerosas y prestigiosas empresas. Empresas que han confiado en
nuestra propuesta y cuya dinámica administrativa se apoya hoy sobre el sistema
de Gestión. Nuestros
clientes, procedentes de las más diversas actividades empresariales, son a
través de sus requerimientos, el motor de crecimiento, la mejora continua y el
desarrollo funcional. Brindar soluciones integradas para la gestión, control y desarrollo de negocios
fue desde el comienzo la especialidad de nuestro producto.

---

## [CaracteristicasFuncionales.htm]

## Características
Funcionales Múltiples idiomas. Posibilidad de definir por puesto de trabajo/usuario el idioma de
 visualización del sistema. Múltiples compañías. Posibilidad de definir múltiples empresas, con opciones de interrelacionar
 datos y parametrización. Múltiples impuestos. Posibilitando rápidamente la adaptación, creación y modificación de los
 mismos SIN necesidad de recurrir a nueva programación o nuevas versiones. Múltiples monedas. Posibilidad de definir múltiples monedas, utilizándolas luego en todo tipo
 de registración, informes, consultas, balances, etc. Herramientas de Diseño. Contamos con un diccionario de datos propio, posibilitando al usuario el
 agregado de nuevas tablas, y nuevos campos a las tablas propias del sistema. Herramientas de Programación. Contamos con herramientas de programación para uso interno del cliente,
 disponibles para desarrollos a medida. Reportes y Consultas. Generador de reportes propio, disponible para uso interno del cliente, con
 la posibilidad de generar consultas y reportes en formato gráfico, Html,
 cubo dinámico, Word â ,
 Excel â , etc. Interfases. Generador de interfases de entrada o salida, orientado a objetos del
 sistema propios o del usuario, capaz de leer y grabar archivos en
 cualquier formato. Objetos OLE (Object linkage and embedding) Posibilidad de asociar objetos OLE (ej: Documentos de Word â o Excel â ) a formularios o a tablas del sistema, pudiéndose visualizar en
 forma automática en cualquier punto del sistema. Administrador de Menú Posibilidad de administrar: a) Derechos de acceso por empresa, usuario o por grupo de usuarios. b) Derechos de operaciones (altas, Bajas, Modificaciones, etc.), por
 empresa, usuario o por grupo de usuarios. c) Pantallas de cualquier objeto, por empresa, usuario o por grupo de
 usuarios. d) Opción de utilización en modo seguridad Integrada. Múltiple Base de Datos Mediante Drivers conexiones ODBC, es posible utilizar distintas bases de
 datos como ser: MS SQL, Oracle, MySql, Progress Sql, etc.

---

## [CaracteristicasTecnologicas.htm]

## Características Tecnológicas Arquitectura 32 bits. Orientado a objetos. Tecnología Client-Server. Tecnología 3-ties (3 capas). Software de base
 propio . Web -Enabled. Lenguajes de programación: C, C++, Visual
 Basic, JavaScript, VBScript, HTML, XSL, XML, SQL.

---

## [ArquitecturayDiseno.htm]

Arquitectura y Diseño Arquitectura y Diseño El sistema de gestión está concebido sobre la base de módulos, como se representa en la siguiente figura:

---

## [ArquitecturadeTablas.htm]

## Arquitectura de tablas 
## Objetivo Normalización
de Tablas del sistema de Gestión. 
## Alcance Funcional Todas las
tablas tendrán un máximo de 6 caracteres que se compondrán de acuerdo a la
siguiente estructura: | Posición | Descripción | | Observaciones | 02 | Módulo | | | 01 | Tipo | | | 03 | Código | 03 | Si tipo es T/M | 02 | Si tipo es distinto de T/M | Clasificación | 01 | Si tipo es distinto de T/M | Tipo | Valores posibles | A | Auxiliares de
 cálculo, liquidación, etc. | C | Comprobantes,
 conceptos, formularios. | M | Maestros | R | Movimientos
 de registración | S | Saldos
 Estáticos | T | Tablas
 asociadas | Código | 03 | VND | Vendedores | ACT | Actividades | JUR | Jurisdicciones | ETC | Etc. | Código | 02 | CB | Comprobantes | MV | Movimientos | CC | Cuentas
 corrientes | Clasificación | 01 | H | Encabezado | I | Items | F | Formularios
 por sit. de IVA Ejemplos: La tabla
en la cual se graban las cuentas corrientes de clientes se llama VTRMVC. La tabla
en la cual se graba el encabezado de las facturas de clientes se llama VTRMVH. La tabla
en la cual se graban los items de las facturas de clientes se llama VTRMVI. La tabla
en la cual se graban los clientes se llama VTMCLH. La tabla
en la cual se graban los vendedores se llama VTTVND.

---

## [Configuracion.htm]

## Configuración El
módulo es la Unidad integral del sistema capaz de funcionar en forma independientemente,
teniendo en cuenta las siguientes consideraciones: | | Def. de Parámetros | Estructuras | Tablas y Parámetros | 
## Formularios | Conceptos | Comprobantes | Estructuras de Cálculo | 
## Circuitos | Generales (GR) | P | P | P | | | P | | | Contabilidad General (CG) | P | | P | | | P | | | Cuentas a Cobrar (VT) | P | P | P | P | P | P | P | | Cuentas a Pagar (PV) | P | P | P | P | P | P | P | | Fact. de Productos (FC) | P | | P | | | P | | P | Fact. de Contratos (CV) | P | | P | | | P | | | Compras (CO) | P | | P | | | P | | P | Tesorería (CJ) | P | P | P | | P | P | | | Sueldos y Jornales (SJ) | P | P | P | | P | P | P | | Recursos Humanos (RH) | P | | P | | | P | | | Control Presupuestario (CP) | P | P | P | | | | | | Informes Gerenciales (IG) | P | P | P | | | | | | Activo Fijo (RV) | P | P | P | | | | | | Conciliación Bancaria (CB) | P | | P | | | P | | | Cash Flow (CF) | P | P | P | | | P | | | Gestión Financiera (EO) | P | P | P | | | | | | Producción (PD) | P | | P | | | P | | P | Costos (CT) | P | | P | | | | | | Inventarios (ST) | P | P | P | P | | P | | | Gestión de Cobranzas (GC) | P | | P | | | P | | | Transferencias (TR) | P | | P | | | | | | Depuraciones (DP) | P | | P | | | | | | Interfases de Entrada (IN) | P | | P | | | | | | Interfases de Salida (IS) | P | | P | | | | | | Soportes Magnéticos (DG) | P | | P | | | | |

---

## [DefiniciondeParametros.htm]

## Definición de Parámetros Todo
módulo tiene características de alta flexibilidad, de ello depende el éxito de
la implementación. Para ello cuenta SIEMPRE con una definición de
parámetros, en la cual se configuran las características globales del mismo.

---

## [Estructuras.htm]

## Estructuras Dependiendo del módulo, es necesario la definición de estructuras, en la cual se define la
máscara de edición y visualización de los elementos principales del módulo. Ej:
Plan de cuentas (cantidad de rubros, cantidad de dígitos por rubro), Clientes,
Proveedores, Legajos, Artículos y Productos, etc.

---

## [EstructurasdeCalculo.htm]

## Estructuras de Cálculo Posibilidad de
establecer estructuras de cálculo con fines Impositivos, Comerciales o Legales. Los módulos que
lo utilizan son Cuentas a Cobrar, Cuentas a Pagar y Liquidación de Sueldos y
Jornales. La estructura de
cálculo se relaciona a través del comprobante, concepto por concepto. Es decir,
según el comprobante que se utilice, se podrá establecer diferentes cálculos
para un mismo concepto. Cualquier
combinación es posible e ilimitada, ya que los parámetros de entorno tienen la
suficiente flexibilidad como para lograrlo. Un claro ejemplo de ello es que la
estructura de cálculo pregunta si el resultado FINAL se sumará o NO en el total
asociado al comprobante. Las estructuras
de cálculo trabajan como cualquier planilla de cálculo. Dicha herramienta se utiliza
comúnmente durante el proceso de implementación para establecer reglas de
negocio, pruebas, mínimos y patrones de cálculo.

---

## [TablasyParametros.htm]

## Tablas y Parámetros Todo módulo
tiene SIEMPRE sus tablas y parámetros propios de definición, en las cuales se
definen las listas o catálogos a utilizar. Cada una de
estas tablas, tiene un rol único y excepcional, que será utilizado en las
transacciones del módulo, o bien formará parte de agrupaciones de las mismas. Ejemplo: Clientes,
condiciones de venta, etc., son tablas a utilizar en las registraciones; categorías,
actividades, son tablas a utilizar por la misma tabla de clientes, mientras que
vendedores será utilizado tanto en la tabla de clientes como vendedor asociado,
siendo posible su visualización y modificación en la facturación.

---

## [Comprobantes.htm]

## Comprobantes Para
efectuar cualquier registración en el sistema, es necesario SIEMPRE , la
definición de los comprobantes. En ellos se definen características de entorno
propios de cada módulo como ser: · Cuentas a Cobrar: Tipo de comprobante (Ventas o Cobranza),
Tipo de registración (Manual o Automática), relación de transferencia hacia la
contabilidad, signo y columna del total (débito o crédito), etc. · Stock: Tipo de comprobante (Ingreso, Egreso, Ajuste o
Transferencia entre depósitos), Tipo de registración (Manual o Automática),
etc. Para
aquellos módulos NO alcanzados por el punto 4, además se deberán definir los
atributos de tipo de numeración, sucursal, reporte de impresión, etc.

---

## [Circuitos.htm]

## Circuitos Con el objetivo de ordenar la empresa,
aparece la figura del circuito. El circuito define los pasos a seguir desde el
inicio y hasta el final de cualquier operación comercial (compra-venta) o de cualquier
proceso productivo. Los módulos que lo utilizan son
Compras, Facturación de productos, Producción. El circuito define pasos y relaciones entre
dichos pasos, por ej. Nota de Pedido / Despacho / Remito / Factura, en esta
definición NO es posible realizar una factura sin antes no haber pasado por la
Nota de Pedido / Despacho / Remito, en ese órden. Cualquier combinación es posible e
ilimitada, ya que los parámetros de entorno tienen la suficiente flexibilidad
como para lograrlo. Un claro ejemplo de ello es que el circuito de facturación,
pregunta sí dicho circuito Actualiza Ventas, Stock, Tesorería y/o Facturación.

---

## [Conceptos.htm]

## Conceptos Con el
objetivo de agrupar características generales, evitar incurrir en errores de
ingreso de datos, simplificar la carga de datos al usuario final, modificar
ciertas definiciones en forma ágil evitando modificaciones GLOBALES y
RIESGOSAS, existe la figura del concepto. El concepto agrupa características de relación como ser: cuenta contable
(evitando que el usuario recuerde y/o ingrese la misma), situación impositiva,
código fiscal para soportes magnéticos, etc. Es requerido para los módulos de Cuentas a Cobrar (incluyendo
Facturación de Productos, Facturación de Contratos y Servicios), Cuentas a
Pagar (incluyendo Compras), Tesorería y Liquidación de Sueldos y Jornales.

---

## [Formularios.htm]

## Formularios Para los
módulos en los cuales la registración de comprobantes intervenga la tabla de
clientes o proveedores, esto es Cuentas a Cobrar, Facturación de Productos,
Facturación de Contratos y Servicios, Cuentas a Pagar, Compras, y Stock, SIEMPRE se deberá definir los formularios de registración y emisión; caso contrario, NUNCA se definirá formularios asociados, ya que la propia definición del comprobante
(6) será el formulario a utilizar. En los
mismos se define el tipo de numeración a utilizar (automática, semi,
renumeración mensual o irrestricta), sucursal a la que pertenece, código de
reporte a utilizar para su impresión, etc.

---

## [Registracion.htm]

## Registración Para todo módulo
de características de registración (*) en la figura 1, es necesario haber
pasado y definido TODOS los puntos sintetizados en CONFIGURACIÓN. La registración
es una única transacción, capaz de actualizar (ya sea modificando o insertando)
datos pertenecientes a la misma, agrupados por módulo que lo generó, código
(formulario o comprobante) y número de transacción, de aquí en adelante
(MODFOR, CODFOR y NROFOR) Cada registración tiene asociada
una tabla de encabezado y posibles tablas de ítems que serán hijas del
encabezado relacionadas a través del MODFOR, CODFOR y NROFOR. Cada
registración es capaz de imprimirse en línea en forma automática o reimprimirse
en forma manual a través del usuario o utilizando la inteligencia del
administrador de tareas. Toda
registración puede terminar en la contabilidad general, en forma agrupada y
ordenada, dependiendo de la definición del comprobante que le dio origen.

---

