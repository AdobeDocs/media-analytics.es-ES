---
seo-title: Seguimiento de errores en JavaScript
title: Seguimiento de errores en JavaScript
uuid: 5 a 4 fc 5 df -2677-4189-92 af -5 cd 074847 b 39
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Seguimiento de errores en JavaScript{#track-errors-on-javascript}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](../../sdk-implement/download-sdks.md)

## Implementación del seguimiento de errores

1. Rastree los errores del reproductor de medios:

   ```js
   onPlayerError = function() { 
       this._mediaHeartbeat.trackError("mediaErrorId"); 
   };
   ```

>[!NOTE]
>
>El seguimiento de los errores del reproductor de medios no detendrá la sesión de seguimiento de medios. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

