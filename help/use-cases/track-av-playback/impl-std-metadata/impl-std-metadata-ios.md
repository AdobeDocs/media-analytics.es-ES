---
title: Obtenga información sobre cómo implementar metadatos estándar en iOS
description: Aprenda a configurar los metadatos de anuncios y vídeos estándar para enviarlos con llamadas de seguimiento en iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 100%

---

# Implementación de metadatos estándar en iOS{#implement-standard-metadata-on-ios}

## Constantes de metadatos

| Nombre de la constante | Descripción   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constante para adjuntar metadatos estándar en `MediaInfo ADBMediaObject` |

## Implementación

1. Cree un diccionario de pares de clave-valor para los metadatos estándar usando `ADBStandardMetadataKeys`.
   [Claves de metadatos de IOS](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Establezca el diccionario de metadatos estándar en la instancia `MediaInfo` `ADBMediaObject` mediante el uso de la constante de metadatos estándar para los metadatos.

1. Proporcione este objeto de `MediaInfo` e invoque la API `trackSessionStart`.

### Implementación de muestra

Cree una instancia de un objeto de metadatos estándar, rellene las variables deseadas y establezca el objeto de metadatos en el objeto de Media Heartbeat. Por ejemplo:

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```
