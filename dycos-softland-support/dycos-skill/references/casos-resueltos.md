# Base de Conocimiento de Casos Resueltos — Dycos Softland

Este archivo consolida las **20 fichas técnicas de casos reales y tickets resueltos** por el equipo de soporte técnico de Dycos sobre Softland ERP y SQL Server. Sirve como base de conocimiento de referencia rápida para diagnóstico de problemas recurrentes.

---

## Caso 1: Exportación AFIP LSD / Base 9 LRT abultada por concepto no remunerativo

- **Ticket / Ref:** 0006897
- **Fecha:** Octubre 2026
- **Módulo(s):** `SJ` (Sueldos y Jornales)
- **Tablas clave:** `SJTLIC`, `SJTLIP`, `SJCCOH`, `SJRMVI`
- **Cliente / Entorno:** Diagnóstico y Soluciones S.A. (`DIASOL` / Empresa `01`)

### Síntoma
Al exportar el archivo TXT para AFIP Libro de Sueldo Digital (LSD) mediante el proceso `SAR_LIBSUB`, la Base 9 (LRT / ART) del Formulario F.931 arrojaba una base imponible inflada a $1.334.983,02, arrojando una diferencia insubsanable contra los haberes remunerativos liquidados.

### Causa raíz
En la tabla `SJTLIC` (asociación de conceptos al Libro de Sueldos Digital `LSD`), el renglón de orden 24 (correspondiente a Base 9 LRT) tenía indebidamente asignado el acumulador no remunerativo `99929`. Este acumulador arrastraba automáticamente el concepto `58303` (Horas de Acuerdo), el cual está exento de aportes a la ART según la convención colectiva.

### Solución aplicada
1. Identificación y desvinculación transaccional del acumulador erróneo en `SJTLIC`:
```sql
USE DIASOL;

BEGIN TRAN X1;

-- Verificar la asociación previa en el Libro LSD
SELECT * FROM SJTLIC 
WHERE SJTLIC_CODLIB = 'LSD' AND SJTLIC_NORDEN = 24 AND SJTLIC_CODCPT = '99929';

-- Eliminar el acumulador de la base 9
DELETE FROM SJTLIC 
WHERE SJTLIC_CODLIB = 'LSD' AND SJTLIC_NORDEN = 24 AND SJTLIC_CODCPT = '99929';

COMMIT TRAN X1;
```
2. Regeneración del TXT de AFIP LSD desde Softland, constatando que el importe consolidado coincidió al centavo con la liquidación cerrada.

- **Palabras clave:** `SJTLIC`, `LSD`, `Base 9 LRT`, `AFIP F.931`, `99929`, `58303`, `SAR_LIBSUB`.

---

## Caso 2: Reporte colgado por queries N+1 en VBScript cliente

- **Ticket / Ref:** 0006902
- **Fecha:** Octubre 2026
- **Módulo(s):** Report Designer / `VT` (Ventas)
- **Tablas clave:** `CWRMFIELDS`, `CWRMREPORTS`, `FCRMVH`
- **Cliente / Entorno:** DYS Uruguay

### Síntoma
El reporte de auditoría `USR_TABMAUDI2` (asociado a `USR_REPMAUDI`) tardaba más de 20 minutos o directamente congelaba la estación de trabajo y bloqueaba el proceso de Softland.

### Causa raíz
Al analizar la definición en `CWRMFIELDS`, se descubrió que dos columnas agregadas tenían configurado el Tipo de campo `0`. Este tipo fuerza la ejecución de fórmulas VBScript en el cliente (`queryexec(...)`). Al listar miles de renglones, el cliente ejecutaba más de 6.000 consultas individuales consecutivas a SQL Server para leer cabeceras de `FCRMVH` (patrón destructivo N+1 queries).

### Solución aplicada
1. Modificación del Stored Procedure subyacente `sp_USR_REPMAUDI1` para incorporar directamente los campos requeridos de `FCRMVH` mediante un `LEFT JOIN` indexado en el servidor.
2. Cambio en `CWRMFIELDS` de Tipo `0` (VBScript cliente) a Tipo `1` (SQL nativo):
```sql
USE DYS_UY;

BEGIN TRAN X1;

UPDATE CWRMFIELDS 
SET CWRMFI_TIPO = 1 
WHERE CWRMFI_REPID = 'USR_TABMAUDI2' AND CWRMFI_COLUM IN ('FCRMVH_CAE', 'FCRMVH_FCHCAE');

COMMIT TRAN X1;
```
3. El tiempo de generación del reporte cayó de +20 minutos a 4 segundos.

- **Palabras clave:** `CWRMFIELDS`, `queryexec`, `VBScript`, `N+1 queries`, `USR_TABMAUDI2`, `sp_USR_REPMAUDI1`.

