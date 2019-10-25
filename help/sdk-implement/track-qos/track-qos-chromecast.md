---
seo-title: Seguimiento de la calidad de la experiencia en Chromecast
title: Seguimiento de la calidad de la experiencia en Chromecast
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Seguimiento de la calidad de la experiencia en Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## Información general {#overview}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Puede utilizar la API del reproductor de medios para identificar las variables relacionadas con QoS y el seguimiento de errores.

## Eventos del reproductor {#player-events}

### En todos los eventos de cambio de velocidad de bits

* Creación/actualización de la instancia del objeto QoS para la reproducción, `qosObject`
* La llamada `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Para los errores del reproductor

La llamada `trackError(“media error id”);`

## Implementación {#implement}

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   **Variables QoSObject:**

   >[!TIP]
   >
   >Estas variables solo son necesarias si planea realizar un seguimiento de QoS.

   | Variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `bitrate` | Velocidad de bits actual | Sí |
   | `startupTime` | Hora de inicio | Sí |
   | `fps` | Valor FPS | Sí |
   | `droppedFrames` | Número de fotogramas perdidos | Sí |

   **Creación del objeto de QoS:** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. Cuando la velocidad de bits de la reproducción cambie, invoque el evento `BitrateChange` en la instancia de Media Heartbeat: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent).

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >Actualice el objeto QoS y llame al evento de cambio de velocidad de bits en cada cambio de velocidad de bits. Esto proporciona los datos de QoS más precisos.

1. Asegúrese de que el método `getQoSObject()` devuelve la información de QoS más actual.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Consulte [Información general](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >El seguimiento de los errores del reproductor de medios no detendrá la sesión de seguimiento de medios. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

