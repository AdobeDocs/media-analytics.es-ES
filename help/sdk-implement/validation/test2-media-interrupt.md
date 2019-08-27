---
seo-title: Interrupción de la prueba 2 Media
title: Interrupción de la prueba 2 Media
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# Prueba 2: Interrupción de medios{#test-media-interruption}

Este caso de prueba valida el comportamiento de interrupción móvil. Es un elemento requerido de la solicitud de certificación.

## Formulario de solicitud de certificación

**Descargue aquí el formulario de solicitud de certificación: = = &gt;**  [Formulario de solicitud de certificación.](cert_req_form.docx)

## Procedimiento de prueba

Debe completar y registrar estas tareas en el siguiente orden:

1. **Iniciar el reproductor de medios**

   Cuando se inicia el reproductor de medios, se envían las llamadas siguientes en el orden siguiente:

   1. Inicio de Adobe Analytics (appmeasurement)
   1. Inicio de Media Analytics (latidos)
   1. Llamada de inicio de Media Analytics (latidos) Solicitud de inicio de Adobe Analytics
   Las dos primeras llamadas de arriba contienen metadatos y variables adicionales. Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La tercera llamada anterior indica al servidor de Media Analytics que el SDK de medios ha solicitado que la llamada de inicio de Adobe Analytics (`pev2=ms_s`) se envíe al servidor de Adobe Analytics.

1. **Reproducción ininterrumpida del contenido principal durante al menos 5 minutos**

   **Reproducción de contenido**

   Durante la reproducción del contenido, el SDK de medios envía llamadas de reproducción (latidos) al servidor de Media Analytics cada diez segundos.

   Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Mover la aplicación o el navegador al fondo**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **Volver a traer la aplicación o el navegador a primer plano**

   Cuando la aplicación vuelva al primer plano, el contenido se reanudará.

1. **Reproducción ininterrumpida de los medios principales de contenido durante al menos 5 minutos**

   Para obtener parámetros de llamada y metadatos, consulte [Detalles de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Cerrar reproductor de medios**

   Ninguna llamada de seguimiento adicional se activará después de cerrar el reproductor de medios.

