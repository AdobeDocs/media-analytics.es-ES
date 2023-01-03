---
title: Conozca los requisitos previos de los medios de streaming
description: Introducción a Adobe Analytics Streaming Media. Aprenda lo que necesita para implementar Adobe Analytics for Streaming Media.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b022bed6b7be0cc97caaaf6b7bbc42474a57b400
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 96%

---

# Requisitos previos {#prerequisites}

Para implementar Adobe Analytics para Streaming de medios, complete las siguientes tareas:

1. **Confirmar el modelo de precios del Streaming de medios**<br>
El modelo de precios actual se basa en las transmisiones de vídeo. Si es necesario, póngase en contacto con su representante de ventas o administrador de cuentas para firmar un nuevo pedido de ventas, ya que Streaming de medios de Analytics se vende por separado de Adobe Analytics.

1. **Confirmar la implementación de Adobe Analytics**<br>
Streaming de medios para Adobe Analytics también requiere una implementación básica de Adobe Analytics. Consulte [Implementación de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) para obtener más información.

1. **Obtener la URL del servidor de seguimiento de medios**<br>
Solicite a su representante de Adobe Analytics la URL del servidor de seguimiento de medios. Esta es la 
`collection-api-server` URL para el SDK de Mobile, el SDK de JavaScript y el servidor de seguimiento de la API de no recopilación para Roku. Los nombres de dominio para la implementación de API son: `[your_namespace].hb-api.omtrdc.net`.

1. **Descargar Media SDK actual o implementar las extensiones necesarias**<br>
Según la ruta de implementación, [descargue el SDK actual](download-sdks.md) para plataformas web, móviles o de servicios OTT. Las extensiones requeridas deben implementarse para habilitar las rutas de extensiones de Adobe Analytics para medios de streaming.

1. **Habilitar los informes de Adobe Analytics**<br>
Para habilitar los informes en Analytics y ver los datos de contenido y publicidad que está recopilando, debe habilitar los informes en Analytics. Consulte [Habilitación de informes de contenidos](/help/reporting/media-reports-enable.md).

1. **Habilitar Experience Cloud**<br>


## Implementación del servicio de ID de Adobe Experience Platform {#implement-id}

El **servicio de identidad** habilita el marco de identificación común para los servicios principales de Experience Cloud, sus soluciones y los atributos de cliente y las audiencias en el servicio principal People. Funciona asignando ID únicos y persistentes a los visitantes del sitio. Cuando su organización implementa el servicio de ID, este ID le permite identificar el mismo visitante del sitio y sus datos en diferentes soluciones de Experience Cloud.

![Gráfico del servicio de ID](assets/mc_id_service_graphic.png)

El servicio de ID también puede reemplazar los distintos ID específicos de la solución (por ejemplo, Analytics AID). Gracias al [ID de cliente y a los estados de autenticación](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=es), el servicio de ID le permite transferir sus propios ID de cliente a Experience Cloud. No obstante, tenga en cuenta que el servicio de ID solo funciona con las soluciones a las que ya se ha suscrito. Si no se ha registrado para acceder a otros productos, el servicio de ID no proporciona el acceso.

El servicio de ID es un componente integral de muchas funciones, mejoras y servicios de Experience Cloud. En la actualidad, el servicio de ID es compatible con [Analytics](https://www.adobe.com/es/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/es/marketing-cloud/data-management-platform.html) y [Target.](https://www.adobe.com/es/marketing-cloud/testing-targeting.html)

Si no ha implementado el servicio de ID, ahora es el momento de empezar a pensar en una estrategia de migración. Para obtener más información acerca de la importancia y la función que desempeña el servicio de ID, consulte [Por qué debería plantearse el servicio de ID.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

Para obtener más información sobre el Experience Cloud ID, consulte [Información general sobre el Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es) y [Servicio de Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es).
