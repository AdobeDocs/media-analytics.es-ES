---
title: Medición de audio y vídeo en Adobe Analytics
description: 'Adobe Analytics para contenidos (también denominado Media Analytics) proporciona a los clientes una medición de contenidos sólida para el contenido, el audio y la publicidad. '
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: 689b7d4ce632d3ddba6704bb8040eec52bfc326f

---


# Medición de audio y vídeo en Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>La documentación proporcionada aquí es específica para clientes que cuentan con la versión 1.5 o superior de *Media SDK* o la nueva *API de recopilación de contenidos* de Adobe para la medición de latidos. No incluye instrucciones sobre la implementación de Milestone de vídeo. Recomendamos a nuestros clientes que empiecen a usar las dos últimas herramientas de seguimiento de contenidos de Adobe, o al menos una, para que puedan sacar así el máximo partido a las mejoras y las mediciones avanzadas. Puede ver las [ventajas de empezar a usar las nuevas herramientas](media-overview.md#heartbeat-versus-milestone-benefits) a continuación. Aunque el método de seguimiento de vídeos mediante la medición de hitos (método Milestone) seguirá siendo compatible, no habrá más actualizaciones, correcciones ni mejoras de funciones. Si tiene más preguntas, póngase en contacto con el administrador de su cuenta de Adobe.

## Información general {#overview}

Adobe Analytics para contenidos (también denominado Media Analytics) es un complemento del producto base Analytics que ofrece a los clientes sólidas capacidades de medición de contenidos para el contenido, el audio y los anuncios. Media Analytics cuenta con numerosas ventajas, ya que ofrece a los clientes seguimiento en tiempo real, análisis detallados, información práctica y oportunidades de monetización.

El seguimiento de contenidos se habilita mediante cualquiera de las siguientes opciones:

* **Media SDK:** se integra con los reproductores de contenidos más habituales.
* **API de Media Collection**: (API RESTful) se integra con reproductores para los que no existe compatibilidad con el SDK (o con reproductores con los que no se desea integrar el SDK).

Adobe Analytics para contenidos permite a los clientes realizar un seguimiento de los movimientos de los usuarios en su web, incluido el consumo de contenidos. Estas medidas se integran fácilmente en los informes de Analytics y en otros productos de Experience Cloud. La medición de contenidos permite cortar y fragmentar los datos en diversas dimensiones y segmentos, capturar todos los metadatos necesarios para realizar un análisis detallado completo y atribuir criterios de éxito a contenidos consumidos por completo, el tiempo contenido invertido y los anuncios finalizados.

Las soluciones de contenidos no solo miden las métricas de entrega esenciales relacionadas con la calidad del servicio, como los fotogramas perdidos, el tiempo de almacenamiento en búfer y la velocidad de bits media. Se pueden combinar con los datos de su sitio web o aplicación para visualizar el flujo del cliente y sus intereses, con el fin de poder mejorar las recomendaciones y personalizar la experiencia en Adobe Experience Cloud.

## Beneficios {#benefits}

Algunas de las muchas ventajas que ofrecen las soluciones de medición de contenidos de Adobe son:

* **Análisis puntuales**: tome decisiones fundamentadas y en tiempo real gracias a los resultados de las métricas de rendimiento clave (por ejemplo, la duración) en varios canales. Los eventos de contenido principal se miden en **intervalos de 10 segundos** para monitorizar toda actividad a medida que pasa. Los eventos de seguimiento de anuncios ocurren en intervalos de **1 segundo**.
* **Experiencia del usuario mejorada**: estas soluciones consiguen que los usuarios estén totalmente inmersos gracias a un menor número de eventos de almacenamiento en búfer y a que permiten al cliente comprender dónde y cuándo deben aparecer los anuncios dentro del contenido para que la experiencia sea lo más cómoda y menos intrusiva posible, lo que fomenta que vuelvan a visitarlo y se registren visitas repetidas.
* **Imagen holística:** Combine diversos puntos de datos de todos los distribuidores de contenido y obtenga información de toda la actividad de contenidos. También puede medir la participación y las visualizaciones/escuchas en todos los posibles canales a través de la función [Federated Analytics](/help/federated-analytics.md).
* **Aumento del nivel de granularidad**: evalúe los patrones de visualización al nivel más granular, incluido el tiempo individual de visitante por día, espectadores/oyentes simultáneos por minuto y la duración media del contenido consumido.
* **Medición exacta:** medición en varios dispositivos utilizados para el consumo de contenidos, incluidos OTT, smartphones, tabletas, equipos de escritorio y mucho más, para controlar los patrones de participación del usuario.
* **Segmentación**: estas soluciones clasifican los reproductores, dispositivos, géneros y capítulos, y muestran la forma en que cada uno repercute en las vistas/escuchas generales y la participación de los usuarios con el contenido, el audio, la publicidad y las combinaciones.

## Ventajas de Heartbeat frente a Milestone {#heartbeat-versus-milestone-benefits}

Adobe Analytics para contenidos puede medir de dos formas: mediante el antiguo método Milestone (solo vídeo) o mediante el método Heartbeats actual (audio y vídeo, presentes en Media SDK y la API de recopilación de contenidos). El método de medición de latidos, Heartbeats, es preferible y recomendamos a nuestros clientes que empiecen a usar esta versión (si todavía no lo hacen) para que puedan aprovechar las ventajas que se describen a continuación.

El método Milestone se basa en llamadas individuales al servidor de Analytics para inicios de vídeo, cuartiles, duración y finalizaciones. El método Heartbeats constituye una solución de seguimiento de contenidos más rigurosa que mide el contenido principal en intervalos de 10 segundos para ofrecer métricas estandarizadas y mejoradas. Además, Adobe ha aprendido del método Milestone y ahora ofrece un proceso de implementación más sencillo y rápido mediante el Media SDK o la API de Media Collection que Heartbeats utiliza.

