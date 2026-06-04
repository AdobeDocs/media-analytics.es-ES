---
title: Configuración de Web SDK para medios de streaming
description: Configure Adobe Experience Platform Web SDK (alloy.js) para enviar datos de medios de streaming a Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 5%

---

# Configuración de Web SDK para medios de streaming

El componente `streamingMedia` del Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/js-overview) (`alloy.js`, versión 2.20.0 o posterior) recopila datos de sesión multimedia en el sitio web y los envía a Edge Network. Esta página cubre la configuración en código (`alloy.js`). Para configurar Web SDK mediante etiquetas, consulte [Configurar la extensión de etiquetas de Web SDK para medios de transmisión](web-sdk-tags.md).

* **Requisitos previos**:
   * Complete la [descripción general de la implementación de Edge](overview.md) (esquema, conjunto de datos, secuencia de datos con [!UICONTROL Media Analytics] habilitado).
   * Instale Web SDK 2.20.0 o posterior. Consulte [Instalar Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/install/overview).

## Configuración del componente streaming de medios

Agregar el componente `streamingMedia` a la configuración `alloy`:

```js
alloy("configure", {
  edgeConfigId: "<datastreamID>",
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Para obtener información detallada sobre la configuración, consulte el comando [`streamingMedia` &#x200B;](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/configure/streamingmedia).

### Migración desde Media JS SDK

Si se está moviendo de Media JS (3.x) SDK, el comando Web SDK [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/getmediaanalyticstracker) devuelve una instancia de seguimiento que expone las mismas API que Media SDK [3.x](/help/implementation/analytics-only/javascript.md), de modo que las llamadas de seguimiento existentes seguirán funcionando.

## Seguimiento de eventos de medios

Con el SDK configurado, envíe cada evento multimedia llamando a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview). Consulte la pestaña **Web SDK** en cada [evento](/help/implementation/events/overview.md) y página de [variable](/help/implementation/variables/overview.md) para ver las cargas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones de Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Información general de SDK web](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/js-overview)
>* [Resumen de eventos](/help/implementation/events/overview.md)
>* [Resumen de variables](/help/implementation/variables/overview.md)
