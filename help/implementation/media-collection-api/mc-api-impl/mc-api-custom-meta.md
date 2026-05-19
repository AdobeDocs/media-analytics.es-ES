---
title: Compatibilidad con metadatos personalizados
description: Obtenga información sobre cómo proporcionar pares clave-valor personalizados en los eventos sessionStart, chapterStart y adStart.
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/sEVJa-FPqZiSc4Hdr7lQfNbECS2lxckBmqAYhGHmx2w
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 7%

---

# Compatibilidad con metadatos personalizados{#custom-metadata-support}

La API de recopilación de medios le permite enviar pares de clave-valor personalizados junto con parámetros estándar en eventos `sessionStart`, `adStart` y `chapterStart`. Los metadatos personalizados se reenvían a **Adobe Analytics** con los eventos de cierre de medios correspondientes.

Para que estos datos estén disponibles en Analysis Workspace, los clientes deben definir eVars personalizadas y configurar reglas de procesamiento para rellenarlas según su caso de uso. Una vez asignados a eVars o props, los datos también están disponibles en Adobe Experience Platform a través de las rutas de eVar correspondientes, siempre y cuando se haya configurado el [conector de origen de Analytics](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/analytics).

Para implementaciones basadas en XDM que utilizan Experience Edge, consulte [Compatibilidad con metadatos personalizados: formato XDM](/help/implementation/edge/implementation-edge-custom-metadata.md).

## Información general

Los metadatos personalizados se incluyen en el cuerpo de la solicitud como un objeto `customMetadata`, junto a la clave `params`. Se aplica a tres tipos de eventos:

| Evento | Los Metadatos Se Aplican |
|-------|-------------------|
| `sessionStart` | Contenido principal (toda la sesión) |
| `adStart` | Anuncio individual |
| `chapterStart` | Capítulo o segmento de contenido |

## Estructura

Los metadatos personalizados son un **objeto** plano (pares clave-valor) en el nivel de evento, junto con la clave `params`:

```json
{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "field": "value"
  }
}
```

### Parámetros obligatorios por tipo de evento

| Evento | Se requiere `params` |
|-------|-------------------|
| `sessionStart` | `analytics.trackingServer`, `analytics.reportSuite`, `visitor.marketingCloudOrgId`, `media.id`, `media.length`, `media.contentType`, `media.playerName`, `media.channel` |
| `adStart` | `media.ad.id`, `media.ad.length`, `media.ad.podPosition`, `media.ad.playerName` |
| `chapterStart` | `media.chapter.length`, `media.chapter.offset`, `media.chapter.index` |

### Requisitos de nomenclatura clave

- Evite utilizar el prefijo `media.` en las claves de metadatos personalizadas: se asigna a campos de medios estándar y puede sobrescribirlos en los informes de Analytics
- El prefijo `a.` está reservado para los metadatos estándar de Adobe y no debe usarse

## Metadatos personalizados de contenido principal

Enviado con `sessionStart`. Se aplica a los medios principales de los que se realiza un seguimiento y permanece disponible durante las llamadas de anuncio y capítulo. Cualquier metadato personalizado definido aquí se combinará automáticamente con el back-end de medios en las llamadas de cierre correspondientes. Se incluirá junto con cualquier metadato personalizado específico definido para anuncios y capítulos.

```sh
curl -X POST "https://{uri}/api/v1/sessions" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "analytics.visitorId": "visitor123",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.name": "Sample Video",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "contentCategory": "Live Sports",
    "leagueType": "Professional",
    "broadcastRights": "Premium"
  }
}'
```

## Añadir metadatos personalizados

Enviado con `adStart`. Específico para cada anuncio individual. Los metadatos personalizados de `sessionStart` también se combinan automáticamente por el backend de medios en la llamada de cierre de anuncio junto con cualquier metadato personalizado específico de anuncio definido aquí.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 30,
    "ts": 1646938830000
  },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "summer-sale-2026",
    "media.ad.name": "Summer Sale Ad",
    "media.ad.length": 30,
    "media.ad.playerName": "HTML5 Player",
    "media.ad.podPosition": 1
  },
  "customMetadata": {
    "campaignId": "SUMMER2026",
    "targetAudience": "18-34",
    "adFormat": "skippable"
  }
}'
```

## Metadatos personalizados de capítulo

Enviado con `chapterStart`. Específico para cada capítulo o segmento de contenido. Los metadatos personalizados de `sessionStart` también se combinan automáticamente con el backend de medios en la llamada de cierre de capítulo junto con cualquier metadato personalizado específico de capítulo definido aquí.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 600,
    "ts": 1646938200000
  },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Introduction",
    "media.chapter.length": 300,
    "media.chapter.index": 1,
    "media.chapter.offset": 600
  },
  "customMetadata": {
    "chapterType": "tutorial",
    "difficulty": "beginner",
    "instructor": "Jane Smith"
  }
}'
```

## Comportamiento

- Todos los valores de metadatos personalizados deben ser **strings**. Convierta números y valores booleanos antes de enviar.
- Los metadatos personalizados aparecen en Analytics con un prefijo `c.` (por ejemplo, `contentCategory` → `c.contentCategory`)
- Asignar metadatos personalizados a eVars, props o variables de datos de contexto mediante reglas de procesamiento de Analytics
- `sessionStart` metadatos persisten durante toda la sesión; las actualizaciones requieren una nueva sesión
- Cada evento `adStart` y `chapterStart` puede llevar metadatos personalizados diferentes

## Documentación relacionada

- [Compatibilidad con metadatos personalizados - Formato XDM](/help/implementation/edge/implementation-edge-custom-metadata.md) — Envíe metadatos personalizados mediante Experience Edge a Analytics y a AEP
- [Conector de origen de Adobe Analytics para los datos del grupo de informes](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/analytics): introducir datos de Analytics en Adobe Experience Platform

<!--
- [Session endpoints](sessions.md) — Session lifecycle management
- [Ad endpoints](ads.md) — Track advertising impressions
- [Chapter endpoints](chapters.md) — Segment content into chapters
-->
