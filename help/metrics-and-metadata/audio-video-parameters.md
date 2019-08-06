---
seo-title: Parámetros de audio y vídeo
title: Parámetros de audio y vídeo
uuid: fdacfb 8 b-db 3 e -46 fb-b 9 ad-c 3 a 749555 b 2 a
translation-type: tm+mt
source-git-commit: a9e1c8ba7c8a95120e4c66460ff6d742c0855652

---


# Parámetros de audio y vídeo{#audio-and-video-parameters}

>[!IMPORTANT]
>
>El 7 de febrero de 2019, Adobe Analytics para Video y Audio lanzó un cambio de nombre de métrica. <i>Inicio de medio</i> pasará a llamarse <i>Comienzo de medio</i>. Este cambio se realizó para reflejar los estándares del sector en métricas e informes, y para que la métrica se identifique fácilmente en los informes.

>[!NOTE]
>
>A partir del 13 de septiembre de 2018, se realizaron cambios en las etiquetas de algunas dimensiones, métricas e informes, para permitir el seguimiento de contenido cruzado de análisis de audio y vídeo. Algunas de las etiquetas que han cambiado son: *inicios de vídeo* a *inicios de medio*, *duración del vídeo* a *duración del contenido* y *nombre del vídeo* a *nombre del contenido*. Los informes de vídeo de Reports and Analytics se han actualizado para incluir el nombre “medio” en lugar de “vídeo”. Los cambios de etiqueta no modifican la recopilación de datos ni los datos históricos. Tome nota de estos cambios en caso de que las utilice en el Report Builder o en cualquier otro medio externo de extracción automatizada de datos al que pueda afectar el cambio.

En este tema se presenta una lista de datos de contenido de audio y vídeo, incluidos los valores de datos de contexto que Adobe recopila mediante las variables de solución.

Descripción de los datos de la tabla:

* **Implementación**: información sobre los valores y requisitos de implementación.
   * *Clave*: variable que se establece manualmente en la aplicación o automáticamente mediante el Adobe Media SDK.
   * *Requerido*: indica si el parámetro es necesario para el seguimiento básico de audio y vídeo.
   * *Tipo*: especifica el tipo de variable que se va a definir, una cadena o un número.
   * *Enviado con* : Indica cuándo se envían los datos: *Start Start* es la llamada de análisis enviada al inicio de medios, Inicio *de anuncio* es la llamada de análisis enviada al inicio de la publicidad, etc. Las *llamadas Cerrar* son las llamadas de análisis compiladas enviadas directamente desde el servidor de Heartbeat al servidor de Analytics al final de la sesión de medios, o al final de la publicidad, capítulo, etc. Las llamadas Cerrar no están disponibles en llamadas de paquetes de red.
   * *Versión del SDK mínima*: indica la versión del SDK necesaria para acceder al parámetro.
   * *Valor de muestra*: proporciona un ejemplo de uso de una variable común.
* **Parámetros de red**: muestra los valores que se transfieren a los servidores de Adobe Analytics o Heartbeat. En esta columna se muestran los nombres de los parámetros que aparecen en las llamadas de red generadas por los Adobe Media SDK.
* **Informes**: información sobre cómo ver y analizar los datos de audio y vídeo.
   * *Disponible*: indica si los datos están disponibles en los informes de manera predeterminada (*Sí*) o se requiere una configuración personalizada (*Personalizado*)
   * *Variable reservada*: indica si los datos se capturan como un evento, eVar, prop o clasificación en una variable reservada.
   * *Caducidad*: indica si los datos caducan después de cada hit o cada visita.
   * *Nombre del informe*: nombre del informe de Adobe Analytics para la variable
   * *Datos de contexto*: nombre de los datos de contexto de Adobe Analytics que se transfieren al servidor de informes y se utilizan en las reglas de procesamiento.
   * *Fuente de datos*: nombre de columna para la variable que se encuentra en fuentes de datos Clickstream o Live Stream
   * *Audience Manager*: nombre de característica que se encuentra en Adobe Audience Manager

>[!IMPORTANT]
>
>No cambie los nombres de clasificación de las variables enumeradas a continuación que se describen en Informes/Variable reservada como "clasificación".\
>Las clasificaciones de medios se definen cuando un grupo de informes está habilitado para el seguimiento de medios. Cada cierto tiempo, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las nuevas propiedades de medios. Durante el proceso de actualización, Adobe determina si las clasificaciones están habilitadas marcando los nombres de las variables. Si falta alguno, Adobe agrega los que faltan.