---

## Caso 3: Renovación de Certificados ARCA/AFIP para Facturación CAE

- **Ticket / Ref:** 0006904
- **Fecha:** Octubre 2026
- **Módulo(s):** `FC` (Facturación) / ARCA WSAA
- **Tablas clave:** Parámetros de facturación electrónica
- **Cliente / Entorno:** Diagnóstico y Soluciones S.A. (CUIT 30-70820747-7) y DYS Córdoba (CUIT 30-71516329-9)

### Síntoma
Vencimiento del certificado digital de delegación de servicios ante ARCA/AFIP impidiendo la solicitud de CAE para facturas electrónicas A y B.

### Causa raíz
Expiración del período de validez de 2 años del certificado X.509 en el web service de autenticación (WSAA).

### Solución aplicada
Ejecución del protocolo OpenSSL estandarizado:
1. Generación de clave privada RSA 2048:
   `openssl genrsa -out dys_privada_2026.key 2048`
2. Generación del CSR con Distinguished Name estricto:
   `openssl req -new -key dys_privada_2026.key -subj "/C=AR/O=DIAGNOSTICO Y SOLUCIONES SA/CN=DYS_FACTURACION/serialNumber=CUIT 30708207477" -out dys_pedido.csr`
3. Tramitación del certificado firmado (`dys_cert_2026.crt`) en el portal ARCA mediante Administrador de Certificados Digitales.
4. Validación cruzada de integridad por hash MD5:
   `openssl rsa -noout -modulus -in dys_privada_2026.key | openssl md5`
   `openssl x509 -noout -modulus -in dys_cert_2026.crt | openssl md5`
5. Empaquetado en `.pfx` sin clave:
   `openssl pkcs12 -export -out dys_factura.pfx -inkey dys_privada_2026.key -in dys_cert_2026.crt -passout pass:`
6. Copia al servidor de facturación y reactivación exitosa del servicio de facturación.

- **Palabras clave:** `ARCA`, `AFIP`, `WSAA`, `CAE`, `OpenSSL`, `RSA 2048`, `CSR`, `PFX`.

---

## Caso 4: Corte de remito a 17 líneas rígidas por configuración preimpresa

- **Ticket / Ref:** 0006907
- **Fecha:** Octubre 2026
- **Módulo(s):** `FC` / `VT` / `ST`
- **Tablas clave:** `GRCFOR`, `VTCFOR`
- **Cliente / Entorno:** Videojet (`VIDEOJET`) / Cuenta Unilever

### Síntoma
Al emitir la Nota de Venta de Servicios (`NVS 27386`) con 25 ítems, Softland fraccionaba el comprobante cortando la impresión en el renglón 17 y generando múltiples números de remito innecesarios.

### Causa raíz
En la tabla `GRCFOR`, el talonario `REMVT3` tenía asignado el parámetro `GRCFOR_IMPRES = 4`. En la arquitectura de Softland, el valor `4` corresponde a formularios preimpresos/continuos, forzando un límite inmutable de 17 renglones físicos por hoja.

### Solución aplicada
Actualización controlada del talonario para permitir remitos multipágina continuos:
```sql
USE VIDEOJET;

BEGIN TRAN X1;

SELECT GRCFOR_CODFOR, GRCFOR_DESCRP, GRCFOR_IMPRES, GRCFOR_CANREN 
FROM GRCFOR WHERE GRCFOR_CODFOR = 'REMVT3';

UPDATE GRCFOR 
SET GRCFOR_IMPRES = 1 -- Impresión estándar / láser multipágina
WHERE GRCFOR_CODFOR = 'REMVT3';

COMMIT TRAN X1;
```
La reemisión de la NVS 27386 se procesó en un único comprobante multipágina sin fraccionar el remito.

- **Palabras clave:** `GRCFOR`, `GRCFOR_IMPRES`, `REMVT3`, `NVS`, `17 renglones`, `formulario continuo`.

---

## Caso 5: Baja lógica segura de usuarios en base de seguridad cwSGcore

- **Ticket / Ref:** 0006910
- **Fecha:** Octubre 2026
- **Módulo(s):** `cwSGcore` (Seguridad Softland)
- **Tablas clave:** `CWOMUSERS`, `CWOMLINKS`
- **Cliente / Entorno:** Videojet

### Síntoma
Solicitud formal del cliente para dar de baja definitiva a los usuarios de Softland `CMARTINEZ` y `CSALGADO`.

### Causa raíz
Si se ejecuta un `DELETE` físico sobre `CWOMUSERS`, SQL Server arroja `Msg 547` por violación de clave foránea debido a la existencia de movimientos históricos registrados con esos IDs (`CWOMUS_USERID`).

