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

- **Cuenta en Claude:** necesitás tener una cuenta activa en [claude.ai](https://claude.ai). Las skills requieren el plan **Pro** o superior (no funcionan con el plan gratuito).
- **Acceso a este repositorio:** necesitás estar logueado en GitHub con tu cuenta del equipo Dycos para poder descargar el archivo.
- **Navegador compatible:** Chrome, Firefox, Safari o Edge en su versión actual. No se recomienda instalar desde el navegador del celular.

---

### Paso 1 — Descargar el archivo de la skill

1. En este repositorio de GitHub, buscá el archivo `dycos-softland-support.skill` en la lista de archivos de la página principal.
2. Hacé clic en el nombre del archivo para abrirlo.
3. En la página del archivo, buscá el ícono de descarga en la esquina superior derecha del panel de contenido — es un botón con una flecha hacia abajo y dice **"Download raw file"** al pasar el mouse.
4. Hacé clic en ese botón. El archivo se va a descargar como `dycos-softland-support.skill` en tu carpeta de descargas.

> **Tip:** si el navegador intenta abrir el archivo en lugar de descargarlo, hacé clic derecho en el botón de descarga y elegí **"Guardar enlace como..."**

---

### Paso 2 — Ingresar a Claude

1. Abrí [claude.ai](https://claude.ai) en el navegador.
2. Iniciá sesión con tu cuenta (la que tiene el plan Pro).
3. Asegurate de estar en la pantalla principal de chats antes de continuar.

---

### Paso 3 — Abrir la Configuración

1. Buscá tu foto de perfil o inicial en la esquina **inferior izquierda** de la pantalla.
2. Hacé clic sobre ella para abrir el menú de usuario.
3. En el menú desplegable, seleccioná **"Configuración"** (o **"Settings"** si tu cuenta está en inglés).

---

### Paso 4 — Ir a la sección Skills

1. Dentro de Configuración, vas a ver un menú lateral con varias secciones.
2. Buscá la sección llamada **"Skills"** en ese menú lateral.
3. Si no ves la sección Skills, revisá que tu plan sea Pro o Team — el plan gratuito no la tiene.

---

### Paso 5 — Instalar la skill

1. Dentro de la sección Skills, hacé clic en el botón **"Instalar skill"** (o **"Install skill"**).
2. Se va a abrir una ventana del explorador de archivos de tu computadora.
3. Navegá hasta tu carpeta de Descargas y seleccioná el archivo `dycos-softland-support.skill`.
4. Hacé clic en **Abrir** (o **Open**).
5. Claude va a mostrar un resumen de lo que contiene la skill y te va a pedir confirmación.
6. Confirmá la instalación.

La skill va a aparecer listada en la sección Skills con el nombre **"Dycos Softland Support"**.

---

### Paso 6 — Verificar que la instalación funcionó

1. Cerrá la Configuración y abrí un **chat nuevo** (hacé clic en "Nuevo chat" o el botón **+**).
2. En el chat, escribí:

```
/dycos
```

3. Si la skill está instalada correctamente, Claude va a responder con el mensaje de bienvenida de Dycos, listando los comandos disponibles y pidiéndote el contexto del ticket.

> **Si Claude no reconoce el comando `/dycos`**, revisá la sección [Solución de problemas](#solución-de-problemas) más abajo.

---

### Actualización de la skill

Cuando haya una versión nueva de la skill (vas a verlo como un nuevo commit en este repositorio):

1. Descargá el nuevo archivo `.skill` siguiendo el Paso 1.
2. Ingresá a Configuración → Skills.
3. Buscá la skill instalada y hacé clic en **"Desinstalar"** o **"Remove"**.
4. Volvé a instalar siguiendo los Pasos 5 y 6.

No hace falta desinstalar primero en todas las versiones — si Claude te permite instalar la nueva encima de la anterior, podés saltear ese paso.

---

### Solución de problemas

**El archivo se descarga con extensión incorrecta (ej: `.skill.txt`)**
El sistema operativo a veces cambia la extensión. Antes de instalarlo, renombrá el archivo para que quede exactamente como `dycos-softland-support.skill`.

**No encuentro la sección "Skills" en Configuración**
La sección Skills solo está disponible en los planes Pro y Team. Verificá en Configuración → Plan y facturación cuál es tu plan actual.

**La skill aparece instalada pero `/dycos` no funciona**
- Asegurate de escribir `/dycos` en un **chat nuevo**, no en uno existente.
- Cerrá y volvé a abrir el navegador.
- Si sigue sin funcionar, desinstalá la skill y volvé a instalarla desde cero.

**Me pide permisos o muestra una advertencia al instalar**
Esto es normal. Claude te muestra qué capacidades tiene la skill antes de activarla. Revisá que el nombre y la descripción coincidan con la skill de Dycos y confirmá la instalación.

**La instalación falla o el archivo no se reconoce**
- Verificá que el archivo pese más de 0 KB (si pesa 0 es que la descarga falló — volvé a descargar).
- Asegurate de que la extensión sea `.skill` y no `.zip` u otra.
- Probá con otro navegador.

**No tengo el plan Pro**
Hablá con el responsable del equipo para que revisen la cuenta. La skill no funciona sin un plan pago.

---

## Cómo usar la skill en el día a día

### Inicio de un ticket

Abrí un chat nuevo en Claude y escribí `/dycos`. Podés iniciar de dos formas:

1. **Directo con contexto (Flujo inteligente recomendado):** Si el mensaje inicial ya contiene el ticket, síntoma o contexto técnico, la skill **omite el mensaje genérico de bienvenida** y pasa de inmediato al diagnóstico técnico:

```
/dycos

Ticket #456 — Cliente: Securitas
Problema: no pueden cerrar el mes, les tira error al intentar cerrar noviembre.
Hablé con el cliente por Teams, me dijo que el error apareció después de cargar 
las últimas facturas del mes.

SELECT * FROM FCRMVH WHERE codemp = '001' AND modfor = 'FC'
```

2. **Sin contexto previo:** Si escribís únicamente `/dycos` (o un saludo sin datos del caso), Claude te responderá con el mensaje de bienvenida estándar indicándote qué datos necesita para comenzar.

> **Importante:** sin el `/dycos`, Claude funciona como asistente normal y no aplica ninguna lógica de Dycos.

---

## Comandos disponibles

En cualquier momento del chat podés escribir estos comandos para activar funcionalidades específicas:

### `/dycos-horas`
Genera una justificación técnica profesional, estructurada y defendible de las horas dedicadas al ticket en 4 fases técnicas (Diagnóstico, Auditoría en BD, Ejecución transaccional y Verificación funcional), lista para asentar en el sistema de tickets (Mantis, Jira, Redmine) o presentar ante gerencia y clientes. Podés especificar la duración deseada (ej. `/dycos-horas 1.5h`, `/dycos-horas 2h`, `/dycos-horas 4h`).

### `/dycos-ia`
Analiza todo lo que trabajaron en el chat y detecta oportunidades donde la IA podría agregar valor real: automatizaciones, validaciones preventivas, templates reutilizables.

> Usalo cuando hayas resuelto un ticket y quieras explorar si hay algo que se pueda mejorar o automatizar para el futuro.

### `/dycos-respuesta`
Genera la respuesta formal para cerrar el ticket, lista para copiar y pegar en el sistema de tickets. Está escrita en lenguaje accesible para el cliente, sin tecnicismos.

### `/dycos-resumen`
Genera un resumen técnico interno del ticket: problema, causa raíz, tablas involucradas, queries usados, solución aplicada. Útil para documentación interna o para tickets similares en el futuro.

### `/dycos-checklist`
Muestra una checklist de seguridad antes de ejecutar un UPDATE, DELETE o INSERT. Muy útil para no saltarse ningún paso crítico.

### `/dycos-aprender`
Genera una ficha del caso resuelto (síntoma, causa raíz, módulo/tablas, solución, query clave, palabras clave) lista para pegar en este repositorio, para que el equipo vaya armando una base de casos conocidos.

> **Importante:** este comando no guarda nada automáticamente — Claude no puede escribir en el repositorio ni modificar la skill instalada por su cuenta. Genera el texto y vos lo pegás donde corresponda (ver [Cómo documentar un caso resuelto](#cómo-documentar-un-caso-resuelto) abajo).

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

## Cómo documentar un caso resuelto

Cuando termines de resolver un ticket, si te parece que puede servirle a otro compañero en el futuro, escribí `/dycos-aprender` en el mismo chat. Claude va a generar una ficha con el problema, la causa raíz, las tablas involucradas, la solución y algunas palabras clave para poder encontrarla después.

Esa ficha **no se guarda sola en ningún lado** — la skill instalada en tu Claude es un archivo estático, Claude no puede escribirla ni modificarla por su cuenta. El paso manual que falta es tuyo:

1. Copiá la ficha que generó Claude.
2. Pegala en este repositorio, de una de estas dos formas:
   - Como comentario en un **Issue nuevo** (pestaña Issues → New issue), con el título sugerido que te da la ficha.
   - Agregándola al final de `casos-resueltos.md` en la raíz del repo (si todavía no existe el archivo, creálo).
3. El responsable del repo va a revisar los casos acumulados de tanto en tanto e incorporar los más relevantes a una sección de "Casos conocidos" dentro de la skill, en una próxima versión.

Es el mismo mecanismo que ya usamos para reportar mejoras (ver abajo), solo que acá el objetivo es acumular conocimiento de casos resueltos en vez de reportar bugs.

---

## ¿Cómo reportar una mejora o problema con la skill?

Si encontrás algo que la skill no maneja bien, o tenés una idea para mejorarla:

1. Abrí un **Issue** en este repositorio (pestaña Issues → New issue)
2. Describí el problema o la mejora con el mayor detalle posible: qué preguntaste, qué respondió Claude, y qué esperabas que respondiera
3. El responsable del repo va a actualizar la skill y subir la nueva versión

Cuando haya una versión nueva, vas a verlo como un nuevo commit en la página principal del repositorio. El proceso de actualización está detallado en la sección [Actualización de la skill](#actualización-de-la-skill) más arriba.

---

## Preguntas frecuentes

**¿Tengo que reinstalar la skill cada vez que abro Claude?**
No. Una vez instalada queda activa en tu cuenta de Claude. Solo la reinstalás cuando haya una nueva versión publicada en este repositorio.

**¿La skill funciona en todos mis chats?**
La skill está disponible en todos los chats nuevos, pero se activa únicamente cuando escribís `/dycos` al inicio del mensaje. Sin ese comando, Claude funciona como asistente genérico.

**¿Mis conversaciones son privadas?**
Sí. La skill solo le da contexto a Claude sobre cómo trabajar para Dycos — no comparte tus conversaciones ni los datos de los tickets con otros usuarios.

**¿Puedo usar Claude sin la skill?**
Sí, pero vas a tener que explicarle el contexto de Dycos y Softland manualmente en cada chat nuevo.

**¿Qué pasa si escribo `/dycos` en el medio de un chat ya empezado?**
La skill se va a activar en ese punto, pero es mejor empezar un chat nuevo para evitar que el contexto anterior interfiera con las respuestas.

**¿La skill funciona en el celular?**
Sí, podés usar Claude desde el celular y la skill va a funcionar. Sin embargo, la instalación inicial tiene que hacerse desde un navegador de escritorio.

**¿Cuánto tarda en instalarse?**
La instalación es inmediata. Una vez que confirmás en la pantalla de Configuración → Skills, la skill está activa en el siguiente chat que abras.

**¿Qué hago si tengo un problema que no está en la guía?**
Reportalo como un Issue en este repositorio o contactá directamente al responsable del repo.

---

*Repositorio mantenido por el equipo Dycos. Ante dudas, consultá con el responsable del repo.*
