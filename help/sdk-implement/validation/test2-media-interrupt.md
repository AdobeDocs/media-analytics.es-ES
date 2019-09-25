---
seo-title: Test 2  Media interruption
title: Test 2  Media interruption
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# Test 2: Media interruption{#test-media-interruption}

This test case validates mobile interruption behavior. It is a required element of your certification request.

## Certification Request Form

**Descargue el formulario de solicitud de certificación aquí: ==&gt;Formulario** de solicitud de [certificación.](cert_req_form.docx)

## Test procedure

Debe completar y registrar estas tareas en el siguiente orden:

1. **Iniciar el reproductor de medios**

   Cuando se inicia el reproductor de medios, las siguientes llamadas se envían en el siguiente orden:

   1. Inicio de Adobe Analytics (AppMeasurement)
   1. Inicio de Media Analytics (latidos)
   1. Llamada de inicio de Adobe Analytics (latidos) de Media Analytics solicitada
   Las dos primeras llamadas anteriores contienen metadatos y variables adicionales. Para ver los parámetros y metadatos de la llamada, consulte Detalles [de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La tercera llamada anterior indica al servidor de Media Analytics que el SDK de medios solicitó que la llamada de inicio (`pev2=ms_s`) de Adobe Analytics se enviara al servidor de Adobe Analytics.

1. **Play main content for at least 5 minutes uninterrupted**

   **Reproducción de contenido**

   Durante la reproducción de contenido, el SDK de medios envía llamadas de reproducción (latidos) al servidor de Media Analytics cada diez segundos.

   Para ver los parámetros y metadatos de la llamada, consulte Detalles [de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Mover la aplicación o el navegador al fondo**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **Bring app or browser back to foreground**

   Cuando la aplicación vuelva al primer plano, el contenido se reanudará.

1. **Play main content media for at least 5 minutes uninterrupted**

   Para ver los parámetros y metadatos de la llamada, consulte Detalles [de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Cerrar reproductor multimedia**

   Ninguna llamada de seguimiento adicional debe activarse después de cerrar el reproductor multimedia.

