---
title: ID del recurso
description: Establezca el ID del recurso, un identificador estable del sector para el recurso de medios, como un ID de EIDR o un ID de TMS/Gracenote.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 13%

---


# ID del recurso

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **ID de recurso**. Ver [ID de recurso](/help/reporting/dimensions/asset-id.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de ID de recurso es el identificador único del recurso de medios subyacente (por ejemplo, un ID de episodio, un ID de película o un ID de evento en directo). Normalmente, provienen de autoridades de metadatos como EIDR, TMS/Gracenote o Rovi, pero también se aceptan ID propietarios o internos. Utilícelo cuando necesite comparar la participación en distintas plataformas de distribución que puedan asignar ID de contenido diferentes al mismo recurso subyacente.

>[!NOTE]
>
>El campo de colección XDM utiliza `ID` en mayúsculas: `assetID`.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.asset` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Requerido** | No |
| **Enviado con** | Inicio de sesión, cierre de sesión |

## SDK web

Establecer `assetID` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        assetID: "89745363"
      },
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase el ID del recurso como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.ASSET_ID`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para establecer `assetID` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "assetID": "89745363"
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `assetID` dentro de `mediaCollection.sessionDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "assetID": "89745363"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pasar el id. de recurso en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.AssetId`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AssetId] = "89745363";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API de Media Collection

Incluir `media.assetId` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.assetId": "89745363"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
