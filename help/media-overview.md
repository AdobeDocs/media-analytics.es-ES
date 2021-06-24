---
title: 'Medios de transmisión de Adobe en Adobe Analytics '
description: '"Profundizar en la medición de medios de transmisión más avanzada para contenido, audio y anuncios. Obtenga información sobre Adobe Analytics para medios de transmisión".'
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 95%

---

# Medición de Streaming Media en Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Acerca de Adobe Analytics para Streaming Media

Adobe Analytics para Streaming Media es un complemento de Adobe Analytics que ofrece potentes herramientas de medición de audio, vídeo y anuncios. Adobe Analytics forma parte de Adobe Experience Platform.

Adobe Analytics para Streaming Media le permite hacer un seguimiento del recorrido completo del cliente a través del sitio. Las métricas se integran fácilmente en los informes de Adobe Analytics y en otros productos de Adobe Experience Cloud. La medición de Media le permite categorizar los datos en varias dimensiones y segmentos, capturando todos los metadatos que necesita para hacer un análisis completo y detallado. A continuación, puede analizar los datos y atribuir los criterios de éxito a los medios totalmente consumidos, el tiempo promedio empleado y los anuncios completados.

Puede medir las métricas de entrega esenciales relacionadas con la calidad del servicio, como los fotogramas perdidos, el tiempo de almacenamiento en búfer y la velocidad de bits media. Además, las métricas se pueden combinar con los datos de su sitio web o aplicación para visualizar la ruta y los intereses del cliente, a fin de ofrecer recomendaciones mejoradas y personalizar las experiencias de los clientes mediante Adobe Experience Cloud.

## Funciones {#features}

Las ventajas de Adobe Analytics para Streaming Media incluyen monitorización en tiempo real, análisis detallado, perspectivas procesables y oportunidades de monetización.
* **Análisis en tiempo real**: Tome decisiones procesables en tiempo real usando métricas clave de rendimiento como inicios de contenido en varios canales.
* **Mejore la participación**: involucre completamente a los usuarios mediante menos eventos de almacenamiento en búfer y mediante la comprensión de dónde y cuándo debe reproducirse la publicidad dentro del contenido para proporcionar una experiencia agradable y menos intrusiva que genere visitas más frecuentes.
* **Imagen holística**: combine diversos puntos de datos de todos los distribuidores de contenido y obtenga información de toda la actividad de contenidos. También puede medir la participación y las visualizaciones/escuchas en todos los posibles canales a través de la función Federated Analytics.
* **Mayor granularidad**: evalúe el comportamiento de visualización en el nivel más granular, incluida la hora del día de cada visitante individual, los espectadores/oyentes simultáneos por minuto y la duración promedio de consumo del contenido.
* **Medición exacta**: medición en varios dispositivos utilizados para el consumo de contenidos, incluidos OTT, smartphones, tabletas, equipos de escritorio y mucho más, para controlar los patrones de participación del usuario.
* **Segmentación**: aplique clasificaciones a sus reproductores, dispositivos, géneros, capítulos y programas para ver cómo cada uno de ellos tiene un impacto en sus vistas/escuchas generales y en la participación de los clientes con el contenido, el audio, los anuncios y la combinación.

## Medición de Heartbeat {#heartbeat}

Adobe Analytics utiliza «latidos» para recopilar métricas de vídeo. Durante la reproducción de vídeo, los latidos se envían al servidor de seguimiento de Heartbeat para medir el tiempo de reproducción. Las llamadas de Heartbeat se envían cada diez segundos. Los latidos generan métricas de participación en vídeo granulares e informes de visitas en el orden previsto de vídeo más precisos. Adobe Analytics para Streaming Media mide los latidos mediante Adobe Launch con la extensión Media Analytics, Media SDK y la API de Media Collection. Los componentes `AppMeasurement` y `VisitorID` se utilizan para recibir datos de vídeo.

El uso de latidos de Adobe Analytics para Streaming Media ofrece las siguientes ventajas:

| Función | Descripción |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Eventos de contenidos | Los eventos detallados y personalizados se envían cada 10 segundos para el contenido principal y cada 1 segundo para los anuncios |
| Métricas y dimensiones | Borrar métricas, dimensiones y puntos de referencia estandarizados entre proveedores<br>Con una solución estandarizada en todas las plataformas, puede usar variables uniformes y estandarizadas en todos los medios y las plataformas para permitir una comparación más eficiente entre campañas, dispositivos y proveedores. |
| Integraciones | El Experience Cloud ID está vinculado a Adobe Experience Cloud para facilitar el análisis cruzado<br>Con la integración automática de Adobe Experience Cloud, puede segmentar sus audiencias de medios, dirigirlas y hacer recomendaciones de medios en función de las preferencias del usuario. |
| Precio | Seguimiento transparente por emisión de contenido (única) |
| Implementación y compatibilidad | Configuración optimizada con actualizaciones y mejoras continuas<br>Con un proceso de implementación optimizado, puede asignar rápidamente variables a través de la API del reproductor y validar implementaciones mediante la herramienta de depuración de Adobe para garantizar que todas las variables necesarias se rastrean con precisión. |
| Uso compartido de socios | Federated Analytics y métricas certificadas<br>Con los datos compartidos a través de Federated Analytics, rentabilice las opciones de compartir contenidos más novedosas y realice una evaluación integral de los datos de todos sus socios de distribución de contenidos: operadores, programadores y distribuidores. |
| Seguimiento avanzado | Seguimiento de contenido descargado, seguimiento de recuperación de errores y visualizadores simultáneos<br>Puede hacer un seguimiento del contenido de Streaming Media que se descarga y reproduce en un dispositivo, independientemente de su conectividad. |



## Seguridad {#security}

En Adobe, nos tomamos muy en serio la seguridad de sus recursos digitales. Desde nuestra rigurosa integración de la seguridad en un proceso interno de desarrollo de software y herramientas hasta nuestros equipos interfuncionales de respuesta a incidentes, nos esforzamos por ser proactivos y ágiles. Además, nuestro trabajo colaborativo con socios, investigadores y otras organizaciones del sector nos ayuda a comprender las últimas amenazas y las prácticas recomendadas de seguridad, así como a incorporar la seguridad en los productos y servicios que ofrecemos.


### Seguridad de la capa de transporte {#transport-layer-security}

**Aviso TLS:** Adobe cuenta con estándares de seguridad que requieren la finalización de la vida útil de protocolos de seguridad más antiguos. Para seguir cumpliendo con los estándares de protocolo de seguridad en evolución, Adobe promueve el uso de TLS 1.2 con el fin de tener la versión más actualizada y segura en uso. A partir del 20 de febrero de 2019, Adobe solo admitirá TLS 1.1 o posteriores. Con este cambio, Adobe ya no recopilará datos de usuarios finales con dispositivos o navegadores web más antiguos que implementen TLS 1.0. La migración a TLS 1.2 ofrece una seguridad mejorada. Es importante que revise los detalles específicos y que planifique los cambios para garantizar una transición sin contratiempos.

>[!NOTE]
>
>TLS es el protocolo de seguridad más implementado que se usa para navegadores web y otras aplicaciones que requieren que los datos se intercambien de forma segura en una red.
