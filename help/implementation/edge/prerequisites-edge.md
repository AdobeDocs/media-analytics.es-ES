---
title: Requisitos previos para implementaciones solo de Adobe Analytics
description: Conozca los requisitos previos para utilizar la recopilación de medios de streaming con implementaciones solo de Adobe Analytics o implementaciones de Edge
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
TQID: https://experienceleague.adobe.com/OqimGafihuirpnAaZ4AvrX2lrOmCtr0FLXk3QwoVTew
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
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
source-wordcount: 212
ht-degree: 16%

---

# Requisitos previos para implementaciones de Edge

Los requisitos previos descritos en esta sección son específicos para implementar Adobe Streaming Media Collection con implementaciones de Edge.

1. **Completar los requisitos previos generales**<br>
Tanto si implementa la recopilación de medios de streaming para implementaciones solo de Adobe Analytics como para implementaciones de Edge, asegúrese de cumplir los [requisitos previos generales](/help/getting-started/prereqs.md).

1. **Confirme que está implementando una solución de Adobe compatible con Edge Network y Streaming Media Collection**<br>
Al implementar la recopilación de medios de streaming con Edge, también debe tener una implementación de Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer o Real-Time Customer Data Platform en funcionamiento. Consulte los siguientes recursos de documentación para obtener más información:
   * [Guía de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=es)
   * [Implementación de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es)
   * [Documentación de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es)
   * [Documentación de Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=es)

1. **Obtener la URL del servidor de seguimiento de medios**<br>
Solicite a su representante de Customer Journey Analytics la URL del servidor de seguimiento de medios. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementar la colección de medios de streaming mediante Edge Network**<br>
Siga los pasos de [Implementar la colección de medios de streaming con Edge Network](/help/implementation/edge/implementation-edge.md).
