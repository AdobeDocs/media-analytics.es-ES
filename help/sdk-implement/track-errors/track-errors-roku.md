---
seo-title: Seguimiento de errores en Roku
title: Seguimiento de errores en Roku
uuid: 4 e 0165 f 9-9169-47 ed -9 f 11-ea 8 a 8778 f 663
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Seguimiento de errores en Roku{#track-errors-on-roku}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](../../sdk-implement/download-sdks.md)

## Implementación del seguimiento de errores

1. Rastree los errores del reproductor de medios:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(), 
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>El seguimiento de los errores del reproductor de medios no detendrá la sesión de seguimiento de medios. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

