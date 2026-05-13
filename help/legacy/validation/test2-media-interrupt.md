---
title: 'Prueba 2: Interrupción de contenido'
description: Obtenga información sobre la prueba de interrupción de medios que se utiliza en la validación.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gVEDMjM05nDnzCB6l-9CjyUzoArcmyN4jgsjmjllRiY
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 100%

---

# Prueba 2: Interrupción de contenido{#test-media-interruption}

Este caso de prueba valida el comportamiento de la interrupción móvil.

## Procedimiento de prueba

Debe completar y registrar estas tareas en el siguiente orden:

1. **Iniciar el reproductor de contenidos**

   Cuando se inicia el reproductor de contenido, estas llamadas se envían en el siguiente orden:

   1. Inicio de Adobe Analytics (AppMeasurement)
   1. Inicio de Media Analytics (latidos)
   1. Llamada de inicio de Adobe Analytics (latidos) de Media Analytics solicitada

   Las dos primeras llamadas descritas contienen metadatos y variables adicionales. Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   La tercera llamada descrita indica al servidor de Media Analytics que Media SDK solicitó que la llamada de inicio (`pev2=ms_s`) de Adobe Analytics se enviara al servidor de Adobe Analytics.

1. **Reproducir el contenido principal durante 5 minutos sin pausarlo**

   **Reproducción de contenido**

   Durante la reproducción de contenido, Media SDK envía llamadas de reproducción (latidos) al servidor de Media Analytics cada diez segundos.

   Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/legacy/validation/test-call-details.md#play-main-content)

   Consulte también las instrucciones de [Seguimiento de anuncios](/help/use-cases/track-ads/track-ads-overview.md) de su plataforma para obtener información adicional sobre estas llamadas a anuncios.

1. **Mover la aplicación o el navegador al fondo**

   Mientras la aplicación se ejecuta en segundo plano, solo las llamadas de `main:pause` se enviarán al servidor de Media Analytics, a partir de la versión VHL 1.6.6.

1. **Traer la aplicación o el explorador al primer plano**

   Cuando la aplicación vuelva al primer plano, el contenido se reanudará.

1. **Reproducir el contenido principal durante 5 minutos sin pausarlo**

   Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Cerrar reproductor multimedia**

   No se activarán llamadas de seguimiento adicionales tras cerrar el reproductor de contenido.
