---
title: Implementación de metadatos de publicidad estándar en Roku
description: Cómo usar metadatos de anuncio estándar en el seguimiento de anuncios en Roku.
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementación de metadatos de publicidad estándar en Roku{#implement-standard-ad-metadata-on-roku}

## Metadatos de anuncio estándar de implementación

Para los metadatos de anuncio estándar, cree un diccionario de pares de clave valor para los metadatos de anuncio estándar con las claves de su plataforma:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

