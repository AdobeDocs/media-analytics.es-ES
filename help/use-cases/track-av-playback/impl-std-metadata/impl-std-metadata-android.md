---
title: Aprenda a implementar metadatos estándar en Android
description: Aprenda a configurar los metadatos estándar de vídeo y anuncios que se enviarán con las llamadas de seguimiento en Android.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '106'
ht-degree: 100%

---

# Implementación de metadatos estándar en Android{#implement-standard-metadata-on-android}

## Constantes de metadatos estándar

| Nombre de la constante | Descripción   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Constante para adjuntar metadatos estándar en `MediaObject`. |

## Referencia de la API de claves de metadatos

* Cree un `HashMap` de pares de clave valor de metadatos estándar.
   * [Claves de metadatos de vídeo](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Claves de metadatos de audio](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Establezca el `HashMap` de metadatos estándar en `MediaInfo` mediante el uso de la constante de metadatos estándar para los metadatos.
* Proporcione este objeto de `MediaInfo` e invoque la API `trackSessionStart()`.

## Implementaciones de muestra

### Vídeo

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### Audio

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```