### Solución aplicada
Baja lógica respetando los campos de auditoría nativos de Softland:
```sql
USE cwSGcore;

BEGIN TRAN X1;

SELECT CWOMUS_USERID, CWOMUS_NOMBRE, CWOMUS_DEBAJA, CWOMUS_FECMOD 
FROM CWOMUSERS 
WHERE CWOMUS_USERID IN ('CMARTINEZ', 'CSALGADO');

UPDATE CWOMUSERS 
SET CWOMUS_DEBAJA = 'S', 
    CWOMUS_FECMOD = GETDATE(), 
    CWOMUS_ULTOPR = 'M' 
WHERE CWOMUS_USERID IN ('CMARTINEZ', 'CSALGADO');

COMMIT TRAN X1;
```
Los accesos quedaron revocados sin alterar la integridad referencial histórica.

- **Palabras clave:** `cwSGcore`, `CWOMUSERS`, `CWOMUS_DEBAJA`, `baja lógica`, `Msg 547`.

---

## Caso 6: Creación de login SQL de interfaz bajo Principio de Menor Privilegio

- **Ticket / Ref:** 0006911
- **Fecha:** Octubre 2026
- **Módulo(s):** Motor SQL Server / Interfaces
- **Tablas clave:** Permisos de base de datos
- **Cliente / Entorno:** Diagnóstico y Soluciones (`DIASOL`)

### Síntoma
Un proveedor externo de una aplicación web solicitaba un usuario con rol `sysadmin` o `SA` para consultar la base de datos de Softland.

### Causa raíz
Mala práctica de seguridad por parte del proveedor externo. Otorgar `sysadmin` exponía a la empresa a modificaciones no auditadas que corrompen el ERP.

### Solución aplicada
Creación de login específico `SL` restringido a roles de lectura y ejecución de Stored Procedures sin permisos DDL ni acceso de modificación destructiva:
```sql
USE master;
CREATE LOGIN [SL_Interface] WITH PASSWORD = '...', CHECK_POLICY = ON;

USE DIASOL;
CREATE USER [SL_Interface] FOR LOGIN [SL_Interface];
ALTER ROLE db_datareader ADD MEMBER [SL_Interface];
GRANT EXECUTE TO [SL_Interface];
DENY DELETE ON DATABASE::DIASOL TO [SL_Interface];
```

- **Palabras clave:** `Seguridad SQL`, `db_datareader`, `menor privilegio`, `login`, `sysadmin`.

---

## Caso 7: Error en Liquidación Mensual por concepto RESTA sin concepto base

- **Ticket / Ref:** 0006916
- **Fecha:** Octubre 2026
- **Módulo(s):** `SJ` (Sueldos y Jornales)
- **Tablas clave:** `SJCCOI`, `SJCCOH`
- **Cliente / Entorno:** Diagnóstico y Soluciones (`01` / `DIASOL`)

### Síntoma
Al iniciar la liquidación mensual de haberes en Softland, el asistente se interrumpía con un error crítico en el paso *"Cargando conceptos"*, bloqueando la liquidación para todos los legajos mensuales.

### Causa raíz
En la tabla `SJCCOI`, el concepto `99938` (`Horas acuerdo RESTA`, cuya fórmula es `Cpt_58303 * -1`) estaba habilitado para el tipo de liquidación Mensual (`CODLIQ = 'M'`). Sin embargo, su concepto base `58303` estaba inhabilitado para liquidaciones mensuales. Al evaluar el árbol de dependencias de fórmulas, el compilador abortaba el proceso.

### Solución aplicada
Deshabilitación controlada del concepto subordinado para las liquidaciones no aplicables:
```sql
USE DIASOL;

BEGIN TRAN X1;

SELECT * FROM SJCCOI 
WHERE SJCCOI_CODCPT = '99938' AND SJCCOI_CODLIQ IN ('M', 'A', 'D', 'V');

UPDATE SJCCOI 
SET SJCCOI_HABILI = 'N' 
WHERE SJCCOI_CODCPT = '99938' AND SJCCOI_CODLIQ IN ('M', 'A', 'D', 'V');

COMMIT TRAN X1;
```
La liquidación mensual compiló de inmediato sin errores.

- **Palabras clave:** `SJCCOI`, `SJCCOH`, `Cargando conceptos`, `CODLIQ`, `99938`, `fórmula dependiente`.

---

## Caso 8: Padrón AGIP fallido por disco lleno y formato de fechas

- **Ticket / Ref:** 0006917
- **Fecha:** Octubre 2026
- **Módulo(s):** `DG` (Impuestos) / Motor SQL Server
- **Tablas clave:** `DGHTXT`, `10DGPROESTLEGWIZ`
- **Cliente / Entorno:** Diagnóstico y Soluciones (`DIASOL`)

