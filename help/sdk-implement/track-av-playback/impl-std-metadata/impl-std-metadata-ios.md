---
title: Implementación de metadatos estándar en iOS
description: Describe la configuración de metadatos de anuncios y vídeos estándar para enviarlos con llamadas de seguimiento en iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementación de metadatos estándar en iOS{#implement-standard-metadata-on-ios}

## Constantes de metadatos

| Nombre de la constante | Descripción   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constante para adjuntar metadatos estándar en `MediaInfo ADBMediaObject` |

## Implementación

1. Create a dictionary of standard metadata key value pairs using the `ADBStandardMetadataKeys`
   [Teclas de metadatos de IOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Establezca el diccionario de metadatos estándar en la instancia `MediaInfo``ADBMediaObject`   mediante el uso de la constante de metadatos estándar para los metadatos.

1. Provide this `MediaInfo` object while invoking the `trackSessionStart` API.

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

