---
title: Configuración de Roku Edge para medios de streaming
description: Configure Adobe Experience Platform Roku SDK para enviar datos de medios de streaming a Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Configuración de Roku Edge para medios de streaming

[Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku) (BrightScript) recopila datos de sesión de medios en su canal de Roku y los envía a Edge Network. Roku está configurado en el código; no utiliza etiquetas.

* **Requisitos previos**:
   * Complete la [descripción general de la implementación de Edge](overview.md) (esquema, conjunto de datos, secuencia de datos con [!UICONTROL Media Analytics] habilitado).
   * Descargue SDK de [versiones de GitHub](https://github.com/adobe/aepsdk-roku/releases) y agréguelo a su canal, tal como se describe en la [guía de introducción](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md).

## Configuración de Roku Edge SDK para contenidos

Inicialice SDK y establezca la configuración de flujo de datos y medios:

```brightscript
m.aepSdk = AdobeAEPSDKInit()
ADB_CONSTANTS = AdobeAEPSDKConstants()

configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<datastreamID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "sample_channel"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
m.aepSdk.updateConfiguration(configuration)
```

A continuación, abra una sesión con `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": { "name": "video-123", "length": 128, "contentType": "vod", "streamType": "video" },
            "playhead": 0
        }
    }
})
```

>[!IMPORTANT]
>
>Envíe un evento `media.ping` al menos una vez por segundo con el valor más reciente del cabezal de reproducción durante la reproducción. La SDK de Roku Edge se basa en estos pings para funcionar correctamente.

Para obtener las claves de configuración y la API completa, consulte la [Referencia de la API de SDK de Roku Edge](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md).

## Seguimiento de eventos de medios

Una vez abierta la sesión, envíe cada evento multimedia con `sendMediaEvent`. Consulta la pestaña **Roku Edge** en cada [evento](/help/implementation/events/overview.md) y [variable](/help/implementation/variables/overview.md) para ver las cargas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones de Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku)
>* [Resumen de eventos](/help/implementation/events/overview.md)
>* [Resumen de variables](/help/implementation/variables/overview.md)
