---
title: Prueba 2  Interrupción de contenido
description: Obtenga información sobre la prueba de interrupción de contenido que se utiliza en la validación.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 96%

---

# Prueba 2: Interrupción de contenido {#test-media-interruption}

Este caso de prueba valida el comportamiento de la interrupción móvil.

## Procedimiento de prueba

Debe completar y registrar estas tareas en el siguiente orden:

1. **Iniciar el reproductor de contenidos**

   Cuando se inicia el reproductor de contenido, estas llamadas se envían en el siguiente orden:

   1. Inicio de Adobe Analytics (AppMeasurement)
   1. Inicio de Media Analytics (latidos)
   1. Llamada de inicio de Adobe Analytics (latidos) de Media Analytics solicitada

   Las dos primeras llamadas descritas contienen metadatos y variables adicionales. Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La tercera llamada descrita indica al servidor de Media Analytics que Media SDK solicitó que la llamada de inicio (`pev2=ms_s`) de Adobe Analytics se enviara al servidor de Adobe Analytics.

1. **Reproducir el contenido principal durante 5 minutos sin pausarlo**

   **Reproducción de contenido**

   Durante la reproducción de contenido, Media SDK envía llamadas de reproducción (latidos) al servidor de Media Analytics cada diez segundos.

   Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Además, consulte las instrucciones de [Seguimiento de anuncios](/help/sdk-implement/track-ads/track-ads-overview.md) de su plataforma para obtener más información sobre las llamadas de anuncio.

1. **Mover la aplicación o el navegador al fondo**

   Mientras la aplicación se ejecuta en segundo plano, solo las llamadas de `main:pause` se enviarán al servidor de Media Analytics, a partir de la versión VHL 1.6.6.

1. **Traer la aplicación o el explorador al primer plano**

   Cuando la aplicación vuelva al primer plano, el contenido se reanudará.

1. **Reproducir el contenido principal durante 5 minutos sin pausarlo**

   Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Cerrar reproductor multimedia**

   No se activarán llamadas de seguimiento adicionales tras cerrar el reproductor de contenido.
