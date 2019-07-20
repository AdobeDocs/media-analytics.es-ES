---
description: 'null'
seo-description: 'null'
seo-title: Implementación de metadatos de publicidad estándar en JavaScript
title: Implementación de metadatos de publicidad estándar en JavaScript
uuid: 4 ea 10 c 5 a-ae 2 b -45 d 0-aad 3-9 f 10028 ee 7 c 3
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implementación de metadatos de publicidad estándar en JavaScript{#implement-standard-ad-metadata-on-javascript}

## Constantes publicitarias

| Nombre de la constante | Descripción   |
|---|---|
| `StandardAdMetadata` | Constante para adjuntar metadatos de publicidad estándar en un objeto de publicidad |

## Metadatos de anuncios estándar de implementación

Para los metadatos de anuncio estándar, cree un diccionario de pares de clave valor de clave estándar usando las claves para su plataforma:

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

