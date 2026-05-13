---
title: Resumen de medios de streaming de Adobe
description: Utilice las soluciones de medios de streaming de Adobe para obtener una potente insight para el contenido, el audio y los anuncios.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/EJ6osO9PkXBubSF7a7HebRJhpSTamNnghofASOs7E-E
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: df312454-73c4-43f6-a90e-18f5043f074cid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5520579-b31f-4df7-9281-f0d9f91e2edcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 606
ht-degree: 53%

---

# Información general de los servicios de medios de streaming Adobe

![Banner](./assets/media_analytics_banner.png)

Los servicios de medios de streaming de Adobe proporcionan potentes herramientas de recopilación, medición y personalización de contenido de medios de streaming, como audio, vídeo y publicidad para los proveedores de medios de streaming. Puede combinar métricas de medios de streaming con funcionalidades como Audience Analytics, Mobile o Cross-Device Analytics.

Los datos de medios de streaming se integran fácilmente en los siguientes productos de Adobe Experience Platform:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Para implementar los servicios de medios de streaming, póngase en contacto con su representante de ventas o con el equipo de cuenta de Adobe de Adobe para asegurarse de que el complemento Customer Journey Analytics Streaming Media Collection o Adobe Analytics para Streaming Media Add-on forme parte de su catálogo de productos.

## Funciones principales

Las ventajas de los servicios de medios de streaming incluyen monitorización en tiempo real, análisis detallado, perspectivas procesables, oportunidades de monetización y más.

* **Análisis en tiempo real**: tome decisiones procesables en tiempo real utilizando métricas de rendimiento clave como los inicios de medios en varios canales.

  Con los servicios de medios de streaming, obtiene detalles granulares y casi en tiempo real sobre la duración, las paradas y los inicios que le permiten evaluar y combinar métricas de vídeo y audio. Estas perspectivas le permiten comprender los hábitos de visualización y escucha de sus clientes y aumentar la participación con recomendaciones altamente personalizadas.

* **Mejore la participación**: involucre completamente a los usuarios mediante menos eventos de almacenamiento en búfer y mediante la comprensión de dónde y cuándo debe reproducirse la publicidad dentro del contenido para proporcionar una experiencia agradable y menos intrusiva que genere visitas más frecuentes.

* **Imagen integral**: combine diversos puntos de datos de todos los distribuidores de contenido y obtenga información de toda la actividad multimedia. Mida la participación y las visualizaciones/escuchas en todos los canales posibles.

  Los servicios de medios de streaming le permiten hacer un seguimiento del recorrido total del cliente en su sitio y en las aplicaciones de streaming para visualizar la ruta y los intereses del cliente, así como ofrecer recomendaciones mejoradas y personalizar las experiencias del cliente.  La medición de Media le permite categorizar los datos en varias dimensiones y segmentos, capturando todos los metadatos que necesita para hacer un análisis completo y detallado. A continuación, puede analizar los datos y atribuir los criterios de éxito a los medios totalmente consumidos, el tiempo promedio empleado y los anuncios completados.

* **Métricas vitales**: mida las métricas de envío esenciales relacionadas con la calidad de la experiencia (QoE), como los fotogramas perdidos, el tiempo de almacenamiento en búfer y la velocidad de bits media.

* **Mayor granularidad**: evalúe el comportamiento de visualización en el nivel más granular, incluida la hora del día de cada visitante individual, los espectadores/oyentes simultáneos por minuto y la duración promedio de consumo del contenido.

* **Medición exacta**: medición en varios dispositivos utilizados para el consumo de medios, incluidos OTT, smartphones, tabletas, equipos de escritorio y mucho más, para monitorizar los patrones y hábitos de participación del usuario.

* **Segmentación**: aplique clasificaciones a sus reproductores, dispositivos, géneros, capítulos y programas para ver cómo cada uno de ellos tiene un impacto en sus vistas/escuchas generales y en la participación de los clientes con el contenido, el audio, los anuncios y la combinación.


## Funcionamiento

Los datos de seguimiento de los servicios de medios de streaming se recopilan de un reproductor mediante Media for Edge Network SDK/Extension, Media Extension with Tags, Media SDK, la API de Media Edge o la API de Media Collection.

Todos los datos granulares (hasta 10 segundos) se envían al servicio de Media Analytics o a Experience Edge (en función del [método de implementación](/help/implementation/overview.md) que elija), que recopilan y procesan los datos de cada sesión de reproducción individual.

Una vez finalizada la sesión de reproducción, los datos de seguimiento calculados se envían a Adobe Analytics o a Customer Journey Analytics para su almacenamiento y para la creación de informes.

>[!NOTE]
>
>Con las implementaciones de Customer Journey Analytics, los datos se pueden enviar a Customer Journey Analytics mediante Experience Edge o mediante el conector de datos de Analytics (ADC).


Para obtener información detallada sobre los distintos métodos de implementación, consulte [Implementación de servicios de medios de transmisión para Adobe Analytics o Customer Journey Analytics](/help/implementation/overview.md).
