---
title: Compatibilidad con metadatos personalizados
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Compatibilidad con metadatos personalizados{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Esta información debe proporcionarse en la clave JSON, `customMetadata`, junto a la clave `params`.

The `customMetadata` JSON key should contain an object of key:value pairs. La clave debe contener únicamente caracteres alfanuméricos, subrayado y puntos.

[Eventos de API de recopilación de MA](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

