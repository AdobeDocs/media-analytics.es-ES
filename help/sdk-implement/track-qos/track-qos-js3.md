---
title: Rastree la calidad de la experiencia con JavaScript 3.x
description: En este tema se describe la implementación del seguimiento de calidad de experiencia (QoE, QoS) mediante el SDK de medios en aplicaciones de navegador que utilizan JavaScript 3x.
translation-type: tm+mt
source-git-commit: b165c9d133637fd0f1c529a98a936f8f31b72465
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 49%

---


# Rastree la calidad de la experiencia con JavaScript 3.x{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## QOE de implementación

1. Identify when the bitrate changes during media playback and create the `qoeObject` instance using the QoE information.

   Variables de QoEObject:

   >[!TIP]
   >
   >Estas variables solo son necesarias si planea realizar seguimientos de QoS.

   | Variable | Tipo | Descripción |
   | --- | --- | --- |
   | `bitrate` | entero | Velocidad de bits actual |
   | `startupTime` | entero | Hora de inicio |
   | `fps` | entero | Valor FPS |
   | `droppedFrames` | entero | Número de fotogramas perdidos |

   Creación de objetos QoE:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
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
   >Actualice el objeto QoE y llame al evento de cambio de velocidad de bits en cada cambio de velocidad de bits. Esto proporciona los datos de QoE más precisos.

1. Asegúrese de llamar al `updateQoEObject()` método para proporcionar la información de QoE más actualizada al SDK.
1. Cuando el reproductor de contenido encuentre un error, y el evento de error esté disponible con la API del reproductor, utilice el evento `trackError()` para capturar la información de error. (Consulte [Información general](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >El seguimiento de los errores del reproductor de contenidos no detendrá la sesión de seguimiento de contenidos. Si el reproductor de contenidos impide que continúe la reproducción, asegúrese de que la sesión de seguimiento de contenidos se cierre llamando a `trackSessionEnd()` después de invocar a `trackError()`.
