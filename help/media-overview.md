---
seo-title: Medición de audio y vídeo en Adobe Analytics
title: Medición de audio y vídeo en Adobe Analytics
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: 4a14e2faae6401a3f885eb5e341c1344d7f1e94d

---


# Medición de audio y vídeo en Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>The documentation provided here is specific to clients utilizing version 1.5 or higher of Adobe's *Media SDK* for heartbeat measurement, or Adobe's newer *Media Collection API* for heartbeat measurement. No incluye instrucciones sobre la implementación de vídeo de hitos heredados. Recomendamos a nuestros clientes que empiecen a usar las dos últimas herramientas de seguimiento de medios de Adobe, o al menos una, para que puedan sacar así el máximo partido a las mejoras y las mediciones avanzadas. Puede ver las [ventajas de empezar a usar las nuevas herramientas](media-overview.md#section_cnj_5st_p1b) a continuación. Aunque seguiremos admitiendo el método Milestone de seguimiento de videos, no habrá actualizaciones, correcciones ni mejoras de funciones planificadas. Si tiene más preguntas, póngase en contacto con el administrador de su cuenta de Adobe.

## Información general {#section_8BFE4F8DA64B4A5F826A4940B11AA466}

Adobe Analytics para medios (también denominado Media Analytics) es un complemento del producto base Analytics que ofrece a los clientes sólidas capacidades de medición de medios para el contenido, el audio y los anuncios. Media Analytics cuenta con numerosas ventajas, ya que ofrece a los clientes seguimiento en tiempo real, análisis detallados, información práctica y oportunidades de monetización.

El seguimiento de medios se habilita mediante cualquiera de las siguientes opciones:

* **Media SDK**: se integra con los reproductores de medios más habituales.
* **API de Media Collection**: (API RESTful) se integra con reproductores para los que no existe compatibilidad con el SDK (o con reproductores con los que no se desea integrar el SDK).

Adobe Analytics para medios permite a los clientes realizar un seguimiento de los movimientos de los usuarios en su web, incluido el consumo de medios. Estas medidas se integran fácilmente en los informes de Analytics y en otros productos de Experience Cloud. La medición de medios permite cortar y fragmentar los datos en diversas dimensiones y segmentos, capturar todos los metadatos necesarios para realizar un análisis detallado completo y atribuir criterios de éxito a medios consumidos por completo, el tiempo medio invertido y los anuncios finalizados.

Las soluciones de medios no solo miden las métricas de entrega esenciales relacionadas con la calidad del servicio, como los fotogramas perdidos, el tiempo de almacenamiento en búfer y la velocidad de bits media. Se pueden combinar con los datos de su sitio web o aplicación para visualizar el flujo del cliente y sus intereses, con el fin de poder mejorar las recomendaciones y personalizar la experiencia en Adobe Experience Cloud.

## Ventajas {#section_7712BA90EAE64C118218D1C581EF68B7}

Algunas de las muchas ventajas que ofrecen las soluciones de medición de medios de Adobe son:

* **Análisis puntuales**: tome decisiones fundamentadas y en tiempo real gracias a los resultados de las métricas de rendimiento clave (por ejemplo, la duración) en varios canales. Los eventos de contenido principal se miden en **intervalos de 10 segundos** para monitorizar toda actividad a medida que pasa. Los eventos de seguimiento de anuncios ocurren en intervalos de **1 segundo**.
* **Experiencia del usuario mejorada**: estas soluciones consiguen que los usuarios estén totalmente inmersos gracias a un menor número de eventos de almacenamiento en búfer y a que permiten al cliente comprender dónde y cuándo deben aparecer los anuncios dentro del contenido para que la experiencia sea lo más cómoda y menos intrusiva posible, lo que fomenta que vuelvan a visitarlo y se registren visitas repetidas.
* **Holistic picture - Combine multiple data points across all of your content distributors to get a full view of all your media activity, and measure engagement and views/listens across all possible channels through the Federated Analytics feature.**[](data-sharing/federated-analytics.md)
* **Aumento del nivel de granularidad**: evalúe los patrones de visualización al nivel más granular, incluido el tiempo individual de visitante por día, espectadores/oyentes simultáneos por minuto y la duración media del contenido consumido.
* **Medición exacta**: medición en varios dispositivos utilizados para el consumo de medios, incluidos OTT, smartphones, tabletas, equipos de escritorio y mucho más, para controlar los patrones de participación del usuario.
* **Segmentación**: estas soluciones clasifican los reproductores, dispositivos, géneros y capítulos, y muestran la forma en que cada uno repercute en las vistas/escuchas generales y la participación de los usuarios con el contenido, el audio, la publicidad y las combinaciones.

## Ventajas de Heartbeat frente a Milestone {#section_cnj_5st_p1b}

