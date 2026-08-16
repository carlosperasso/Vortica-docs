# Vórtica

**AI-driven commercial prospecting engine — from raw company to a qualified conversation.**

🇬🇧 English (below) · 🇦🇷 [Español](#vórtica-español)

---

## Table of contents

- [What Vórtica is](#what-vórtica-is)
- [What it does](#what-it-does)
- [Architecture](#architecture)
- [Principles](#principles)
- [Status](#status)

---

## What Vórtica is

Vórtica is a commercial prospecting engine. It takes a company that might be worth selling to
and carries it all the way to a conversation with the right person — researching the company,
identifying who actually decides, writing the approach, running the outreach across every
channel, and handing the sales rep a live conversation instead of a list.

It is **not** a contact database, and it is **not** a bulk sending tool. The unit of work is a
single company studied properly, not ten thousand rows sprayed with the same template.

The product is built around one uncomfortable commitment: **the system says what it actually
knows.** A score with no analysis behind it is not displayed. A figure with no source is not
displayed. When the system cannot verify something, it says so rather than filling the gap with
something plausible.

## What it does

**Research.** Given a company, it gathers what is publicly available, cross-checks sources
against each other, and builds a dossier: what the company does, its size and sector, signals of
activity, and the concrete pain the offer speaks to. Sources that disagree are flagged, not
averaged.

**Decision-maker identification.** It finds the person with actual authority for this specific
purchase — distinguishing authority from mere reachability, which are not the same thing and are
routinely confused. Confidence in that identification is measured and shown.

**Qualification.** A single score, with a plain-language verdict attached. One number, one
meaning. Temperature (how ready they are) is tracked separately from fit (how good a match they
are) — collapsing the two hides exactly the cases worth looking at.

**Outreach across channels.** Email, WhatsApp, SMS and voice, run as a sequence with real
timing, not a blast. The AI writes each message for that company and that person, from the
dossier. A voice agent can place and take calls, transcribe them, and hand off to a human at the
right moment.

**Cadence and rules.** Business-hours windows, do-not-contact enforcement, deduplication across
channels, burnout detection on channels that stop working, and automatic de-confliction when a
human and the system are both working the same lead.

**Handoff.** When a lead responds, it is routed to the right rep with the full history attached.
Inbound is never left unanswered — that is a hard rule, not a setting.

**Role-based panels.** Different people see different systems: the rep sees their own pipeline,
the supervisor sees the team, the administrator sees the account, the operator sees the fleet.
Reps are independent of one another by design.

**Cost and margin visibility.** Every AI call, every enrichment, every message is priced and
attributed. The cost of producing a lead is a number the operator can see, not an estimate.

## Architecture

**A master instance and a fleet.** One central instance holds the commercial relationship,
plans, limits and the provider credentials. Each client runs their own installation, with their
own database, their own domain and their own data. The two talk over a single authenticated
channel — the client's installation asks, using its own key; the master never reaches into it.
A client's data never leaves their installation.

This is deliberately **not** multi-tenant. Isolation is physical, not a `WHERE` clause.

**Domain-free deliberation engine.** The reasoning core is separated from the business domain: a
multi-agent engine that investigates, argues with itself, audits its own conclusions
adversarially, and escalates to deeper analysis only when the question warrants the cost. It
knows nothing about sales — the domain is configuration handed to it.

**Escalating analysis.** Work is tiered. Cheap, shallow passes handle most companies; expensive,
deep multi-agent deliberation is reserved for the ones that earn it. A person decides when to
escalate to the most expensive tier — the system does not spend that money on its own.

**Channel drivers behind one interface.** Every messaging and voice provider sits behind a common
driver contract, so a provider can be swapped without touching the engine. Nothing in the core
knows which vendor is delivering a message.

**Workflow engine.** Outreach sequences are data, not code: steps, conditions, waits and
branches, executed by an engine that can resume, retry and refuse. Failures are recorded as
states, not swallowed.

**Fail loudly.** Missing configuration stops a run at startup with the exact name of what is
missing. There are no default credentials, no silent fallbacks, and no code path that guesses
when it should ask.

## Principles

These are the rules the system is actually built to, in the order they get defended:

1. **Silence is never an option.** A lead that has been picked up and then ignored is worse than
   a lead never touched. Every path out of the system ends in a response.
2. **If the client writes, they get an answer.** Always. Business-hours windows apply to
   outbound only — never to someone who reached out.
3. **One score, one verdict.** No competing numbers, no rating without the analysis that
   produced it, no figure without a source.
4. **Honesty over optimism.** The system does not report success it has not verified. If a third
   party decides the outcome, the system asks that third party rather than assuming.
5. **Never touch real data in tests.** Backups first, fictitious records, and a filter that keeps
   test runs off production rows.
6. **Running out of credit stops spending, never data.** A client behind on payment loses
   outbound activity — never their leads, their history, or their inbound.
7. **Every alert declares its audience.** Infrastructure noise goes to operators, never to
   clients.
8. **Reps are independent.** Each rep owns their own leads; visibility is granted, not assumed.
9. **Cost is measured, not estimated.** If the price of a model is unknown, it is recorded as
   unknown rather than guessed.

## Status

In production, used commercially. Under active development. The source code is private; this
repository is the public description of the product.

---
---

<a id="vórtica-español"></a>

# Vórtica (Español)

**Motor de prospección comercial con IA — de una empresa cualquiera a una conversación con quien
decide.**

🇦🇷 Español · 🇬🇧 [English](#vórtica)

---

## Índice

- [Qué es Vórtica](#qué-es-vórtica)
- [Qué hace](#qué-hace)
- [Arquitectura](#arquitectura-1)
- [Principios](#principios)
- [Estado](#estado)

---

## Qué es Vórtica

Vórtica es un motor de prospección comercial. Agarra una empresa a la que quizás valga la pena
venderle y la lleva hasta una conversación con la persona correcta: investiga la empresa,
identifica quién decide de verdad, escribe el acercamiento, ejecuta el contacto por todos los
canales y le entrega al vendedor una conversación viva en lugar de una lista.

**No** es una base de contactos y **no** es una herramienta de envío masivo. La unidad de trabajo
es una empresa estudiada en serio, no diez mil filas rociadas con la misma plantilla.

El producto está construido alrededor de un compromiso incómodo: **el sistema dice lo que
realmente sabe.** Un score sin análisis detrás no se muestra. Una cifra sin fuente no se muestra.
Cuando el sistema no puede verificar algo, lo dice, en vez de tapar el hueco con algo verosímil.

## Qué hace

**Investigación.** Dada una empresa, junta lo que hay disponible públicamente, cruza las fuentes
entre sí y arma un dossier: a qué se dedica, tamaño y sector, señales de actividad, y el dolor
concreto al que le habla la oferta. Cuando las fuentes se contradicen, se marca la
contradicción — no se promedia.

**Identificación del decisor.** Encuentra a la persona con autoridad real sobre esa compra en
particular, distinguiendo **autoridad** de **accesibilidad**, que no son lo mismo y se confunden
todo el tiempo. La confianza en esa identificación se mide y se muestra.

**Calificación.** Un score único, con un veredicto en castellano al lado. Un número, un
significado. La **temperatura** (qué tan listo está) se sigue por separado del **encaje** (qué tan
buen candidato es): mezclarlos esconde justo los casos que hay que mirar.

**Contacto multicanal.** Email, WhatsApp, SMS y voz, ejecutados como una secuencia con tiempos
reales, no como una descarga. La IA escribe cada mensaje para esa empresa y esa persona, a partir
del dossier. Un agente de voz puede llamar y atender, transcribir, y pasarle la llamada a una
persona en el momento justo.

**Cadencia y reglas.** Ventanas de horario comercial, respeto de las listas de no-contactar,
deduplicación entre canales, detección de canales quemados, y desconflicción automática cuando
una persona y el sistema trabajan el mismo lead a la vez.

**Traspaso.** Cuando un lead responde, se enruta al vendedor que corresponde con todo el
historial encima. El inbound nunca queda sin respuesta: es una regla dura, no una preferencia.

**Paneles por rol.** Cada persona ve un sistema distinto: el vendedor ve su cartera, el
supervisor ve al equipo, el administrador ve la cuenta, el operador ve la flota. Los vendedores
son independientes entre sí por diseño.

**Costo y margen a la vista.** Cada llamada a un modelo, cada enriquecimiento y cada mensaje
tienen precio y dueño. Lo que cuesta producir un lead es un número que el operador ve, no una
estimación.

## Arquitectura

**Una maestra y una flota.** Una instancia central sostiene la relación comercial, los planes,
los topes y las credenciales de los proveedores. Cada cliente corre su propia instalación, con su
base, su dominio y sus datos. Las dos hablan por un único canal autenticado: la instalación del
cliente **pregunta**, con su propia llave; la maestra nunca entra. Los datos de un cliente no
salen de su instalación.

Esto **no** es multi-tenant, a propósito. El aislamiento es físico, no una cláusula `WHERE`.

**Motor de deliberación sin dominio.** El núcleo de razonamiento está separado del negocio: un
motor multiagente que investiga, discute consigo mismo, audita sus propias conclusiones de forma
adversarial, y escala a un análisis más profundo sólo cuando la pregunta justifica el costo. No
sabe nada de ventas: el dominio es configuración que se le entrega.

**Análisis en escalera.** El trabajo está escalonado. Pasadas baratas y superficiales resuelven la
mayoría de las empresas; la deliberación multiagente cara queda reservada para las que se la
ganan. El salto al escalón más caro **lo dispara una persona**: el sistema no gasta esa plata
solo.

**Los canales, detrás de una sola interfaz.** Cada proveedor de mensajería y de voz vive detrás de
un contrato común, así que se puede cambiar de proveedor sin tocar el motor. Nada en el núcleo
sabe qué empresa está entregando un mensaje.

**Motor de workflows.** Las secuencias de contacto son datos, no código: pasos, condiciones,
esperas y ramas, ejecutados por un motor que sabe retomar, reintentar y negarse. Las fallas quedan
registradas como estados, no se las traga nadie.

**Fallar fuerte.** Si falta configuración, la corrida se detiene al arrancar diciendo el nombre
exacto de lo que falta. No hay credenciales por defecto, no hay fallbacks callados, y no hay
camino que adivine donde debería preguntar.

## Principios

Estas son las reglas a las que el sistema está realmente construido, en el orden en que se
defienden:

1. **El silencio nunca es opción.** Un lead que alguien tomó y después dejó colgado es peor que un
   lead que nadie tocó. Todos los caminos de salida terminan en una respuesta.
2. **Si el cliente escribe, se le responde.** Siempre. El horario comercial aplica sólo al
   outbound, nunca a alguien que se acercó.
3. **Un score, un veredicto.** Sin números que compitan, sin rótulo sin el análisis que lo
   produjo, sin cifra sin fuente.
4. **Honestidad antes que optimismo.** El sistema no reporta un éxito que no verificó. Si el
   resultado lo decide un tercero, se le pregunta al tercero en vez de suponerlo.
5. **Nunca tocar datos reales en pruebas.** Backup primero, registros ficticios, y un filtro que
   mantenga las corridas de prueba lejos de las filas de producción.
6. **Quedarse sin crédito frena el gasto, nunca los datos.** Un cliente atrasado pierde actividad
   saliente; nunca sus leads, su historial ni su inbound.
7. **Cada alerta declara a quién va.** El ruido de infraestructura va al operador, nunca al
   cliente.
8. **Los vendedores son independientes.** Cada uno es dueño de sus leads; la visibilidad se
   otorga, no se asume.
9. **El costo se mide, no se estima.** Si el precio de un modelo no se conoce, se registra como
   desconocido en vez de inventarlo.

## Estado

En producción, en uso comercial. En desarrollo activo. El código fuente es privado; este
repositorio es la descripción pública del producto.
