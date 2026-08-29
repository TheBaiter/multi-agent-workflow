# multi-agent-workflow

[![skills.sh](https://skills.sh/b/TheBaiter/multi-agent-workflow)](https://skills.sh/TheBaiter/multi-agent-workflow)

Skill experimental para organizar trabajo con **subagentes** mediante ciclos de investigación y validación, en lugar de confiar en una única planificación lineal.

> Estado actual: definición de alcance. La arquitectura completa, los perfiles y los contratos entre agentes todavía se están diseñando.

## Por qué existe

La idea nace de un problema práctico: las automatizaciones y los agentes actuales pueden funcionar "bien", pero no necesariamente detectan todos los errores ni validan correctamente cada etapa.

Un agente puede encontrar algo que parece un problema y producir una explicación razonable. El riesgo aparece cuando esa primera conclusión se convierte en una verdad asumida por todo lo que viene después.

Eso puede provocar, entre otras cosas:

- que un **falso positivo** sea aceptado por el resto de la cadena;
- que el **alcance real** del problema quede incompleto;
- que una planificación aparentemente correcta tenga **huecos o supuestos no comprobados**;
- que una mejora local termine introduciendo una **regresión** en otra parte del sistema;
- que una sola IA fuerce las piezas para que encajen con su primera hipótesis.

## Idea central

Este proyecto pretende convertir ese proceso en un workflow de subagentes con objetivos acotados.

La primera detección puede ser directa: un agente detective puede identificar un posible problema y dejarlo como candidato.

A partir de ahí, las etapas posteriores **no deben aceptar automáticamente la conclusión anterior ni resolver todo de una sola vez**.

Cada etapa relevante debe volver sobre el problema mediante ciclos de búsqueda, inspección, contraste y validación. Las conclusiones heredadas se tratan como hipótesis que pueden ser confirmadas, ampliadas, corregidas o rechazadas.

Los resultados de esos ciclos deben quedar registrados para que el proceso sea auditable y para evitar que una conclusión importante exista solamente dentro del contexto temporal de un agente.

## Principios iniciales

1. **Usar subagentes reales.** La separación de responsabilidades debe implicar contextos de trabajo independientes cuando la plataforma lo permita.
2. **Un objetivo principal por subagente.** Evitar agentes que detectan, diagnostican, planifican, implementan y validan todo a la vez.
3. **No confiar ciegamente en el paso anterior.** Su salida es evidencia de entrada, no una verdad definitiva.
4. **Evitar la planificación one-shot.** Las etapas posteriores a la detección deben investigar y validar en múltiples pases.
5. **Buscar contradicciones.** El workflow debe intentar demostrar que sus propias hipótesis están equivocadas, no sólo reunir evidencia que las confirme.
6. **Persistir evidencia y dudas.** Cada ciclo debería dejar constancia de qué buscó, qué encontró, qué contradicciones aparecieron y qué quedó sin resolver.
7. **No avanzar con huecos críticos.** Una etapa puede terminar como inconclusa o rechazada; completar el workflow no es más importante que detectar incertidumbre real.

## El costo

Este enfoque será más lento que pedirle a un único agente que analice el problema y produzca inmediatamente un plan.

También será más costoso en tokens, llamadas a herramientas y ejecuciones de subagentes. Sí: probablemente bastante costoso 😭.

La intención no es eliminar ese costo artificialmente, porque parte del valor proviene precisamente de realizar comprobaciones independientes. El objetivo será hacerlo **eficiente dentro de una estrategia deliberadamente exhaustiva**: contextos pequeños, objetivos concretos y ciclos que aporten nueva evidencia en lugar de repetir el mismo análisis.

## Alcance actual

Por ahora, esta skill define únicamente las bases:

- está diseñada para trabajar con subagentes;
- la detección inicial puede realizarse en una única etapa;
- la investigación, validación y planificación posteriores no deben ser lineales ni one-shot;
- cada conclusión importante debe poder ser cuestionada por etapas posteriores;
- el workflow debe conservar evidencia de sus ciclos.

Todavía **no** están fijados:

- los perfiles definitivos de los subagentes;
- la cantidad exacta de ciclos o pases por etapa;
- los criterios de aprobación y rechazo;
- el formato definitivo de los artefactos de evidencia;
- el orquestador y sus reglas de retorno;
- el proceso de implementación y QA final.

Esos puntos se definirán antes de considerar estable la skill.

## Instalación

Con [skills.sh](https://skills.sh/):

```bash
npx skills add TheBaiter/multi-agent-workflow
```

## Estado

**Experimental / en diseño.**

La prioridad actual es definir correctamente el método antes de añadir complejidad, perfiles o automatizaciones concretas.
