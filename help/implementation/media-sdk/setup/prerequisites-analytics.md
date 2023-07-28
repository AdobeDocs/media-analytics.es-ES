---
title: Requisitos previos para implementaciones solo de Adobe Analytics
description: Conozca los requisitos previos para utilizar medios de streaming con implementaciones solo de Adobe Analytics
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: c4d058ee82f4995f42bfe21c0442004f1f7ea4af
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 58%

---

# Requisitos previos para implementaciones solo de Adobe Analytics

Los requisitos previos descritos en esta sección son específicos para implementar Streaming Media con implementaciones solo de Adobe Analytics (cuando no se usa Edge).

1. **Complete los requisitos previos generales**<br>
Tanto si implementa Streaming Media para implementaciones solo de Adobe Analytics como para implementaciones de Edge, asegúrese de cumplir con las [requisitos previos generales](/help/getting-started/prereqs.md).

1. **Confirme que tiene una implementación de Adobe Analytics.**<br>
Al implementar Streaming Media con una implementación solo de Analytics, también se requiere una implementación básica de Adobe Analytics. Consulte [Implementación de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) para obtener más información.

1. **Obtener la URL del servidor de seguimiento de medios**<br>
Solicite a su representante de Adobe Analytics la URL del servidor de seguimiento de medios. Esta es la `collection-api-server` URL para el SDK de Mobile, el SDK de JavaScript y el servidor de seguimiento de la API de no recopilación para Roku. Los nombres de dominio para la implementación de API son: `[your_namespace].hb-api.omtrdc.net`.

1. **Descargar Media SDK actual o implementar las extensiones necesarias**<br>
Según la ruta de implementación, [descargue el SDK actual](/help/getting-started/download-sdks.md) para plataformas web, móviles o de servicios OTT. Las extensiones necesarias deben implementarse para habilitar Adobe Analytics para medios de transmisión.

1. **Habilitar los informes de Adobe Analytics**<br>
Para habilitar los informes en Analytics y ver los datos de contenido y publicidad que está recopilando, debe habilitar los informes en Analytics. Véase [Habilitación de informes multimedia](/help/reporting/media-reports-enable.md).
