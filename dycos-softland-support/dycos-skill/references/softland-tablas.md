# Referencia de Tablas y Nomenclatura Softland

## Arquitectura del sistema

Softland es un ERP multiempresa modular. Al instalarse sobre SQL Server crea 4 bases de datos estructurales:
1. Base de datos de la empresa cliente (ej: `DIASOL`, `VIDEOJET`, `GRPBUE`, `capacitacion`)
2. `cwSGcore` (seguridad, perfiles, licencias y usuarios globales)
3. `cwSGCoreIMode`
4. `cwSGModel`

En una misma instancia suelen coexistir bases de producción, bases de testing (`testing_CAC`, `BS AS TESTING`) y bases de plantillas (`Template_2015`). **Siempre anteponer `USE <NombreBase>;` antes de consultar o modificar datos.**

---

## Módulos del sistema

| Código | Módulo |
|--------|--------|
| FC | Facturación |
| ST | Stock |
| CO | Compras |
| VT | Clientes / Ventas |
| CJ | Tesorería |
| PV | Proveedores |
| CG | Contabilidad General |
| GR | Generales |
| SJ | Sueldos y Jornales (Nómina) |
| CB | Conciliación Bancaria |
| CF | Cash Flow |
| CP | Control Presupuestario |
| CT | Costos |
| CV | Facturación de Contratos |
| DD | Diccionario de Datos |
| DG | Impuestos / Padrones |
| DP | Depuraciones |
| EC | E-Commerce |
| EO | Análisis de Gestión Financiera (EOAF) |
| GC | Gestión de Cobranzas |
| GP | Gestión de Proyectos |
| IG | Informes Gerenciales |
| IM | Importaciones |
| IN | Interfaces |
| ME | Mantenimiento de Equipos |
| PD | Producción |
| RH | Recursos Humanos |
| RP | Repartos |
| RV | Activo Fijo |
| SP | Seguimiento de Proyectos |
| TR | Transferencias |
| WA | Autorización |
| WG | Wizard Generator |

---

## Nomenclatura de tablas físicas

Las tablas físicas de Softland tienen exactamente **6 caracteres**, con esta estructura de codificación:

```
[MO][T][DD][P]
 ↑   ↑   ↑  ↑
 │   │   │  └── Pertenencia (H/I/D/G/P/C/Z)
 │   │   └───── Detalle/descripción (2 chars)
 │   └────────── Tipo de tabla (1 char)
 └────────────── Módulo (2 chars)
```

**Ejemplo:** `FCRMVH`
- `FC` = Módulo Facturación
- `R` = Tipo Registración
- `MV` = Movimiento
- `H` = Header (encabezado)

### Tipos de tabla (posición 3)

| Código | Tipo | Descripción |
|--------|------|-------------|
| T | Tablas | Jurisdicciones, Situación IVA, parámetros |
| A | Auxiliares | Tablas temporarias de reportes o interfaces |
| S | Estáticos | Saldos estáticos de cuentas contables |
| R | Registraciones | Toda tabla involucrada en registraciones transaccionales |
| M | Maestros | Clientes, Proveedores, Artículos, Conceptos |
| C | Comprobantes | Conceptos, talonarios, formularios, circuitos |

### Pertenencia (posición 6)

| Código | Pertenencia | Descripción |
|--------|-------------|-------------|
| H | Header | Cabecera / Encabezado del comprobante |
| I | Ítems | Detalle de renglones / cuentas sin dimensión |
| D | Dimensiones | Cabecera de cuentas dimensionadas |
| G | Subcuentas | Detalle de subcuentas dimensionadas |
| C | Cuotas | Fechas y montos de vencimientos financieros |
| P | Percepciones | Detalle impositivo de retenciones/percepciones |
| Z | Series / Lotes | Trazabilidad de números de serie y partidas |

---

## Nomenclatura de campos

- **Campos físicos:** Prefijo de 6 caracteres (nombre de la tabla) + `_` + nombre del campo.
  - Ejemplo: `FCRMVH_NROCTA`, `STRMVZ_SERMOV`, `SJCCOH_FORPLA`.
- **Campos virtuales:** Prefijo `VIRT_` + nombre del campo (calculados en memoria por el cliente).
  - Ejemplo: `VIRT_INDICA`.
- **Tablas de usuario:** Deben comenzar con el prefijo `USR_` (ej. `USR_GRTSEC`, `USR_MAILS`).
- **Campos de usuario:** Llevan el prefijo `USR_` (ej. `USR_VTMCLC_CODPOS`).