### Síntoma
La importación mensual del padrón de retenciones/percepciones de AGIP CABA mediante el wizard `10DGPROESTLEGWIZ` (archivo de 129 MB con 3.250.000 filas) fallaba repetidamente.

### Causa raíz
Dos fallas concurrentes:
1. `Msg 9002 The transaction log for database 'DIASOL' is full`: El disco de logs `J:\` tenía menos de 1 MB libre, agotándose en la inserción masiva.
2. `Msg 242 The conversion of a date/time data type resulted in an out-of-range value`: El login SQL procesaba fechas en formato inglés (`us_english`), fallando en fechas como `'31/10/2026'`.

### Solución aplicada
1. Ampliación y saneamiento de disco `J:\` y vaciado de logs mediante backup transaccional.
2. Inclusión de `SET DATEFORMAT dmy;` antes de correr el script del wizard.
3. Procesamiento completo de los 3.25 millones de registros en `DGHTXT` sin errores.

- **Palabras clave:** `DGHTXT`, `AGIP`, `10DGPROESTLEGWIZ`, `Msg 9002`, `Msg 242`, `SET DATEFORMAT dmy`.

---

## Caso 9: Eliminación segura de factura por base y decremento de talonario

- **Ticket / Ref:** 0006921
- **Fecha:** Octubre 2026
- **Módulo(s):** `FC` / `VT` / `GR`
- **Tablas clave:** `FCRMVH`, `FCRMVI`, `VTRMVH`, `VTRMVI`, `VTROAP`, `GRCFOR`
- **Cliente / Entorno:** Diagnóstico y Soluciones (`01`)

### Síntoma
Se emitió por error la factura `FCA002 0002-00021870`. No llegó a obtener CAE fiscal ni fue entregada al cliente. Se requería borrarla por completo de la base y permitir que el sistema vuelva a emitir la factura número 21870.

### Causa raíz
Comprobante erróneo sin validez fiscal pendiente de reutilización de talonario.

### Solución aplicada
Ejecución del protocolo estricto de eliminación jerárquica:
1. Validaciones previas:
   - `SELECT FCRMVH_CAE, FCRMVH_NROASI FROM FCRMVH WHERE FCRMVH_CODEMP = '01' AND FCRMVH_CODFOR = 'FA0002' AND FCRMVH_NROFOR = 21870;` (confirmó `CAE IS NULL` y `NROASI = 0`).
   - `SELECT COUNT(*) FROM VTROAP WHERE VTROAP_CODEMP = '01' AND ((VTROAP_MODFOR = 'VT' AND VTROAP_CODFOR = 'FA0002' AND VTROAP_NROFOR = 21870) OR (VTROAP_APLMOD = 'VT' AND VTROAP_APLCOD = 'FA0002' AND VTROAP_APLNRO = 21870));` (confirmó 0 aplicaciones).
   - `SELECT GRCFOR_ULTNRO FROM GRCFOR WHERE GRCFOR_CODFOR = 'FA0002';` (confirmó que 21870 era el último emitido).
2. Borrado jerárquico bajo transacción:
```sql
USE DIASOL;

BEGIN TRAN X1;

DECLARE @emp varchar(6) = '01', @mod varchar(2) = 'VT', @cod varchar(6) = 'FA0002', @nro int = 21870;

DELETE FROM VTRMVG WHERE VTRMVG_CODEMP = @emp AND VTRMVG_MODFOR = @mod AND VTRMVG_CODFOR = @cod AND VTRMVG_NROFOR = @nro;
DELETE FROM VTRMVD WHERE VTRMVD_CODEMP = @emp AND VTRMVD_MODFOR = @mod AND VTRMVD_CODFOR = @cod AND VTRMVD_NROFOR = @nro;
DELETE FROM VTRMVI WHERE VTRMVI_CODEMP = @emp AND VTRMVI_MODFOR = @mod AND VTRMVI_CODFOR = @cod AND VTRMVI_NROFOR = @nro;
DELETE FROM VTRMVC WHERE VTRMVC_CODEMP = @emp AND VTRMVC_MODFOR = @mod AND VTRMVC_CODFOR = @cod AND VTRMVC_NROFOR = @nro;
DELETE FROM VTRMVP WHERE VTRMVP_CODEMP = @emp AND VTRMVP_MODFOR = @mod AND VTRMVP_CODFOR = @cod AND VTRMVP_NROFOR = @nro;
DELETE FROM VTRMVH WHERE VTRMVH_CODEMP = @emp AND VTRMVH_MODFOR = @mod AND VTRMVH_CODFOR = @cod AND VTRMVH_NROFOR = @nro;

