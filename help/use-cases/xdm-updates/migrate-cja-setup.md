---
title: Migración de audiencias al nuevo tipo de datos de Adobe Analytics para medios de streaming
description: Obtenga información sobre cómo migrar audiencias al nuevo tipo de datos de Adobe Analytics para medios de streaming
feature: Streaming Media
role: User, Admin, Developer
exl-id: 67e67a4b-bd61-4247-93b7-261bd348d29b
TQID: https://experienceleague.adobe.com/Y-Y-xWKm-zOzaQm8kMbgGx8r6BTNLl-Q5AltlF5v7aA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 759
ht-degree: 1%

---

# Migrar Customer Journey Analytics para utilizar los nuevos campos de medios de streaming

En este documento se describe cómo se debe actualizar una configuración de Customer Journey Analytics que usa el tipo de datos de servicios de medios de streaming de Adobe denominado &quot;Medios&quot; para usar el nuevo tipo de datos correspondiente denominado &quot;[Detalles de informes de medios](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.

## Migrar Customer Journey Analytics

Para migrar una configuración de Customer Journey Analytics del tipo de datos anterior denominado &quot;Medios&quot; al nuevo tipo de datos denominado &quot;[Detalles de informes de medios](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;, debe actualizar las configuraciones siguientes que usan el tipo de datos anterior:

* Vistas de datos

* Campos derivados

### Migración de vistas de datos

Para migrar las vistas de datos al nuevo tipo de datos:

1. Busque todas las vistas de datos con el tipo de datos obsoleto &quot;Medios&quot;. Estos son todos los campos para los que la ruta de acceso comienza por `media.mediaTimed`.

1. Realice cualquiera de los siguientes pasos:

   * En esas vistas de datos, inserte los campos del nuevo tipo de datos Detalles de creación de informes de contenidos.

   * Cree un campo derivado que utilice el nuevo tipo de datos &quot;Detalles de creación de informes de contenidos&quot; si está establecido, o que vuelva al antiguo tipo de datos &quot;Detalles de creación de informes de contenidos&quot; si no está establecido.

### Migrar campos derivados

Para migrar campos derivados al nuevo tipo de datos:

1. Busque todos los campos derivados utilizando el tipo de datos obsoleto &quot;Medios&quot;. Son todos campos derivados que contienen campos para los que la ruta de acceso comienza por `media.mediaTimed`.

1. Reemplace todos los campos antiguos del campo derivado por el nuevo campo correspondiente de &quot;Detalles de creación de informes de medios&quot;.

Consulte el parámetro [Content ID](/help/reporting/dimensions/content.md) y el resto de las variables de medios de streaming documentadas en [Servicios de medios de streaming](/help/media-overview.md) para asignar entre los campos antiguos y los campos nuevos. La ruta de campo antigua se encuentra en la propiedad &quot;Ruta de campo XDM&quot;, mientras que la nueva ruta de campo se encuentra en la propiedad &quot;Ruta de campo XDM de creación de informes&quot;.

![Rutas de campo XDM antiguas y nuevas](assets/field-paths-updated.jpeg)

## Ejemplo

Para facilitar el seguimiento de las directrices de migración, tenga en cuenta el siguiente ejemplo que contiene una vista de datos con campos del antiguo tipo de datos obsoleto &quot;Medios&quot;. En esta vista de datos, debe agregar los nuevos campos correspondientes.

### Actualización de la vista de datos

Puede utilizar cualquiera de las siguientes opciones para actualizar la vista de datos:

#### Opción 1

1. Busque una métrica o una dimensión que utilice el campo antiguo del tipo de datos obsoleto.

   ![Ruta de campo antigua en la vista de datos](assets/old-field-data-view.jpeg)

1. Compruebe el nuevo campo correspondiente en el artículo [Desplazamiento de capítulo](/help/reporting/dimensions/chapter-offset.md).

1. Busque el nuevo campo correspondiente en la vista de datos.

   ![Nueva ruta de campo en la vista de datos](assets/new-field-data-view.jpeg)

1. Arrastre el nuevo campo a la métrica o dimensión.

1. Repita este proceso para todas las métricas y dimensiones que utilicen campos del tipo de datos obsoleto &quot;Medios&quot;.

#### Opción 2

Esta opción crea un campo derivado que selecciona el valor del campo antiguo o el valor del nuevo campo en función del cual existe uno para un evento específico. Este campo derivado reemplaza el tipo de datos &quot;Medios&quot; antiguo en cualquier proyecto en el que se utilice.

Si desea crear un campo derivado para el &quot;Nombre del capítulo&quot; que utilice el nuevo tipo de datos &quot;Detalles de informes de contenidos&quot; si está establecido, o que vuelva al antiguo tipo de datos &quot;Detalles de informes de contenidos&quot; si no está establecido:

1. Arrastre una cláusula &quot;Case When&quot; a los campos derivados.

   ![Personalice el nuevo campo para crear una vista de datos](assets/create-derived-field2.jpeg)

1. Rellene la cláusula [!UICONTROL **If**] con el valor de **Ruta del campo XDM de creación de informes**, como se muestra en la página [Nombre del capítulo](/help/reporting/dimensions/chapter-name.md).

   ![Nombre de capítulo](assets/chapter-name.jpeg)

   ![Nombre de capítulo](assets/chapter-name2.jpeg)

   ![Condición de campo derivada](assets/derived-field-condition.jpeg)

   ![Nombre de capítulo de campo derivado](assets/derived-field-chapter-name.jpeg)

1. Rellene el valor de reserva con el campo antiguo del tipo de datos obsoleto &quot;Medios&quot;.

   ![Valor de reserva](assets/fallback-value.jpeg)

   ![Valor de reserva](assets/fallback-value2.jpeg)

   Esta es la definición final del campo derivado.

   ![Campo derivado completado](assets/derived-field-complete.jpeg)

1. Para actualizar los campos derivados, busque un campo derivado que utilice los campos obsoletos antiguos (ruta de acceso que comienza por `media.mediaTimed`).

   ![campo derivado](assets/old-derived-field.jpeg)

1. Pase el cursor sobre el campo derivado que quiera actualizar y luego seleccione el icono [!UICONTROL **Editar**].

1. Busque todos los campos del tipo de datos anterior (ruta de acceso que comienza por `media.mediaTimed`) y reemplácelos por el nuevo campo correspondiente.

   ![Localizar campo con tipo de datos antiguo](assets/locate-fields-with-old-datatype.jpeg)

1. Compruebe el nuevo campo correspondiente en el artículo [Nombre de contenido](/help/reporting/dimensions/content-name.md).

1. Reemplace el campo antiguo por el nuevo.

   ![Nuevo campo](assets/derived-field-new.jpeg)

1. Repita este proceso para todos los campos derivados mediante campos del antiguo tipo de datos obsoleto &quot;Medios&quot;.

   Se completó la migración de la configuración de CJA.
