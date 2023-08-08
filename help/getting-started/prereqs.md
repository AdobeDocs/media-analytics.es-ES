---
title: Conozca los requisitos previos de los medios de streaming
description: Introducción a Adobe Analytics Streaming Media. Aprenda lo que necesita para implementar Adobe Analytics for Streaming Media.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: ht
source-wordcount: '442'
ht-degree: 100%

---

# Requisitos previos  {#prerequisites}

Antes de empezar a implementar medios de streaming, complete las siguientes tareas:

1. **Revise la información general de medios de streaming**<br>
Antes de empezar a implementar los medios de streaming, revise la [Información general sobre medios de streaming](/help/media-overview.md) para asegurarse de que esta opción satisface sus necesidades.

1. **Confirme el modelo de precios del Streaming de medios**<br>
El modelo de precios actual se basa en las transmisiones de vídeo. Si es necesario, póngase en contacto con su equipo de ventas o con el equipo de cuentas de Adobe, ya que los medios de streaming se venden por separado, como complemento de Adobe Analytics.<!--update when media SKUs are added to other AEP apps -->

1. **Habilitar los informes de Adobe Analytics**<br>
Para habilitar los informes en Analytics y ver los datos de contenido y publicidad que está recopilando, debe habilitar los informes en Analytics. Véase [Habilitación de informes multimedia](/help/reporting/media-reports-enable.md).

1. **Implementación del servicio de identidad de Adobe Experience Platform en Experience Cloud**

   El **servicio de identidad** habilita el marco de identificación común para los servicios principales de Experience Cloud, sus soluciones y los atributos de cliente y las audiencias en el servicio principal People. Funciona asignando ID únicos y persistentes a los visitantes del sitio. Cuando su organización implementa el servicio de ID, este ID le permite identificar el mismo visitante del sitio y sus datos en diferentes soluciones de Experience Cloud.

   ![Gráfico del servicio de ID](assets/mc_id_service_graphic.png)

   El servicio de ID también puede reemplazar los distintos ID específicos de la solución (por ejemplo, Analytics AID). Gracias al [ID de cliente y a los estados de autenticación](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=es), el servicio de ID le permite transferir sus propios ID de cliente a Experience Cloud. No obstante, tenga en cuenta que el servicio de ID solo funciona con las soluciones a las que ya se ha suscrito. Si no se ha registrado para acceder a otros productos, el servicio de ID no proporciona el acceso.

   El servicio de ID es un componente integral de muchas funciones, mejoras y servicios de Experience Cloud. En la actualidad, el servicio de ID es compatible con [Analytics](https://www.adobe.com/es/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/es/marketing-cloud/data-management-platform.html) y [Target.](https://www.adobe.com/es/marketing-cloud/testing-targeting.html)

   Si no ha implementado el servicio de ID, ahora es el momento de empezar a pensar en una estrategia de migración. Para obtener más información acerca de la importancia y la función que desempeña el servicio de ID, consulte [Por qué debería plantearse el servicio de ID.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Para obtener más información sobre el Experience Cloud ID, consulte [Información general sobre el Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es) y [Servicio de Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es).

1. **Ver requisitos previos adicionales para el método de implementación**

   Según cómo planee implementar los medios de streaming, consulte los requisitos previos para cualquiera de los siguientes métodos de implementación:

   * [Requisitos previos para implementaciones solo de Adobe Analytics](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Requisitos previos para implementaciones de Edge](/help/implementation/edge/prerequisites-edge.md)

   Utilice la [Información general sobre implementación](/help/implementation/overview.md) para determinar qué método de implementación es el adecuado para usted.
