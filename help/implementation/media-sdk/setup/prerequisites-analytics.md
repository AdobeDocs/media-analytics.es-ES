---
title: Requisitos previos para implementaciones solo de Adobe Analytics
description: Conozca los requisitos previos para utilizar el complemento de Adobe Analytics para medios de streaming para implementaciones solo de Adobe Analytics
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
TQID: https://experienceleague.adobe.com/falbDtUtqAMtmtQs2jLpEvUKmwvATotVu8njuTNZ09k
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 243
ht-degree: 14%

---

# Requisitos previos para implementaciones solo de Adobe Analytics

Los requisitos previos descritos en esta sección son específicos para implementar el complemento de Adobe Analytics para medios de streaming para implementaciones solo de Adobe Analytics (cuando no se utiliza Edge).

1. **Completar los requisitos previos generales**<br>
Tanto si implementa servicios de medios de streaming para implementaciones solo de Adobe Analytics como para implementaciones de Edge, debe cumplir [los requisitos previos generales](/help/getting-started/prereqs.md).

1. **Confirme que tiene una implementación de Adobe Analytics**<br>
Al implementar el complemento de Adobe Analytics para medios de streaming en una implementación solo de Analytics, también se requiere una implementación básica de Adobe Analytics. Consulte [Implementación de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) para obtener más información.

1. **Obtener la URL del servidor de seguimiento de medios**<br>
Solicite a su representante de Adobe Analytics la URL del servidor de seguimiento de medios. Esta es la URL `collection-api-server` para Mobile SDK, JavaScript SDK y el servidor de seguimiento de la API de no recopilación para Roku. Los nombres de dominio para la implementación de API son: `[your_namespace].hb-api.omtrdc.net`.

1. **Descargar Media SDK actual o implementar las extensiones necesarias**<br>
Según la ruta de implementación, [descargue el SDK actual](/help/getting-started/download-sdks.md) para plataformas web, móviles o de servicios OTT. Las extensiones necesarias deben implementarse para habilitar el complemento de Adobe Analytics para medios de streaming.

1. **Habilitar informes de Adobe Analytics**<br>
Para habilitar los informes en Analytics y ver los datos de contenido y publicidad que está recopilando, debe habilitar los informes en Analytics. Véase [Habilitación de informes multimedia](/help/reporting/media-reports-enable.md).
