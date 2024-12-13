---
title: Requisitos previos para implementaciones solo de Adobe Analytics
description: Conozca los requisitos previos para utilizar la recopilación de medios de streaming con implementaciones solo de Adobe Analytics o implementaciones de Edge
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 10%

---

# Requisitos previos para implementaciones de Edge

Los requisitos previos descritos en esta sección son específicos para implementar la recopilación de medios de streaming de Adobe con implementaciones de Edge.

1. **Complete los requisitos previos generales**<br>
Tanto si implementa la recopilación de medios de streaming para implementaciones solo de Adobe Analytics como para implementaciones de Edge, asegúrese de cumplir los [requisitos previos generales](/help/getting-started/prereqs.md).

1. **Confirme que está implementando una solución de Adobe compatible con Edge Network y Streaming Media Collection**<br>
Al implementar la recopilación de medios de streaming con Edge, también debe tener un Customer Journey Analytics en funcionamiento, Adobe Analytics, Adobe Journey Optimizer o una implementación de Real-time Customer Data Platform. Consulte los siguientes recursos de documentación para obtener más información:
   * [Guía de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=es)
   * [Implementación de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es)
   * [Documentación de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es)
   * [Documentación de Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **Obtener la URL del servidor de seguimiento de medios**<br>
Solicite a su representante de Customer Journey Analytics la URL del servidor de seguimiento de medios. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementar la colección de medios de transmisión mediante el Edge Network**<br>
Siga los pasos de [Implementar la colección de medios de streaming con el Edge Network](/help/implementation/edge/implementation-edge.md).
