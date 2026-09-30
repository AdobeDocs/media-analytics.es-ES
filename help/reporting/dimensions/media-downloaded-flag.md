---
title: Medios descargados
description: Indica las sesiones que reprodujeron contenido sin conexión descargado.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%
---

# Medios descargados

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informes **Medios descargados**. Consulte [Indicador de medios descargados](/help/implementation/variables/core/media-downloaded-flag.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Medios descargados** indica sesiones que se reprodujeron contenido sin conexión descargado anteriormente en lugar de un flujo en directo desde Internet. Utilícelo para separar la reproducción sin conexión de las sesiones transmitidas al comparar la participación, la finalización o la calidad.

## Cómo se rellena esta dimensión

El reproductor establece el indicador descargado de una de las tres maneras siguientes. Inicialice el rastreador con el indicador (Mobile SDK), envíe `sessionStart` a la variante de extremo `/downloaded` (API de Media Edge directa) o incluya `media.downloaded: true` en los parámetros `sessionStart` (API de Media Collection).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.downloaded` a un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.downloaded`) |
| Audience Manager | `c_contextdata.a.media.downloaded` |

## Elementos de dimensión

| Valor | Descripción |
| --- | --- |
| `true` | La sesión reprodujo el contenido sin conexión descargado. |
| (vacío) | La sesión reprodujo un flujo en directo. El campo se omite en lugar de establecerse en `false`. |
