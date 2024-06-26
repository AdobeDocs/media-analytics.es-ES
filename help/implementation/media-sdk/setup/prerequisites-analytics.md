---
title: Requisitos previos para implementaciones solo de Adobe Analytics
description: Conozca los requisitos previos para utilizar el complemento de recopilación de medios de streaming con implementaciones solo de Adobe Analytics
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 43%

---

# Requisitos previos para implementaciones solo de Adobe Analytics

Los requisitos previos descritos en esta sección son específicos para implementar el complemento de recopilación de medios de streaming con implementaciones solo de Adobe Analytics (cuando no se utiliza Edge).

1. **Complete los requisitos previos generales**<br>
Tanto si implementa el complemento de recopilación de medios de streaming para implementaciones solo de Adobe Analytics como para implementaciones de Edge, asegúrese de cumplir los requisitos siguientes [requisitos previos generales](/help/getting-started/prereqs.md).

1. **Confirme que tiene una implementación de Adobe Analytics.**<br>
Al implementar el complemento de recopilación de medios de streaming con una implementación solo de Analytics, también se requiere una implementación básica de Adobe Analytics. Consulte [Implementación de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) para obtener más información.

1. **Obtener la URL del servidor de seguimiento de medios**<br>
Solicite a su representante de Adobe Analytics la URL del servidor de seguimiento de medios. Este es el `collection-api-server` URL para el SDK de Mobile, el SDK de JavaScript y el servidor de seguimiento de la API de no recopilación para Roku. Los nombres de dominio para la implementación de API son: `[your_namespace].hb-api.omtrdc.net`.

1. **Descargar Media SDK actual o implementar las extensiones necesarias**<br>
Según la ruta de implementación, [descargue el SDK actual](/help/getting-started/download-sdks.md) para plataformas web, móviles o de servicios OTT. Las extensiones necesarias deben implementarse para habilitar las rutas de las extensiones del complemento de recopilación de medios de streaming.

1. **Habilitar los informes de Adobe Analytics**<br>
Para habilitar los informes en Analytics y ver los datos de contenido y publicidad que está recopilando, debe habilitar los informes en Analytics. Véase [Habilitación de informes multimedia](/help/reporting/media-reports-enable.md).
