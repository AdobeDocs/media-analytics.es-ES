---
title: Obtenga información sobre cómo implementar metadatos de publicidad estándar en Roku
description: Cómo usar metadatos de anuncio estándar en el seguimiento de anuncios en Roku.
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
exl-id: d2c0a1e0-8d40-4f60-a82d-5860550ac152
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 82%

---

# Implementación de metadatos de publicidad estándar en Roku {#implement-standard-ad-metadata-on-roku}

## Implemente los metadatos de publicidad estándar

Para los metadatos de publicidad estándar, cree un diccionario de conexiones de clave/valor de metadatos de publicidad estándar con el uso de las claves correspondientes a su plataforma:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```