## Datos básicos de audio y vídeo {#section_y55_y1m_n1b}

### Tipo de emisión {#stream-type}

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.streamType </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK Versión del SDK:** 2.2 <br/><br/>Disponible en [Información general de la API de recopilación de medios](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Valor de muestra:** <br/>"video" </li> <li> **Descripción:**<br/> Identifica el tipo de flujo. Los valores válidos son "audio", "video" y "all".  <br/><br/>[Segmentos de informes](/help/metrics-and-metadata/segments.md): <br/><br/>Tipo de flujo de medios: Todos - <br/>Segmentar todos los datos del flujo de medios; Regla: El contenido (ID) existe <br/><br/>Tipo de flujo de medios: Audio - <br/>Segmentar todos los datos de flujo de audio; Regla: El contenido (ID) existe y el tipo de flujo de medios = Tipo de flujo <br/><br/>de audio de audio: " Vídeo ": <br/>segmentar todos los datos de flujo de vídeo; Regla: El contenido (ID) existe y el tipo de flujo de medios.= audio <br/><br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. streamtype) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. streamtype) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Contenido </li> <li> **Datos de contexto:**<br/> (a. media. streamtype) </li> <li> **Fuente de datos:** <br/>videostreamtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.id </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"4586695ABC" </li> <li>**Descripción:**<br/> ID de contenido del contenido, que puede utilizarse para volver a vincularse con otros ID de industria/CMS, igual al último valor de `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. name) </li> <li> **Latidos:**<br/> (s: recurso: video_ id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Contenido </li> <li> **Datos de contexto:**<br/> (a. media. name) </li> <li> **Fuente de datos:**<br/>video </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Duración del contenido (variable)

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.length </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> VOD: 128; Activo: 86400; Lineal: 1800. </li><li> **Descripción:**<br/> Longitud de clip/Tiempo de ejecución: es la longitud máxima (o duración) del contenido que se va a consumir (en segundos). It equals the last value of `l:asset:length` from events of type Main. <br/>Si `l:asset:length` no se establece, se utilizará el último valor de `l:asset:duration` . <br/>En los informes, la duración del vídeo es la clasificación, y la duración del contenido (variable) es la eVar.  <br/> **Importante:** Esta propiedad se utiliza para calcular varias métricas, tales como las de seguimiento de progreso o la audiencia media por minuto. Estas métricas no estarán disponibles si no se configuran o no son superiores a cero.  En los medios activos con una duración desconocida, el valor predeterminado es 86 400. <br/>Pre Version 1.5.1, esto fue `l:asset:duration`; después de 1.5.1, es `l:asset:length.`<br/> **Fecha de la versión: 13/9/18** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. length) </li> <li> **Latidos:**<br/> (l: recurso: length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Duración del contenido (variable) </li> <li> **Datos de contexto:**<br/> (a. media. length) </li> <li> **Fuente de datos:**<br/>videolength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Duración del vídeo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.length </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> VOD: 128; Activo: 86400; Lineal: 1800. </li> <li> **Descripción:**<br/> Longitud de clip/Tiempo de ejecución: es la longitud máxima (o duración) del contenido que se va a consumir (en segundos). It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. En los informes, la duración del vídeo es la clasificación, y la duración del contenido (variable) es la eVar.  <br/> **Importante:** Esta propiedad se utiliza para calcular varias métricas, tales como las de seguimiento de progreso o la audiencia media por minuto. Estas métricas no estarán disponibles si no se configuran o no son superiores a cero.  En los medios activos con una duración desconocida, el valor predeterminado es 86 400. Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. length) </li> <li> **Latidos:**<br/> (l: recurso: length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Duración del vídeo </li> <li> **Datos de contexto:**<br/> (a. media. length) </li> <li> **Fuente de datos:** <br/>videoclassificationlength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Tipo de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.contentType </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>cadena restringida </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"vod" </li> <li> **Descripción:**<br/> Valores disponibles por **tipo de flujo**: <br/> _Audio:_ " song "," podcast "," audiobook "," radio " <br/> _Vídeo:_ " Vod "," Live "," Linear "," UGC "," dvod " <br/> , los clientes pueden proporcionar valores personalizados para este parámetro. Esto es igual `s:stream:type.` a Si no está configurado, es igual a `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. contenttype) </li> <li> **Latidos:**<br/> (s: stream: type) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Tipo de contenido </li> <li> **Datos de contexto:**<br/> (a. contenttype) </li> <li> **Fuente de datos:**<br/>videocontenttype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID de sesión de medio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>obtenida del servidor </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.8 </li> <li> **Valor de muestra:**<br/>1482236761294786918253 </li> <li> **Descripción:**<br/> Identifica una instancia de flujo de contenido único para una reproducción individual.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. vsid) </li> <li> **Heartbeat:**<br/> (s: event: sid) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a. media. vsid) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.vsid) </li> </ul> |

