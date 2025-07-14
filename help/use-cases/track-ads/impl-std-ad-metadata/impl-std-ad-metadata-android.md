---
title: Obtenga información sobre cómo implementar metadatos de publicidad estándar en Android
description: Cómo usar metadatos de anuncio estándar en el seguimiento de anuncios en Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 100%

---

# Implementación de metadatos de publicidad estándar en Android {#implement-standard-ad-metadata-on-android}

## Constantes de publicidad

| Nombre de la constante | Descripción   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante para adjuntar metadatos de publicidad estándar en `MediaObject` de publicidad. |

## Implemente los metadatos de publicidad estándar

Para los metadatos de publicidad estándar, cree un diccionario de conexiones de clave/valor de metadatos de publicidad estándar con el uso de las claves correspondientes a su plataforma:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```
