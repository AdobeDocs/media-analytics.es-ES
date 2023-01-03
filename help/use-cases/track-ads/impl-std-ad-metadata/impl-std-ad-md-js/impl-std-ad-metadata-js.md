---
title: Aprenda a implementar metadatos de publicidad estándar con JavaScript 2.x
description: Cómo usar metadatos de publicidad estándar en el seguimiento de anuncios en un explorador con aplicaciones JavaScript 2.x.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
exl-id: b331db87-ab4e-44fa-a97c-9691974cacd4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 54%

---

# Implementación de metadatos de publicidad estándar con JavaScript 2.x{#implement-standard-ad-metadata-on-javascript}

## Constantes de publicidad

| Nombre de la constante | Descripción   |
|---|---|
| `StandardAdMetadata` | Constante para adjuntar metadatos de publicidad estándar en un objeto de publicidad |

## Implemente los metadatos de publicidad estándar

Para los metadatos de publicidad estándar, cree un diccionario de conexiones de clave/valor de metadatos de publicidad estándar con el uso de las claves correspondientes a su plataforma:

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>);

// Set standard Ad Metadata
var standardAdMetadata = {};
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```