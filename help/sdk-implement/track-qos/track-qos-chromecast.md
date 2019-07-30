---
seo-title: Seguimiento de la calidad de la experiencia en Chromecast
title: Seguimiento de la calidad de la experiencia en Chromecast
uuid: d 0 cdc 8 cd -4 db 0-45 ef -9470-1 cba 3996305 b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Seguimiento de la calidad de la experiencia en Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## Información general {#section_DDB8DFA47C5744AB9A04392AD5959BF7}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Puede utilizar la API de reproductor de medios para identificar las variables relacionadas con qos y el seguimiento de errores.

## Player events {#player-events}

### En todos los eventos de cambio de velocidad de bits

* Creación/actualización de la instancia del objeto QoS para la reproducción, `qosObject`
* La llamada `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Para los errores del reproductor

La llamada `trackError(“media error id”);`

## Implementación {#section_3B8EBEB167624D0481E8AF4761F83047}

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   **Variables QoSObject:**

   >[!TIP]
   >
   >Estas variables solo se requieren si planea rastrear qos.

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
   >Actualice el objeto qos y llame al suceso change de velocidad de bits en cada cambio de velocidad de bits. Esto proporciona los datos de QoS más precisos.

1. Asegúrese de que el método `getQoSObject()` devuelve la información de QoS más actual.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Consulte [Información general](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >El seguimiento de los errores del reproductor de medios no detendrá la sesión de seguimiento de medios. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