---

## Tablas verificadas de los 8 módulos críticos

A continuación se detallan las tablas físicas reales comprobadas en auditoría técnica de tickets, sus claves primarias y campos operativos críticos.

---

### 1. Sueldos y Jornales (`SJ`)

Módulo de nómina, liquidación de haberes y presentación de libros legales (AFIP LSD, Decreto 407/2026).

| Tabla | Tipo | Descripción y Claves | Campos Críticos |
|---|---|---|---|
| `SJCCOH` | Maestro | Catálogo global de conceptos de sueldo. **Nota:** No tiene `CODEMP` (maestro global de la base). | `CODCPT` (PK), `DESCRP`, `TIPCPT` (1=Remunerativo, 2=No remunerativo, 3=Descuento, 4=Aporte patronal), `CLACPT` (clase), `FORPLA` (fórmula histórica, **tipo TEXT: requiere `CAST`**), `DEBAJA` ('S'/'N'). |
| `SJCCOI` | Detalle | Habilitación de conceptos por tipo de liquidación. | `CODCPT`, `CODLIQ` (1=1ra quincena, 2=2da quincena, M=Mensual, A=Aguinaldo 1, B=Aguinaldo 2, D=Vacaciones, V=Especial), `HABILI` ('S'/'N'). |
| `SJTLIH` | Cabecera | Cabecera de definición de Libros de Sueldos (Libro `RECIBO`, Libro `LSD`, `SICOSS`). | `CODLIB` (PK), `DESCRP`, `TIPLIB`. |
| `SJTLIP` | Detalle | Párrafos / Renglones del Libro. Estructura jerárquica. | `CODLIB`, `NORDEN` (PK múltiple). **Convención:** múltiplos de 10 (10, 20, 30...) son Títulos; el resto son Subtítulos (11, 12: Empleador/Empleado). `TITULO`, `SUBTIT`, `ZONREP`. |
| `SJTLIC` | Detalle | Asignación de conceptos a renglones de Libro. | `CODLIB`, `NORDEN`, `CODCPT`. **Regla:** En Libro `RECIBO`, la fila terminada en 0 DEBE contener todos los conceptos para totalizar títulos y alimentar el gráfico de torta en `SJF_MVH_RES`. En Libro `LSD`, la orden 24 no debe tener acumuladores no remunerativos como `99929`. |
| `SJMLGH` | Maestro | Legajos de empleados. | `NROLEG` (PK), `APENOM`, `CUIL`, `FECING`, `FECEGR`, `CODCAT`, `CODSEC`, `DEBAJA`. |
| `SJRMVH` | Header | Cabecera de liquidación emitida. | `CODEMP`, `PERIOD`, `NROLIQ`, `TIPLIQ`, `NROLEG` (PK compuesta), `FECLIQ`, `TOTREM`, `TOTNO`, `TOTRET`, `NETO`. |
| `SJRMVI` | Ítems | Detalle de conceptos liquidados por legajo. | `CODEMP`, `PERIOD`, `NROLIQ`, `TIPLIQ`, `NROLEG`, `CODCPT` (PK), `IMPORT`, `CANTID`, `CALCUL` (fórmula resuelta). |

---

### 2. Ventas y Facturación (`VT` / `FC`)

Módulo transaccional de facturación electrónica (CAE), notas de venta, remitos y cuenta corriente de clientes.

