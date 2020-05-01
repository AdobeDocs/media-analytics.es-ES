---
title: Medición de audio y vídeo en Adobe Analytics
description: Adobe Analytics para contenidos (también denominado Media Analytics) proporciona a los clientes una medición de contenidos sólida para el contenido, el audio y la publicidad.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: bddcbcd844145788518c60399bee9e4744e42d3a

---


# Medición de audio y vídeo en Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Acerca de Adobe Analytics para audio y vídeo

Adobe Analytics para audio y vídeo es un complemento de Adobe Analytics que proporciona potentes herramientas de medición para audio, vídeo y anuncios. Adobe Analytics forma parte de la plataforma Adobe Experience.

Adobe Analytics para audio y vídeo le permite realizar un seguimiento del viaje completo de los clientes a través del sitio. Las métricas se integran fácilmente en los informes de Adobe Analytics y otros productos de Adobe Experience Cloud. La medición de medios le permite categorizar los datos en varias dimensiones y segmentos, capturando todos los metadatos que necesita para realizar una análisis completa y detallada. A continuación, puede analizar los datos y atribuir los criterios de éxito a los medios totalmente consumidos, el tiempo promedio empleado y las publicidades completadas.

Puede medir métricas de envío vitales relacionadas con QoS, como fotogramas perdidos, tiempo empleado en almacenamiento en búfer y velocidad de bits promedio. Además, las métricas se pueden combinar con los datos de su sitio web o aplicación para visualizar la ruta y los intereses del cliente, a fin de ofrecer recomendaciones mejoradas y personalizar las experiencias de los clientes mediante Adobe Experience Cloud.

## Funciones {#features}

Las ventajas de Adobe Analytics para audio y vídeo incluyen supervisión en tiempo real, análisis detallada, perspectivas procesables y oportunidades de monetización.
* **análisis** en tiempo real: tome decisiones procesables en tiempo real utilizando métricas de rendimiento clave como duration, ex2 y ex3, en varios canales. Los eventos del contenido principal se miden en intervalos de 10 segundos para capturar toda la actividad a medida que se produce. Los eventos de seguimiento de anuncios se producen en intervalos de 1 segundo.
* **Impulse la participación**: haga participar a los usuarios mediante menos eventos de almacenamiento en búfer y mediante la comprensión de dónde y cuándo deben reproducirse las publicidades dentro del contenido para proporcionar una experiencia fluida y menos intrusiva que ofrezca visitas repetidas.
* **Imagen** holística: combina varios puntos de datos en todos los distribuidores de contenido para obtener una vista completa de toda la actividad de medios. Mida la participación y las vistas/escuchas en todos los canales posibles mediante la función Federated Analytics.
* **Mayor granularidad**: evalúe el comportamiento de visualización en el nivel más granular, incluida la hora del día del visitante individual, los visores/oyentes simultáneos por minuto y la duración promedio del contenido consumido.
* **Medición** precisa: mida en todos los dispositivos utilizados para el consumo de medios, incluidos los dispositivos OTT, smartphone, tablet, escritorio y mucho más, para monitorear los patrones y hábitos de participación del usuario.
* **Segmentación**: Aplique clasificaciones a sus reproductores, dispositivos, géneros, capítulos y programas para ver cómo cada uno de ellos tiene un impacto en sus vistas/escuchas generales y en la participación del cliente con contenido, audio, anuncios y combinados.

## Medición de Heartbeat {#heartbeat}

Adobe Analytics utiliza latidos para recopilar métricas de vídeo. Durante la reproducción de vídeo, los latidos se envían al servidor de seguimiento de Heartbeat para medir el tiempo de reproducción. Las llamadas de Heartbeat se envían cada diez segundos. Los latidos dan como resultado métricas de participación en vídeo granulares e informes de visitas en el orden previsto de vídeo más precisos. Adobe Analytics para audio y vídeo mide los latidos mediante Adobe Launch con la extensión Media Analytics, el SDK de medios y la API de Media Collection. Los componentes `AppMeasurement` y `VisitorID` se utilizan para recibir datos de vídeo.

El uso de latidos de Adobe Analytics para audio y vídeo ofrece las siguientes ventajas:

| Función | Descripción |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Eventos de contenidos | Los Eventos detallados y personalizados se envían cada 10 segundos para el contenido principal y cada 1 segundo para los anuncios |
| Métricas y dimensiones | Borrar métricas, dimensiones y puntos de referencia estandarizados entre<br>proveedoresCon una solución estandarizada en todas las plataformas, puede utilizar variables uniformes y estandarizadas en todos los medios y plataformas para permitir una comparación más eficiente entre campañas, dispositivos y proveedores. |
| Integraciones | El ID de Experience Cloud está vinculado a Adobe Experience Cloud para facilitar el<br>análisis cruzadoCon la integración automática de Adobe Experience Cloud, puede segmentar sus audiencias de medios, darles destinatario y hacer recomendaciones de medios en función de las preferencias del usuario. |
| Precio  | Seguimiento transparente por emisión de contenido (única) |
| Implementación y compatibilidad | Configuración optimizada con actualizaciones y<br>mejoras continuasCon un proceso de implementación optimizado, puede asignar rápidamente variables a través de la API del reproductor y validar implementaciones mediante la herramienta de depuración de Adobe para garantizar que todas las variables necesarias se rastrean con precisión. |
| Uso compartido de socios | Federated Analytics and Certified Metrics<br>With shared data through Federated Analytics, you can capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors. |
| Seguimiento avanzado | Seguimiento de contenido descargado, Seguimiento de recuperación de errores y<br>visores simultáneosPuede realizar un seguimiento del contenido de audio y vídeo que se descarga y reproduce en un dispositivo independientemente de su conectividad. |



## Seguridad {#security}

En Adobe, nos tomamos en serio la seguridad de sus recursos digitales. Desde nuestra rigurosa integración de la seguridad en nuestro proceso interno de desarrollo de software y herramientas hasta nuestros equipos interfuncionales de respuesta a incidentes, nos esforzamos por ser proactivos y ágiles. Además, nuestro trabajo colaborativo con socios, investigadores y otras organizaciones del sector nos ayuda a comprender las últimas amenazas y las mejores prácticas de seguridad, así como a incorporar la seguridad en los productos y servicios que oferta.


### Seguridad de la capa de transporte {#transport-layer-security}

**Aviso TLS:** Adobe cuenta con estándares de seguridad que requieren la finalización de la vida útil de protocolos de seguridad más antiguos. Para seguir cumpliendo con los estándares de protocolo de seguridad en evolución, Adobe promueve el uso de TLS 1.2 con el fin de tener la versión más actualizada y segura en uso. A partir del 20 de febrero de 2019, Adobe solo admitirá TLS 1.1 o posteriores. Con este cambio, Adobe ya no recopilará datos de usuarios finales con dispositivos o navegadores web más antiguos que implementen TLS 1.0. La migración a TLS 1.2 ofrece una seguridad mejorada. Es importante que revise los detalles específicos y que planifique los cambios para garantizar una transición sin contratiempos.

>[!NOTE]
>
>TLS es el protocolo de seguridad más implementado que se usa para navegadores web y otras aplicaciones que requieren que los datos se intercambien de forma segura en una red.
