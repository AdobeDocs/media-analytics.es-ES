---
seo-title: Compatibilidad con metadatos personalizados
title: Compatibilidad con metadatos personalizados
uuid: df 4109 dd -9 fca -4 c 33-a 7 d 5-8 e 6 eec 257527
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Compatibilidad con metadatos personalizados{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Esta información debe proporcionarse en la clave JSON, `customMetadata`, junto a la clave `params`.

The `customMetadata` JSON key should contain an object of key:value pairs. La clave debe contener únicamente caracteres alfanuméricos, subrayado y puntos.

[Eventos API de recopilación de MA](../mc-api-ref/mc-api-events-req.md)

