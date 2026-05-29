---
title: Migración de JavaScript SDK 2.x a 3.x
description: Guía de migración y comparación de código para actualizar de Media SDK JavaScript 2.x a SDK 3.x.
feature: Streaming Media
role: User, Admin, Developer
exl-id: b7e2d5a1-8c3f-4a9d-b6e7-2c1b4f0d8a3e
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 12%

---


# Migración de 2.x JS SDK a 3.x JS SDK

## Nuevas características

* Uso de API de MediaCollection
* Seguimiento de estado personalizado

## Mejoras

* Proporcionar configuración global para la biblioteca de medios
* Creación sencilla del rastreador
* Se han agregado API para proporcionar información de QoE y cabezal de reproducción
* API para destruir la instancia de seguimiento
* Simplificar la configuración de metadatos estándar/personalizados para contenidos y anuncios

## Comparación de API

### Clase de medios

| Funcionalidad | 2.x | 3.x |
| ------ | ------ | ------ |
| **Espacio de nombres** | `ADB.va.MediaHeartbeat` | **`ADB.Media`** |
| **Configuración** | Parámetro del constructor `MediaHeartbeat` | **`configure(mediaConfig, appMeasurement)`** |
| **Crear rastreador** | `new MediaHeartbeat(...)` | **`getInstance()`** |
| **Métodos estáticos** | |  |
|  | `createMediaObject(...)` | `createMediaObject(...)` |
|  | `createAdBreakObject(...)` | `createAdBreakObject(...)` |
|  | `createAdObject(...)` | `createAdObject(...)` |
|  | `createChapterObject(...)` | `createChapterObject(...)` |
|  | `createQoSObject(...)` | **`createQoEObject(...)`** |
|  | n/a | **`createStateObject()`** |
| **Métodos de instancia** | |  |
|  | `trackSessionStart(...)` | `trackSessionStart(...)` |
|  | `trackPlay()` | `trackPlay()` |
|  | `trackPause()` | `trackPause()` |
|  | `trackComplete()` | `trackComplete()` |
|  | `trackSessionEnd()` | `trackSessionEnd()` |
|  | `trackEvent(...)` | `trackEvent(...)` |
|  | `trackError(...)` | `trackError(...)` |
|  | N/D | **`updatePlayhead(playhead)`** |
|  | N/D | **`updateQoEObject(qoeObject)`** |
| **Destruir Rastreador** | n/a | **`destroy()`** |

### Clase MediaConfig

| Funcionalidad | 2.x | 3.x |
| ------ | ------ | ------ |
| **Espacio de nombres** | ` ADB.va.MediaHeartbeatConfig` | **`ADB.MediaConfig`** |
| **Constructor** | `new MediaHeartbeatConfig()` | **`new MediaConfig()`** |
| **Parámetros de configuración** | | |
| | `trackingServer` | `trackingServer` |
| | `channel` | `channel` |
| | `ovp` | n/a |
| | `appVersion` | `appVersion` |
| | `playerName` | `playerName` |
| | `ssl` | `ssl` |
| | `debugLogging` | `debugLogging` |

## Comparación de código

### Configuración y creación del rastreador

#### 2.x

```javascript
    var MediaHeartbeat = ADB.va.MediaHeartbeat;
    var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
    var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;

    // Create MediaHeartbeatConfig object
    var mediaConfig = new MediaHeartbeatConfig();
    mediaConfig.trackingServer = "tracking_server";
    mediaConfig.playerName = "player_name";
    mediaConfig.channel = "sample_channel";
    mediaConfig.ovp = "sample_ovp";
    mediaConfig.appVersion = "app_version";
    mediaConfig.debugLogging = true;
    mediaConfig.ssl = true;

    // Instance of MediaHeartbeatDelegate to return playhead and qosInfo to the tracker
    ADB.core.extend(SampleMediaHeartbeatDelegate.prototype,
                         MediaHeartbeatDelegate.prototype);
    function SampleMediaHeartbeatDelegate() { ... }
    SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() {
        // Returns the current playhead from the player.
    }
    SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() {
        // Returns the current QOS information if available from the player.
    }

    // Create tracker instance by passing mediaConfig, appMeasurement instancee and player delegate
    var tracker = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(),
                                      mediaConfig,
                                      appMeasurement);
```

#### 3.x