DELETE FROM FCRMVG WHERE FCRMVG_CODEMP = @emp AND FCRMVG_MODFOR = 'FC' AND FCRMVG_CODFOR = @cod AND FCRMVG_NROFOR = @nro;
DELETE FROM FCRMVD WHERE FCRMVD_CODEMP = @emp AND FCRMVD_MODFOR = 'FC' AND FCRMVD_CODFOR = @cod AND FCRMVD_NROFOR = @nro;
DELETE FROM FCRMVI WHERE FCRMVI_CODEMP = @emp AND FCRMVI_MODFOR = 'FC' AND FCRMVI_CODFOR = @cod AND FCRMVI_NROFOR = @nro;
DELETE FROM FCRMVH WHERE FCRMVH_CODEMP = @emp AND FCRMVH_MODFOR = 'FC' AND FCRMVH_CODFOR = @cod AND FCRMVH_NROFOR = @nro;

UPDATE GRCFOR SET GRCFOR_ULTNRO = GRCFOR_ULTNRO - 1 
WHERE GRCFOR_CODFOR = @cod AND GRCFOR_ULTNRO = @nro;

COMMIT TRAN X1;
```

- **Palabras clave:** `Eliminación factura`, `sin CAE`, `VTROAP`, `GRCFOR_ULTNRO`, `FCRMVH`, `VTRMVH`.

---

## Caso 10: Código MiPyME impreso como 001 en lugar de 201 en reporte

- **Ticket / Ref:** 0006931
- **Fecha:** Octubre 2026
- **Módulo(s):** `FC` / Report Designer
- **Tablas clave:** `VTCFOR`, `FCRMVH`, `USR_VTF_MVH_DYS_MIPY`
- **Cliente / Entorno:** Diagnóstico y Soluciones (`01`)

### Síntoma
En la factura electrónica MiPyME emitida bajo talonario `FCA006` N° 2451, AFIP había otorgado CAE con código oficial `201` (Factura de Crédito Electrónica MiPyME A), pero en el PDF impreso salía impreso el código `001`.

### Causa raíz
Al auditar la plantilla `USR_VTF_MVH_DYS_MIPY` en el Diseñador de Reportes de Softland, se comprobó que el cuadro del código de comprobante bajo la letra "A" tenía hardcodeado el texto estático `'001'` debido a una personalización antigua, en lugar de leer el campo impositivo dinámico `VTCFOR_CODIMP`.

### Solución aplicada
1. Apertura de la plantilla desde Report Designer de Softland.
2. Modificación del cuadro de texto estático reemplazándolo por el campo dinámico o el literal `201`.
3. Reemisión del PDF verificando que la impresión reflejó correctamente el código fiscal 201.

- **Palabras clave:** `MiPyME`, `Código 201`, `001`, `VTCFOR_CODIMP`, `Report Designer`, `USR_VTF_MVH_DYS_MIPY`.

---

## Caso 11: Error GR000008 al anular Recibo por correlatividad cronológica

- **Ticket / Ref:** 0006934
- **Fecha:** Octubre 2026
- **Módulo(s):** `CJ` (Tesorería) / `VT`
- **Tablas clave:** `CJRMVH`, `CJRAPL`, `TCANUWIZ`
- **Cliente / Entorno:** Diagnóstico y Soluciones (`BS AS TESTING`)

### Síntoma
Al intentar anular un Recibo de Cobranza (`RC`) mediante el asistente de anulaciones `TCANUWIZ`, el sistema arrojaba el error `GR000008: Fecha fuera de secuencia cronológica` y cancelaba la operación.

### Causa raíz
El usuario intentaba generar el contracomprobante `ARC 13` con fecha `28/09/2026`. Sin embargo, el último contracomprobante registrado en ese talonario (`ARC 12`) tenía fecha `09/10/2026`. Softland impide emitir un comprobante con fecha anterior al último número emitido del mismo talonario.

### Solución aplicada
1. Desimputación previa de cobranzas en `CJRAPL`.
2. Emisión de la anulación en `TCANUWIZ` fijando la fecha del contracomprobante en `09/10/2026` (igual o superior al último emitido).
3. Grabación exitosa del comprobante `ARC 13`.

- **Palabras clave:** `GR000008`, `TCANUWIZ`, `ARC`, `correlatividad cronológica`, `anulación recibo`.

---

## Caso 12: Error GR000024 en Ajuste de Stock con Series por sector sin saldo

- **Ticket / Ref:** 0006940
- **Fecha:** Octubre 2026
- **Módulo(s):** `ST` (Stock)
- **Tablas clave:** `STRMVZ`, `STRMVI`, `STMATI`
- **Cliente / Entorno:** Videojet (`VIDEOJET`)

### Síntoma
Al registrar un ajuste de inventario negativo (`DIFINN`), el usuario obtenía el error `GR000024: Cantidad de serie no válida` impidiendo grabar el movimiento.

### Causa raíz
El usuario digitó manualmente el número de serie `NO APLICA1` seleccionando el depósito `SERV` y sector `M BOGADO`. Sin embargo, en la tabla `STRMVZ` ese número de serie tenía existencia en el sector `CON GARANTIA`. Al tipear la serie en un sector donde el saldo era 0, Softland interpretó la operación como un alta de serie con cantidad negativa `-1`, lo cual está bloqueado por el motor del ERP.

### Solución aplicada
1. Verificación por SQL de la ubicación real de la serie:
```sql
USE VIDEOJET;

