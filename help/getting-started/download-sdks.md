---
title: Obtención de SDK, extensiones y API de medios
description: Vínculos a las descargas de SDK para plataformas disponibles, como Android, iOS, JavaScript, Chromecast y Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 625
ht-degree: 30%

---

# Obtención de SDK, extensiones y API de medios

## Implementaciones de Edge (recomendado) {#edge-sdks}

Las implementaciones de Edge recopilan datos una vez y los entregan a través de Adobe Experience Platform Edge Network a varios destinos: Adobe Analytics, Customer Journey Analytics, Adobe Journey Optimizer y Real-Time CDP. Para plataformas sin un SDK nativo (como Smart TV, consolas de juegos y decodificadores), utilice la API de Media Edge.

| | Documentación | Muestra |
|:---:|---|---|
| [![Icono de JavaScript](assets/javascript-icon.png)](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/install/overview)<br>[Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/install/overview) | [Configurar Web SDK para los medios de transmisión](/help/implementation/edge/web-sdk.md) | [Muestra](https://github.com/adobe/alloy-samples/blob/main/media-collection/STANDALONE.md) |
| [![Icono de extensión](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html)<br>[Extensión de etiqueta Web SDK](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html) | [Configurar la extensión de etiquetas Web SDK para los medios de transmisión](/help/implementation/edge/web-sdk-tags.md) | [Muestra](https://github.com/adobe/alloy-samples/blob/main/media-collection/TAGS_IMPL.md) |
| [![Icono de Android](assets/android.png)](https://github.com/adobe/aepsdk-media-android)<br>[Android SDK](https://github.com/adobe/aepsdk-media-android) | [Configurar Android para los medios de transmisión](/help/implementation/edge/android.md) | [Muestra](https://github.com/adobe/aepsdk-media-android/tree/main/code/testapp) |
| [![Icono de Apple iOS](assets/apple.png)](https://github.com/adobe/aepsdk-media-ios)<br>[iOS / tvOS SDK](https://github.com/adobe/aepsdk-media-ios) | [Configurar iOS para los medios de transmisión](/help/implementation/edge/ios.md) | [Muestra](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| [![Icono de extensión](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Extensión de etiqueta Android](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Configurar la extensión de etiquetas de Android para los medios de transmisión](/help/implementation/edge/android-tags.md) | |
| [![Icono de extensión](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Extensión de etiqueta iOS / tvOS](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Configurar la extensión de etiquetas de iOS para los medios de transmisión](/help/implementation/edge/ios-tags.md) | |
| [![Icono de Roku](assets/roku-icon.png)](https://github.com/adobe/aepsdk-roku)<br>[SDK de Roku Edge](https://github.com/adobe/aepsdk-roku) | [Configurar Roku Edge para los medios de transmisión](/help/implementation/edge/roku.md) | [Muestra](https://github.com/adobe/aepsdk-roku/tree/main/sample/simple-videoplayer-channel) |
| [![Icono de API](assets/api.png)](https://developer.adobe.com/data-collection-apis/docs/api/media-edge)<br>[API de Media Edge](https://developer.adobe.com/data-collection-apis/docs/api/media-edge) | [Configurar la API de Media Edge](/help/implementation/edge/media-edge-api.md) | [Muestra](https://developer.adobe.com/data-collection-apis/docs/getting-started/media-edge-examples) |

## Implementaciones solo de Analytics {#analytics-only-sdks}

Estos SDK y extensiones envían datos directamente a Adobe Analytics. Para nuevas implementaciones, utilice las implementaciones de Edge anteriores. Para llevar los datos existentes de Analytics a Customer Journey Analytics u otras aplicaciones de Experience Platform, usa el [conector de origen de Analytics](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/analytics).

| | Documentación | Muestra |
|:---:|---|---|
| [![Icono de JavaScript](assets/javascript-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2)<br>[Media SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Configurar JavaScript para los medios de transmisión](/help/implementation/analytics-only/javascript.md) | [Muestra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| [![Icono de extensión](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=es)<br>[Extensión de medios](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=es) | [Configurar JavaScript mediante etiquetas para los medios de transmisión](/help/implementation/analytics-only/javascript-tags.md) | [Muestra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| [![Icono de Chromecast](assets/chromecast-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3)<br>[Chromecast SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Configurar Chromecast para los medios de transmisión](/help/implementation/analytics-only/chromecast.md) | [Muestra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/chromecast/samples/BasicPlayerSample) |
| [![Icono de Roku](assets/roku-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.7)<br>[Roku SDK 2.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.7) | [Configuración de Roku 2.x para medios de transmisión](/help/implementation/analytics-only/roku-2x.md) | [Muestra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/roku/samples) |
| [![Icono de API](assets/api.png)](/help/implementation/media-collection-api/mc-api-overview.md)<br>[API de recopilación de medios](/help/implementation/media-collection-api/mc-api-overview.md) | [Configurar la API de Media Collection](/help/implementation/analytics-only/media-collection-api.md) | |
