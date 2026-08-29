# multi-agent-workflow

[![skills.sh](https://skills.sh/b/TheBaiter/multi-agent-workflow)](https://skills.sh/TheBaiter/multi-agent-workflow)

Skill experimental para investigar, corregir y validar **fallos funcionales de backend** mediante subagentes independientes que se cuestionan entre sí y dejan trazabilidad en la misma Issue.

## Por qué existe

La idea nace de un problema práctico: las automatizaciones y los agentes pueden funcionar "bien", pero no necesariamente detectan todos los errores ni validan correctamente cada etapa.

Un agente puede encontrar algo que parece un problema, construir una explicación razonable y luego forzar las piezas siguientes para que encajen con esa primera hipótesis. Si el primer hallazgo era un falso positivo, si el alcance estaba incompleto o si la planificación tenía un hueco, el error puede propagarse por toda la cadena.

Este proyecto intenta reducir ese riesgo mediante un workflow deliberadamente iterativo:

- un agente detecta un candidato;
- otro intenta demostrar si realmente existe;
- otro delimita causa y alcance;
- otro propone la solución mínima;
- otro intenta romper esa propuesta;
- otro diseña y ejecuta casos de prueba;
- otro implementa sin aprovechar para refactorizar cosas ajenas;
- un validador final vuelve a desconfiar de todo el proceso.

Si una etapa posterior encuentra una premisa incorrecta, puede devolver el caso a cualquier etapa anterior, incluso al principio.

## Alcance: sólo backend funcional

Esta skill **no es un code reviewer genérico**.

Busca defectos funcionales reales de backend, por ejemplo:

- lógica de negocio que produce un resultado incorrecto;
- persistencia o integridad de datos incorrecta;
- estados imposibles o transiciones inválidas;
- migraciones defectuosas;
- schemas y contratos backend incumplidos;
- transacciones o flujos backend que dejan el sistema en un estado funcionalmente incorrecto;
- integraciones entre capas backend cuyo comportamiento viola el contrato esperado;
- regresiones funcionales demostrables.

Quedan fuera por sí solos:

- frontend, UI, CSS o comportamiento visual;
- simplificaciones de código;
- code smells;
- renombrados;
- refactors estéticos;
- funciones largas;
- duplicación;
- arquitectura "fea" o con demasiadas responsabilidades;
- optimizaciones sin un defecto funcional demostrado.

Una arquitectura inestable puede explicar un bug, pero **la arquitectura inestable no es el bug**. Ese análisis debería pertenecer a otra skill especializada salvo que exista una consecuencia funcional verificable.

## Organización de agentes

Cada rol tiene un perfil separado para poder modificar su personalidad, límites y objetivos sin alterar a los demás. Todos los nombres visibles pertenecen a **Devil May Cry**; el protocolo depende del `Agent-Key`, no del personaje.

| Agent-Key | Agente | Rol | Ciclo |
| --- | --- | --- | --- |
| detective | Dante Sparda | Detectar candidatos funcionales backend | descubrimiento continuo |
| analyzer | Vergil | Confirmar, delimitar causa, origen y alcance | 8 pases |
| planner | V | Diseñar el arreglo mínimo coherente | 5 pases |
| challenger | Lady | Buscar huecos y contradicciones | 3 pases |
| test-strategist | Nico Goldstein | Diseñar y ejecutar/respaldar casos de prueba | 5 pases |
| executor | Nero | Implementar y reducir el cambio al mínimo acordado | variable |
| validator | Trish | Validación adversarial final | 10 pases |

Los nombres visibles son identidad humana. El identificador estable es Agent-Key, por lo que una personalidad puede renombrarse más adelante sin romper el protocolo.

## Una Issue es la sala de trabajo

Todos los agentes pueden operar usando la misma cuenta de GitHub. GitHub no distingue qué subagente escribió cada comentario, así que la skill impone propiedad lógica.

Cada agente mantiene **un comentario de estado vivo** que comienza, por ejemplo:

~~~text
Agente: Dante Sparda
Agent-Key: detective
Rol: Detective
Estado: INVESTIGATING
Paso: discovery
State-Revision: 4
~~~

Antes de editar, el agente lee la Issue y busca exactamente su Agent-Key:

- 0 coincidencias -> crea su comentario de estado;
- 1 coincidencia -> puede actualizar ese comentario;
- más de 1 -> STATE_CONFLICT; no edita ninguno hasta resolver la duplicación.

Un agente **nunca edita el estado de otro agente**.

No es necesario persistir ni recordar comment_id como parte del contrato. El agente reconstruye su identidad leyendo la Issue.

## Estado vivo + eventos permanentes

Editar únicamente el comentario de estado perdería contexto histórico. Por eso existen dos capas:

1. **State comment**: fotografía actual del agente. Se edita.
2. **Event comments**: preguntas, respuestas, rechazos, nueva evidencia, retornos y decisiones materiales. No se reescriben.

Toda decisión material debe indicar:

- decisión;
- motivo;
- evidencia;
- impacto sobre el workflow.

No vale "LGTM", "me parece bien" o "no me convence".

## Los agentes pueden cuestionarse

Un agente aprobado normalmente queda inactivo. No sigue hablando sólo porque la Issue cambió.

Puede reactivarse cuando:

- recibe una pregunta dirigida a su Agent-Key;
- aparece evidencia nueva que afecta una premisa bajo su responsabilidad;
- una etapa posterior detecta una divergencia, regresión o hueco;
- el workflow retorna explícitamente a su etapa.

Ejemplo conceptual:

~~~text
VALIDATOR -> PLANNER
QUESTION

La solución asume que X ocurre antes de Y.
¿Se consideró el fallo de Y después de persistir Z?

Reason:
...

Evidence:
...
~~~

El Planner debe revisar su propia decisión. Puede defenderla con evidencia o admitir que faltaba el caso y retroceder.

El objetivo no es defender el trabajo propio. El objetivo es defender la evidencia.

## Consenso

La Issue sólo puede cerrarse cuando **todos los roles obligatorios** están en APPROVED y cada aprobación está justificada.

Silencio no significa aprobación.

WAITING, BLOCKED, INCONCLUSIVE, REJECTED, REOPENED o APPROVED_WITH_RISK no forman consenso final.

Si el último agente encuentra un fallo que invalida el análisis original, el workflow puede volver desde validación hasta detección. El costo ya gastado no cuenta como evidencia.

## Ciclos, no prompts repetidos

"x8", "x5" o "x10" no significa repetir la misma pregunta varias veces.

Cada pase tiene un propósito diferente: contrato esperado, falsificación, alcance, datos, migraciones, dependencias, regresiones, contraejemplos, etc.

Al completar su último pase y aprobar, el agente se vuelve inactivo hasta que exista una razón material para reabrirlo.

## Companion: agent-context-foundation

Este proyecto está organizado siguiendo [$agent-context-foundation](https://github.com/TheBaiter/agent-context-foundation) para mantener el repositorio y el contexto de agentes ordenado, con progressive disclosure y un dueño canónico por regla.

Responsabilidades separadas:

- agent-context-foundation: contexto durable del repositorio, routing, organización de Agent/, conocimiento reusable y trazabilidad base;
- multi-agent-workflow: investigación y resolución de una Issue funcional backend mediante subagentes especializados.

La historia concreta del incidente debe permanecer en la Issue. Sólo conclusiones verificadas y reutilizables deberían promoverse al contexto durable del repositorio.

## Estructura

~~~text
SKILL.md
agents/
  openai.yaml
  README.md
  detective/PROFILE.md
  analyzer/PROFILE.md
  planner/PROFILE.md
  challenger/PROFILE.md
  test-strategist/PROFILE.md
  executor/PROFILE.md
  validator/PROFILE.md
references/
  scope.md
  workflow.md
  issue-protocol.md
  state-machine.md
  consensus.md
  agent-context-foundation.md
~~~

SKILL.md funciona como router. Los perfiles y referencias se cargan sólo cuando corresponden.

## Costo

Este workflow es intencionalmente más lento y costoso que pedirle a una sola IA que encuentre un problema y lo arregle de una vez.

Probablemente consuma bastantes tokens y ejecuciones de subagentes 😭.

La intención no es eliminar ese costo, porque la independencia de las comprobaciones es parte del beneficio. La optimización consiste en mantener contextos pequeños, objetivos acotados y pases distintos que aporten nueva evidencia.

## Instalación

~~~bash
npx skills add TheBaiter/multi-agent-workflow
~~~

Companion recomendado:

~~~bash
npx skills add TheBaiter/agent-context-foundation
~~~

## Estado

**Experimental.**

Los roles, estados, protocolo de Issue y consenso ya tienen una primera definición. La skill seguirá evolucionando a medida que se pruebe contra casos reales.
