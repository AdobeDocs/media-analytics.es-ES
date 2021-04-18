---
title: Requisitos previos
description: Requisitos previos
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 100%

---

# Requisitos previos {#prerequisites}

## Decisiones {#decision}

Antes de comenzar la implementación de seguimiento, tiene que tomar algunas decisiones anticipadas, con respecto a qué implementación tiene mayor sentido para su situación:

* **Media Analytics:** uso del Media SDK más reciente (la implementación estándar recomendada) o la API de Media Collection (RESTful)
* **Milestone:** La implementación de seguimiento de Adobe más antigua
* **API de inserción de datos:** Implementación del seguimiento sin usar Media SDK

## Tareas {#prereq-tasks}

Para una implementación de *Media Analytics*, estas son las tareas que debe completar antes de comenzar:

1. **Habilitar Experience Cloud**.

   Debe implementar el servicio de identidad de Adobe Experience Platform.

   El servicio de identidad habilita el marco de identificación común para los servicios principales de Experience Cloud, sus soluciones, los atributos de cliente y las audiencias en el servicio principal Personas. Funciona asignando ID únicos y persistentes a los visitantes del sitio. Cuando su organización implementa el servicio de ID, este ID le permite identificar el mismo visitante del sitio y sus datos en diferentes soluciones de Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   El servicio de ID también puede reemplazar los distintos ID específicos de la solución (por ejemplo, Analytics AID). Gracias al [ID de cliente y a los estados de autenticación](https://docs.adobe.com/content/help/es-ES/id-service/using/reference/authenticated-state.html), el servicio de ID le permite transferir sus propios ID de cliente a Experience Cloud. No obstante, tenga en cuenta que el servicio de ID solo funciona con las soluciones a las que ya se ha suscrito. Si no se ha registrado para acceder a otros productos, el servicio de ID no proporciona el acceso.

   De ahora en adelante, el servicio de ID será un componente integral de muchas funciones, mejoras y servicios tanto actuales como futuros de Experience Cloud. En la actualidad, el servicio de ID es compatible con [Analytics](https://www.adobe.com/es/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/es/marketing-cloud/data-management-platform.html) y [Target.](https://www.adobe.com/es/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Para participar en la cooperación de dispositivos de Adobe Experience Cloud, se requiere el servicio de Experience Cloud ID.

   Si no ha implementado el servicio de ID, ahora es el momento de empezar a pensar en una estrategia de migración. Para obtener más información acerca de la importancia y la función que desempeña el servicio de ID, consulte [Por qué debería plantearse el servicio de ID.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >Si no hubiera información de ID de usuario presente en las llamadas específicas al contenido, se aplicarán los análisis predeterminados de los [Métodos de identificación secundarios](https://docs.adobe.com/content/help/es-ES/analytics/technotes/visitor-identification.translate.html).

   Para obtener más información sobre el Experience Cloud ID, consulte [Información general sobre el Experience Cloud ID](https://docs.adobe.com/content/help/es-ES/id-service/using/intro/overview.html) y [Servicio de Adobe Experience Platform.](https://docs.adobe.com/content/help/es-ES/id-service/using/home.html)

1. **Habilitar los informes de Adobe Analytics**.

   Para habilitar los informes en Analytics y ver los datos de contenido y de publicidad que está recopilando, consulte [Habilitación de informes de contenidos.](/help/media-reports/media-reports-enable.md)