### Nombre del reproductor de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.playerName </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> " Brightcove " </li> <li> **Descripción:**<br/> Nombre del reproductor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>playerName) </li> <li> **Latidos:**<br/> (s: sp: player_ name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Nombre del reproductor de contenido </li> <li> **Datos de contexto:**<br/> (a. media. playername) </li> <li> **Fuente de datos:**<br/>videoplayername </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.playerName) </li> </ul> |

### Canal de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.channel </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"Sports" </li> <li> **Descripción:**<br/> Estación de distribución/Canales o donde se reproduce el contenido. Aquí se acepta cualquier valor de cadena.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. channel) </li> <li> **Latidos:**<br/> (s: sp: channel) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Canal de contenido </li> <li> **Datos de contexto:**<br/> (a. media. channel) </li> <li> **Fuente de datos:**<br/>videochannel </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.channel) </li> </ul> |

### Segmento de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> "0-10" </li> <li> **Descripción:**<br/> Intervalo que describe la parte del contenido que se ha visto (en minutos). El segmento se calcula como un mínimo y un máximo de los valores del cabezal de reproducción durante una sesión de reproducción.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Segmento de contenido </li> <li> **Datos de contexto:**<br/> (a. media. segment) </li> <li> **Fuente de datos:**<br/>videosegment </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.segment) </li> </ul> |

### Nombre del contenido (variable)

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.name </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.1 </li> <li> **Valor de muestra:**<br/>"The Big Bang Theory" </li> <li> **Descripción:**<br/>Es el nombre descriptivo (legible en lenguaje natural) del contenido, igual al último valor de `s:asset:name.`<br/>En los informes, el nombre del video es la clasificación y el nombre del contenido (variable) es la evar. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Friendlyname) </li> <li> **Latidos:**<br/> (s: recurso: name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Nombre del contenido (variable) </li> <li> **Datos de contexto:**<br/> (a. media. friendlyname) </li> <li> **Fuente de datos:**<br/>videoname </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Nombre del vídeo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.name </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.1 </li> <li> **Valor de muestra:**<br/>"The Big Bang Theory" </li> <li> **Descripción:**<br/> Es el nombre descriptivo (legible en lenguaje natural) del contenido, igual al último valor de `s:asset:name.`<br/>En los informes, el nombre del video es la clasificación y el nombre del contenido (variable) es la evar. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Friendlyname) </li> <li> **Latidos:**<br/> (s: recurso: name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Nombre del vídeo </li> <li> **Datos de contexto:**<br/> (a. media. friendlyname) </li> <li> **Fuente de datos:** <br/>videoclassificationname </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Ruta de vídeo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"4586695ABC" </li> <li> **Descripción:**<br/> Proporciona la capacidad de rastrear la ruta de un visor en un sitio o aplicación, para ver la ruta que tomaron para ver un vídeo concreto. Cualquier combinación de números enteros y/o letras.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. name) </li> <li> **Latidos:**<br/> (s: recurso: video_ id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>prop </li> <li> **Nombre del informe:**<br/>ruta de vídeo </li> <li> **Datos de contexto:**<br/> (a. media. name) </li> <li> **Fuente de datos:**<br/>videopath </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

### Versión de SDK

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.sdkVersion </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"2.62.0_release" </li> <li> **Descripción:**<br/> La versión del SDK que utiliza el reproductor. Esto podría contener cualquier valor personalizado que sea adecuado para el reproductor. <br/><br/>Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Sdkversion) </li> <li> **Latidos:**<br/> (s: sp: sdk) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a. media. sdkversion) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### Versión de VHL

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"js-2.0.1.88-c8c0b1" </li> <li> **Descripción:**<br/> La versión del SDK de medios utilizada para la sesión de seguimiento. <br/><br/>Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  <br/><br/>[Mediaheartbeat. version ();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Vhlversion) </li> <li> **Latidos:**<br/> (s: sp: hb_ version) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a. media. vhlversion) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Metadatos estándar de audio y vídeo {#section_pfc_hbm_n1b}

### Show

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SHOW </li> <li> **Clave de API:**<br/>media.show </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> " Familia moderna "" Lista negra "" Nueva niña " </li> <li> **Descripción:**<br/> Nombre del programa o Nombre <br/>del programa Solo es obligatorio si el programa forma parte de una serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. show) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. show) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Programa </li> <li> **Datos de contexto:**<br/> (a. media. show) </li> <li> **Fuente de datos:**<br/>videoshow </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.show) </li> </ul> |

