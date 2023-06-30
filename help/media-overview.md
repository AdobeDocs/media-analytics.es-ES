---
title: Información general de Adobe Analytics para medios de transmisión
description: Utilice medios de streaming de Analytics para obtener un conocimiento exhaustivo del contenido, el audio y los anuncios.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c546a8cf4cf471d47e1ae43661821f3c3a6b4a44
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 68%

---

# Información general de Adobe Analytics para medios de transmisión

![Banner](./assets/media_analytics_banner.png)

Adobe Analytics para medios de streaming es un complemento de Adobe Analytics y Customer Journey Analytics que proporciona potentes herramientas de medición para audio, vídeo y anuncios. Con Analytics para medios de streaming, puede obtener detalles granulares y casi en tiempo real sobre la duración, las paradas y los inicios que le permiten evaluar y combinar métricas de vídeo y audio. Estas perspectivas le permiten comprender los hábitos de visualización y escucha de sus clientes y aumentar la participación con recomendaciones altamente personalizadas.

Adobe Analytics para medios de transmisión le permite hacer un seguimiento del recorrido del cliente completo en su sitio y en las aplicaciones de streaming. Las métricas de medios de streaming se pueden combinar con otras funcionalidades de Adobe Analytics, como Audience Analytics y análisis móvil o entre dispositivos. Las métricas se integran con facilidad en los informes de Adobe Analytics y en otros productos de Adobe Experience Platform. La medición de Media le permite categorizar los datos en varias dimensiones y segmentos, capturando todos los metadatos que necesita para hacer un análisis completo y detallado. A continuación, puede analizar los datos y atribuir los criterios de éxito a los medios totalmente consumidos, el tiempo promedio empleado y los anuncios completados.

Puede medir las métricas de envío esenciales relacionadas con la calidad de la experiencia (QoE), como los fotogramas perdidos, el tiempo de almacenamiento en búfer y la velocidad de bits media. Además, las métricas se pueden combinar con los datos de su sitio web o aplicación para visualizar la ruta y los intereses del cliente, a fin de ofrecer recomendaciones mejoradas y personalizar las experiencias de los clientes mediante Adobe Experience Platform.

## Funcionamiento

Los datos de seguimiento de medios de streaming se recopilan de un reproductor mediante Media para Edge Network SDK/Extension, Media Extension con etiquetas, Media SDK, Media Edge API o la API de Media Collection.

Todos los datos granulares (hasta 10 segundos) se envían al servicio de Media Analytics o a Experience Edge (en función de la variable [método de implementación](/help/implementation/overview.md) elija), que recopilan y procesan los datos de cada sesión de reproducción individual.

Una vez finalizada la sesión de reproducción, los datos de seguimiento calculados se envían a Adobe Analytics o a Customer Journey Analytics para su almacenamiento y para la creación de informes.

>[!NOTE]
>
>Con las implementaciones de Customer Journey Analytics, los datos se pueden enviar al Customer Journey Analytics mediante Experience Edge o mediante el conector de datos de Analytics (ADC).


Consulte [Implementación de medios de streaming para Adobe Analytics o Customer Journey Analytics](/help/implementation/overview.md) para obtener más información.

## Funciones

Las ventajas de Adobe Analytics para Streaming Media incluyen monitorización en tiempo real, análisis detallado, perspectivas procesables y oportunidades de monetización.

* **Análisis en tiempo real**: tome decisiones procesables en tiempo real utilizando métricas de rendimiento clave como los inicios de medios en varios canales.

* **Mejore la participación**: involucre completamente a los usuarios mediante menos eventos de almacenamiento en búfer y mediante la comprensión de dónde y cuándo debe reproducirse la publicidad dentro del contenido para proporcionar una experiencia agradable y menos intrusiva que genere visitas más frecuentes.

* **Imagen integral**: combine diversos puntos de datos de todos los distribuidores de contenido y obtenga información de toda la actividad de medios. También puede medir la participación y las visualizaciones/escuchas en todos los posibles canales a través de la funcionalidad Federated Analytics.

* **Mayor granularidad**: evalúe el comportamiento de visualización en el nivel más granular, incluida la hora del día de cada visitante individual, los espectadores/oyentes simultáneos por minuto y la duración promedio de consumo del contenido.

* **Medición exacta**: medición en varios dispositivos utilizados para el consumo de medios, incluidos OTT, smartphones, tabletas, equipos de escritorio y mucho más, para monitorizar los patrones y hábitos de participación del usuario.

* **Segmentación**: aplique clasificaciones a sus reproductores, dispositivos, géneros, capítulos y programas para ver cómo cada uno de ellos tiene un impacto en sus vistas/escuchas generales y en la participación de los clientes con el contenido, el audio, los anuncios y la combinación.
