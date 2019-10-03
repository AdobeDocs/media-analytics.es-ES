---
seo-title: Parámetros de audio y vídeo
title: Parámetros de audio y vídeo
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: a3e400a135af532be4320c7510032d518c4b6865

---


# Parámetros de audio y vídeo{#audio-and-video-parameters}

>[!IMPORTANT]
>
>El 7 de febrero de 2019, Adobe Analytics para vídeo y audio publicó un cambio de nombre de métrica. <i>Inicio de medio</i> pasará a llamarse <i>Comienzo de medio</i>. Este cambio se realizó para reflejar los estándares del sector en las métricas y los informes, y para hacer que la métrica se pueda identificar fácilmente en los informes.

>[!NOTE]
>
>A partir del 13 de septiembre de 2018, se realizó un cambio en las etiquetas de algunas dimensiones, métricas e informes para permitir el seguimiento de contenido cruzado de los análisis de audio y vídeo. Algunas de las etiquetas que han cambiado son: *inicios de vídeo* a *inicios de medio*, *duración del vídeo* a *duración del contenido* y *nombre del vídeo* a *nombre del contenido*. Los informes de vídeo de Reports and Analytics se han actualizado para incluir el nombre “medio” en lugar de “vídeo”. Los cambios de etiqueta no modifican la recopilación de datos ni los datos históricos. Tome nota de estos cambios en caso de que las utilice en el Report Builder o en cualquier otro medio externo de extracción automatizada de datos al que pueda afectar el cambio.

En este tema se presenta una lista de datos de contenido de audio y vídeo, incluidos los valores de datos de contexto que Adobe recopila mediante las variables de solución.

Descripción de los datos de la tabla:

* **Implementación**: información sobre los valores y requisitos de implementación.
   * *Clave*: variable que se establece manualmente en la aplicación o automáticamente mediante el Adobe Media SDK.
   * *Requerido*: indica si el parámetro es necesario para el seguimiento básico de audio y vídeo.
   * *Tipo*: especifica el tipo de variable que se va a definir, una cadena o un número.
   * *Enviado con* : indica cuándo se envían los datos: Inicio *de* medios es la llamada de análisis que se envía al inicio de medios, Inicio de *publicidad* es la llamada de análisis que se envía al inicio de anuncio, etc.; las llamadas de *cierre* son las llamadas de análisis compiladas que se envían directamente desde el servidor de Heartbeat al servidor de Analytics al final de la sesión de medios o al final del anuncio, capítulo, etc. Las llamadas de cierre no están disponibles en llamadas de paquetes de red.
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
>No cambie los nombres de clasificación de ninguna de las variables enumeradas a continuación que se describan en Informes/Variable reservada como "clasificación".\
>Las clasificaciones de medios se definen cuando se habilita un grupo de informes para el seguimiento de medios. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las propiedades de los nuevos medios. Durante el proceso de actualización, Adobe determina si las clasificaciones están habilitadas mediante la comprobación de los nombres de las variables. Si falta alguno de ellos, Adobe agrega los que faltan de nuevo.

## Datos básicos de audio y vídeo {#section_y55_y1m_n1b}

