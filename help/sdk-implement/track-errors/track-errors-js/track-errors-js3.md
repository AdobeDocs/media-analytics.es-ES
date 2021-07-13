---
title: Descubra cómo rastrear errores usando JavaScript 3.x
description: Obtenga información sobre la implementación del seguimiento de errores mediante Media SDK en aplicaciones de navegador (JS).
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 73%

---

# Seguimiento de errores con JavaScript 3.x{#track-errors-on-javascript}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 3.x. Si va implementar cualquier versión anterior del SDK, puede descargar las guías del desarrollador aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

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
