---
title: Conozca los requisitos previos de la recopilación de medios de streaming de Adobe
description: Introducción a la recopilación de medios de streaming. Aprenda lo que necesita para la implementación de.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 64%

---

# Requisitos previos {#prerequisites}

Antes de empezar a implementar la recopilación de medios de streaming de Adobe, complete las siguientes tareas:

1. **Revisar la información general de la colección de medios de streaming**<br>
Antes de comenzar a implementar Streaming Media Collection, revise la [descripción general de Streaming Media Collection](/help/media-overview.md) para asegurarse de que se ajuste a sus necesidades.

1. **Confirmar el modelo de precios**<br>
El modelo de precios actual para el complemento de recopilación de medios de streaming de Adobe se basa en las transmisiones de vídeo. Si es necesario, póngase en contacto con su representante de ventas o con el equipo de cuenta de Adobe, ya que el complemento se vende por separado para Adobe Analytics y Adobe Experience Platform.

1. **Habilitar informes de Adobe Analytics**<br>
Para habilitar los informes en Analytics o Customer Journey Analytics y ver los datos de contenido y publicidad que está recopilando, debe habilitar los informes. Véase [Habilitación de informes multimedia](/help/reporting/media-reports-enable.md).

1. **Implementación del servicio de identidad de Adobe Experience Platform en Experience Cloud**

   El **servicio de identidad** habilita el marco de identificación común para los servicios principales de Experience Cloud, sus soluciones y los atributos de cliente y las audiencias en el servicio principal People. Funciona asignando ID únicos y persistentes a los visitantes del sitio. Cuando su organización implementa el servicio de ID, este ID le permite identificar el mismo visitante del sitio y sus datos en diferentes soluciones de Experience Cloud.

   ![Gráfico del servicio de ID](assets/mc_id_service_graphic.png)

   El servicio de ID también puede reemplazar los distintos ID específicos de la solución (por ejemplo, Analytics AID). Gracias al [ID de cliente y a los estados de autenticación](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=es), el servicio de ID le permite transferir sus propios ID de cliente a Experience Cloud. No obstante, tenga en cuenta que el servicio de ID solo funciona con las soluciones a las que ya se ha suscrito. Si no se ha registrado para acceder a otros productos, el servicio de ID no proporciona el acceso.

   El servicio de ID es un componente integral de muchas funciones, mejoras y servicios de Experience Cloud. En la actualidad, el servicio de ID es compatible con [Analytics](https://www.adobe.com/es/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/es/marketing-cloud/data-management-platform.html) y [Target.](https://www.adobe.com/es/marketing-cloud/testing-targeting.html)

   Si no ha implementado el servicio de ID, ahora es el momento de empezar a pensar en una estrategia de migración. Para obtener más información acerca de la importancia y la función que desempeña el servicio de ID, consulte [Por qué debería plantearse el servicio de ID.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Para obtener más información sobre el Experience Cloud ID, consulte [Información general sobre el Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es) y [Servicio de Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es).

1. **Ver requisitos previos adicionales para el método de implementación**

   Según cómo planee implementar la recopilación de medios de streaming, consulte los requisitos previos para cualquiera de los siguientes métodos de implementación:

   * [Requisitos previos para implementaciones solo de Adobe Analytics](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Requisitos previos para implementaciones de Edge](/help/implementation/edge/prerequisites-edge.md)

   Utilice la [Información general sobre implementación](/help/implementation/overview.md) para determinar qué método de implementación es el adecuado para usted.
