---
title: Configurar la extensión de etiquetas de Web SDK para los medios de streaming
description: Configure la recopilación de medios de streaming en la extensión de etiquetas Adobe Experience Platform Web SDK.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Configurar la extensión de etiquetas de Web SDK para los medios de streaming

La extensión de etiquetas Adobe Experience Platform Web SDK permite configurar la recopilación de medios de streaming en la interfaz de usuario de recopilación de datos sin el código de configuración `alloy.js`. Esta página cubre la configuración de Etiquetas. Para configurar Web SDK en código, consulte [Configurar Web SDK para medios de transmisión](web-sdk.md).

* **Requisitos previos**:
   * Complete la [descripción general de la implementación de Edge](overview.md) (esquema, conjunto de datos, secuencia de datos con [!UICONTROL Media Analytics] habilitado).
   * Instale y configure la extensión de etiquetas Web SDK. Consulte la [descripción general de la extensión de etiquetas Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/tags/extensions/client/web-sdk/overview).

## Configuración de medios de streaming en la extensión

1. En la IU de recopilación de datos, abra su propiedad web y seleccione **[!UICONTROL Extensiones]**.
1. En la extensión **Adobe Experience Platform Web SDK** instalada, seleccione **[!UICONTROL Configurar]**.
1. Expanda la sección **[!UICONTROL Medios de transmisión]** y establezca lo siguiente:
   * **[!UICONTROL Canal]**: El nombre del canal indicado en cada sesión.
   * **[!UICONTROL Nombre del reproductor]**: El nombre del reproductor multimedia en uso.
   * **[!UICONTROL Versión de la aplicación]**: La versión de la aplicación de reproducción.
   * **[!UICONTROL Intervalo de ping principal]** e **[!UICONTROL intervalo de ping de anuncio]**: La cadencia de ping (en segundos) para el contenido principal y los anuncios.
1. Guarde la configuración de la extensión y publique los cambios.

## Seguimiento de eventos de medios

Con la extensión configurada, envíe cada evento multimedia con la acción **[!UICONTROL Enviar evento]** (o el comando `sendEvent`). Consulte la pestaña **Web SDK** en cada [evento](/help/implementation/events/overview.md) y página de [variable](/help/implementation/variables/overview.md) para ver las cargas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones de Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Información general sobre la extensión de etiquetas Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/tags/extensions/client/web-sdk/overview)
>* [Configurar Web SDK para medios de transmisión (en código)](web-sdk.md)
>* [Resumen de eventos](/help/implementation/events/overview.md)