SELECT STRMVZ_CODEMP, STRMVZ_ARTCOD, STRMVZ_DEPMOV, STRMVZ_SECMOV, STRMVZ_SERMOV, STRMVZ_CANTID 
FROM STRMVZ 
WHERE STRMVZ_SERMOV = 'NO APLICA1';
```
2. En la interfaz de Softland, abrir la ventana de *Apertura de Series* y seleccionar la unidad existente en el sector `CON GARANTIA` en lugar de tipear el texto a mano.
3. El ajuste de egreso se registró sin errores.

- **Palabras clave:** `GR000024`, `STRMVZ`, `DIFINN`, `Series`, `Apertura de series`.

---

## Caso 13: Implementación del Nuevo Recibo de Sueldo (Decreto 407/2026)

- **Ticket / Ref:** 06817 / Bueras
- **Fecha:** Septiembre / Octubre 2026
- **Módulo(s):** `SJ` (Sueldos y Jornales)
- **Tablas clave:** `SJTLIP`, `SJTLIC`, `SJCCOH`, `SJF_MVH_RES`
- **Cliente / Entorno:** Grupo Bueras (`GRB003` - CCT Camioneros 40/89) / DYS

### Síntoma
Adecuación obligatoria del recibo al modelo exigido por el Decreto 407/2026 (reglamentario del art. 140 LCT) para mostrar en el anverso el desglose del costo laboral a cargo del empleador en el reporte `SJF_MVH_RES`. Al configurarlo inicialmente, los subtotales salían en blanco y el gráfico de torta salía como "(sin etiqueta)".

### Causa raíz
El reporte `SJF_MVH_RES` evalúa los campos calculados de cabecera (`ESTITU`, `TITULT`, `TOTTI2`) esperando que exista una fila en `SJTLIC` con `NORDEN` terminado en 0 (la fila del Título). Si la fila 0 no tiene conceptos asociados, no consolida.

### Solución aplicada
Parametrización jerárquica en Libro `RECIBO` (`SJTLIP`/`SJTLIC`) en múltiplos de 10:
- Orden 10: Título *Total Costo Sindical* (asociar en `SJTLIC` cuota sindical y contribuciones patronales).
- Orden 20: Título *Total Seguridad Social* (asociar jubilación 11% `60300` y patronal `90200`).
- Orden 30: Título *Total Obra Social* (asociar `60360` y patronal `90300`).
- Orden 40: Título *Total Costo INSSJP* (asociar ley 19.032 `60320` y patronal `90210`).
- Orden 50: Título *Total Costo ART* (asociar `90340` y `90341`).
- Orden 60: Título *Total Costo SCVO* (asociar `90339`).
- Orden 70: Título *Sueldo Neto* (asociar `80100`).
No crear conceptos artificiales. Con esta estructura, el gráfico de costos y títulos consolida al 100%.

- **Palabras clave:** `Decreto 407/2026`, `Libro RECIBO`, `SJTLIP`, `SJTLIC`, `SJF_MVH_RES`, `costo patronal`.

---

## Caso 14: Auditoría de proveedores con envío de mails en cola USR_MAILS

- **Ticket / Ref:** Securitas Uruguay
- **Fecha:** Octubre 2026
- **Módulo(s):** `PV` / Auditoría
- **Tablas clave:** `PVMCLH`, `USR_MAILS`, `USR_RAUDIT`
- **Cliente / Entorno:** Securitas Uruguay

### Síntoma
Requerimiento de auditar cambios en teléfonos, emails y condiciones de pago de proveedores en el maestro `PVMCLH`, enviando una alerta automática al correo de auditoría interna sin degradar la performance de carga.

### Causa raíz
Un intento previo de trigger bloqueaba el guardado de proveedores cuando el servidor SMTP demoraba en responder.

### Solución aplicada
Creación de una cola asincrónica desacoplada:
1. Creación de tabla intermedia `USR_MAILS` para encolar notificaciones.
2. Modificación del trigger `Final_Trigger` sobre `PVMCLH` para que inserte en `USR_MAILS` únicamente los campos modificados comparando las tablas virtuales `inserted` y `deleted`.
3. Job de SQL Server en background encargado de despachar los correos de `USR_MAILS`.

- **Palabras clave:** `PVMCLH`, `USR_MAILS`, `Trigger`, `Auditoría`, `Securitas`.

---

## Caso 15: Desfasaje de fin de mes en Jobs de carga de padrón Tucumán

- **Ticket / Ref:** Padrón Tucumán
- **Fecha:** Octubre 2026
- **Módulo(s):** `DG` (Impuestos) / Jobs SQL
- **Tablas clave:** `DGHTXT`, `sp_Carga_Datos_Acreditan_Tucuman`
- **Cliente / Entorno:** Diagnóstico y Soluciones (`DIASOL`)

### Síntoma
El último día de los meses con 31 días (ej. 31 de octubre), el sistema dejaba de aplicar las percepciones `PIBTC` y retenciones `RIBTC`, cobrando sin alícuota a los clientes de Tucumán.

### Causa raíz
En el Stored Procedure `DBO.Carga_Datos_Acreditan_Tucuman`, la fecha fin del padrón mensual se construía concatenando el día `'30'` en lugar del último día real del mes, dejando el día 31 descubierto en la tabla `DGHTXT`.

### Solución aplicada
Corrección del SP utilizando la función nativa `EOMONTH`:
```sql
USE DIASOL;

