---
description: 'null'
seo-description: 'null'
seo-title: Implementación de metadatos de publicidad estándar en iOS
title: Implementación de metadatos de publicidad estándar en iOS
uuid: f 15 fb 727-5 a 5 b -46 c 5-bf 12-93 b 376 c 10 fd 1
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implementación de metadatos de publicidad estándar en iOS{#implement-standard-ad-metadata-on-ios}

## Constantes publicitarias

| Nombre de la constante | Descripción   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## Metadatos de anuncios estándar de implementación

Para los metadatos de anuncio estándar, cree un diccionario de pares de clave valor de clave estándar usando las claves para su plataforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Claves de metadatos de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
