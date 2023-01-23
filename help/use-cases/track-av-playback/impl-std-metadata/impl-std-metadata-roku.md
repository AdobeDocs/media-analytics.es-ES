---
title: Obtenga información sobre cómo implementar metadatos estándar en Roku
description: Aprenda a configurar los metadatos estándar de vídeo y anuncios que se envían con las llamadas de seguimiento en Roku.
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '63'
ht-degree: 100%

---

# Implementación de metadatos estándar en Roku {#implement-standard-metadata-on-roku}

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

Consulte la lista completa de metadatos de vídeo aquí: [Parámetros de audio y vídeo](/help/implementation/variables/audio-video-parameters.md).