BEGIN TRAN X1;

-- Validar registros previos con vencimiento desfasado
SELECT COUNT(*) FROM DGHTXT 
WHERE CODRET = 'PIBTC' AND FCHHAS < EOMONTH(FCHDES);

UPDATE DGHTXT 
SET FCHHAS = EOMONTH(FCHDES) 
WHERE CODRET = 'PIBTC' AND FCHHAS < EOMONTH(FCHDES);

COMMIT TRAN X1;
```
Reprocesamiento del job con vigencia hasta el último segundo del mes.

- **Palabras clave:** `Tucumán`, `DGHTXT`, `EOMONTH`, `PIBTC`, `RIBTC`, `fin de mes`.

---

## Caso 16: Error de formulario no asociado en comprobante FCC en GRCCBF

- **Ticket / Ref:** Matriz MiPyME
- **Fecha:** Octubre 2026
- **Módulo(s):** `FC` / `GR`
- **Tablas clave:** `GRCCBF`, `GRCFOR`, `VTCFOR`
- **Cliente / Entorno:** Diagnóstico y Soluciones (`01`)

### Síntoma
Al emitir una factura de compra o crédito se presentaba el error: *"Falta asociar un formulario con Código impositivo 001 en el comprobante FCC para la sucursal 0006 y situación impositiva I"*.

### Causa raíz
Inconsistencia en la matriz impositiva `GRCCBF` (asignación de talonarios por combinación de comprobante, sucursal y condición impositiva). Al dar de alta una nueva sucursal, no se replicaron las filas correspondientes.

### Solución aplicada
Inserción controlada en `GRCCBF` bajo transacción:
```sql
USE DIASOL;

BEGIN TRAN X1;

INSERT INTO GRCCBF (GRCCBF_MODCOM, GRCCBF_CODCOM, GRCCBF_EMPIVA, GRCCBF_CODFOR, GRCCBF_CODIMP)
VALUES ('FC', 'FCC', 'I', 'FCA006', '001');

COMMIT TRAN X1;
```

- **Palabras clave:** `GRCCBF`, `Falta asociar formulario`, `Código impositivo`, `FCC`.

---

## Caso 17: Error Msg 547 Foreign Key en sincronización de Requerimientos API

- **Ticket / Ref:** Bueras Sync API
- **Fecha:** Septiembre 2026
- **Módulo(s):** `CO` (Compras) / Web API
- **Tablas clave:** `CORMVH`, `CORMVI`, `CORMVD`, `CORMVG`
- **Cliente / Entorno:** Grupo Bueras (`GRPBUE`)

### Síntoma
La integración de compras entre la app móvil y Softland fallaba con `Msg 547: The DELETE statement conflicted with the REFERENCE constraint` al intentar actualizar renglones de requerimientos existentes.

### Causa raíz
El script de sincronización intentaba eliminar ítems de `CORMVI` sin eliminar previamente sus dimensiones asociadas en `CORMVD` y subcuentas en `CORMVG`.

### Solución aplicada
Reordenamiento estricto de borrado en cascada con filtros obligatorios de empresa y módulo:
```sql
USE GRPBUE;

BEGIN TRAN X1;

DECLARE @emp varchar(6) = 'GRB003', @mod varchar(2) = 'CO', @cod varchar(6) = @cod, @nro int = @nro;