### Tipo de emisión {#stream-type}

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.streamType </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK** Versión del SDK: 2.2 <br/><br/>Disponible en [Media Collection API Overview](/help/media-collection-api/mc-api-overview.md) o [Download SDKs - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Valor de muestra:** <br/>"video" </li> <li> ****<br/> Descripción: Identifica el tipo de flujo. Los valores válidos son "audio", "video" y "all".  <br/><br/>[Segmentos](/help/metrics-and-metadata/segments.md)de informes: Tipo <br/><br/>de flujo de medios: Todos: <br/>segmentar todos los datos de flujo de medios; Regla: El contenido (ID) existe como tipo de flujo <br/><br/>de medios: Audio: <br/>segmentar todos los datos del flujo de audio; Regla: El contenido (ID) existe Y el tipo de flujo de medios = tipo de flujo de <br/><br/>medios de audio: "Vídeo": <br/>segmente todos los datos del flujo de vídeo; Regla: El contenido (ID) existe Y el tipo de flujo de medios!= audio <br/><br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.streamType) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Contenido </li> <li> ****<br/> Datos de contexto: (a.media.streamType) </li> <li> **Fuente de datos:** <br/>videostreamtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.id </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"4586695ABC" </li> <li>****<br/> Descripción: ID de contenido del contenido, que se puede utilizar para enlazar con otros ID de industria/CMS, igual al último valor de `s:asset:video_id.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.name) </li> <li> ****<br/> Latidos: (s:asset:video_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Contenido </li> <li> ****<br/> Datos de contexto: (a.media.name) </li> <li> **Fuente de datos:**<br/>video </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Duración del contenido (variable)

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.length </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Sample value:**<br/> VOD: 128; Live: 86400; Linear: 1800. </li><li> **Description:**<br/> Clip Length/Runtime - This is the maximum length (or duration) of the content being consumed (in seconds). It equals the last value of `l:asset:length` from events of type Main. <br/>If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. <br/>En los informes, la duración del vídeo es la clasificación, y la duración del contenido (variable) es la eVar.  <br/> **Importante:** Esta propiedad se utiliza para calcular varias métricas, tales como las de seguimiento de progreso o la audiencia media por minuto. Estas métricas no estarán disponibles si no se configuran o no son superiores a cero.  En los medios activos con una duración desconocida, el valor predeterminado es 86 400. <br/>Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.` <br/> **Fecha de la versión: 13/9/18** </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.length) </li> <li> **Heartbeats:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Duración del contenido (variable) </li> <li> ****<br/> Context Data: (a.media.length) </li> <li> **Fuente de datos:**<br/>videolength </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Duración del vídeo

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.length </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Sample value:**<br/> VOD: 128; Live: 86400; Linear: 1800. </li> <li> ****<br/> Descripción: Duración/Tiempo de ejecución del clip: es la duración máxima (o duración) del contenido que se está consumiendo (en segundos). It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. En los informes, la duración del vídeo es la clasificación, y la duración del contenido (variable) es la eVar.  <br/> **Importante:** Esta propiedad se utiliza para calcular varias métricas, tales como las de seguimiento de progreso o la audiencia media por minuto. Estas métricas no estarán disponibles si no se configuran o no son superiores a cero.  En los medios activos con una duración desconocida, el valor predeterminado es 86 400. Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.length) </li> <li> ****<br/> Latidos: (l:asset:length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Duración del vídeo </li> <li> ****<br/> Datos de contexto: (a.media.length) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Tipo de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.contentType </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>cadena restringida </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"vod" </li> <li> ****<br/> Descripción: Valores disponibles por tipo **de flujo**: <br/> __ Audio: "canción", "podcast", "audiobook", "radio" <br/> __ Vídeo: "VoD", "Activo", "Lineal", "UGC", "DVoD" <br/> Los clientes pueden proporcionar valores personalizados para este parámetro. Esto es igual a `s:stream:type.` Si no está configurado, es igual a `missing_content_type.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.contentType) </li> <li> ****<br/> Latidos: (s:stream:type) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Tipo de contenido </li> <li> ****<br/> Datos de contexto: (a.contentType) </li> <li> **Fuente de datos:**<br/>videocontenttype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID de sesión de medios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>obtenida del servidor </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.8 </li> <li> **Valor de muestra:**<br/>1482236761294786918253 </li> <li> ****<br/> Descripción: Identifica una instancia de un flujo de contenido exclusivo para una reproducción individual.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.vsid) </li> <li> ****<br/> Heartbeat: (s:event:sid) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> ****<br/> Datos de contexto: (a.media.vsid) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### Marca de descarga de medios

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>obtenida del servidor </li> <li> **Requerido:**<br/>no </li> <li> ****<br/> Tipo:booleano </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 2.2 </li> <li> ****<br/> Sample value:true </li> <li> ****<br/> Descripción: Se establece en true cuando se genera la visita debido a la reproducción de una sesión multimedia de contenido descargado. No está presente cuando el contenido descargado no se reproduce.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.download) </li> <li> ****<br/> Heartbeat: (s:meta:a.media.download) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> ****<br/> Datos de contexto: (a.media.download) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.download) </li> </ul> |

### Nombre del reproductor de contenido

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.playerName </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: "Brightcove" </li> <li> ****<br/> Descripción: Nombre del reproductor.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>playerName) </li> <li> **Heartbeats:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Nombre del reproductor de contenido </li> <li> **Context Data:**<br/> (a.media.playerName) </li> <li> **Fuente de datos:**<br/>videoplayername </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Canal de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.channel </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"Sports" </li> <li> ****<br/> Descripción: Estación de distribución/canales o donde se reproduce el contenido. Aquí se acepta cualquier valor de cadena.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.channel) </li> <li> ****<br/> Heartbeats: (s:sp:channel) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Canal de contenido </li> <li> ****<br/> Datos de contexto: (a.media.channel) </li> <li> **Fuente de datos:**<br/>videochannel </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Segmento de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> "0-10" </li> <li> ****<br/> Descripción: Intervalo que describe la parte del contenido que se ha visto (en minutos). El segmento se calcula como un mínimo y un máximo de los valores del cabezal de reproducción durante una sesión de reproducción.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Segmento de contenido </li> <li> ****<br/> Datos de contexto: (a.media.segment) </li> <li> **Fuente de datos:**<br/>videosegment </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.segment) </li> </ul> |

### Nombre del contenido (variable)

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.name </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.1 </li> <li> **Valor de muestra:**<br/>"The Big Bang Theory" </li> <li> **Description:This is the "friendly" (human-readable) name of the content, equal to the last value of In reporting, Video Name is the classification, and Content Name (variable) is the eVAR.**<br/>`s:asset:name.`<br/><br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> Latidos: (s:asset:name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Nombre del contenido (variable) </li> <li> ****<br/> Datos de contexto: (a.media.friendlyName) </li> <li> **Fuente de datos:**<br/>videoname </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Nombre del vídeo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.name </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.1 </li> <li> **Valor de muestra:**<br/>"The Big Bang Theory" </li> <li> ****<br/> Descripción: Es el nombre "práctico" (legible en lenguaje natural) del contenido, igual al último valor de `s:asset:name.` <br/>En los informes, Nombre del vídeo es la clasificación y Nombre del contenido (variable) es la eVAR.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> Latidos: (s:asset:name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Nombre del vídeo </li> <li> ****<br/> Datos de contexto: (a.media.friendlyName) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Ruta de vídeo

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"4586695ABC" </li> <li> ****<br/> Descripción: Proporciona la capacidad de realizar un seguimiento de la ruta de un visor a través de un sitio o aplicación, para ver la ruta que tomó para ver un vídeo en particular. Cualquier combinación de números enteros y/o letras.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.name) </li> <li> **Heartbeats:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>prop </li> <li> **Nombre del informe:**<br/>ruta de vídeo </li> <li> ****<br/> Context Data: (a.media.name) </li> <li> **Fuente de datos:**<br/>videopath </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.name) </li> </ul> |

### Versión de SDK

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.sdkVersion </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"2.62.0_release" </li> <li> **Description:**<br/> The SDK version used by the player. Esto podría contener cualquier valor personalizado que sea adecuado para el reproductor. <br/><br/>Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>sdkVersion) </li> <li> ****<br/> Latidos: (s:sp:sdk) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/> </li> <li> ****<br/> Datos de contexto: (a.media.sdkVersion) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### Versión de VHL

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"js-2.0.1.88-c8c0b1" </li> <li> ****<br/> Descripción: Versión del SDK de medios utilizada para la sesión de seguimiento. <br/><br/>Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>vhlVersion) </li> <li> ****<br/> Latidos: (s:sp:hb_version) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> ****<br/> Datos de contexto: (a.media.vhlVersion) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Metadatos estándar de audio y vídeo {#section_pfc_hbm_n1b}

### Show

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SHOW </li> <li> **Clave de API:**<br/>media.show </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> ****<br/> Sample value: "Modern Family" "Blacklist" "New Girl" </li> <li> ****<br/> Descripción: Nombre del programa/serie Nombre del <br/>programa sólo es necesario si el programa forma parte de una serie.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.show) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Programa </li> <li> ****<br/> Datos de contexto: (a.media.show) </li> <li> **Fuente de datos:**<br/>videoshow </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.show) </li> </ul> |

### Formato de la emisión

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>STREAM_FORMAT </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Live" </li> <li> ****<br/> Descripción: Formato del flujo (Activo, VOD, Lineal).  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.format) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> ****<br/> Context Data: (a.media.format) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.format) </li> </ul> |

### Temporada

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SEASON </li> <li> **Clave de API:**<br/>media.season </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "2" </li> <li> **Description:**<br/> The season number the show belongs to.  Season Series is required only if the show is part of a series.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.season) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Temporada </li> <li> **Context Data:**<br/> (a.media.season) </li> <li> **Fuente de datos:**<br/>videoseason </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.season) </li> </ul> |

### Episodio

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>EPISODE </li> <li> **Clave de API:**<br/>media.episode </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "13" </li> <li> ****<br/> Descripción: Número del episodio.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.episode) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Episodio </li> <li> ****<br/> Datos de contexto: (a.media.episode) </li> <li> **Fuente de datos:**<br/>videoepisode </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.episode) </li> </ul> |

### Recurso

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>ASSET_ID </li> <li> **Clave de API:**<br/>media.assetId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "89745363" </li> <li> ****<br/> Descripción: Es el identificador único del contenido del recurso de medios, como el identificador de episodio de la serie de TV, el identificador de recurso de película o el identificador de evento en directo. Estos ID se derivan de autoridades de metadatos como EIDR, TMS/Gracenote o Rovi. Estos identificadores también pueden ser de otros sistemas privados o internos.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.asset) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> ID del recurso </li> <li> ****<br/> Datos de contexto: (a.media.asset) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Género

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>GENRE </li> <li> **Clave de API:**<br/>media.genre </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> ****<br/> Valor de muestra: "Drama", "Comedia" </li> <li> ****<br/> Descripción: Tipo o agrupación de contenido según la definición del productor de contenido. Los valores deben estar delimitados por comas en la implementación de variables. En los informes, la lista eVar divide cada valor en un elemento de línea y cada uno de ellos recibe un grosor de métricas igual.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.genre) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>Lista eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Género </li> <li> ****<br/> Datos de contexto: (a.media.genre) </li> <li> **Fuente de datos:**<br/>videogenre </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Fecha de la primera emisión

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>FIRST_AIR_DATE </li> <li> **Clave de API:**<br/>media.firstAirDate </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Start </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "2016-01-25" </li> <li> ****<br/> Descripción: Fecha en la que el contenido se emitió por primera vez en televisión. Cualquier formato de fecha es aceptable, pero Adobe recomienda: AAAA-MM-DD </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.airDate) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Fecha de la primera publicación </li> <li> ****<br/> Datos de contexto: (a.media.airDate) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Fecha de primera emisión digital

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>FIRST_DIGITAL_DATE </li> <li> **Clave de API:**<br/>media.firstDigitalDate </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "2016-01-25" </li> <li> **Description:**<br/> The date when the content first aired on any digital channel or platform. Cualquier formato de fecha es aceptable, pero Adobe recomienda: AAAA-MM-DD </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.digitalDate) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.digitalDate)<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> Fecha del primer uso digital </li> <li> ****<br/> Context Data: (a.media.digitalDate) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Clasificación del contenido

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>RATING </li> <li> **Clave de API:**<br/>media.rating </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>TVY, TVG, TVPG, TVMA </li> <li> **Description:**<br/> Rating as defined by TV Parental Guidelines.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.rating) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> Clasificación del contenido </li> <li> ****<br/> Datos de contexto: (a.media.rating) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Creador

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>ORIGINATOR </li> <li> **Clave de API:**<br/>media.originator </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Warner Brothers", "Sony", "Disney" </li> <li> ****<br/> Descripción: Creador del contenido.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.originator) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> Creador </li> <li> ****<br/> Datos de contexto: (a.media.originator) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Red

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave del SDK:**<br/>NETWORK </li> <li> **Clave de API:**<br/>media.network </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Fox", "Bravo", "ESPN" </li> <li> ****<br/> Descripción: Nombre de red/canal.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.network) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Red </li> <li> ****<br/> Datos de contexto: (a.media.network) </li> <li> **Fuente de datos:**<br/>videonetwork </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.network) </li> </ul> |

### Tipo de programa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SHOW_TYPE </li> <li> **Clave de API:**<br/>media.showType </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> ****<br/> Valor de muestra: "0" = episodio completo; "1" = Vista previa/remolque; "2" = Clip; "3" = Otro. </li> <li> ****<br/> Descripción: Tipo de contenido, expresado como un entero entre 0 y 3.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.type) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Tipo de programa </li> <li> ****<br/> Datos de contexto: (a.media.type) </li> <li> **Fuente de datos:**<br/>videoshowtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>MVPD </li> <li> **Clave de API:**<br/>media.pass.mvpd </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Comcast", "DirecTV", "Dish" </li> <li> ****<br/> Descripción: MVPD proporcionado mediante la autenticación de Adobe.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.pass.mvpd) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.pass.<br/><br/>mvpd) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>MVPD </li> <li> ****<br/> Context Data: (a.media.pass.mvpd) </li> <li> **Fuente de datos:**<br/>videomvpd </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Con autorización

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>AUTHORIZED </li> <li> **Clave de API:**<br/>media.pass.auth </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> ****<br/> Valor de muestra: "TRUE" </li> <li> ****<br/> Description: The user has been authorized via Adobe authentication.  <br/>**Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.pass.auth) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.pass.<br/><br/>auth) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Autorizado </li> <li> ****<br/> Datos de contexto: (a.media.pass.auth) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Parte del día

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>DAY_PART </li> <li> **Clave de API:**<br/>media.dayPart </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li> <li> ****<br/> Descripción: Propiedad que define la hora del día en que se reprodujo o reprodujo el contenido. Podría tener cualquier valor establecido como petición del cliente.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.dayPart) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Parte del día </li> <li> ****<br/> Datos de contexto: (a.media.dayPart) </li> <li> **Fuente de datos:**<br/>videodaypart </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Tipo de fuente de medios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>FEED </li> <li> **Clave de API:**<br/>media.feed </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"East-HD", "West-HD", "East-SD" </li> <li> ****<br/> Descripción: Tipo de fuente.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.feed) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Tipo de fuente de medios </li> <li> ****<br/> Datos de contexto: (a.media.feed) </li> <li> **Fuente de datos:**<br/>videofeedtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Artista

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.artist </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK** Versión del SDK: 1.5.7 <br/>Disponible en [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) o [Download SDKs - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"The Beatles" </li> <li> ****<br/> Descripción: Nombre del artista.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.artista) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> ****<br/> Datos de contexto: (a.media.artista) </li> <li> **Fuente de datos:** <br/>videoaudioartist </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.artist) </li> </ul> |

### Álbum

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.album </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK** Versión del SDK: 1.5.7 <br/>Disponible en [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) o [Download SDKs - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:**<br/>"Revolver" </li> <li> ****<br/> Descripción: Nombre del álbum.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.album) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.album)<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Context Data:**<br/> (a.media.album) </li> <li> **Fuente de datos:** <br/>videoaudioalbum </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.album) </li> </ul> |

### Etiqueta

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.label </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versión del SDK** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **Valor de muestra:**<br/>"Revolver" </li> <li> ****<br/> Descripción: Nombre de la etiqueta del registro.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.label) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.label)<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> ****<br/> Datos de contexto: (a.media.label) </li> <li> **Fuente de datos:** <br/>videoaudiolabel </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.label) </li> </ul> |

### Autor

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.author </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versión del SDK** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **Valor de muestra:** <br/>"John Kennedy Toole" </li> <li> ****<br/> Descripción: Nombre del autor (de un audiolibro).  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.author) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> ****<br/> Datos de contexto: (a.media.author) </li> <li> **Fuente de datos:** <br/>videoaudioauthor </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.author) </li> </ul> |

### Emisora

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.station </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK** Versión del SDK: 1.5.7 <br/>Disponible en [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) o [Download SDKs - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"NPR" </li> <li> ****<br/> Descripción: Nombre / ID de la estación de radio.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.station) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> ****<br/> Datos de contexto: (a.media.station) </li> <li> **Fuente de datos:**<br/>videoaudiostation </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.station) </li> </ul> |

### Editor

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.publisher </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK** Versión del SDK: 1.5.7 <br/>Disponible en [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) o [Download SDKs - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"Random Bauhaus" </li> <li> ****<br/> Descripción: Nombre del editor de contenido de audio.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.publisher) </li> <li> ****<br/> Latidos: (s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> ****<br/> Context Data: (a.media.publisher) </li> <li> **Fuente de datos:**<br/>videoaudiopublisher </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.publisher) </li> </ul> |

## Métricas de audio y vídeo {#section_3D5F9C555274428AA6030D07596177E9}

### Inicios de medios

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente</li> <li> **Clave de API:**<br/>N/D</li> <li> **Tipo:**<br/> cadena</li> <li> ****<br/> Enviado con: Inicio de medios</li> <li> **Versión del SDK mínima:** cualquiera</li> <li> **Valor de muestra:**<br/>TRUE </li> <li> ****<br/> Description: Load event for the media. (Ocurre cuando el usuario hace clic en el botón _Reproducir_). Se contará incluso si hay anuncios pre-roll, almacenamiento en búfer, errores, etc.  <br/>**Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.view) </li> <li> ****<br/> Heartbeats: (s:event:type=start)<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> ****<br/> Report Name: Media Starts </li> <li> **Context Data:**<br/> (a.media.view) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.view) </li> </ul> |

### Inicio de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> ****<br/> Descripción: Se consume el primer fotograma de medios. If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Se inicia el contenido </li> <li> ****<br/> Datos de contexto: (a.media.play) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.play) </li> </ul> |

### Contenido finalizado {#content-complete}

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> ****<br/> Descripción: Flujo que se vio hasta la finalización. This does not necessarily mean the user watched or listened to the whole stream; they could have skipped ahead. Esto solo significa que el usuario llegó al final del flujo, 100%. <br/>Consulte también Fin [](quality-parameters.md#session-end) de sesión <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> ****<br/> Latidos: (s:event:<br/>type=complete) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>El contenido finaliza </li> <li> ****<br/> Datos de contexto: (a.media.complete) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.complete) </li> </ul> |

### tiempo invertido en contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 105 </li> <li> **Description:**<br/> Sums the event duration (in seconds) for all events of type PLAY on the main content.  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Tiempo invertido en contenido </li> <li> **Context Data:**<br/> (a.media.timePlayed) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### tiempo invertido en medio

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 120 </li> <li> **Description:**<br/> Sums the event duration (in seconds) for all events of type PLAY, both main and ad content.  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> Tiempo invertido en medio </li> <li> **Context Data:**<br/> (a.media.totalTimePlayed) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Tiempo de reproducción única

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 94 </li> <li> ****<br/> Descripción: Valor en segundos de los segmentos únicos de contenido reproducidos durante una sesión. Se excluye el tiempo de reproducción en los casos en los que se vuelve atrás y el usuario ve el mismo segmento de contenido varias veces.  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> ****<br/> Datos de contexto: (a.media.uniqueTimePlayed) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### Marcador de progreso del 10 %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> ****<br/> Descripción: El cursor de reproducción pasa el marcador del 10 % del contenido en función de la longitud. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 10 % </li> <li> ****<br/> Datos de contexto: (a.media.progress10) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### Marcador de progreso del 25 %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> ****<br/> Descripción: El cursor de reproducción pasa el marcador del 25 % del contenido en función de la longitud del contenido. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 25 % </li> <li> ****<br/> Datos de contexto: (a.media.progress25) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### Marcador de progreso del 50 %

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Description:**<br/> Playhead passes the 50% marker of content based on content length. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 50 % </li> <li> **Context Data:**<br/> (a.media.progress50) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### Marcador de progreso del 75 %

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> **N/D** </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> ****<br/> Descripción: El cursor de reproducción pasa el marcador del 75 % del contenido en función de la longitud del contenido. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 75 % </li> <li> ****<br/> Datos de contexto: (a.media.progress75) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### Marcador de progreso del 95 %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> ****<br/> Descripción: El cursor de reproducción pasa el marcador del 95 % del contenido en función de la longitud del contenido. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 95 % </li> <li> ****<br/> Datos de contexto: (a.media.progress95) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Promedio de audiencia por minuto

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>mayor o igual que 1 </li> <li> ****<br/> Descripción: La métrica de audiencia media por minuto se calcula como el tiempo total de contenido empleado, para un elemento de medios específico, dividido por su duración para todas las sesiones de reproducción: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Audiencia media por minuto </li> <li> ****<br/> Datos de contexto: (a.media.averageMinuteAudience) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Datos federados

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> ****<br/> Tipo:booleano </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Sample value:true  </li> <li> ****<br/> Description: Set to true when the hit is federated (i.e., received by the customer as part of a federated data share, rather than their own implementation). </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>N/D </li> <li> ****<br/> Datos de contexto: (a.media.federated) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.federated) </li> </ul> |

### Emisiones previstas

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 1 - Durante una reproducción de 19 minutos; <br/>2 - Durante una reproducción de 31 minutos; <br/>3: para una reproducción de 78 minutos. </li> <li> **Description:**<br/> The estimated number of video or audio streams per each individual content. Este valor aumenta cada 30 minutos de tiempo de reproducción (contenido + publicidad). Los clientes deben crear sus propias reglas de procesamiento para disponer el valor para los informes. <br/><br/>A stream is counted every 30 minutes, based on the `ms_s` (or totalTimePlayed = Video Total Time), similar to: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Context Data:**<br/> (a.media.estimatedStreams) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.calculatedStreams) </li> </ul> |

### Flujos afectados por la pausa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> ****<br/> Descripción: Este valor es true o false. El valor es verdadero si se producen una o más pausas durante la reproducción de un elemento multimedia.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> ****<br/> Latidos: (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Emisiones afectadas en pausa </li> <li> ****<br/> Datos de contexto: (a.media.pause) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pause) </li> </ul> |

### Pausar eventos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>2 </li> <li> ****<br/> Descripción: Esta métrica se calcula como un recuento de los períodos de pausa que se dan durante una sesión de reproducción.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> ****<br/> Latidos: (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Pausar eventos </li> <li> ****<br/> Datos de contexto: (a.media.pauseCount) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Duración de la pausa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>190 </li> <li> **Description:**<br/> Sums the duration (in seconds) of all events of type PAUSE. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Duración total de la pausa </li> <li> **Context Data:**<br/> (a.media.pauseTime) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Reanudación de contenido

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> **media.resume** </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Description:**<br/> A Resume is counted for each playback that resumes after more than 30 minutes of buffer, pause, or stall period OR if this value is set by the player on the VideoInfo trackPlay. <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=resume) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Reanudación del contenido </li> <li> **Context Data:**<br/> (a.media.resume) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.resume) </li> </ul> |

### Vistas de segmentos de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> ****<br/> Descripción: Número de vistas del contenido principal. Se cuenta una vista de segmento de contenido cuando se ha visto al menos un fotograma.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Vistas del segmento de contenido </li> <li> ****<br/> Datos de contexto: (a.media.segmentView) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.segmentView) </li> </ul> |

### Recuento de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> ****<br/> Clave de SDK: N/D </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 2 </li> <li> ****<br/> Descripción: Número de anuncios iniciados durante la sesión de medios.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> ****<br/> Datos de contexto: (a.media.adCount) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Recuento de capítulos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> ****<br/> Clave de SDK: N/D </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 2 </li> <li> ****<br/> Descripción: Número de capítulos que se iniciaron durante la sesión de medios.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> ****<br/> Datos de contexto: (a.media.chapterCount) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |

## California Consumer Privacy Act (CCPA) Parameters {#ccpa-params}

### Opt Out Server Side Forwarding

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> ****<br/> API Key: analytics.optOutServerSideForwarding </li> <li> **Requerido:**<br/>no </li> <li> ****<br/> Type: boolean </li> <li> ****<br/> Enviado con: Inicio de medios </li> <li> **Versión del SDK** Versión del SDK: N/D </li> <li> ****<br/> Sample value:true </li> <li>****<br/> Description: Set to true when the end user has opted out of their data being shared between Adobe Analytics and other Experience Cloud solutions (e.g. Audience Manager). </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (opt.dmp) </li> <li> ****<br/> Latidos: (s:meta:cm.ssf) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Contenido </li> <li> ****<br/> Datos de contexto: N/D </li> <li> **Fuente de datos:**<br/>video </li> <li> ****<br/> Audience Manager: N/D </li> </ul> |

### Compartir exclusión

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> ****<br/> Clave de API: analytics.optOutShare </li> <li> **Requerido:**<br/>no </li> <li> ****<br/> Tipo:booleano </li> <li> ****<br/> Enviado con: Inicio de medios </li> <li> **Versión del SDK** Versión del SDK: N/D </li> <li> ****<br/> Sample value:true </li> <li>****<br/> Descripción: Se establece en true cuando el usuario final ha optado por no publicar sus datos (por ejemplo, para otros clientes de Adobe Analytics). </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (opt.oos) </li> <li> ****<br/> Latidos: (s:meta:cm.oos) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Contenido </li> <li> ****<br/> Context Data: N/A </li> <li> **Fuente de datos:**<br/>video </li> <li> ****<br/> Audience Manager: N/A </li> </ul> |

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

