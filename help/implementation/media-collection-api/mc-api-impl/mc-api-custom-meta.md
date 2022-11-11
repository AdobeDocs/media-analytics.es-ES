---
title: Compatibilidad con metadatos personalizados
description: '"Aprenda a proporcionar pares de clave:valor personalizadas en los eventos sessionStart, chapterStart y adStart".'
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 47%

---

# Compatibilidad con metadatos personalizados{#custom-metadata-support}

Puede proporcionar pares de clave:valor personalizadas en los eventos `sessionStart`, `chapterStart` y `adStart`. Esta información debe proporcionarse en la clave JSON, `customMetadata`, junto a la clave `params`.

La clave JSON `customMetadata` debe contener un objeto de pares de clave:valor. La clave debe contener únicamente caracteres alfanuméricos, subrayado y puntos.

[Eventos de API de recopilación de MA](../mc-api-ref/mc-api-events-req.md)

## Ejemplo

Actualmente puede enviar un `sessionStart` con el siguiente par clave:valor:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

Para la configuración anterior, los datos de informes enviados a analytics son los siguientes:

`c.a.media.channel=channel-2`

### Recomendación

Se recomienda utilizar un área de nombres independiente para los metadatos personalizados. Por ejemplo:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

En el ejemplo recomendado, los datos de informes para metadatos personalizados enviados a analytics son los siguientes:

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
