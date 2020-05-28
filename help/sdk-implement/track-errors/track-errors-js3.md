---
title: Seguimiento de errores con JavaScript 3.x
description: En este tema se describe el seguimiento de errores de implementación mediante el uso de Media SDK en aplicaciones de navegador (JS).
translation-type: tm+mt
source-git-commit: 5f274452b9ff5770908f7e2e450935be572a22ea
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 69%

---


# Seguimiento de errores con JavaScript 3.x{#track-errors-on-javascript}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implementación del seguimiento de errores

1. Seguimiento de errores del reproductor de contenidos:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>El seguimiento de los errores del reproductor de contenidos no detendrá la sesión de seguimiento de contenidos. Si el reproductor de contenidos impide que continúe la reproducción, asegúrese de que la sesión de seguimiento de contenidos se cierre llamando a `trackSessionEnd` después de invocar a `trackError`.
