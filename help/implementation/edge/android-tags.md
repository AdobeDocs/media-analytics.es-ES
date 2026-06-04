---
title: Configuración de Android para medios de streaming con etiquetas
description: Configure la recopilación de medios de streaming para Android con la extensión de etiquetas Adobe Streaming Media for Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Configuración de Android para medios de streaming con etiquetas

Puede configurar la recopilación de medios de streaming para su aplicación de Android a través de una propiedad móvil Etiquetas con la configuración de medios administrada en la IU de recopilación de datos. Esta página cubre la configuración de Etiquetas. Para configurar SDK en código, consulte [Configurar Android para medios de streaming](android.md).

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
1. Publique los cambios y, a continuación, agregue las dependencias `Core`, `Edge`, `EdgeIdentity` y `EdgeMedia` a la aplicación y regístrelos en Mobile Core.

## Seguimiento de eventos de medios

Con la propiedad publicada y el rastreador creado, rastree cada evento de medios mediante su método de rastreador. Consulte la pestaña **Android** en cada página de [evento](/help/implementation/events/overview.md) y [variable](/help/implementation/variables/overview.md) para ver las llamadas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones de Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Medios de streaming de Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configurar Android para medios de transmisión (en código)](android.md)
>* [Resumen de eventos](/help/implementation/events/overview.md)
