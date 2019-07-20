---
seo-title: Seguimiento de errores en Android
title: Seguimiento de errores en Android
uuid: 7 d 0 c 77 e 5-924 c -4619-8 e 29-3484748 ab 736
translation-type: tm+mt
source-git-commit: 5ff3566fae2c1df559341057fafdd289774e4b2f

---


# Seguimiento de errores en Android{#track-errors-on-android}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](../../sdk-implement/download-sdks.md)

1. Rastree los errores del reproductor de medios:

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>El seguimiento de los errores del reproductor de medios no detendrá la sesión de seguimiento de medios. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

