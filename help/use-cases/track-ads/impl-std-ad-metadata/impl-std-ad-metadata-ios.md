---
title: Obtenga información sobre cómo implementar metadatos de publicidad estándar en iOS
description: Cómo utilizar metadatos de anuncio estándar en el seguimiento de anuncios en iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 86%

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

[Claves de metadatos de iOS](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