```javascript
    var Media = ADB.Media;
    var MediaConfig = ADB.MediaConfig;

    // Create MediaConfig object (same as above)
    var mediaConfig = new MediaConfig();
    mediaConfig.trackingServer = "tracking_server";
    mediaConfig.playerName = "player_name";
    mediaConfig.channel = "sample_channel";
    mediaConfig.appVersion = "app_version";
    mediaConfig.debugLogging = true;
    mediaConfig.ssl = true;

    // Configuration is only done once per page
    // and applies to all tracker instances created.
    Media.configure(mediaConfig, appMeasurement);

    // Tracker creation.
    var tracker = Media.getInstance();
```

### Proporcionar información de cabezal de reproducción y QoE al rastreador

#### 2.x

```javascript
    // Instance of MediaHeartbeatDelegate to return playhead and qosInfo to the tracker
    ADB.core.extend(SampleMediaHeartbeatDelegate.prototype,
                         MediaHeartbeatDelegate.prototype);
    function SampleMediaHeartbeatDelegate(player) { this.player = player }
    SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() {
        // Returns the current playhead from the player.
        return this.player.playhead;
    };
    SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() {
        // Returns the current QOS information if available from the player.
        var qosInfo = MediaHeartbeat.createQoSObject(this._player.bitrate,
                                                     this._player.startupTime,
                                                     this._player.fps,
                                                     this._player.droppedFrames);
        return qosInfo;
    };

    // Pass the delegate instance when creating the tracker.
    var tracker = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(),
                                      mediaConfig,
                                      appMeasurement);
```

#### 3.x

```javascript
        // When playhead changes, call
        tracker.updatePlayhead(this._player.playhead)

        // When new QoE information is available, call
        var qoeInfo = Media.createQoEObject(this._player.bitrate,
                                                     this._player.startupTime,
                                                     this._player.fps,
                                                     this._player.droppedFrames);
        tracker.updateQoEObject(qoeInfo)
```

### Metadatos estándar y personalizados para contenidos y anuncios

#### Medios

#### 2.x

```javascript
    var mediaObject = MediaHeartbeat.createMediaObject("name",
                                                       "id",
                                                       60.0,
                                                       MediaHeartbeat.StreamType.VOD,
                                                       MediaHeartbeat.MediaType.Video);
    // standard metadata
    var standardMetadata = {};
    standardMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "sample season";
    standardMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "sample show";
    // Set standard metadata on media object.
    mediaObject.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata,
                               standardMetadata);

    // custom metadata
    var customMetadata = {
        "customKey1" : "custom value",
        "customKey2" : "custom value"
    };

    mediaTracker.trackSessionStart(mediaObject, customMetadata);
```

#### 3.x

```javascript
    var mediaObject = Media.createMediaObject("name",
                                           "id",
                                           60.0,
                                           Media.StreamType.VOD,
                                           Media.MediaType.Video);

    var metadata = {};
    // standard metadata
    metadata[Media.VideoMetadataKeys.Season] = "sample season";
    metadata[Media.VideoMetadataKeys.Show] = "sample show";
    // custom metadata
    metadata["customKey1"] = "custom value";
    metadata["customKey2"] = "custom value";

    mediaTracker.trackSessionStart(mediaObject, metadata);
```

#### Anuncios

#### 2.x

```javascript
    var adObject = MediaHeartbeat.createAdObject("adName",
                                                 "adId",
                                                  1,
                                                  15.0);

    // standard metadata
    var standardAdMetadata = {};
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
    // Set standard metadata on ad object.
    adObject.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata,
                               standardAdMetadata);

    // custom metadata
    var customMetadata = {
        "customKey1" : "custom value",
        "customKey2" : "custom value"
    };

    mediaTracker.trackEvent(MediaHeartbeat.Event.AdStart, adObject, customMetadata);
```

#### 3.x

```javascript
    var adObject = Media.createAdObject("adName",
                                                 "adId",
                                                  1,
                                                  15.0);


    var metadata = {};
    // standard metadata
    metadata[Media.AdMetadataKeys.Advertiser] = "Sample Advertiser";
    metadata[Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
    // custom metadata
    metadata["customKey1"] = "custom value";
    metadata["customKey2"] = "custom value";

    mediaTracker.trackEvent(Media.Event.AdStart, adObject, metadata);
```
