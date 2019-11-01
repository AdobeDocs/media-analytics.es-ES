---
title: Implementación de metadatos de publicidad estándar en Android
description: Cómo usar metadatos de anuncio estándar en el seguimiento de anuncios en Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementación de metadatos de publicidad estándar en Android{#implement-standard-ad-metadata-on-android}

## Constantes de publicidad

| Nombre de la constante | Descripción   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante para adjuntar metadatos de publicidad estándar en `MediaObject` de publicidad. |

## Metadatos de anuncio estándar de implementación

Para los metadatos de anuncio estándar, cree un diccionario de pares de clave valor para los metadatos de anuncio estándar con las claves de su plataforma:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

