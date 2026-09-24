---
title: Versión de aplicación
description: Configure la cadena de versión de la aplicación de reproducción de contenido.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 2%
---

# Versión de aplicación

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Versión de aplicación**. Ver [Versión de la aplicación](/help/reporting/dimensions/app-version.md) para la dimensión de informes correspondiente.*

>[!ENDSHADEBOX]

La variable de versión de la aplicación identifica la versión de la aplicación del reproductor de contenidos. Configúrelo una vez durante la inicialización de SDK; el valor se incluye automáticamente en cada solicitud de inicio de sesión posterior. Utilice una cadena de versión que coincida con el ciclo de lanzamiento de su aplicación (por ejemplo, `"2.1.0"` o `"prod-YYYY-03-15"`).

>[!NOTE]
>
>Este campo registra la versión de su **aplicación de reproducción multimedia**, no la biblioteca SDK de Adobe. La versión de la biblioteca SDK de Adobe se recopila automáticamente como un campo interno independiente.

| Propiedad | Valor |
| --- | --- |
| **Campo de colección XDM** | [`xdm.mediaCollection.sessionDetails.appVersion`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Parámetro de API de recopilación de medios** | `media.sdkVersion` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md) |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `appVersion` en el objeto de configuración `streamingMedia` al llamar a [`configure`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia):

```javascript
alloy("configure", {
  streamingMedia: {
    channel: "Sports Channel",
    playerName: "HTML5 Player",
    appVersion: "2.1.0",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

>[!TAB iOS]

Establezca `edgeMedia.appVersion` en la configuración de la aplicación antes de inicializar el rastreador de medios:

```swift
var config: [String: Any] = [:]
config["edgeMedia.channel"] = "sample_channel"
config["edgeMedia.playerName"] = "player_name"
config["edgeMedia.appVersion"] = "2.1.0"
MobileCore.updateConfiguration(config)
```

>[!TAB Android]

Establezca `edgeMedia.appVersion` en la configuración de la aplicación antes de inicializar el rastreador de medios:

```kotlin
val config: Map<String, Any> = mapOf(
    "edgeMedia.channel" to "sample_channel",
    "edgeMedia.playerName" to "player_name",
    "edgeMedia.appVersion" to "2.1.0"
)
MobileCore.updateConfiguration(config)
```

>[!TAB Roku Edge]

Establezca la versión de la aplicación en la configuración de SDK mediante `ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION`:

```brightscript
ADB_CONSTANTS = AdobeAEPSDKConstants()
configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<YOUR_CONFIG_ID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "channel_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION] = "2.1.0"
m.aepSdk.updateConfiguration(configuration)
```

>[!TAB API de Media Edge]

Incluir `appVersion` en el objeto `sessionDetails` de la solicitud [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "appVersion": "2.1.0"
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Establezca `appVersion` en el objeto `MediaConfig` antes de llamar a `ADB.Media.configure`:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "2.1.0";
ADB.Media.configure(mediaConfig, appMeasurement);
```

>[!TAB Chromecast]

Establezca `sdkVersion` en la sección `mediaHeartbeat` de la configuración de ADBMobile. Este campo captura la versión de la aplicación de reproducción, no la versión de la biblioteca de SDK de Chromecast.

```javascript
var ADBMobileConfig = {
  "mediaHeartbeat": {
    "server": "obumobile5.hb-api.omtrdc.net",
    "publisher": "<YOUR_PUBLISHER_ID>@AdobeOrg",
    "channel": "sample-channel",
    "ssl": true,
    "playerName": "Chromecast Player",
    "sdkVersion": "2.1.0"
  }
};
```

>[!TAB Roku 2.x]

Establezca `sdkVersion` en la sección `mediaHeartbeat` de `ADBMobileConfig.json`. Este campo captura la versión de la aplicación de reproducción, no la versión de la biblioteca SDK Roku 2.x:

```json
"mediaHeartbeat": {
  "sdkVersion": "2.1.0"
}
```

>[!TAB API de recopilación de medios]

Incluir `media.sdkVersion` en el objeto `params` de su solicitud POST de `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "sample-html5-api-player",
    "media.sdkVersion": "2.1.0",
    "media.channel": "sample-channel"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
