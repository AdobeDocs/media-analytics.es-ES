---
description: 'null'
seo-description: 'null'
seo-title: Implementación de metadatos estándar en Roku
title: Implementación de metadatos estándar en Roku
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implementación de metadatos estándar en Roku{#implement-standard-metadata-on-roku}

Cree una instancia de un objeto de metadatos estándar, rellene las variables deseadas y establezca el objeto de metadatos en el objeto de Media Heartbeat.

**Vídeo:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

**Audio:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

Consulte la lista completa de metadatos de vídeo aquí: [Parámetros de audio y vídeo](/help/metrics-and-metadata/audio-video-parameters.md).

