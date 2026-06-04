---
title: Configuración de iOS para medios de streaming
description: Configure Adobe Experience Platform Mobile SDK en iOS para enviar datos de medios de streaming a Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Configuración de iOS para medios de streaming

La extensión de Adobe Streaming Media para Edge Network (`AEPEdgeMedia`) recopila datos de sesión de medios en la aplicación de iOS o tvOS y los envía a Edge Network. Esta página describe la configuración en código. Para configurar SDK a través de una propiedad móvil de etiquetas, consulte [Configurar iOS para medios de streaming con etiquetas](ios-tags.md).

* **Requisitos previos**:
   * Complete la [descripción general de la implementación de Edge](overview.md) (esquema, conjunto de datos, secuencia de datos con [!UICONTROL Media Analytics] habilitado).
   * Agregue las extensiones `AEPCore`, `AEPEdge`, `AEPEdgeIdentity` y `AEPEdgeMedia` a su aplicación. Consulte [Medios de streaming de Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/) para la instalación y el registro.

## Configuración de medios para iOS

Defina las claves de configuración de medios al inicializar SDK:

```swift
let configuration = [
  "edgeMedia.channel": "sample_channel",
  "edgeMedia.playerName": "player_name",
  "edgeMedia.appVersion": "app_version"
]
MobileCore.updateConfiguration(configuration)
```

A continuación, cree un rastreador para administrar una sesión de medios:

```swift
let tracker = Media.createTracker()
```

Para obtener las claves de configuración y la API de seguimiento completa, consulte la [Referencia de la API de Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/).

## Seguimiento de eventos de medios

Con el rastreador creado, rastree cada evento de medios mediante su método de rastreador. Consulte la pestaña **iOS** en cada página de [evento](/help/implementation/events/overview.md) y [variable](/help/implementation/variables/overview.md) para ver las llamadas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones de Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Medios de streaming de Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configurar iOS para medios de transmisión con etiquetas](ios-tags.md)
>* [Resumen de eventos](/help/implementation/events/overview.md)
