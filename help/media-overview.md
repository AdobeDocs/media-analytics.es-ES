---
title: Información general de Adobe Analytics para medios de transmisión
description: Utilice medios de streaming de Analytics para obtener un conocimiento exhaustivo del contenido, el audio y los anuncios.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: ht
source-wordcount: '590'
ht-degree: 100%

---

# Información general de Adobe Analytics para medios de streaming

![Banner](./assets/media_analytics_banner.png)

Adobe Analytics para medios de streaming proporciona potentes herramientas de medición para audio, vídeo y anuncios. Las métricas de medios de streaming se pueden combinar con otras funcionalidades de Adobe Analytics, como Audience Analytics y análisis móvil o entre dispositivos.

Los medios de streaming se pueden comprar como complemento de Adobe Analytics<!-- update this when SKUs are available for other AEP products --> y las métricas de medios de streaming se integran fácilmente en los siguientes productos de Adobe Experience Platform:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Para implementar los medios de streaming de Adobe Analytics, póngase en contacto con su representante de ventas o el equipo de cuentas de Adobe para asegurarse de que formen parte de su catálogo de productos.

## Funciones principales

Las ventajas de Adobe Analytics para medios de streaming incluyen monitorización en tiempo real, análisis detallado, perspectivas procesables, oportunidades de monetización y más.

* **Análisis en tiempo real**: tome decisiones procesables en tiempo real utilizando métricas de rendimiento clave como los inicios de medios en varios canales.

  Con Analytics para medios de streaming, conseguirá detalles granulares y casi en tiempo real sobre la duración, las paradas y los inicios que le permiten evaluar y combinar métricas de vídeo y audio. Estas perspectivas le permiten comprender los hábitos de visualización y escucha de sus clientes y aumentar la participación con recomendaciones altamente personalizadas.

* **Mejore la participación**: involucre completamente a los usuarios mediante menos eventos de almacenamiento en búfer y mediante la comprensión de dónde y cuándo debe reproducirse la publicidad dentro del contenido para proporcionar una experiencia agradable y menos intrusiva que genere visitas más frecuentes.

* **Imagen holística**: combine diversos puntos de datos de todos los distribuidores de contenido y obtenga información de toda la actividad de medios. También puede medir la participación y las visualizaciones/escuchas en todos los posibles canales.

  Adobe Analytics para medios de streaming le permite hacer un seguimiento del recorrido completo del cliente en su sitio y en las aplicaciones de streaming para visualizar la ruta y los intereses del cliente, así como ofrecer recomendaciones mejoradas y personalizar las experiencias del cliente.  La medición de Media le permite categorizar los datos en varias dimensiones y segmentos, capturando todos los metadatos que necesita para hacer un análisis completo y detallado. A continuación, puede analizar los datos y atribuir los criterios de éxito a los medios totalmente consumidos, el tiempo promedio empleado y los anuncios completados.

* **Métricas vitales**: mida las métricas de envío esenciales relacionadas con la calidad de la experiencia (QoE), como los fotogramas perdidos, el tiempo de almacenamiento en búfer y la velocidad de bits media.

* **Mayor granularidad**: evalúe el comportamiento de visualización en el nivel más granular, incluida la hora del día de cada visitante individual, los espectadores/oyentes simultáneos por minuto y la duración promedio de consumo del contenido.

* **Medición exacta**: medición en varios dispositivos utilizados para el consumo de medios, incluidos OTT, smartphones, tabletas, equipos de escritorio y mucho más, para monitorizar los patrones y hábitos de participación del usuario.

* **Segmentación**: aplique clasificaciones a sus reproductores, dispositivos, géneros, capítulos y programas para ver cómo cada uno de ellos tiene un impacto en sus vistas/escuchas generales y en la participación de los clientes con el contenido, el audio, los anuncios y la combinación.


## Funcionamiento

Los datos de seguimiento de medios de streaming se recopilan mediante los medios para SDK/extensión de Edge Network, la extensión de medios con etiquetas, Media SDK, la API de Media Edge o la API de colección de medios.

Todos los datos granulares (hasta 10 segundos) se envían al servicio de Media Analytics o a Experience Edge (en función del [método de implementación](/help/implementation/overview.md) que elija), que recopilan y procesan los datos de cada sesión de reproducción individual.

Una vez finalizada la sesión de reproducción, los datos de seguimiento calculados se envían a Adobe Analytics o a Customer Journey Analytics para su almacenamiento y para la creación de informes.

>[!NOTE]
>
>Con las implementaciones de Customer Journey Analytics, los datos se pueden enviar a Customer Journey Analytics mediante Experience Edge o mediante el conector de datos de Analytics (ADC).


Para obtener información detallada sobre los distintos métodos de implementación, consulte [Implementación de medios de streaming para Adobe Analytics o Customer Journey Analytics](/help/implementation/overview.md).