### Formato de la emisión

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>STREAM_FORMAT </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Live" </li> <li> **Descripción:**<br/> Formato del flujo (Activo, VOD, Lineal).  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. format) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. format) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a. media. format) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.format) </li> </ul> |

### Temporada

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SEASON </li> <li> **Clave de API:**<br/>media.season </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "2" </li> <li> **Descripción:**<br/> Número de temporada al que pertenece la presentación. La serie de temporada solo es obligatoria si el programa forma parte de una serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. season) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. season) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Temporada </li> <li> **Datos de contexto:**<br/> (a. media. season) </li> <li> **Fuente de datos:**<br/>videoseason </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.season) </li> </ul> |

### Episodio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>EPISODE </li> <li> **Clave de API:**<br/>media.episode </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "13" </li> <li> **Descripción:**<br/> Número del episodio.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. episode) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. episode) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Episodio </li> <li> **Datos de contexto:**<br/> (a. media. episode) </li> <li> **Fuente de datos:**<br/>videoepisode </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.episode) </li> </ul> |

### Recurso

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>ASSET_ID </li> <li> **Clave de API:**<br/>media.assetId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "89745363" </li> <li> **Descripción:**<br/> Identificador exclusivo del contenido del recurso multimedia, como el identificador de episodio de serie de TV, el identificador de recurso de película o el identificador de evento en directo. Estos ID se derivan de autoridades de metadatos como EIDR, TMS/Gracenote o Rovi. Estos identificadores también pueden ser de otros sistemas privados o internos.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. asset) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. asset) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> ID del recurso </li> <li> **Datos de contexto:**<br/> (a. media. asset) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.asset) </li> </ul> |

### Género

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>GENRE </li> <li> **Clave de API:**<br/>media.genre </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> " Drama "," Comedia " </li> <li> **Descripción:**<br/> Escriba o agrupe el contenido según lo definido por el productor de contenido. Los valores deben estar delimitados por comas en la implementación de variables. En los informes, la lista eVar divide cada valor en un elemento de línea y cada uno de ellos recibe un grosor de métricas igual.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. genre) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. genre) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>Lista eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Género </li> <li> **Datos de contexto:**<br/> (a. media. genre) </li> <li> **Fuente de datos:**<br/>videogenre </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.genre) </li> </ul> |

### Fecha de la primera emisión

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>FIRST_AIR_DATE </li> <li> **Clave de API:**<br/>media.firstAirDate </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "2016-01-25" </li> <li> **Descripción:**<br/> Fecha en la que el contenido se retransmitió por primera vez por televisión. Cualquier formato de fecha es aceptable, pero Adobe recomienda: AAAA-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. airdate) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. airdate) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Fecha de la primera publicación </li> <li> **Datos de contexto:**<br/> (a. media. airdate) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.airDate) </li> </ul> |

### Fecha de primera emisión digital

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>FIRST_DIGITAL_DATE </li> <li> **Clave de API:**<br/>media.firstDigitalDate </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "2016-01-25" </li> <li> **Descripción:**<br/> Fecha en la que el contenido se difundió por primera vez en cualquier canal digital o plataforma. Cualquier formato de fecha es aceptable, pero Adobe recomienda: AAAA-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. digitaldate) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. digitaldate) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> Fecha del primer uso digital </li> <li> **Datos de contexto:**<br/> (a. media. digitaldate) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Clasificación del contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>RATING </li> <li> **Clave de API:**<br/>media.rating </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>TVY, TVG, TVPG, TVMA </li> <li> **Descripción:**<br/> Clasificación definida por las Pautas paternas de televisión.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. rating) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. rating) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> Clasificación del contenido </li> <li> **Datos de contexto:**<br/> (a. media. rating) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.rating) </li> </ul> |