| Tabla | Tipo | Descripción y Claves | Campos Críticos |
|---|---|---|---|
| `FCRMVH` | Header | Registración de Facturación (cabecera). | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR` (PK), `FCHMOV`, `CAE` (código autorización fiscal), `FCHCAE` (vencimiento CAE), `NROASI` (número asiento contable). |
| `FCRMVI` | Ítems | Renglones de facturación. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM` (PK), `ARTCOD`, `CANTID`, `PRECIO`, `NETO`. |
| `FCRMVD` | Dim. | Dimensiones contables de facturación. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM`. |
| `FCRMVG` | Subctas | Subcuentas de facturación. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM`. |
| `VTRMVH` | Header | Registración de Comprobantes de Venta (cabecera cuenta corriente). | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR` (PK), `NROCTA` (cliente), `FCHMOV`, `SUCURS` (punto de venta), `IMPTOT`. **Nota: `VTRMVH_TOTAPL` no existe.** |
| `VTRMVI` | Ítems | Ítems de comprobante de venta. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM`. |
| `VTRMVD` | Dim. | Dimensiones de comprobante de venta. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM`. |
| `VTRMVG` | Subctas | Subcuentas de comprobante de venta. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM`. |
| `VTRMVC` | Cuotas | Vencimientos financieros de comprobante de venta. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `CUOTA` (PK), `FCHVNC`, `IMPORTE`. |
| `VTRMVP` | Percep. | Percepciones impositivas aplicadas. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `CODTRI` (PK), `BASEIM`, `IMPORTE`. |
| `GRCFOR` | Maestro | Formularios y talonarios del sistema. | `CODFOR` (PK), `DESCRP`, `ULTNRO` (último número emitido), `IMPRES` (4=continuo/preimpreso 17 renglones, láser/electrónico=multipágina), `CANREN`, `NOMREP`. |
| `VTCFOR` | Maestro | Autorizaciones y talonarios de venta. | `CODFOR` (PK), `CODCOM`, `SUCURS`, `CODIMP` (código comprobante AFIP/ARCA, ej. 001, 201 MiPyME). |
| `GRCCBF` | Matriz | Asignación de formulario por comprobante y condición IVA. | `MODCOM`, `CODCOM`, `EMPIVA`, `CODFOR`, `CODIMP`. Clave para destrabar errores de facturación MiPyME. |
| `VTROAP` | Registr. | Aplicaciones e imputaciones de comprobantes de clientes. | `MODFOR`, `CODFOR`, `NROFOR` (origen), `APLMOD`, `APLCOD`, `APLNRO` (destino aplicado), `IMPORTE`. Tabla real para verificar aplicaciones antes de borrar comprobantes. |
| `FCTCIH` / `FCTCII` | Circuitos | Circuitos de facturación electrónica. | `CIRCOM` (código circuito), `CIRAPL` (circuito aplicado). |

---

### 3. Stock e Inventarios (`ST`)

Módulo de movimientos de stock, artículos, depósitos, sectores y trazabilidad de series/lotes.

| Tabla | Tipo | Descripción y Claves | Campos Críticos |
|---|---|---|---|
| `STMATH` | Maestro | Catálogo de artículos (cabecera). | `ARTCOD` (PK), `DESCRP`, `UNIMED`, `TIPART`, `DEBAJA` ('S'/'N'). |
| `STMATI` | Detalle | Stock y parametrización de artículo por depósito y sector. | `ARTCOD`, `DEPMOV`, `SECMOV` (PK múltiple), `STKACT` (stock actual), `STKMIN`, `STKMAX`. |
| `STRMVH` | Header | Cabecera de movimientos de stock (remitos, ingresos, egresos, ajustes). | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR` (PK), `FCHMOV`, `TIPMOV`. |
| `STRMVI` | Ítems | Renglones de movimiento de stock. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM` (PK), `ARTCOD`, `CANTID`, `DEPMOV`, `SECMOV`. |
| `STRMVZ` | Series | **Trazabilidad de números de serie, lotes y partidas por movimiento.** | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM`, `SERMOV` (PK compuesta), `ARTCOD`, `DEPMOV`, `SECMOV`, `CANTID`, `DESPACHO`. **Clave para prevención de `GR000024`.** |

---

### 4. Compras y Proveedores (`CO` / `PV`)

Módulo de requerimientos de compra, órdenes de compra y facturación de proveedores.

| Tabla | Tipo | Descripción y Claves | Campos Críticos |
|---|---|---|---|
| `CORMVH` | Header | Cabecera de compras y requerimientos. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR` (PK), `NROCTA` (proveedor), `FCHMOV`, `ESTADO`. |
| `CORMVI` | Ítems | Detalle de artículos en compras. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM` (PK), `ARTCOD`, `CANTID`, `PRECIO`, `PENDIE` (saldo remanente pendiente). |
| `CORMVD` | Dim. | Dimensiones contables de compras. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM`. |
| `CORMVG` | Subctas | Subcuentas contables de compras. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM`. |
| `PVRMVH` | Header | Comprobantes y órdenes de pago a proveedores. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR` (PK), `NROCTA`, `FCHMOV`. |

---

### 5. Tesorería (`CJ`)

Módulo de movimientos de fondos, cajas, bancos y cobranzas.

