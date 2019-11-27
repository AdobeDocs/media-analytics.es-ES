---
title: Requisitos previos
description: null
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Requisitos previos {#prerequisites}

## Decisiones {#decision}

Antes de empezar la implementación del seguimiento, deberá tomar algunas decisiones importantes sobre qué implementación se adapta más a su situación:

* **Media Analytics**: uso de los Media SDK más recientes (estándar, implementación recomendada) o de la API de Media Collection (RESTful).
* **Milestone**: implementación de seguimiento anterior de Adobe.
* **Data Insertion API**: implementación del seguimiento sin el uso de Media SDK.

## Tareas {#prereq-tasks}

Para una implementación de *Media Analytics*, estas son las tareas que debe completar antes de comenzar:

1. **Habilitar Experience Cloud**.

   Debe implementar el servicio de identidad de Adobe Experience Platform.

   El servicio de identidad habilita el marco de identificación común para los servicios principales de Experience Cloud, sus soluciones, los atributos de cliente y las audiencias en el servicio principal Personas. Funciona asignando ID únicos y persistentes a los visitantes del sitio. Cuando la organización implementa el servicio de ID, este ID le permite identificar al mismo visitante del sitio y sus datos en diferentes soluciones de Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   El servicio de ID también puede sustituir los distintos ID de soluciones específicas (por ejemplo, Analytics AID). A través de las funciones [Estados de autenticación de los IDs de cliente](https://marketing.adobe.com/resources/help/es_ES/mcvid/mcvid-authenticated-state.html), el servicio de ID le permite pasar sus propios ID de cliente a Experience Cloud. Sin embargo, tenga en cuenta que el servicio de ID solo funciona con las soluciones a las que ya se ha suscrito. Si no se ha registrado para acceder a otros productos, el servicio de ID no le proporcionará acceso.

   De ahora en adelante, el servicio de ID será un componente integral de muchas funciones, mejoras y servicios tanto actuales como futuros de Experience Cloud. En la actualidad, el servicio de ID es compatible con [Analytics](https://www.adobe.com/es/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/es/marketing-cloud/data-management-platform.html) y [Target.](https://www.adobe.com/es/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Para participar en la cooperación de dispositivos de Adobe Experience Cloud, se requiere el servicio de Experience Cloud ID.

   Si no ha implementado el servicio de ID, ahora es el momento de empezar a pensar en una estrategia de migración. Para obtener más información acerca de la importancia y la función que desempeña el servicio de ID, consulte [Por qué debería plantearse el servicio de ID.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >Si no hubiera información de ID de usuario presente en las llamadas específicas al contenido, se aplicarán los análisis predeterminados de los [Métodos de identificación secundarios](https://docs.adobe.com/content/help/es-ES/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html).

   Para obtener más información sobre el Experience Cloud ID, consulte [Información general sobre el Experience Cloud ID](https://marketing.adobe.com/resources/help/es_ES/mcvid/mcvid-overview.html) y [Servicio de Adobe Experience Platform.](https://marketing.adobe.com/resources/help/es_ES/mcvid/)

1. **Habilitar los informes de Adobe Analytics**.

   Para habilitar los informes en Analytics y ver los datos de contenido y de publicidad que está recopilando, consulte [Habilitación de informes de contenidos.](/help/media-reports/media-reports-enable.md)

