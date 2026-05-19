---
title: Aprenda a controlar la calidad de la experiencia con JavaScript 2.x
description: Obtenga información acerca de la implementación del seguimiento de calidad de experiencia (QoE, QoS) mediante Media SDK en aplicaciones de navegador con JavaScript 2.x.
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
exl-id: 5924eba4-15a9-405b-9a05-8a7308ddec47
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/S4UPE2qnHPcqM0znf4PVJy0p98rzv8FVlBBYqjer-7s
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 226
ht-degree: 90%

---

# Seguimiento de la calidad de la experiencia con JavaScript 2.x{#track-quality-of-experience-on-javascript}

En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

## Implementación de QOS

1. Identifique cuándo cambia la velocidad de bits durante la reproducción de contenido y cree la instancia de `MediaObject` con la información de QoS.

   Variables QoSObject:

   >[!TIP]
   >
   >Estas variables solo son necesarias si planea realizar seguimientos de QoS.

   | Variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `bitrate` | Velocidad de bits actual | Sí |
   | `startupTime` | Hora de inicio | Sí |
   | `fps` | Valor FPS | Sí |
   | `droppedFrames` | Número de fotogramas perdidos | Sí |

   Creación del objeto de QoS:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>);
   ```

1. Cuando la velocidad de bits de la reproducción cambie, invoque el evento `BitrateChange` en la instancia de Media Heartbeat:

   ```js
   _onBitrateChange = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject);
   };
   ```

   >[!IMPORTANT]
   >
   >Actualice el objeto QoS e invoque el evento de cambio de velocidad de bits en cada cambio. Esto proporciona los datos de QoS más precisos.

1. Asegúrese de que el método `getQoSObject()` devuelve la información de QoS más actualizada.
1. Cuando el reproductor de contenido encuentre un error, y el evento de error esté disponible con la API del reproductor, utilice el evento `trackError()` para capturar la información de error. (Consulte [Información general](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >El seguimiento de los errores del reproductor de contenidos no detendrá la sesión de seguimiento de contenidos. Si el error del reproductor de contenidos impide que continúe la reproducción, asegúrese de que la sesión de seguimiento de contenidos se cierre llamando a `trackSessionEnd()` después de invocar a `trackError()`.
