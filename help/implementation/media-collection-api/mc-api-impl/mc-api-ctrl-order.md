---
title: Control del orden de los eventos
description: Obtenga información sobre cómo controlar el orden de los eventos y cómo, en algunos casos, se reordenan los eventos en función de la marca de tiempo proporcionada en el objeto playerTime.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LSKiNN-obuHzVYKbAai52SQ2MvI6-gzgb-G-x0DH2dE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 73%

---

# Control del orden de los eventos{#controlling-the-order-of-events}

El seguimiento de secuencias de vídeo es una operación que depende en gran medida del tiempo y, en ocasiones, las llamadas de seguimiento de la Media Collection API llegan al servidor fuera de orden. En esta situación, el servidor intenta poner en cola y reordenar los eventos basándose en la marca de tiempo proporcionada en el objeto `playerTime`.  Esto ocurre con algunos límites. Actualmente, la reordenación puede fallar si los retrasos entre las llamadas a un pedido son de más de un segundo. En futuras actualizaciones, el “tiempo de demora aceptable” puede optimizarse y configurarse.

## Ejemplo de evento desordenado

Los eventos desordenados se producen cuando los eventos pasan por la red, lo que a veces provoca un retraso.

Por ejemplo, puede enviar un `adBreakStart` seguido de un `adStart` evento. Este es un caso de uso común, ya que es necesario para que un anuncio comience dentro de una pausa publicitaria.

Si el anuncio está listo y no se necesita búfer, ambos eventos se producen casi instantáneamente y el `playerTime.ts` de ambos eventos está muy cerca uno del otro. Sin embargo, nunca deben ser iguales, ya que el algoritmo de ordenación no sabría qué evento se produjo primero. Mantenga siempre al menos una diferencia de marca de tiempo de 1 milisegundo para cualquier evento consecutivo.

Puesto que ambos eventos se producen muy cerca entre sí en el momento en que se activan las llamadas de red, es posible que lleguen desordenados. En este ejemplo, el evento `adStart` llega antes del evento `adBreakStart`.

Hay una ventana temporizada de eventos: 5 segundos o un máximo de 10 eventos. Los eventos se almacenan en búfer antes de enviarlos a la canalización de procesamiento. Cuando se cumplen las condiciones (han transcurrido 5 segundos o se han recibido más de 10 eventos), los eventos se reordenan en función de `playerTime.ts` y, a continuación, se envían en el nuevo orden a la canalización de procesamiento.

>[!IMPORTANT]
>
>Hay un evento de excepción que se envía a la canalización de procesamiento de inmediato y que es el evento `sessionStart`.
