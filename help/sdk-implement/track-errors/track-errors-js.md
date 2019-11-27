---
title: Seguimiento de errores en JavaScript
description: En este tema se describe el seguimiento de errores de implementación mediante el uso de Media SDK en aplicaciones de navegador (JS).
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Seguimiento de errores en JavaScript {#track-errors-on-javascript}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## Implementación del seguimiento de errores

1. Seguimiento de errores del reproductor de contenidos:

   ```js
   onPlayerError = function() { 
       this._mediaHeartbeat.trackError("mediaErrorId"); 
   };
   ```

>[!NOTE]
>
>El seguimiento de los errores del reproductor de contenidos no detendrá la sesión de seguimiento de contenidos. Si el reproductor de contenidos impide que continúe la reproducción, asegúrese de que la sesión de seguimiento de contenidos se cierre llamando a `trackSessionEnd` después de invocar a `trackError`.

