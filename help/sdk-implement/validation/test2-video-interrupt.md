---
seo-title: Interrupción del vídeo 2 de prueba
title: Interrupción del vídeo 2 de prueba
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Prueba 2: Interrupción de vídeo{#test-video-interruption}

Esta prueba es necesaria como parte del formulario de solicitud de certificación y valida el comportamiento de interrupción de dispositivos móviles.

Download the certification request here: [Certification Request Form.](cert_req_form_nielsen.docx)

Debe completar y registrar estas tareas en el siguiente orden:

1. **Inicio del reproductor de vídeo**

   Cuando se inicia el reproductor de vídeo, estas llamadas se envían en el siguiente orden:

   1. Inicio de análisis de medios
   1. Inicio de Heartbeat
   1. Inicio del análisis de Heartbeat
   Las dos primeras llamadas de arriba contienen metadatos y variables adicionales. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

1. **Reproducir el vídeo durante 5 minutos sin pausarlo**

   **Reproducción de contenido**

   Durante la reproducción de contenido principal normal, las llamadas de Heartbeat se envían al servidor cada diez segundos.

   For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](../../sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Mover la aplicación o el navegador al fondo**

   Mientras la aplicación se ejecuta en segundo plano, solo las llamadas main:pause se enviarán al servidor de Heartbeat, a partir de la versión VHL 1.6.6.

1. **Llevar la aplicación o el navegador al fondo**

   Cuando la aplicación vuelva al primer plano, el contenido se reanudará.

1. **Reproducir el vídeo durante 5 minutos sin pausarlo**

   For call parameters and metadata, see [Test Call Details.](../../sdk-implement/validation/test-call-details.md)

1. **Cerrar el reproductor de vídeo**

   No deben activarse llamadas de seguimiento adicionales después de cerrar el reproductor de vídeo.