Algunas de las numerosas ventajas del método Heartbeats son:

* **Proceso de implementación agilizado**: asigne variables de forma más sencilla a través de la API del reproductor y valide las implementaciones a través de la herramienta Adobe Debug para asegurar que todas las variables necesarias se rastrean correctamente.
* **Integración automática con Adobe Experience Cloud**: aproveche la integración automática con Adobe Experience Cloud mediante el Experience Cloud ID, segmente la audiencia de los contenidos, oriente el contenido para dichas audiencias y cree recomendaciones de contenidos basadas en las preferencias de los usuarios.
* **Datos compartidos a través de Federated Analytics:** rentabilice las opciones de compartir contenidos más novedosas y realice una evaluación integral de los datos de todos sus socios de distribución de contenidos: operadores, programadores y distribuidores.
* **Una solución estandarizada para todas las plataformas:** habilite variables coherentes y estandarizadas para todos los contenidos y plataformas que permitan una comparación de dispositivos y proveedores más eficaz y para todas las campañas.
* **Seguimiento del contenido descargado:** Realice un seguimiento del contenido multimedia (vídeo y audio) descargado y reproducido en un dispositivo, independientemente de la conectividad.

### Tabla comparativa

|  | Video Analytics: Milestone | Media Analytics: Heartbeats |
|---|---|---|
| **Eventos de contenidos** | Eventos estándar de alto nivel | Eventos detallados y personalizados cada 10 segundos para el contenido principal y cada segundo en el caso de los anuncios |
| **Métricas y dimensiones** | Diferencias entre proveedores, métricas y dimensiones sin estandarizar | Borrar, métricas estandarizadas, dimensiones y referencias entre proveedores |
| **Integraciones con productos de Adobe** | Sesiones individuales con algunas asignaciones e integraciones | Experience Cloud ID unidos y vinculados a Adobe Experience Cloud por completo para hacer más sencillo el análisis cruzado. |
| **Precio** | Rastreado y facturado con cada llamada al servidor | Seguimiento transparente por emisión de contenido (única) |
| **Implementación y compatibilidad** | Integraciones más largas con compatibilidad limitada en versiones anteriores y sin actualizaciones | Configuración ágil con actualizaciones y mejoras continuas |
| **Colaboraciones** | N/A | Federated Analytics y Certified Metrics |
| **Seguimiento avanzado** | N/A | Seguimiento de recuperación de errores y espectadores simultáneos |

## Dispositivos compatibles {#devices-supported}

Adobe Analytics para contenidos ha evolucionado a la par que el sector y ofrece potentes herramientas que garantizan que se recopilan los datos de cada emisión de contenido y se elabora un informe para los dispositivos más habituales. Nuestro Media SDK se ha desarrollado para los dispositivos más utilizados, entre los que se incluyen:

* Smartphones y tablets iOS y Android
* Dispositivos OTT para ROKU, Apple TV, FireTV y Android TV
* Explorador JavaScript para ordenadores de mesa y portátiles

El SDK se actualiza normalmente cuando salen al mercado nuevas versiones de estos dispositivos, y se puede utilizar integrándolo con la mayoría de los grandes reproductores de contenidos actuales, incluidos Brightcove y Ooyala.

En el caso de dispositivos o plataformas que actualmente no sean compatibles con SDK (e incluso si lo son), puede implementar la API de Media Collection, a través de la cual se pueden realizar llamadas de API RESTful directamente desde el dispositivo/plataforma al servidor de Media Analytics.

En la tabla que aparece a continuación puede comprobar los dispositivos compatibles actualmente con nuestra implementación de Media SDK y de la API de Media Collection. Para descargar la versión más actualizada del SDK, consulte [Descarga de SDK.](sdk-implement/download-sdks.md) Si busca un dispositivo que no aparece en la lista, póngase en contacto con el Servicio de atención al cliente o su asesor para obtener más información.

|      | Media SDK | API de Media Collection |
|---|:---:|:---:|
| **Navegador JavaScript** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Dispositivos iOS** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Dispositivos Android** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Plataforma Universal de Windows (UWP)** |  | ![](assets/icon-blue-check.png) |
| **BlackBerry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (nuevas/anteriores)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (aplicación nativa)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **FireTV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **PS3/PS4 de Sony** |  | ![](assets/icon-blue-check.png) |
| **(Otros/nuevos dispositivos conectados)** |  | ![](assets/icon-blue-check.png) |

Para Media SDK, consulte [Compatibilidad con versiones de plataforma mínima](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Seguridad de la capa de transporte {#transport-layer-security}

**Aviso TLS:** Adobe cuenta con estándares de seguridad que requieren la finalización de la vida útil de protocolos de seguridad más antiguos. Para seguir cumpliendo con los estándares de protocolo de seguridad en evolución, Adobe promueve el uso de TLS 1.2 con el fin de tener la versión más actualizada y segura en uso. A partir del 20 de febrero de 2019, Adobe solo admitirá TLS 1.1 o posteriores. Con este cambio, Adobe ya no recopilará datos de usuarios finales con dispositivos o navegadores web más antiguos que implementen TLS 1.0. La migración a TLS 1.2 ofrece una seguridad mejorada. Es importante que revise los detalles específicos y que planifique los cambios para garantizar una transición sin contratiempos.

>[!NOTE]
>
>TLS es el protocolo de seguridad más implementado que se usa para navegadores web y otras aplicaciones que requieren que los datos se intercambien de forma segura en una red.

