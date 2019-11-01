---
title: Implementación de metadatos de publicidad estándar en JavaScript
description: Cómo usar metadatos de anuncio estándar en el seguimiento de anuncios en aplicaciones de explorador (JS).
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementación de metadatos de publicidad estándar en JavaScript{#implement-standard-ad-metadata-on-javascript}

## Constantes de publicidad

| Nombre de la constante | Descripción   |
|---|---|
| `StandardAdMetadata` | Constante para adjuntar metadatos de publicidad estándar en un objeto de publicidad |

## Metadatos de anuncio estándar de implementación

Para los metadatos de anuncio estándar, cree un diccionario de pares de clave valor para los metadatos de anuncio estándar con las claves de su plataforma:

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

