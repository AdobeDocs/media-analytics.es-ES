---
title: Compatibilidad con metadatos personalizados
description: Obtenga información sobre cómo proporcionar pares clave-valor personalizados en los eventos sessionStart, chapterStart y adStart.
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 62%

---

# Compatibilidad con metadatos personalizados{#custom-metadata-support}

Puede proporcionar pares de clave personalizada :value en los eventos `sessionStart`, `chapterStart` y `adStart`. Esta información debe proporcionarse en la clave JSON, `customMetadata`, junto a la clave `params`.

La clave JSON `customMetadata` debe contener un objeto de pares de clave:value. La clave debe contener únicamente caracteres alfanuméricos, subrayado y puntos.

[Eventos de API de recopilación de MA](../mc-api-ref/mc-api-events-req.md)

## Ejemplo

Actualmente puede enviar un evento `sessionStart` con el siguiente par clave:value:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

Para la configuración anterior, los datos de informes enviados a Analytics son los siguientes:

`c.a.media.channel=channel-2`

### Recomendación

Se recomienda utilizar un área de nombres independiente para los metadatos personalizados. Por ejemplo:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

En el ejemplo recomendado, los datos de creación de informes para metadatos personalizados enviados a Analytics son los siguientes:

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
