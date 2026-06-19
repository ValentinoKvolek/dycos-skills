# Dycos Skills — Documentación interna

Este repositorio contiene las **skills de IA** desarrolladas por Dycos para potenciar el trabajo diario con Claude en el soporte técnico de Softland.

---

## ¿Qué es una skill?

Una skill es un archivo que le "enseña" a Claude cómo trabajar específicamente para Dycos. Sin la skill, Claude es un asistente genérico. Con la skill instalada, Claude ya sabe:

- Que trabajamos con Softland y SQL Server
- Cómo es nuestro flujo de trabajo con tickets
- Las reglas de seguridad SQL que usamos (transacciones, filtros obligatorios)
- La estructura de tablas de Softland
- Los comandos especiales que podemos usar

**En la práctica:** en lugar de explicarle el contexto de Dycos en cada chat nuevo, la skill lo hace por vos automáticamente.

---

## Skills disponibles

| Archivo | Descripción |
|---|---|
| `dycos-softland-support.skill` | Skill principal para resolución de tickets Softland |

---

## Instalación paso a paso

### Requisitos previos
- Tener una cuenta en [claude.ai](https://claude.ai)
- Tener acceso a este repositorio de GitHub

### Paso 1 — Descargar la skill

En este repositorio, hacé clic en el archivo `dycos-softland-support.skill` y luego en el botón **Download raw file** (ícono de descarga).

### Paso 2 — Abrir Claude

Ingresá a [claude.ai](https://claude.ai) con tu cuenta.

### Paso 3 — Ir a Configuración

Hacé clic en tu foto de perfil (esquina inferior izquierda) → **Configuración**.

### Paso 4 — Instalar la skill

Dentro de Configuración, buscá la sección **Skills** → hacé clic en **Instalar skill** → seleccioná el archivo `.skill` que descargaste.

### Paso 5 — Verificar

Abrí un chat nuevo en Claude y escribí algo como:
> "Tengo el ticket #123, problema con cierre de mes"

Si la skill está activa, Claude va a responder siguiendo el flujo de trabajo de Dycos automáticamente.

---

## Cómo usar la skill en el día a día

### Inicio de un ticket

Abrí un chat nuevo en Claude y escribí `/dycos`. La skill se activa y te da un mensaje de bienvenida explicándote exactamente qué mandar.

En ese momento mandás el contexto del ticket: número, título, descripción del problema, y todo lo extra que tengas — si ya corriste alguna consulta SQL, si hablaste con el cliente y te dijo algo adicional, o si vos ya tenés alguna idea de por dónde viene el problema.

Por ejemplo:

```
/dycos

Ticket #456 — Cliente: Securitas
Problema: no pueden cerrar el mes, les tira error al intentar cerrar noviembre.
Hablé con el cliente por Teams, me dijo que el error apareció después de cargar 
las últimas facturas del mes.

SELECT * FROM FCRMVH WHERE codemp = '001' AND modfor = 'FC'
```

Claude va a hacer preguntas si le falta contexto y después va a ayudarte a construir la solución con SQL iterativo.

> **Importante:** sin el `/dycos`, Claude funciona como asistente normal y no aplica ninguna lógica de Dycos.

---

## Comandos disponibles

En cualquier momento del chat podés escribir estos comandos para activar funcionalidades específicas:

### `/dycos-ia`
Analiza todo lo que trabajaron en el chat y detecta oportunidades donde la IA podría agregar valor real: automatizaciones, validaciones preventivas, templates reutilizables.

> Usalo cuando hayas resuelto un ticket y quieras explorar si hay algo que se pueda mejorar o automatizar para el futuro.

### `/dycos-respuesta`
Genera la respuesta formal para cerrar el ticket, lista para copiar y pegar en el sistema de tickets. Está escrita en lenguaje accesible para el cliente, sin tecnicismos.

### `/dycos-resumen`
Genera un resumen técnico interno del ticket: problema, causa raíz, tablas involucradas, queries usados, solución aplicada. Útil para documentación interna o para tickets similares en el futuro.

### `/dycos-checklist`
Muestra una checklist de seguridad antes de ejecutar un UPDATE, DELETE o INSERT. Muy útil para no saltarse ningún paso crítico.

### `/ayuda`
Lista todos los comandos disponibles.

---

## Reglas de seguridad SQL

La skill aplica estas reglas automáticamente, pero es importante que todos las conozcamos:

### Transacciones obligatorias
Cualquier operación que modifique datos **siempre** debe ir dentro de una transacción:

```sql
BEGIN TRAN X1

-- tu UPDATE / DELETE / INSERT acá

-- Si el resultado es el esperado:
COMMIT TRAN X1

-- Si algo salió mal:
ROLLBACK TRAN X1
```

Si le compartís a Claude un UPDATE o DELETE sin transacción, te lo va a señalar antes de que lo ejecutes.

### Filtros obligatorios
Toda consulta debe filtrar por estas columnas cuando la tabla las tiene:

- `codemp` — Código de empresa
- `modfor` — Módulo del comprobante
- `codfor` — Código de formulario
- `nrofor` — Número de formulario

---

## ¿Cómo reportar una mejora o problema con la skill?

Si encontrás algo que la skill no maneja bien, o tenés una idea para mejorarla:

1. Abrí un **Issue** en este repositorio (pestaña Issues → New issue)
2. Describí el problema o la mejora
3. El responsable del repo va a actualizar la skill y subir la nueva versión

Cuando haya una versión nueva, vas a ver el commit en la página principal del repositorio. Para actualizar simplemente descargás el nuevo `.skill` y lo reinstalás en Claude (mismo proceso que la instalación inicial).

---

## Preguntas frecuentes

**¿Tengo que reinstalar la skill cada vez que abro Claude?**
No. Una vez instalada queda activa en tu cuenta. Solo reinstalás cuando haya una versión nueva.

**¿La skill funciona en todos mis chats?**
Sí, en todos los chats nuevos que abras en Claude.

**¿Mis conversaciones son privadas?**
Sí. La skill solo le da contexto a Claude sobre cómo trabajar, no comparte tu información con otros usuarios.

**¿Puedo usar Claude sin la skill?**
Sí, pero vas a tener que explicarle el contexto de Dycos y Softland en cada chat nuevo.

---

*Repositorio mantenido por el equipo Dycos. Ante dudas, consultá con el responsable del repo.*
