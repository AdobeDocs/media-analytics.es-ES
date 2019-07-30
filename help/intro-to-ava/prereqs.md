---
seo-title: Requisitos previos
title: Requisitos previos
uuid: 4 c 0 b 37 f 3-8615-4 cc 0-b 9 c 9-eeb 029067064
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Requisitos previos{#prerequisites}

## Decisions {#decision}

Antes de empezar la implementación del seguimiento, deberá tomar algunas decisiones importantes sobre qué implementación se adapta más a su situación:

* **Media Analytics**: uso de los Media SDK más recientes (estándar, implementación recomendada) o de la API de Media Collection (RESTful).
* **Milestone**: implementación de seguimiento anterior de Adobe.
* **Data Insertion API**: implementación del seguimiento sin el uso de Media SDK.

## Tareas {#prereq-tasks}

For a *Media Analytics* implementation, here are the tasks you must complete before you begin:

1. **Habilitar Experience Cloud**.

   Debe implementar el servicio de identidad de Adobe Experience Platform.

   El servicio de identidad habilita el marco de identificación común para los servicios principales, las soluciones y los atributos del cliente y las audiencias del cliente en el servicio principal Personas. Funciona asignando ID únicos y persistentes a los visitantes del sitio. Cuando la organización implementa el servicio de ID, este ID le permite identificar al mismo visitante del sitio y sus datos en diferentes soluciones de Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   El servicio de ID también puede sustituir los distintos ID de soluciones específicas (por ejemplo, Analytics AID). A través de las funciones [Estados de autenticación de los IDs de cliente](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html), el servicio de ID le permite pasar sus propios ID de cliente a Experience Cloud. Sin embargo, tenga en cuenta que el servicio de ID solo funciona con las soluciones a las que ya se ha suscrito. Si no se ha registrado para acceder a otros productos, el servicio de ID no le proporcionará acceso.

   De ahora en adelante, el servicio de ID será un componente integral de muchas funciones, mejoras y servicios tanto actuales como futuros de Experience Cloud. Currently, the ID service supports [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) and [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Para participar en Adobe Experience Cloud Device Co-op, es necesario el servicio Experience Cloud ID.

   Si no ha implementado el servicio de ID, ahora es el momento de empezar a pensar en una estrategia de migración. For more information about the importance and role of the ID service, see [Why the Identity Service Should be on Your Radar.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In the absence of any user ID information present on the media-specific calls, the default analytics [Fallback ID Methods](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) will apply.

   For additional information about the Experience Cloud ID, see [Experience Cloud ID Overview,](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) and [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/)

1. **Habilitar los informes de Adobe Analytics**.

   Para habilitar los informes en Analytics y ver los datos de contenido y de publicidad que está recopilando, consulte [Habilitación de informes de medios.](/help/media-reports/media-reports-enable.md)