### Creador

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>ORIGINATOR </li> <li> **Clave de API:**<br/>media.originator </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Warner Brothers", "Sony", "Disney" </li> <li> **Descripción:**<br/> Creador del contenido.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. originator) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. originator) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> Creador </li> <li> **Datos de contexto:**<br/> (a. media. originator) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.originator) </li> </ul> |

### Red

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave del SDK:**<br/>NETWORK </li> <li> **Clave de API:**<br/>media.network </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Fox", "Bravo", "ESPN" </li> <li> **Descripción:**<br/> El nombre de red o canal.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. network) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. network) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Red </li> <li> **Datos de contexto:**<br/> (a. media. network) </li> <li> **Fuente de datos:**<br/>videonetwork </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.network) </li> </ul> |

### Tipo de programa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SHOW_TYPE </li> <li> **Clave de API:**<br/>media.showType </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> " 0 " = episode completo; " 1 " = Vista previa/pie; " 2 " = Clip; " 3 " = Otro. </li> <li> **Descripción:**<br/> Tipo de contenido, expresado como un número entero entre 0 y 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. type) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. type) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Tipo de programa </li> <li> **Datos de contexto:**<br/> (a. media. type) </li> <li> **Fuente de datos:**<br/>videoshowtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>MVPD </li> <li> **Clave de API:**<br/>media.pass.mvpd </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Comcast", "DirecTV", "Dish" </li> <li> **Descripción:**<br/> MVPD que se proporciona mediante autenticación de Adobe.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. pass. mvpd) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. pass.<br/>mvpd) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>MVPD </li> <li> **Datos de contexto:**<br/> (a. media. pass. mvpd) </li> <li> **Fuente de datos:**<br/>videomvpd </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Con autorización

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>AUTHORIZED </li> <li> **Clave de API:**<br/>media.pass.auth </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> " TRUE " </li> <li> **Descripción:**<br/> El usuario ha sido autorizado por autenticación de Adobe. <br/>**Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. pass. auth) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. pass.<br/>auth) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Autorizado </li> <li> **Datos de contexto:**<br/> (a. media. pass. auth) </li> <li> **Fuente de datos:**<br/>videoauthorized </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Parte del día

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>DAY_PART </li> <li> **Clave de API:**<br/>media.dayPart </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li> <li> **Descripción:**<br/> Una propiedad que define la hora del día en que se retransmitió o reprodujo el contenido. Podría tener cualquier valor establecido como petición del cliente.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. daypart) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. daypart) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Parte del día </li> <li> **Datos de contexto:**<br/> (a. media. daypart) </li> <li> **Fuente de datos:**<br/>videodaypart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.dayPart) </li> </ul> |

### Tipo de fuente de medios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>FEED </li> <li> **Clave de API:**<br/>media.feed </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"East-HD", "West-HD", "East-SD" </li> <li> **Descripción:**<br/> Tipo de fuente. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. feed) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. feed) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Tipo de fuente de medios </li> <li> **Datos de contexto:**<br/> (a. media. feed) </li> <li> **Fuente de datos:**<br/>videofeedtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.feed) </li> </ul> |

### Artista

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.artist </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de medios](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"The Beatles" </li> <li> **Descripción:**<br/> Nombre del artista. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. artist) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. artist) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a. media. artist) </li> <li> **Fuente de datos:** <br/>videoaudioartist </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.artist) </li> </ul> |

### Álbum

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.album </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de medios](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:**<br/>"Revolver" </li> <li> **Descripción:**<br/> Nombre del álbum. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. album) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. album) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a. media. album) </li> <li> **Fuente de datos:** <br/>videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.album) </li> </ul> |

### Etiqueta

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.label </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de medios](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:**<br/>"Revolver" </li> <li> **Descripción:**<br/> Nombre de la etiqueta del registro. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. label) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. label) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a. media. label) </li> <li> **Fuente de datos:** <br/>videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.label) </li> </ul> |

