---
description: 'null'
seo-description: 'null'
seo-title: Implementación de metadatos de publicidad estándar en Roku
title: Implementación de metadatos de publicidad estándar en Roku
uuid: 20 a 437 d 7-18 b 8-4099-ac 81-9 f 3628384236
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implementación de metadatos de publicidad estándar en Roku{#implement-standard-ad-metadata-on-roku}

## Metadatos de anuncios estándar de implementación

Para los metadatos de anuncio estándar, cree un diccionario de pares de clave valor de clave estándar usando las claves para su plataforma:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

