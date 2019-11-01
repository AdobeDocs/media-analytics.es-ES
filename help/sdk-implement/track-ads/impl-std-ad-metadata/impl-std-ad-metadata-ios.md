---
title: Implementación de metadatos de publicidad estándar en iOS
description: Cómo utilizar metadatos de anuncio estándar en el seguimiento de anuncios en iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementación de metadatos de publicidad estándar en iOS{#implement-standard-ad-metadata-on-ios}

## Constantes de publicidad

| Nombre de la constante | Descripción   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## Metadatos de anuncio estándar de implementación

Para los metadatos de anuncio estándar, cree un diccionario de pares de clave valor para los metadatos de anuncio estándar con las claves de su plataforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Claves de metadatos de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
