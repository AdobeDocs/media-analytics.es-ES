---
title: Conozca los requisitos previos de los servicios de medios de streaming de Adobe
description: Introducción a los servicios de medios de streaming. Aprenda lo que necesita para la implementación de.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 10%

---

# Requisitos previos {#prerequisites}

Antes de empezar a implementar los servicios de medios de streaming de Adobe, complete las siguientes tareas:

1. **Confirmar el modelo de precios**<br>
El modelo de precios actual para el complemento de recopilación de medios de streaming de Customer Journey Analytics y el complemento de medios de streaming de Adobe Analytics se basa en las transmisiones de vídeo. Si es necesario, póngase en contacto con su representante de ventas o con el equipo de cuenta de Adobe, ya que el complemento se vende por separado para Adobe Analytics y Adobe Experience Platform.

1. **Habilitar informes de Adobe Analytics** *(implementaciones solo de Analytics)*<br>
Para habilitar los informes en Analytics y ver los datos de contenido y publicidad que está recopilando, debe habilitar los informes. Consulte [Configurar informes para implementaciones solo de Analytics](/help/reporting/setup/analytics-reporting.md).

1. **Configurar identidad**<br>

   Los requisitos de configuración de identidad difieren según el método de implementación:

   * **Implementaciones de Edge**: La identidad se administra mediante la configuración del área de nombres de identidad de Adobe Experience Platform. No se requiere una configuración del servicio de identidad independiente. Consulte [Descripción general de la implementación de Edge](/help/implementation/edge/overview.md) para obtener detalles.

   * **Implementaciones solo de Analytics**: El servicio de identidad de Adobe Experience Platform debe estar habilitado para identificar visitantes de manera consistente en todas las soluciones de CX Enterprise. El servicio de identidad asigna un ID único y persistente a cada visitante del sitio y permite que dicho ID se comparta en todas las soluciones de CX Enterprise a las que se suscriba.

     Para obtener más información, consulte la [documentación del servicio de identidad de Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es).

1. **Ver requisitos previos adicionales para el método de implementación**

   Según cómo planee implementar los servicios de medios de streaming, consulte los requisitos previos para cualquiera de los siguientes métodos de implementación:

   * [Resumen de implementación solo de Analytics](/help/implementation/analytics-only/overview.md)

   * [Información general sobre la implementación Edge](/help/implementation/edge/overview.md)

   Utilice la [Información general sobre implementación](/help/implementation/overview.md) para determinar qué método de implementación es el adecuado para usted.
