---
title: Migración de audiencias al nuevo tipo de datos de Adobe Analytics para medios de streaming
description: Obtenga información sobre cómo migrar audiencias al nuevo tipo de datos de Adobe Analytics para medios de streaming
feature: Streaming Media
role: User, Admin, Developer
exl-id: 5664bf56-b228-430a-944c-faaab55fa108
TQID: https://experienceleague.adobe.com/TqsfcR2JgxVjDNx3-CBBa9n6pwvuGk9JgQ--DvWeHg0
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 92e1a77339d29b0ef7ec8adc76817b2ac61ee900
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 1%

---

# Migración de audiencias a los nuevos campos de medios de streaming

En este documento se describe cómo se debe migrar una audiencia que usa campos del tipo de datos de los servicios de medios de streaming de Adobe llamados &quot;medios&quot; para que use el nuevo tipo de datos correspondiente denominado &quot;[Detalles de informes de medios](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.

## Migración de una audiencia

Para migrar una audiencia del tipo de datos anterior denominado &quot;Medios&quot; al nuevo tipo de datos denominado &quot;[Detalles de informes de medios](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;, debe editar la audiencia y, en cada regla, reemplazar el campo anterior del tipo de datos obsoleto por el nuevo campo correspondiente del nuevo tipo de datos:

1. Busque reglas que contengan campos del tipo de datos &quot;Medios&quot; obsoleto. Estos son todos los campos que comienzan con la ruta de acceso `media.mediaTimed`.

1. Duplique esas reglas utilizando campos del nuevo tipo de datos &quot;[Detalles de informes de medios](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.

1. Mantenga ambas reglas en su lugar hasta que valide que las audiencias funcionan según lo esperado.

1. Elimine las reglas que contienen campos del tipo de datos &quot;Medios&quot; obsoleto.

1. Compruebe que las audiencias siguen funcionando según lo esperado.

Consulte el parámetro [Content ID](/help/reporting/dimensions/content.md) y el resto de las variables de medios de streaming documentadas en [Servicios de medios de streaming](/help/media-overview.md) para asignar entre los campos antiguos y los campos nuevos. La ruta de campo antigua se encuentra en la propiedad &quot;Ruta de campo XDM&quot;, mientras que la nueva ruta de campo se encuentra en la propiedad &quot;Ruta de campo XDM de creación de informes&quot;.

![Rutas de campo XDM antiguas y nuevas](../../assets/field-paths-updated.jpeg)

## Ejemplo

Para facilitar el seguimiento de las directrices de migración, observe el siguiente ejemplo, que contiene una audiencia con una sola regla. Dado que la audiencia tiene una sola regla, solo es necesario aplicar las directrices de migración una vez.

1. Seleccione el botón **[!UICONTROL Editar audiencia]** en la esquina superior derecha.

1. Busque las reglas configuradas para la audiencia.

   ![Editar audiencia](../../assets/audience-edit.jpeg)

   ![Editar audiencia](../../assets/audience-edit2.jpeg)

1. Seleccione la regla para abrir su configuración.

   ![Editar audiencia](../../assets/audience-edit3.jpeg)

1. (Opcional) Para ver la ruta del campo utilizado en la regla, seleccione el botón de información junto al nombre del campo.

   ![Editar audiencia](../../assets/audience-edit4.jpeg)

1. Identifique el nombre del campo (en este caso, &quot;Inicio de contenidos&quot;).

   ![Editar audiencia](../../assets/audience-edit5.jpeg)

1. Consulte las variables de medios de streaming documentadas en [Servicios de medios de streaming](/help/media-overview.md) para asignar entre los campos antiguos. La ruta de campo antigua se encuentra en la propiedad &quot;Ruta de campo XDM&quot;, mientras que la nueva ruta de campo se puede encontrar en la propiedad &quot;Ruta de campo XDM de creación de informes&quot;. A modo de ejemplo, para el parámetro [Comienzos de medios](/help/reporting/metrics/media-starts.md), el corresponsal de `media.mediaTimed.impressions.value` es `xdm.mediaReporting.sessionDetails.isViewed`.

   ![Ruta XDM actualizada](../../assets/updated-xdm-path.jpeg)

1. Añada la misma regla que la existente utilizando el nuevo campo.

   ![Añadir regla](../../assets/add-rule.jpeg)

   ![Añadir regla](../../assets/add-rule2.jpeg)

   ![Añadir regla](../../assets/add-rule3.jpeg)

1. Seleccione **[!UICONTROL Guardar]** para guardar la audiencia. Puede mantener esta configuración durante el tiempo que necesite para validar que la audiencia sigue funcionando según lo esperado.

1. Una vez completada la validación, quita el campo antiguo y selecciona **[!UICONTROL Guardar]** para guardar la audiencia.

   ![Añadir regla](../../assets/add-rule4.jpeg)

1. Vuelva a validar la audiencia.

   El proceso de migración de audiencias ha finalizado.
