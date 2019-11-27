---
title: Seguimiento de errores en Android
description: En este tema se describe el seguimiento de errores de implementación mediante el uso de Media SDK en Android.
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Seguimiento de errores en Android {#track-errors-on-android}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

1. Seguimiento de errores del reproductor de contenidos:

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>El seguimiento de los errores del reproductor de contenidos no detendrá la sesión de seguimiento de contenidos. Si el reproductor de contenidos impide que continúe la reproducción, asegúrese de que la sesión de seguimiento de contenidos se cierre llamando a `trackSessionEnd` después de invocar a `trackError`.