### Autor

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.author </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de medios](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"John Kennedy Toole" </li> <li> **Descripción:**<br/> Nombre del autor (de una audiobook). <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. author) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. author) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a. media. author) </li> <li> **Fuente de datos:** <br/>videoaudioauthor </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.author) </li> </ul> |

### Emisora

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.station </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de medios](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"NPR" </li> <li> **Descripción:**<br/> Nombre/ID de la estación de radio. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. station) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. station) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a. media. station) </li> <li> **Fuente de datos:**<br/>videoaudiostation </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.station) </li> </ul> |

### Editor

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.publisher </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de medios](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"Random Bauhaus" </li> <li> **Descripción:**<br/> Nombre del editor de contenido de audio. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. publisher) </li> <li> **Latidos:**<br/> (s: meta:<br/>a. media. publisher) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a. media. publisher) </li> <li> **Fuente de datos:**<br/>videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.publisher) </li> </ul> |

## Métricas de audio y vídeo {#section_3D5F9C555274428AA6030D07596177E9}

### Inicios de medios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente</li> <li> **Clave de API:**<br/>N/D</li> <li> **Tipo:**<br/> cadena</li> <li> **Enviado con:**<br/> Inicio de medios</li> <li> **Versión del SDK mínima:** cualquiera</li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Cargar evento para el medio. (Ocurre cuando el usuario hace clic en el botón _Reproducir_). Se contará incluso si hay anuncios pre-roll, almacenamiento en búfer, errores, etc.  <br/>**Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. view) </li> <li> **Latidos:**<br/> (s: event:<br/>type = start) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> Inicios de medios </li> <li> **Datos de contexto:**<br/> (a. media. view) </li> <li> **Fuente de datos:**<br/>videostart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.view) </li> </ul> |

### Inicio de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Se utiliza el primer fotograma de medios. If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Se inicia el contenido </li> <li> **Datos de contexto:**<br/> (a. media. play) </li> <li> **Fuente de datos:**<br/>videoplay </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.play) </li> </ul> |

### Contenido finalizado {#content-complete}

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Flujo que se vio hasta la finalización. Esto no necesariamente significa que el usuario haya visto o escuchado todo el flujo; pueden haber omitido la acción. Esto solo significa que el usuario llegó al final del flujo, 100%. <br/>Consulte [también Fin de sesión](quality-parameters.md#session-end)<br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Latidos:**<br/> (s: event:<br/>type = complete) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>El contenido finaliza </li> <li> **Datos de contexto:**<br/> (a. media. complete) </li> <li> **Fuente de datos:**<br/>videocomplete </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.complete) </li> </ul> |

### tiempo invertido en contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 105 </li> <li> **Descripción:**<br/> Suma la duración del evento (en segundos) para todos los eventos de tipo PLAY en el contenido principal. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Tiempo invertido en contenido </li> <li> **Datos de contexto:**<br/> (a. media. timeplayed) </li> <li> **Fuente de datos:**<br/>videotime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.timePlayed) </li> </ul> |

### tiempo invertido en medio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 120 </li> <li> **Descripción:**<br/> Suma la duración del evento (en segundos) para todos los eventos de tipo PLAY, tanto principal como publicitario. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> Tiempo invertido en medio </li> <li> **Datos de contexto:**<br/> (a. media. totaltimeplayed) </li> <li> **Fuente de datos:**<br/>videototaltime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Tiempo de reproducción única

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 94 </li> <li> **Descripción:**<br/> Valor en segundos de los segmentos únicos de contenido reproducidos durante una sesión. Se excluye el tiempo de reproducción en los casos en los que se vuelve atrás y el usuario ve el mismo segmento de contenido varias veces.  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a. media. uniquetimeplayed) </li> <li> **Fuente de datos:**<br/>videouniquetimeplayed </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. uniquetimeplayed) </li> </ul> |

### Diez marcadores de progreso

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> El cursor de reproducción pasa el 10% del contenido en función de la longitud. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 10 % </li> <li> **Datos de contexto:**<br/> (a. media. progress 10) </li> <li> **Fuente de datos:**<br/>videoprogress10 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress10) </li> </ul> |

### Marcador de progreso de 25 %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> El cursor de reproducción pasa el marcador del 25% del contenido en función de la duración del contenido. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 25 % </li> <li> **Datos de contexto:**<br/> (a. media. progress 25) </li> <li> **Fuente de datos:**<br/>videoprogress25 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress25) </li> </ul> |

