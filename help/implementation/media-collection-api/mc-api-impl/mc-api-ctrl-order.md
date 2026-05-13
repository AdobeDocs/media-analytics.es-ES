---
title: Control del orden de los eventos
description: Obtenga información sobre cómo controlar el orden de los eventos y cómo, en algunos casos, se reordenan los eventos en función de la marca de tiempo proporcionada en el objeto playerTime.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LSKiNN-obuHzVYKbAai52SQ2MvI6-gzgb-G-x0DH2dE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 342
ht-degree: 100%

---

# Control del orden de los eventos{#controlling-the-order-of-events}

El seguimiento de secuencias de vídeo es una operación que depende en gran medida del tiempo y, en ocasiones, las llamadas de seguimiento de la Media Collection API llegan al servidor fuera de orden. En esta situación, el servidor intenta poner en cola y reordenar los eventos basándose en la marca de tiempo proporcionada en el objeto `playerTime`.  Esto ocurre con algunos límites. Actualmente, la reordenación puede fallar si los retrasos entre las llamadas a un pedido son de más de un segundo. En futuras actualizaciones, el “tiempo de demora aceptable” puede optimizarse y configurarse.

## Ejemplo de evento desordenado

Los eventos desordenados se producen cuando los eventos pasan por la red, lo que a veces provoca un retraso.

Por ejemplo, puede enviar un `adBreakStart` seguido de un `adStart` evento. Este es un caso de uso común, ya que es necesario para que un anuncio comience dentro de una pausa publicitaria.

Si el anuncio está listo y no se necesita búfer, ambos eventos se producen casi instantáneamente y la variable `playerTime.ts` para ambos eventos son muy cercanos entre sí, pero nunca deben ser iguales.

> &quot;playerTime.ts&quot; de eventos nunca debe ser igual para ningún evento, ya que el algoritmo de clasificación no sabría qué evento ocurrió primero. Debe haber al menos 1 milisegundo de diferencia de marca de tiempo para cada 2 eventos consecutivos.

Puesto que ambos eventos se producen muy cerca entre sí en el momento en que se activan las llamadas de red, es posible que lleguen desordenados. En este ejemplo, el evento `adStart` llega antes del evento `adBreakStart`.


Hay una ventana temporizada de eventos: 5 segundos o un máximo de 10 eventos. Los eventos se almacenan en búfer antes de enviarlos a la canalización de procesamiento. Cuando se cumplen las condiciones: han transcurrido 5 segundos o se han recibido más de 10 eventos, los eventos se reordenan en función de la variable `playerTime.ts` y luego se envían en el nuevo pedido a la canalización de procesamiento.

>[!IMPORTANT]
>
>Hay un evento de excepción que se envía a la canalización de procesamiento de inmediato y que es el evento `sessionStart`.
