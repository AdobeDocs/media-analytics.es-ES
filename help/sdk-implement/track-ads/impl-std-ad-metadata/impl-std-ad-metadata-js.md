---
title: Implementar metadatos de anuncio estándar con JavaScript 2.x
description: Cómo utilizar metadatos de anuncio estándar en el seguimiento de anuncios en un navegador mediante aplicaciones JavaScript 2.x.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 30ed54924c75a9c33e6122b2d7ddbb84c06b8c0c
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 55%

---


# Implementar metadatos de anuncio estándar con JavaScript 2.x{#implement-standard-ad-metadata-on-javascript}

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
