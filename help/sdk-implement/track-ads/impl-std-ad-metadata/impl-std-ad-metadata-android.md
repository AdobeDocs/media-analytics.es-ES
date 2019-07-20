---
description: 'null'
seo-description: 'null'
seo-title: Implementación de metadatos de publicidad estándar en Android
title: Implementación de metadatos de publicidad estándar en Android
uuid: 19 b 98 bc 1-c 659-4182-a 4 ff-b 3340 fe 2453 c
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implementación de metadatos de publicidad estándar en Android{#implement-standard-ad-metadata-on-android}

## Constantes publicitarias

| Nombre de la constante | Descripción   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante para adjuntar metadatos de publicidad estándar en `MediaObject` de publicidad. |

## Metadatos de anuncios estándar de implementación

Para los metadatos de anuncio estándar, cree un diccionario de pares de clave valor de clave estándar usando las claves para su plataforma:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

