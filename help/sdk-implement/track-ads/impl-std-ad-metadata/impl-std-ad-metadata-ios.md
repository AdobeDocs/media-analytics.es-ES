---
title: Implementación de metadatos de publicidad estándar en iOS
description: Cómo utilizar metadatos de anuncio estándar en el seguimiento de anuncios en iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementación de metadatos de publicidad estándar en iOS {#implement-standard-ad-metadata-on-ios}

## Constantes de publicidad

| Nombre de la constante | Descripción   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constante para adjuntar metadatos de publicidad estándar en `AdInfo ADBMediaObject` |

## Implemente los metadatos de publicidad estándar

Para los metadatos de publicidad estándar, cree un diccionario de conexiones de clave/valor de metadatos de publicidad estándar con el uso de las claves correspondientes a su plataforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Claves de metadatos de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
