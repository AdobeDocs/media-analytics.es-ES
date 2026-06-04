---
title: Configuración de Android para medios de streaming
description: Configure Adobe Experience Platform Mobile SDK en Android para enviar datos de medios de streaming a Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Configuración de Android para medios de streaming

La extensión de Adobe Streaming Media for Edge Network (`EdgeMedia`) recopila datos de sesión de medios en la aplicación de Android y los envía a Edge Network. Esta página describe la configuración en código. Para configurar SDK a través de una propiedad móvil de etiquetas, consulte [Configurar Android para medios de streaming con etiquetas](android-tags.md).

* **Requisitos previos**:
   * Complete la [descripción general de la implementación de Edge](overview.md) (esquema, conjunto de datos, secuencia de datos con [!UICONTROL Media Analytics] habilitado).
   * Agregue las extensiones `Core`, `Edge`, `EdgeIdentity` y `EdgeMedia` a su aplicación. Consulte [Medios de streaming de Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/) para la instalación y el registro.

## Configuración de medios para Android

Defina las claves de configuración de medios al inicializar SDK:

```kotlin
val configuration = mapOf(
  "edgeMedia.channel" to "sample_channel",
  "edgeMedia.playerName" to "player_name",
  "edgeMedia.appVersion" to "app_version"
)
MobileCore.updateConfiguration(configuration)
```

A continuación, cree un rastreador para administrar una sesión de medios:

```kotlin
val tracker = Media.createTracker()
```

Para obtener las claves de configuración y la API de seguimiento completa, consulte la [Referencia de la API de Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/).

## Seguimiento de eventos de medios

Con el rastreador creado, rastree cada evento de medios mediante su método de rastreador. Consulte la pestaña **Android** en cada página de [evento](/help/implementation/events/overview.md) y [variable](/help/implementation/variables/overview.md) para ver las llamadas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones de Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Medios de streaming de Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configurar Android para medios de transmisión con etiquetas](android-tags.md)
>* [Resumen de eventos](/help/implementation/events/overview.md)
