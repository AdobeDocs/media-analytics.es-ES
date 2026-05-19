---
title: Aprenda a controlar la calidad de la experiencia con JavaScript 3.x
description: Obtenga información acerca de la implementación del seguimiento de calidad de experiencia (QoE, QoS) mediante Media SDK en aplicaciones de navegador con JavaScript 3x.
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/aR7oVHv3n2xQnrMGHowhLFCYxhRyP1vyIrlXbKHEa5A
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 227
ht-degree: 90%

---

# Seguimiento de la calidad de la experiencia con JavaScript 3.x{#track-quality-of-experience-on-javascript}

En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x.

>[!IMPORTANT]
>
>Si va a implementar cualquier versión anterior del SDK, puede descargar las guías del desarrollador aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

## Implementación de QOE

1. Identifica cuándo cambia la velocidad de bits durante la reproducción multimedia y crea la instancia `qoeObject` utilizando la información de QoE.

   Variables QoEObject:

   >[!TIP]
   >
   >Estas variables solo son necesarias si planea realizar seguimientos de QoS.

   | Variable | Tipo | Descripción |
   | --- | --- | --- |
   | `bitrate` | number | Velocidad de bits actual |
   | `startupTime` | number | Hora de inicio |
   | `fps` | number | Valor FPS |
   | `droppedFrames` | number | Número de fotogramas perdidos |

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
   >Actualiza el objeto QoE y llama al evento de cambio de velocidad de bits en cada cambio de velocidad de bits. Esto proporciona los datos de QoE más precisos.

1. Asegúrese de llamar al método `updateQoEObject()` para proporcionar la información de QoE más actualizada al SDK.
1. Cuando el reproductor de contenido encuentre un error, y el evento de error esté disponible con la API del reproductor, utilice el evento `trackError()` para capturar la información de error. (Consulte [Información general](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >El seguimiento de los errores del reproductor de contenidos no detendrá la sesión de seguimiento de contenidos. Si el error del reproductor de contenidos impide que continúe la reproducción, asegúrese de que la sesión de seguimiento de contenidos se cierre llamando a `trackSessionEnd()` después de invocar a `trackError()`.
