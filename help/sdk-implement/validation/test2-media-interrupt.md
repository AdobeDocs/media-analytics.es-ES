---
seo-title: Interrupción de la prueba 2 Media
title: Interrupción de la prueba 2 Media
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Prueba 2: Interrupción de medios{#test-media-interruption}

Esta prueba es necesaria como parte del formulario de solicitud de certificación y valida el comportamiento de interrupción de dispositivos móviles.

Download the certification request here: [Certification Request Form.](cert_req_form.docx)

Debe completar y registrar estas tareas en el siguiente orden:

1. **Iniciar el reproductor de medios**

   Cuando se inicia el reproductor de medios, se envían las llamadas siguientes en el orden siguiente:

   1. Inicio de análisis de medios
   1. Inicio de Heartbeat
   1. Inicio del análisis de Heartbeat
   Las dos primeras llamadas de arriba contienen metadatos y variables adicionales. Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md)

1. **Reproducción ininterrumpida de los medios principales de contenido durante al menos 5 minutos**

   **Reproducción de contenido**

   Durante la reproducción de contenido principal normal, las llamadas de Heartbeat se envían al servidor cada diez segundos.

   Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Mover la aplicación o el navegador al fondo**

   Mientras la aplicación se ejecuta en segundo plano, solo las llamadas main:pause se enviarán al servidor de Heartbeat, a partir de la versión VHL 1.6.6.

1. **Llevar la aplicación o el navegador al fondo**

   Cuando la aplicación vuelva al primer plano, el contenido se reanudará.

1. **Reproducción ininterrumpida de los medios principales de contenido durante al menos 5 minutos**

   Para obtener parámetros de llamada y metadatos, consulte [Detalles de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md)

1. **Cerrar reproductor de medios**

   Ninguna llamada de seguimiento adicional se activará después de cerrar el reproductor de medios.

