---
title: Requisitos previos para implementaciones solo de Adobe Analytics
description: Conozca los requisitos previos para utilizar medios de streaming con implementaciones solo de Adobe Analytics
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 13%

---

# Requisitos previos para implementaciones de Edge

Los requisitos previos descritos en esta sección son específicos para implementar Streaming Media con implementaciones de Edge.

1. **Complete los requisitos previos generales**<br>
Tanto si implementa Streaming Media para implementaciones solo de Adobe Analytics como para implementaciones de Edge, asegúrese de cumplir con las [requisitos previos generales](/help/getting-started/prereqs.md).

1. **Confirme que va a implementar una solución de Adobe compatible con Edge y Streaming Media**<br>
Al implementar Streaming Media con Edge, también debe tener un Customer Journey Analytics en funcionamiento, Adobe Analytics, Adobe Journey Optimizer o una implementación de Real-time Customer Data Platform. Consulte los siguientes recursos de documentación para obtener más información:
   * [Guía de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=es)
   * [Implementación de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es)
   * [Documentación de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es)
   * [Documentación de Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **Obtener la URL del servidor de seguimiento de medios**<br>
Solicite a su representante de Customer Journey Analytics la URL del servidor de seguimiento de medios. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Instalación de Media Analytics con Edge**<br>
Siga los pasos de [Instalación de Media Analytics con Experience Platform Edge](/help/implementation/edge/implementation-edge.md).