DELETE FROM CORMVG WHERE CORMVG_CODEMP = @emp AND CORMVG_MODFOR = @mod AND CORMVG_CODFOR = @cod AND CORMVG_NROFOR = @nro;
DELETE FROM CORMVD WHERE CORMVD_CODEMP = @emp AND CORMVD_MODFOR = @mod AND CORMVD_CODFOR = @cod AND CORMVD_NROFOR = @nro;
DELETE FROM CORMVI WHERE CORMVI_CODEMP = @emp AND CORMVI_MODFOR = @mod AND CORMVI_CODFOR = @cod AND CORMVI_NROFOR = @nro;

COMMIT TRAN X1;
```

- **Palabras clave:** `CORMVI`, `CORMVD`, `CORMVG`, `Msg 547`, `Requerimientos`, `Foreign Key`.

---

## Caso 18: Conflicto de Collation Msg 468 entre Modern_Spanish y Latin1_General

- **Ticket / Ref:** Videojet Wollday
- **Fecha:** Octubre 2026
- **Módulo(s):** `FC` / Infraestructura IIS
- **Tablas clave:** SP `ACTUALIZA_ESTADO_HISTORIAL_FACTURAS`, `VTRMVH`
- **Cliente / Entorno:** Videojet

### Síntoma
Tras migrar el servidor de facturación a una nueva máquina virtual, la interfaz arrojaba: `Msg 468: Cannot resolve the collation conflict between "Latin1_General_CI_AS" and "Modern_Spanish_CI_AS" in the equal to operation`.

### Causa raíz
La base del ERP estaba en `Modern_Spanish_CI_AS`, mientras que `tempdb` y la base de la interfaz web se crearon con la intercalación por defecto de Windows `Latin1_General_CI_AS`.

### Solución aplicada
Actualización del Stored Procedure agregando `COLLATE database_default` en cada cláusula `ON` y `WHERE` que compara columnas de texto entre tablas temporales y tablas del ERP:
```sql
ON a.nrocta COLLATE database_default = b.VTRMVH_NROCTA COLLATE database_default
```

- **Palabras clave:** `Msg 468`, `Collation conflict`, `Modern_Spanish`, `COLLATE database_default`.

---

## Caso 19: Generación de infraestructura OpenSSL para Facturación Raysan

- **Ticket / Ref:** Raysan Certs
- **Fecha:** Octubre 2026
- **Módulo(s):** `FC` / ARCA
- **Tablas clave:** Parámetros fiscales
- **Cliente / Entorno:** Raysan

### Síntoma
Puesta en marcha de nuevo punto de venta electrónico para cliente Raysan.

### Causa raíz
Generación inicial de claves criptográficas y tramitación de certificado de facturación.

### Solución aplicada
1. Creación de directorio seguro en `/home/kvo/dycos/certificados_raysan`.
2. Generación de clave RSA 2048 y CSR con CUIT de Raysan.
3. Validación de hash del módulo y empaquetado a `.pfx` sin contraseña.
4. Vinculación en el servicio de facturación de Softland.

- **Palabras clave:** `Raysan`, `Certificados`, `OpenSSL`, `ARCA`, `PFX`.

---

## Caso 20: Desfasaje decimal por factor 10 en Horas Acuerdo de Sueldos

- **Ticket / Ref:** Horas Acuerdo
- **Fecha:** Octubre 2026
- **Módulo(s):** `SJ` (Sueldos y Jornales)
- **Tablas clave:** `SJCCOH`, `SJRMVI`
- **Cliente / Entorno:** Diagnóstico y Soluciones (`01`)

### Síntoma
En el legajo 117, el concepto `58303` liquidó $56.904,32 en lugar de $5.690,43 (un factor exacto de 10x superior al valor real).

### Causa raíz
En la fórmula del catálogo `SJCCOH_FORPLA`, la variable de lectura de novedades leía un campo de enteros sin decimales, omitiendo dividir por el divisor de escala 10 configurado en la novedad del legajo.

### Solución aplicada
Ajuste transaccional de la fórmula en `SJCCOH` casteando el campo `TEXT` y aplicando el divisor de escala correspondiente:
```sql
USE DIASOL;

BEGIN TRAN X1;

UPDATE SJCCOH 
SET SJCCOH_FORPLA = 'Horas = Legajo.Concepto("Novh_58303") / 10.0; Resultado = Horas * Valor_Hora;'
WHERE SJCCOH_CODCPT = '58303';

COMMIT TRAN X1;
```
Reliquidación del legajo comprobando el importe exacto.

- **Palabras clave:** `SJCCOH`, `58303`, `Horas acuerdo`, `factor 10`, `escala decimal`.