Adobe Analytics para medios se puede medir mediante dos métodos: el método Milestone heredado (solo vídeo) y el método Heartbeat actual (audio y vídeo, que se incluyen tanto en el SDK de medios como en la API de Media Collection). El método de medición de latidos, Heartbeats, es preferible y recomendamos a nuestros clientes que empiecen a usar esta versión (si todavía no lo hacen) para que puedan aprovechar las ventajas que se describen a continuación.

El método Milestone se basa en llamadas individuales al servidor de Analytics para inicios de vídeo, cuartiles, duración y finalizaciones. El método Heartbeats constituye una solución de seguimiento de medios más rigurosa que mide el contenido principal en intervalos de 10 segundos para ofrecer métricas estandarizadas y mejoradas. Además, Adobe ha aprendido del método Milestone y ahora ofrece un proceso de implementación más sencillo y rápido mediante el Media SDK o la API de Media Collection que Heartbeats utiliza.

Algunas de las numerosas ventajas del método Heartbeats son:

* **Proceso de implementación agilizado**: asigne variables de forma más sencilla a través de la API del reproductor y valide las implementaciones a través de la herramienta Adobe Debug para asegurar que todas las variables necesarias se rastrean correctamente.
* **Integración automática con Adobe Experience Cloud**: aproveche la integración automática con Adobe Experience Cloud mediante el Experience Cloud ID, segmente la audiencia de los medios, oriente el contenido para dichas audiencias y cree recomendaciones de medios basadas en las preferencias de los usuarios.
* **Datos compartidos a través de Federated Analytics**: rentabilice las opciones de compartir medios más novedosas y realice una evaluación integral de los datos de todos sus socios de distribución de medios: operadores, programadores y distribuidores.
* **Colaboraciones con socios certificados de clasificación**: Adobe colabora con Nielsen (clasificaciones de audiencia) para ofrecer un censo de medición neutral de terceros que permita elaborar clasificaciones certificadas y de confianza.
* **Una solución estandarizada para todas las plataformas**: habilite variables coherentes y estandarizadas para todos los medios y plataformas que permitan una comparación de dispositivos y proveedores más eficaz y para todas las campañas.
* **Seguimiento de contenido descargado:** Rastree el contenido multimedia (vídeo y audio) que se descarga y reproduce en un dispositivo independientemente de su conectividad.

### Tabla comparativa

|  | Video Analytics: Milestone | Media Analytics: Heartbeats |
|---|---|---|
| **Eventos de medios** | Eventos estándar de alto nivel | Eventos detallados y personalizados cada 10 segundos para el contenido principal y cada segundo en el caso de los anuncios |
| **Métricas y dimensiones** | Diferencias entre proveedores, métricas y dimensiones sin estandarizar | Borrar, métricas estandarizadas, dimensiones y referencias entre proveedores |
| **Integraciones con productos de Adobe** | Sesiones individuales con algunas asignaciones e integraciones | Experience Cloud ID unidos y vinculados a Adobe Experience Cloud por completo para hacer más sencillo el análisis cruzado. |
| **Precio** | Rastreado y facturado con cada llamada al servidor | Seguimiento transparente por emisión de medio (única) |
| **Implementación y compatibilidad** | Integraciones más largas con compatibilidad limitada en versiones anteriores y sin actualizaciones | Configuración ágil con actualizaciones y mejoras continuas |
| **Colaboraciones** | N/D | Federated Analytics y Certified Metrics |
| **Seguimiento avanzado** | N/D | Seguimiento de recuperación de errores y espectadores simultáneos |

## Dispositivos compatibles {#section_lkm_l5t_p1b}

Adobe Analytics para medios ha evolucionado a la par que el sector y ofrece potentes herramientas que garantizan que se recopilan los datos de cada emisión de medio y se elabora un informe para los dispositivos más habituales. Nuestro Media SDK se ha desarrollado para los dispositivos más utilizados, entre los que se incluyen:

* Smartphones y tablets iOS y Android
* Dispositivos OTT para ROKU, Apple TV, FireTV y Android TV
* Explorador JavaScript para ordenadores de mesa y portátiles

El SDK se actualiza normalmente cuando salen al mercado nuevas versiones de estos dispositivos, y se puede utilizar integrándolo con la mayoría de los grandes reproductores de medios actuales, incluidos Brightcove y Ooyala.

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

For Media SDK, also see Minimum Platform Version Support[](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Transport Layer Security {#transport-layer-security}

**TLS Notice --** Adobe has security compliance standards that require the end-of-life of older security protocols. To continue to meet the evolving security protocol standards, Adobe is moving toward the use of TLS 1.2, in order to have the most up-to-date and secure version in use. From February 20th, 2019, Adobe will support only TLS 1.1 or later. With this change, Adobe will no longer collect data from end users with older devices or web browsers deploying TLS 1.0. Migrating to TLS 1.2 provides improved security. Es importante que revise los detalles específicos y que planifique los cambios para garantizar una transición sin contratiempos.

>[!NOTE]
>
>TLS es actualmente el protocolo de seguridad más utilizado en exploradores web y otras aplicaciones que requieren que los datos se intercambien de forma segura a través de una red.