### Marcador de progreso cincuenta %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Playhead pasa el marcador del 50% del contenido en función de la duración del contenido. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 50 % </li> <li> **Datos de contexto:**<br/> (a. media. progress 50) </li> <li> **Fuente de datos:**<br/>videoprogress50 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress50) </li> </ul> |

### Marcador de progreso de setenta y cinco %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> **N/D** </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> El cursor de reproducción pasa el marcador del 75% del contenido en función de la duración del contenido. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 75 % </li> <li> **Datos de contexto:**<br/> (a. media. progress 75) </li> <li> **Fuente de datos:**<br/>videoprogress75 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress75) </li> </ul> |

### Marcador de progreso Ninety-cinco %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> El cursor de reproducción pasa el marcador del 95% del contenido en función de la duración del contenido. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 95 % </li> <li> **Datos de contexto:**<br/> (a. media. progress 95) </li> <li> **Fuente de datos:**<br/>videoprogress95 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress95) </li> </ul> |

### Promedio de audiencia por minuto

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>mayor o igual que 1 </li> <li> **Descripción:**<br/> La métrica Audiencia promedio de minuto se calcula como Tiempo total empleado, para un elemento de medios específico, dividido por su duración de todas sus sesiones de reproducción: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Audiencia media por minuto </li> <li> **Datos de contexto:**<br/> (a. media. averageminuteaudience) </li> <li> **Fuente de datos:**<br/>videoaverageminuteaudience </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Emisiones previstas

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 1 - Durante una reproducción de 19 minutos; <br/>2 - Durante una reproducción de 31 minutos; <br/>3 - Durante una reproducción de 78 minutos. </li> <li> **Descripción:**<br/> Número calculado de flujos de audio o vídeo por cada contenido individual. Este valor aumenta cada 30 minutos de tiempo de reproducción (contenido + publicidad). Los clientes deben crear sus propias reglas de procesamiento para disponer el valor para los informes. <br/><br/>Un flujo se cuenta cada 30 minutos, según el `ms_s` (o totaltimeplayed = Tiempo total de video), similar a: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a. media. estimmatedstreams) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. estimmatedstreams) </li> </ul> |

### Flujos afectados por la pausa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Este valor es verdadero o falso. El valor es verdadero si se producen una o más pausas durante la reproducción de un elemento multimedia.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Latidos:**<br/> (s: event:<br/>type = pause) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Emisiones afectadas en pausa </li> <li> **Datos de contexto:**<br/> (a. media. pause) </li> <li> **Fuente de datos:**<br/>videopause </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pause) </li> </ul> |

### Pausar eventos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>2 </li> <li> **Descripción:**<br/> Esta métrica se calcula como un recuento de los periodos de pausa que se dan durante una sesión de reproducción.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Latidos:**<br/> (s: event:<br/>type = pause) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Pausar eventos </li> <li> **Datos de contexto:**<br/> (a. media. pausecount) </li> <li> **Fuente de datos:**<br/>videopausecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Duración de la pausa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>190 </li> <li> **Descripción:**<br/> Suma la duración (en segundos) de todos los eventos de tipo PAUSE. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Duración total de la pausa </li> <li> **Datos de contexto:**<br/> (a. media. pausetime) </li> <li> **Fuente de datos:**<br/>videopausetime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Reanudación de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> **media.resume** </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Se cuenta un Reanudar para cada reproducción que se reanuda después de más de 30 minutos de período de búfer, pausa o stall, O si el reproductor establece este valor en videoinfo trackplay. <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Latidos:**<br/> (s: event:<br/>type = resume) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Reanudación del contenido </li> <li> **Datos de contexto:**<br/> (a. media. resume) </li> <li> **Fuente de datos:**<br/>videoresume </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.resume) </li> </ul> |

### Vistas de segmentos de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Número de vistas del contenido principal. Se cuenta una vista de segmento de contenido cuando se ha visto al menos un fotograma.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Vistas del segmento de contenido </li> <li> **Datos de contexto:**<br/> (a. media. segmentview) </li> <li> **Fuente de datos:**<br/>videosegmentviews </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.segmentView) </li> </ul> |

## API relacionadas {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android: [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS: [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript: [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast: [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS: [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