| Tabla | Tipo | Descripción y Claves | Campos Críticos |
|---|---|---|---|
| `CJRMVH` | Header | Movimientos de tesorería y recibos de cobranza (`RC`). | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR` (PK), `FCHMOV`, `IMPTOT`. |
| `CJRMVI` | Ítems | Detalle de valores, cheques, transferencias y retenciones recibidas. | `CODEMP`, `MODFOR`, `CODFOR`, `NROFOR`, `NROITM` (PK), `CODTCO` (tipo de concepto/cartera), `CHEQUE`, `IMPORTE`. |
| `CJRAPL` | Registr. | Aplicaciones de tesorería sobre facturas pendientes. | `MODFOR`, `CODFOR`, `NROFOR`, `APLMOD`, `APLCOD`, `APLNRO`, `IMPORTE`. |

---

### 6. Impuestos y Padrones (`DG`)

Módulo de importación de padrones fiscales (AGIP CABA, ARBA, Tucumán) y alícuotas impositivas.

| Tabla | Tipo | Descripción y Claves | Campos Críticos |
|---|---|---|---|
| `DGHTXT` | Registr. | Tabla física de almacenamiento de padrones fiscales cargados mediante wizards (`10DGPROESTLEGWIZ`). | `FCHDES`, `FCHHAS`, `NRODOC` (CUIT), `TIPRET`, `CODRET`, `TASAIN` (alícuota), `CAMP01` (grupo de riesgo/categoría). |
| `DGMALC` | Maestro | Alícuotas por contribuyente en la base de la empresa. | `NROCTA`, `CODTRI`, `ALICUO`. |
| `GRTTRI` | Tablas | Catálogo general de tributos. | `CODTRI` (PK), `DESCRP`. |
| `GRTTIM` | Tablas | Tipos impositivos (Retención, Percepción, Internos). | `CODTIM` (PK), `DESCRP`. |
| `GRTJUR` | Tablas | Jurisdicciones fiscales provinciales. | `CODJUR` (PK), `DESCRP` (ej. CABA, Buenos Aires, Tucumán). |

---

### 7. Seguridad Global Softland (`cwSGcore`)

Base de datos maestra global del ERP compartida por todas las empresas.

| Tabla | Tipo | Descripción y Claves | Campos Críticos |
|---|---|---|---|
| `CWOMUSERS` | Maestro | Usuarios habilitados en Softland. **Prohibido DELETE físico; siempre baja lógica.** | `CWOMUS_USERID` (PK), `CWOMUS_NOMBRE`, `CWOMUS_DEBAJA` ('S'/'N'), `CWOMUS_FECMOD`, `CWOMUS_ULTOPR` ('M'/'B'). |
| `cwOMObjects` | Tablas | Objetos, menúes y ejecutables del ERP. | `CWOMOB_OBJEID` (PK), `CWOMOB_DESCRP`. |
| `CWOMLINKS` | Enlaces | Relaciones de seguridad y permisos de usuarios sobre objetos. | `CWOMUS_USERID`, `CWOMOB_OBJEID`. |

---

### 8. Motor de Reportes Softland (`CWRM`)

Metadatos de reportes del diseñador (Report Designer / Report Writer).

| Tabla | Tipo | Descripción y Claves | Campos Críticos |
|---|---|---|---|
| `CWRMREPORTS` | Maestro | Catálogo de reportes y plantillas del sistema. | `REPORTID` (PK), `REPORTNAME`, `DESCRIPTION`. |
| `CWRMFIELDS` | Detalle | Definición de columnas y expresiones del reporte. | `REPORTID`, `FIELDNAME`, **columna 4 (Tipo): `0` = evaluado en VBScript cliente (`queryexec`), `1` = evaluado nativamente en el servidor SQL Server.** Prohibido tipo 0 con SQL en reportes de alto volumen. |

---

## Anti-patrones de alucinación frecuentes

Para evitar errores `Msg 208` y `Msg 207` en soporte real, recordar:
- **Tablas inexistentes comunes:** `STMART` (usar `STMATH`), `STMSER` (usar `STRMVZ`), `GRMFOR`/`GRTFOR` (usar `GRCFOR`), `SJEMPH`/`SJMCOH`/`SJCCNH` (usar `SJCCOH`/`SJMLGH`), `GRTNUM` (inexistente).
- **Columnas inexistentes comunes:** `VTRMVH_TOTAPL` (usar tabla `VTROAP`), `VTRMVH_IMPTOT` (usar `VTRMVH_IMPORT`), `SJCCOH_CODEMP` (`SJCCOH` es global sin empresa), `GRCFOR_DESFOR` (usar `GRCFOR_DESCRP`).
