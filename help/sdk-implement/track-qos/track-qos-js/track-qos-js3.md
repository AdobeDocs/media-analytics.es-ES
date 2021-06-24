---
title: Aprenda a rastrear la calidad de la experiencia usando JavaScript 3.x
description: '"Obtenga información sobre la implementación del seguimiento de calidad de experiencia (QoE, QoS) mediante Media SDK en aplicaciones de navegador mediante JavaScript 3x."'
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 58%

---

# Seguimiento de la calidad de la experiencia con JavaScript 3.x{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 3.x. Si va implementar cualquier versión anterior del SDK, puede descargar las guías del desarrollador aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## Implementación de QOE

1. Identifique cuándo cambia la velocidad de bits durante la reproducción de contenido y cree la instancia `qoeObject` con la información de QoE.

   Variables QoEObject:

   >[!TIP]
   >
   >Estas variables solo son necesarias si planea realizar seguimientos de QoS.

   | Variable | Tipo | Descripción |
   | --- | --- | --- |
   | `bitrate` | entero | Velocidad de bits actual |
   | `startupTime` | entero | Hora de inicio |
   | `fps` | entero | Valor FPS |
   | `droppedFrames` | entero | Número de fotogramas perdidos |

   Creación del objeto QoE:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
   ```

1. Cuando la velocidad de bits de la reproducción cambie, invoque el evento `BitrateChange` en la instancia de Media Heartbeat:

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >Actualice el objeto QoE e invoque el evento de cambio de velocidad de bits en cada cambio. Esto proporciona los datos de QoE más precisos.

1. Asegúrese de llamar al método `updateQoEObject()` para proporcionar la información de QoE más actualizada al SDK.
1. Cuando el reproductor de contenido encuentre un error, y el evento de error esté disponible con la API del reproductor, utilice el evento `trackError()` para capturar la información de error. (Consulte [Información general](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >El seguimiento de los errores del reproductor de contenidos no detendrá la sesión de seguimiento de contenidos. Si el reproductor de contenidos impide que continúe la reproducción, asegúrese de que la sesión de seguimiento de contenidos se cierre llamando a `trackSessionEnd()` después de invocar a `trackError()`.
