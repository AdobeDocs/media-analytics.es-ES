---
seo-title: Compatibilidad con metadatos personalizados
title: Compatibilidad con metadatos personalizados
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Compatibilidad con metadatos personalizados{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Esta información debe proporcionarse en la clave JSON, `customMetadata`, junto a la clave `params`.

The `customMetadata` JSON key should contain an object of key:value pairs. La clave debe contener únicamente caracteres alfanuméricos, subrayado y puntos.

[MA Collection API Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

