---
title: Configuración de iOS para medios de streaming con etiquetas
description: Configure la recopilación de medios de streaming para iOS con la extensión de etiquetas Adobe Streaming Media for Edge Network.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%
---
# Configuración de iOS para medios de streaming con etiquetas

Puede configurar la recopilación de medios de streaming para su aplicación de iOS o tvOS a través de una propiedad móvil Etiquetas, con la configuración de medios administrada en la IU de recopilación de datos. Esta página cubre la configuración de Etiquetas. Para configurar SDK en código, consulte [Configurar iOS para medios de streaming](ios.md).

* **Requisitos previos**:
  * Complete la [descripción general de la implementación de Edge](overview.md) (esquema, conjunto de datos, secuencia de datos con [!UICONTROL Media Analytics] habilitado).
  * Cree una propiedad móvil en la interfaz de usuario de la recopilación de datos. Consulte [Medios de streaming de Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/).

## Configuración de la extensión

1. En la IU de recopilación de datos, abra su propiedad móvil y seleccione **[!UICONTROL Extensiones]**.
1. En la ficha **[!UICONTROL Catálogo]**, busque la extensión **Adobe Streaming Media for Edge Network** y seleccione **[!UICONTROL Instalar]**.
1. Establezca lo siguiente y, a continuación, guarde:
   * **[!UICONTROL Canal]**: el nombre del canal indicado en cada sesión.
   * **[!UICONTROL Nombre del reproductor]**: el nombre del reproductor multimedia en uso.
   * **[!UICONTROL Versión de la aplicación]**: la versión de la aplicación de reproducción.
1. Publique los cambios y, a continuación, agregue las dependencias `AEPCore`, `AEPEdge`, `AEPEdgeIdentity` y `AEPEdgeMedia` a la aplicación y regístrelos en Mobile Core.

## Seguimiento de eventos de medios

Con la propiedad publicada y el rastreador creado, rastree cada evento de medios mediante su método de rastreador. Consulte la pestaña **iOS** en cada página de [evento](/help/implementation/events/overview.md) y [variable](/help/implementation/variables/overview.md) para ver las llamadas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones de Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Medios de streaming de Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configurar iOS para medios de transmisión (en código)](ios.md)
>* [Resumen de eventos](/help/implementation/events/overview.md)
