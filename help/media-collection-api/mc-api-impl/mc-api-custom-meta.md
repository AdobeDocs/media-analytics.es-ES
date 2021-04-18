---
title: Compatibilidad con metadatos personalizados
description: Compatibilidad con metadatos personalizados
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# Compatibilidad con metadatos personalizados {#custom-metadata-support}

Puede proporcionar pares de clave:valor personalizadas en los eventos `sessionStart`, `chapterStart` y `adStart`. Esta información debe proporcionarse en la clave JSON, `customMetadata`, junto a la clave `params`.

La clave JSON `customMetadata` debe contener un objeto de pares de clave:valor. La clave debe contener únicamente caracteres alfanuméricos, subrayado y puntos.

[Eventos de API de recopilación de MA](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)
