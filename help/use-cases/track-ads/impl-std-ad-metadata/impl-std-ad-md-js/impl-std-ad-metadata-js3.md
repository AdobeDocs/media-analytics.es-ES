---
title: Aprenda a implementar metadatos de publicidad estándar con JavaScript 3.x
description: Uso de metadatos de publicidad estándar en el seguimiento de anuncios en un explorador con aplicaciones JavaScript 3.x.
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 92%

---

# Implementación de metadatos de publicidad estándar en JavaScript 3.x{#implement-standard-ad-metadata-on-javascript}

## Implementación de metadatos de publicidad estándar

Para los metadatos de publicidad estándar, cree un diccionario de conexiones de clave/valor de metadatos de publicidad estándar con el uso de las claves correspondientes a su plataforma:

```js
var adObject =
ADB.Media.createAdObject(<AD_NAME>,
                              <AD_ID>,
                              <POSITION>,
                              <LENGTH>);

// Set standard Ad Metadata
var adMetadata = {};
adMetadata[MediaHeartbeat.AdMetadataKeys.Advertiser] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CampaignId] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
