---
title: Control del orden de los eventos
description: Control del orden de los eventos
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: 27694ec83de89980404df7a7cc77fa42b3d1a751
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 4%

---

# Control del orden de los eventos {#controlling-the-order-of-events}

El seguimiento de vídeo en flujo es una operación dependiente del tiempo y, ocasionalmente, las llamadas de seguimiento de API de recopilación de contenido llegan al back end sin orden. En esta situación, el back end intenta poner en cola y reordenar eventos basados en la marca de tiempo proporcionada en el objeto `playerTime`.  Esto ocurre con algunos límites. Actualmente, la reordenación puede fallar si los retrasos entre las llamadas desordenadas son superiores a un segundo. En futuras actualizaciones, el &quot;tiempo de demora aceptable&quot; puede optimizarse y configurarse.

## Ejemplo de evento desordenado

Los eventos desordenados se producen cuando los eventos pasan por la red, lo que a veces provoca un retraso.

Por ejemplo, puede enviar un evento `adBreakStart` seguido de un evento `adStart`. Este es un caso de uso común, ya que es necesario para que un anuncio comience dentro de una pausa publicitaria.

Si el anuncio está listo y no se necesita búfer, ambos eventos se producen casi instantáneamente y el `playerTime.ts` para ambos eventos está muy cerca el uno del otro, pero nunca deben ser iguales.

> &quot;playerTime.ts&quot; de eventos nunca debe ser igual para ningún evento, ya que el algoritmo de clasificación no sabría qué evento ocurrió primero. Debe haber al menos 1 milisegundo de diferencia de marca de tiempo para cada 2 eventos consecutivos.

Puesto que ambos eventos se producen muy cerca entre sí en el momento en que se activan las llamadas de red, es posible que lleguen desordenados. En este ejemplo, el evento `adStart` llega antes del evento `adBreakStart`.


Hay una ventana temporizada de eventos: 5 segundos o un máximo de 10 eventos. Los eventos se almacenan en búfer antes de enviarlos a la canalización de procesamiento. Cuando se cumplen las condiciones: han pasado 5 segundos o más de 10 eventos, los eventos se reordenan en función del `playerTime.ts` y luego se envían en el nuevo orden, a la canalización de procesamiento.

>[!IMPORTANT]
>
>Hay un evento de excepción que se envía inmediatamente a la canalización de procesamiento y que es el evento `sessionStart`.
