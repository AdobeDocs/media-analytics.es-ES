---
title: Parámetros de audio y vídeo
description: null
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Parámetros de audio y vídeo {#audio-and-video-parameters}

>[!IMPORTANT]
>
>El 7 de febrero de 2019 se cambió el nombre de una métrica de Adobe Analytics para vídeo y audio. <i>Inicio de contenido</i> pasará a llamarse <i>Comienzo de contenido</i>. El motivo del cambio fue reflejar los estándares del sector en cuanto a métricas e informes, así como facilitar la identificación de la métrica en los informes.

>[!NOTE]
>
>A partir del 13 de septiembre de 2018 tuvo lugar un cambio en las etiquetas de algunas dimensiones, métricas e informes, con el fin de permitir el seguimiento de contenido múltiple de análisis de audio y vídeo. Algunas de las etiquetas que han cambiado son: *inicios de vídeo* a *inicios de contenido*, *duración del vídeo* a *duración del contenido* y *nombre del vídeo* a *nombre del contenido*. Los informes de vídeo de Reports and Analytics se han actualizado para incluir el nombre “contenido” en lugar de “vídeo”. Los cambios de etiqueta no modifican la recopilación de datos ni los datos históricos. Tome nota de estos cambios en caso de que las utilice en el Report Builder o en cualquier otro contenido externo de extracción automatizada de datos al que pueda afectar el cambio.

En este tema se presenta una lista de datos de contenido de audio y vídeo, incluidos los valores de datos de contexto que Adobe recopila mediante las variables de solución.

Descripción de los datos de la tabla:

* **Implementación**: información sobre los valores y requisitos de implementación.
   * *Clave*: variable que se establece manualmente en la aplicación o automáticamente mediante el Adobe Media SDK.
   * *Requerido*: indica si el parámetro es necesario para el seguimiento básico de audio y vídeo.
   * *Tipo*: especifica el tipo de variable que se va a definir, una cadena o un número.
   * *Enviado con*: indica cuándo se envían los datos: *Inicio de contenidos* es la llamada de análisis enviada al inicio del contenido, *Inicio de publicidad* es la llamada de análisis enviada al iniciar el anuncio, etc., las llamadas *Cierre* son llamadas de análisis compiladas enviadas directamente desde el servidor de latidos al servidor de análisis al final de la sesión de contenido, o al final del anuncio, capítulo, etc. Las llamadas Cierre no están disponibles en las llamadas a paquetes de red.
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
>No cambie los nombres de clasificación de ninguna de las variables enumeradas a continuación que se describan en Informes/Variables reservadas como “clasificación”.\
>Las clasificaciones de contenidos se definen cuando se habilita un grupo de informes para el seguimiento de contenidos. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las propiedades de los nuevos contenidos. Durante el proceso de actualización, Adobe determina si las clasificaciones están habilitadas mediante la comprobación de los nombres de las variables. Si falta alguno de ellos, Adobe agrega los que faltan de nuevo.

## Datos básicos de audio y vídeo {#core-audio-and-video-data}

### Tipo de emisión {#stream-type}

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.streamType </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK Versión del SDK:** 2.2 <br/><br/>Disponible en [Información general de la API de recopilación de contenidos](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Valor de muestra:** <br/>"video" </li> <li> **Descripción:**<br/> Identifica el tipo de flujo. Los valores válidos son "audio", "video" y "all".  <br/><br/>[Segmentos de informes](/help/metrics-and-metadata/segments.md): <br/><br/>Tipo de flujo de contenidos: Todos: <br/>Segmentar todos los datos de flujo de contenidos; Regla: Existe contenido (ID) <br/><br/>Tipo de flujo de contenidos: Audio: <br/>Segmentar todos los datos del flujo de audio; Regla: Existe contenido (ID) Y el Tipo de flujo de contenidos = audio <br/><br/>Tipo de flujo de contenidos: “Vídeo”: <br/>Segmentar todos los datos del flujo de vídeo; Regla: Existe contenido (ID) Y Tipo de flujo de contenidos= audio <br/><br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.streamType) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Contenido </li> <li> **Datos de contexto:**<br/> (a.media.streamType) </li> <li> **Fuente de datos:** <br/>videostreamtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.streamType) </li> </ul> |

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
| <ul> <li> **Clave de SDK:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.id </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"4586695ABC" </li> <li>**Descripción:**<br/> ID del contenido (que se puede asociar a otros ID de CMS o del sector) igual al último valor de `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **Heartbeats:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Contenido </li> <li> **Datos de contexto:**<br/> (a.media.name) </li> <li> **Fuente de datos:**<br/>video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

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
| <ul> <li> **Clave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.length </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> VOD: 128; Activo: 86400; Lineal: 1800. </li><li> **Descripción:**<br/> Duración del clip/Tiempo de ejecución: Es la longitud (o duración) máxima del contenido que se está reproduciendo (en segundos). Es igual al último valor de `l:asset:length` desde eventos de tipo principal. <br/>Si no se configura `l:asset:length`, se utiliza el último valor de `l:asset:duration`. <br/>En los informes, la duración del vídeo es la clasificación, y la duración del contenido (variable) es la eVar.  <br/> **Importante:** Esta propiedad se utiliza para calcular varias métricas, tales como las de seguimiento de progreso o la audiencia media por minuto. Estas métricas no estarán disponibles si no se configuran o no son superiores a cero.  En los contenidos activos con una duración desconocida, el valor predeterminado es 86 400. <br/>En la versión previa 1.5.1 era `l:asset:duration`; después de la versión 1.5.1, es `l:asset:length.` <br/> **Fecha de la versión: 13/9/18** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Heartbeats:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Duración del contenido (variable) </li> <li> **Datos de contexto:**<br/> (a.media.length) </li> <li> **Fuente de datos:**<br/>videolength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Duración del vídeo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.length </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> VOD: 128; Activo: 86400; Lineal: 1800. </li> <li> **Descripción:**<br/> Duración del clip/Tiempo de ejecución: Es la longitud (o duración) máxima del contenido que se está reproduciendo (en segundos). Es igual al último valor de `l:asset:length` desde eventos de tipo principal. Si no se configura `l:asset:length`, se utiliza el último valor de `l:asset:duration`. En los informes, la duración del vídeo es la clasificación, y la duración del contenido (variable) es la eVar.  <br/> **Importante:** Esta propiedad se utiliza para calcular varias métricas, tales como las de seguimiento de progreso o la audiencia media por minuto. Estas métricas no estarán disponibles si no se configuran o no son superiores a cero.  En los contenidos activos con una duración desconocida, el valor predeterminado es 86 400. En la versión previa 1.5.1 era `l:asset:duration`; después de la versión 1.5.1, es `l:asset:length.`<br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Heartbeats:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Duración del vídeo </li> <li> **Datos de contexto:**<br/> (a.media.length) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **Clave de SDK:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.contentType </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>cadena restringida </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"vod" </li> <li> **Descripción:**<br/> Valores disponibles por **Tipo de flujo**: <br/> _Audio:_ “song”, “podcast”, “audiobook”, “radio”<br/> _Vídeo:_ “VoD”, “Live”, “Lineal”, “UGC”, “DVoD” <br/> Los clientes pueden proporcionar valores personalizados para este parámetro. Esto es igual a `s:stream:type.` Si no está configurado, es igual a `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.contentType) </li> <li> **Heartbeats:**<br/> (s:stream:type) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Tipo de contenido </li> <li> **Datos de contexto:**<br/> (a.contentType) </li> <li> **Fuente de datos:**<br/>videocontenttype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID de sesión de contenidos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>obtenida del servidor </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.8 </li> <li> **Valor de muestra:**<br/>1482236761294786918253 </li> <li> **Descripción:**<br/> Esto identifica una instancia de una emisión única para una reproducción individual.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.vsid) </li> <li> **Heartbeat:**<br/> (s:event:sid) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.vsid) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### Indicador de descarga de contenidos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> `config.downloadedcontent` </li> <li> **Clave de API:**<br/>obtenida del servidor </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> booleano </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK Versión del SDK:** <br/>Iniciar Android y la extensión iOS versión 1.1.0 </li> <li> **Valor de muestra:**<br/> “true” </li> <li> **Descripción:**<br/> Se establece en “true” cuando se genera la visita debido a la reproducción de una sesión multimedia de contenido descargado. No está presente cuando el contenido descargado no se reproduce.<br/><br/>[Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.downloaded) </li> <li> **Heartbeat:**<br/> (s:meta:a.media.downloaded) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.download) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.downloaded) </li> </ul> |

### Nombre del reproductor de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.playerName </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> “Brightcove” </li> <li> **Descripción:**<br/> Nombre del reproductor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>playerName) </li> <li> **Heartbeats:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Nombre del reproductor de contenido </li> <li> **Datos de contexto:**<br/> (a.media.playerName) </li> <li> **Fuente de datos:**<br/>videoplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Canal de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [canal](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.channel </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"Sports" </li> <li> **Descripción:**<br/> Estación o canales de distribución o donde se reproduce el contenido. Aquí se acepta cualquier valor de cadena.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.channel) </li> <li> **Heartbeats:**<br/> (s:sp:channel) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Canal de contenido </li> <li> **Datos de contexto:**<br/> (a.media.channel) </li> <li> **Fuente de datos:**<br/>videochannel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Segmento de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> “0-10” </li> <li> **Descripción:**<br/> El intervalo que describe la parte del contenido que se ha visualizado (en minutos). El segmento se calcula como un mínimo y un máximo de los valores del cabezal de reproducción durante una sesión de reproducción.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Segmento de contenido </li> <li> **Datos de contexto:**<br/> (a.media.segment) </li> <li> **Fuente de datos:**<br/>videosegment </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segment) </li> </ul> |

### Nombre del contenido (variable)

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Clave de API:**<br/>media.name </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.1 </li> <li> **Valor de muestra:**<br/>"The Big Bang Theory" </li> <li> **Descripción:**<br/>Es el nombre “práctico” (legible en lenguaje natural) del contenido, igual al último valor de `s:asset:name.`<br/>En los informes, Nombre del vídeo es la clasificación y Nombre del contenido (variable) es la eVAR. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **Heartbeats:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Nombre del contenido (variable) </li> <li> **Datos de contexto:**<br/> (a.media.friendlyName) </li> <li> **Fuente de datos:**<br/>videoname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

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
| <ul> <li> **Clave de SDK:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.name </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.1 </li> <li> **Valor de muestra:**<br/>"The Big Bang Theory" </li> <li> **Descripción:**<br/> Es el nombre “práctico” (legible en lenguaje natural) del contenido, igual al último valor de `s:asset:name.`<br/>En los informes, Nombre del vídeo es la clasificación y Nombre del contenido (variable) es la eVAR. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **Heartbeats:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Nombre del vídeo </li> <li> **Datos de contexto:**<br/> (a.media.friendlyName) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Ruta de vídeo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>"4586695ABC" </li> <li> **Descripción:**<br/> Proporciona la capacidad de realizar un seguimiento de la ruta de un espectador a través de un sitio o aplicación, para ver la ruta que tomó para ver un vídeo en particular. Cualquier combinación de números enteros y/o letras.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **Heartbeats:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>prop </li> <li> **Nombre del informe:**<br/>ruta de vídeo </li> <li> **Datos de contexto:**<br/> (a.media.name) </li> <li> **Fuente de datos:**<br/>videopath </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

### Versión de SDK

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **Clave de API:**<br/>media.sdkVersion </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"2.62.0_release" </li> <li> **Descripción:**<br/> La versión del SDK utilizada por el reproductor. Esto podría contener cualquier valor personalizado que sea adecuado para el reproductor. <br/><br/>Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>sdkVersion) </li> <li> **Heartbeats:**<br/> (s:sp:sdk) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a.media.sdkVersion) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### Versión de VHL

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"js-2.0.1.88-c8c0b1" </li> <li> **Descripción:**<br/> Versión de Media SDK utilizado para la sesión de seguimiento. <br/><br/>Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vhlVersion) </li> <li> **Heartbeats:**<br/> (s:sp:hb_version) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.vhlVersion) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Metadatos estándar de audio y vídeo {#standard-audio-and-video-metadata}

### Show

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SHOW </li> <li> **Clave de API:**<br/>media.show </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> “Modern Family” “Blacklist” “New Girl” </li> <li> **Descripción:**<br/> Nombre del episodio/serie <br/>El nombre del episodio solo es necesario si forma parte de una serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.show) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Programa </li> <li> **Datos de contexto:**<br/> (a.media.show) </li> <li> **Fuente de datos:**<br/>videoshow </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.show) </li> </ul> |

### Formato de la emisión

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>STREAM_FORMAT </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Live" </li> <li> **Descripción:**<br/> Formato de la emisión (en directo, VOD, Lineal).  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.format) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.format) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.format) </li> </ul> |

### Temporada

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SEASON </li> <li> **Clave de API:**<br/>media.season </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "2" </li> <li> **Descripción:**<br/> Número de temporada al que pertenece el episodio.  La temporada solo es necesaria si el programa es un episodio de una serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.season) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Temporada </li> <li> **Datos de contexto:**<br/> (a.media.season) </li> <li> **Fuente de datos:**<br/>videoseason </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.season) </li> </ul> |

### Episodio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>EPISODE </li> <li> **Clave de API:**<br/>media.episode </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "13" </li> <li> **Descripción:**<br/> Número de episodio.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.episode) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Episodio </li> <li> **Datos de contexto:**<br/> (a.media.episode) </li> <li> **Fuente de datos:**<br/>videoepisode </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.episode) </li> </ul> |

### ID del recurso

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>ASSET_ID </li> <li> **Clave de API:**<br/>media.assetId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "89745363" </li> <li> **Descripción:**<br/> Es el identificador exclusivo del contenido del recurso de contenidos, como el identificador de episodio de series de TV, el identificador de recursos de película o el identificador de eventos en directo. Estos ID se derivan de autoridades de metadatos como EIDR, TMS/Gracenote o Rovi. Estos identificadores también pueden ser de otros sistemas privados o internos.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.asset) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> ID del recurso </li> <li> **Datos de contexto:**<br/> (a.media.asset) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Género

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>GENRE </li> <li> **Clave de API:**<br/>media.genre </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> “Drama”, “Comedia” </li> <li> **Descripción:**<br/> Clase o agrupación del contenido según el productor de contenido. Los valores deben estar delimitados por comas en la implementación de variables. En los informes, la lista eVar divide cada valor en un elemento de línea y cada uno de ellos recibe un grosor de métricas igual.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.genre) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>Lista eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Género </li> <li> **Datos de contexto:**<br/> (a.media.genre) </li> <li> **Fuente de datos:**<br/>videogenre </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Fecha de la primera emisión

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>FIRST_AIR_DATE </li> <li> **Clave de API:**<br/>media.firstAirDate </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "2016-01-25" </li> <li> **Descripción:**<br/> La fecha en la que se emitió por primera vez el contenido en televisión. Cualquier formato de fecha es aceptable, pero Adobe recomienda: AAAA-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.airDate) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Fecha de la primera publicación </li> <li> **Datos de contexto:**<br/> (a.media.airDate) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Fecha de primera emisión digital

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>FIRST_DIGITAL_DATE </li> <li> **Clave de API:**<br/>media.firstDigitalDate </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> "2016-01-25" </li> <li> **Descripción:**<br/> La fecha en la que se emitió por primera vez el contenido en cualquier canal o plataforma digital. Cualquier formato de fecha es aceptable, pero Adobe recomienda: AAAA-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.digitalDate) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> Fecha del primer uso digital </li> <li> **Datos de contexto:**<br/> (a.media.digitalDate) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Clasificación del contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>RATING </li> <li> **Clave de API:**<br/>media.rating </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>TVY, TVG, TVPG, TVMA </li> <li> **Descripción:**<br/> Según la clasificación de edades de contenido televisivo.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.rating) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> Clasificación del contenido </li> <li> **Datos de contexto:**<br/> (a.media.rating) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Creador

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>ORIGINATOR </li> <li> **Clave de API:**<br/>media.originator </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Warner Brothers", "Sony", "Disney" </li> <li> **Descripción:**<br/> El creador del contenido.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.originator) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/> Creador </li> <li> **Datos de contexto:**<br/> (a.media.originator) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Red

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave del SDK:**<br/>NETWORK </li> <li> **Clave de API:**<br/>media.network </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Fox", "Bravo", "ESPN" </li> <li> **Descripción:**<br/> Nombre de red/canal.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.network) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Red </li> <li> **Datos de contexto:**<br/> (a.media.network) </li> <li> **Fuente de datos:**<br/>videonetwork </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.network) </li> </ul> |

### Tipo de programa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SHOW_TYPE </li> <li> **Clave de API:**<br/>media.showType </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> “0” = episodio completo; “1” = Vista previa/trailer; “2” = Clip; “3” = Otro. </li> <li> **Descripción:**<br/> Tipo de contenido, expresado con un número entero entre 0 y 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.type) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Tipo de programa </li> <li> **Datos de contexto:**<br/> (a.media.type) </li> <li> **Fuente de datos:**<br/>videoshowtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>MVPD </li> <li> **Clave de API:**<br/>media.pass.mvpd </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"Comcast", "DirecTV", "Dish" </li> <li> **Descripción:**<br/> MVPD proporcionadas por la autenticación de Adobe.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.mvpd) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>MVPD </li> <li> **Datos de contexto:**<br/> (a.media.pass.mvpd) </li> <li> **Fuente de datos:**<br/>videomvpd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Con autorización

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>AUTHORIZED </li> <li> **Clave de API:**<br/>media.pass.auth </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> “TRUE” </li> <li> **Descripción:**<br/> El usuario ha sido autorizado mediante la autenticación de Adobe.  <br/>**Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.auth) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Autorizado </li> <li> **Datos de contexto:**<br/> (a.media.pass.auth) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Parte del día

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>DAY_PART </li> <li> **Clave de API:**<br/>media.dayPart </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li> <li> **Descripción:**<br/> Una propiedad que define el momento del día en que el contenido se emite o reproduce. Podría tener cualquier valor establecido como petición del cliente.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.dayPart) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Parte del día </li> <li> **Datos de contexto:**<br/> (a.media.dayPart) </li> <li> **Fuente de datos:**<br/>videodaypart </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Tipo de fuente de contenidos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>FEED </li> <li> **Clave de API:**<br/>media.feed </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>"East-HD", "West-HD", "East-SD" </li> <li> **Descripción:**<br/> Tipo de fuente.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.feed) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> Tipo de fuente de contenidos </li> <li> **Datos de contexto:**<br/> (a.media.feed) </li> <li> **Fuente de datos:**<br/>videofeedtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Artista

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.artist </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de contenidos](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"The Beatles" </li> <li> **Descripción:**<br/> Nombre del artista.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.artist) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.artist) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a.media.artist) </li> <li> **Fuente de datos:** <br/>videoaudioartist </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.artist) </li> </ul> |

### Álbum

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.album </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de contenidos](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:**<br/>"Revolver" </li> <li> **Descripción:**<br/> Nombre del álbum.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.album) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a.media.album) </li> <li> **Fuente de datos:** <br/>videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.album) </li> </ul> |

### Etiqueta

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.label </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de contenidos](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:**<br/>"Revolver" </li> <li> **Descripción:**<br/> Nombre de la etiqueta de registro.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.label) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a.media.label) </li> <li> **Fuente de datos:** <br/>videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.label) </li> </ul> |

### Autor

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.author </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de contenidos](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"John Kennedy Toole" </li> <li> **Descripción:**<br/> Nombre del autor (de un audiolibro).  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.author) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a.media.author) </li> <li> **Fuente de datos:** <br/>videoaudioauthor </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.author) </li> </ul> |

### Emisora

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.station </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de contenidos](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"NPR" </li> <li> **Descripción:**<br/> Nombre/ID de la emisora de radio.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.station) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a.media.station) </li> <li> **Fuente de datos:**<br/>videoaudiostation </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.station) </li> </ul> |

### Editor

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.publisher </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio de contenidos, Cierre de contenidos </li> <li> **Versión del SDK Versión del SDK:** 1.5.7 <br/>Disponible en [Información general de recopilación de contenidos](/help/media-collection-api/mc-api-overview.md) o [Descargar SDK - Versiones 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valor de muestra:** <br/>"Random Bauhaus" </li> <li> **Descripción:**<br/> Nombre del editor del contenido de audio.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.publisher) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a.media.publisher) </li> <li> **Fuente de datos:**<br/>videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.publisher) </li> </ul> |

## Métricas de audio y vídeo {#audio-and-video-metrics}

### Inicios de contenidos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente</li> <li> **Clave de API:**<br/>N/D</li> <li> **Tipo:**<br/> cadena</li> <li> **Enviado con:**<br/> Inicio de contenidos</li> <li> **Versión del SDK mínima:** cualquiera</li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Evento de carga del contenido. (Ocurre cuando el usuario hace clic en el botón _Reproducir_). Se contará incluso si hay anuncios pre-roll, almacenamiento en búfer, errores, etc.  <br/>**Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.view) </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=start) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> Inicio de contenidos </li> <li> **Datos de contexto:**<br/> (a.media.view) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.view) </li> </ul> |

### Inicio de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Se consume el primer fotograma del contenido. Si el usuario lo cierra durante un anuncio o el almacenamiento en búfer, entre otros, no tendrá lugar el evento “Inicio del contenido”.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Se inicia el contenido </li> <li> **Datos de contexto:**<br/> (a.media.play) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.play) </li> </ul> |

### Contenido finalizado {#content-complete}

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Flujo que se vio hasta el final. Esto no significa necesariamente que el usuario haya visto o escuchado todo el flujo; podrían haberse saltado partes. Solo significa que el usuario ha llegado al final de la emisión: el 100 %. <br/>Consulte también [Fin de sesión](quality-parameters.md#session-end) <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=complete) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>El contenido finaliza </li> <li> **Datos de contexto:**<br/> (a.media.complete) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.complete) </li> </ul> |

### Tiempo invertido en contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 105 </li> <li> **Descripción:**<br/> Recoge la duración total del evento (en segundos) para todos los eventos de tipo REPRODUCIR en el contenido principal.  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Tiempo invertido en contenido </li> <li> **Datos de contexto:**<br/> (a.media.timePlayed) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### Tiempo invertido en contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 120 </li> <li> **Descripción:**<br/> Recoge la duración total del evento (en segundos) para todos los eventos de tipo REPRODUCIR, tanto de contenido principal como del contenido publicitario.  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> Tiempo invertido en contenido </li> <li> **Datos de contexto:**<br/> (a.media.totalTimePlayed) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Tiempo de reproducción única

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 94 </li> <li> **Descripción:**<br/> Valor, en segundos, de segmentos de contenido únicos reproducidos durante una sesión. Se excluye el tiempo de reproducción en los casos en los que se vuelve atrás y el usuario ve el mismo segmento de contenido varias veces.  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.uniqueTimePlayed) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### Marcador de progreso del 10 %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> El cabezal de reproducción sobrepasa el marcador del 10 % del contenido en función de la duración. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 10 % </li> <li> **Datos de contexto:**<br/> (a.media.progress10) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### Marcador de progreso del 25 %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> El cabezal de reproducción sobrepasa el marcador del 25% del contenido en función de la duración de este. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 25 % </li> <li> **Datos de contexto:**<br/> (a.media.progress25) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### Marcador de progreso del 50 %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> El cabezal de reproducción sobrepasa el marcador del 50% del contenido en función de la duración de este. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 50 % </li> <li> **Datos de contexto:**<br/> (a.media.progress50) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### Marcador de progreso del 75 %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> **N/D** </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> El cabezal de reproducción sobrepasa el marcador del 75% del contenido en función de la duración de este. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 75 % </li> <li> **Datos de contexto:**<br/> (a.media.progress75) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### Marcador de progreso del 95 %

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> El cabezal de reproducción sobrepasa el marcador del 95% del contenido en función de la duración de este. El marcador se cuenta solo una vez, aunque se retroceda en el vídeo. Si se salta hacia adelante en el vídeo, los marcadores omitidos no se contabilizan.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Marcador de progreso del 95 % </li> <li> **Datos de contexto:**<br/> (a.media.progress95) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Promedio de audiencia por minuto

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>mayor o igual que 1 </li> <li> **Descripción:**<br/> La métrica de audiencia media por minuto se calcula como el tiempo total de contenido consumido (de un elemento multimedia específico) dividido entre la duración de ese vídeo para todas las sesiones de reproducción: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Audiencia media por minuto </li> <li> **Datos de contexto:**<br/> (a.media.averageMinuteAudience) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Datos federados

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> booleano </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> “true”  </li> <li> **Descripción:**<br/> Se establece en true cuando la visita está federada (es decir, recibida por el cliente como parte de un recurso compartido de datos federado, en lugar de su propia implementación). </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>N/D </li> <li> **Datos de contexto:**<br/> (a.media.federated) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.federated) </li> </ul> |

### Emisiones previstas

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 1 - Para una reproducción de 19 minutos; <br/>2 - Para una reproducción de 31 minutos; <br/>3: Para una reproducción de 78 minutos. </li> <li> **Descripción:**<br/> La cantidad de emisiones de vídeo o audio prevista de cada contenido individual. Este valor aumenta cada 30 minutos de tiempo de reproducción (contenido + publicidad). Los clientes deben crear sus propias reglas de procesamiento para disponer el valor para los informes. <br/><br/>Se contabiliza una emisión cada 30 minutos, en función del `ms_s` (o totalTimePlayed = Tiempo total del vídeo), similar a: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.estimatedStreams) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.estimatedStreams) </li> </ul> |

### Flujos afectados por la pausa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Este valor puede ser verdadero o falso. El valor es verdadero si se producen una o más pausas durante la reproducción de un elemento multimedia.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Emisiones afectadas en pausa </li> <li> **Datos de contexto:**<br/> (a.media.pause) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pause) </li> </ul> |

### Pausar eventos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>2 </li> <li> **Descripción:**<br/> Esta métrica se calcula como un recuento de los periodos de pausa que se producen durante una sesión de reproducción.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Pausar eventos </li> <li> **Datos de contexto:**<br/> (a.media.pauseCount) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Duración de la pausa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>190 </li> <li> **Descripción:**<br/> Recoge la duración total del evento (en segundos) para todos los eventos de tipo PAUSA. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/> **Fecha de la versión: 13/9/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Duración total de la pausa </li> <li> **Datos de contexto:**<br/> (a.media.pauseTime) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Reanudación de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> **media.resume** </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** 1.5.6 </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Se contabiliza una reanudación por cada reproducción que se reanude tras más de 30 minutos de almacenamiento en búfer, pausa o detención, o si este valor está definido por el reproductor en VideoInfo trackPlay. <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=resume) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Reanudación del contenido </li> <li> **Datos de contexto:**<br/> (a.media.resume) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.resume) </li> </ul> |

### Vistas de segmentos de contenido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de contenidos </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/>TRUE </li> <li> **Descripción:**<br/> Número de vistas del contenido principal. Se cuenta una vista de segmento de contenido cuando se ha visto al menos un fotograma.  <br/> **Importante:** Esto solo ocurre si se configura. Si no se configura, no devuelve ningún valor. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Heartbeat:**<br/>N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Vistas del segmento de contenido </li> <li> **Datos de contexto:**<br/> (a.media.segmentView) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segmentView) </li> </ul> |

<!--
### Ad Count 

| &nbsp;&nbsp;Implementation&nbsp;&nbsp; | Network&nbsp;Parameters | Reporting |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **API Key:**<br/> N/A </li> <li> **Type:**<br/> number </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. SDK Version:** Any </li> <li> **Sample value:**<br/> 2 </li> <li> **Description:**<br/> The number of ads started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/A </li> <li> **Heartbeats:**<br/> N/A </li> </ul> | <ul> <li> **Available:**<br/> Use custom processing rule </li> <li> **Reserved Variable:**<br/> N/A </li> <li> **Report Name:**<br/> Custom </li> <li> **Context Data:**<br/> (a.media.adCount) </li> <li> **Data Feed:**<br/> N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Chapter Count 

| &nbsp;&nbsp;Implementation&nbsp;&nbsp; | Network&nbsp;Parameters | Reporting |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **API Key:**<br/> N/A </li> <li> **Type:**<br/> number </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. SDK Version:** Any </li> <li> **Sample value:**<br/> 2 </li> <li> **Description:**<br/> The number of chapters started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/A </li> <li> **Heartbeats:**<br/> N/A </li> </ul> | <ul> <li> **Available:**<br/> Use custom processing rule </li> <li> **Reserved Variable:**<br/> N/A </li> <li> **Report Name:**<br/> Custom </li> <li> **Context Data:**<br/> (a.media.chapterCount) </li> <li> **Data Feed:**<br/> N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |
-->

## Parámetros de la Ley de privacidad del consumidor de California (CCPA) {#ccpa-params}

### Excluirse de reenvío del lado del servidor

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> N/D </li> <li> **Clave de API:**<br/> analytics.optOutServerSideForwarding </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> booleano </li> <li> **Enviado con:**<br/> Inicio de contenidos </li> <li> **Versión del SDK Versión del SDK:** N/A </li> <li> **Valor de muestra:**<br/> “true” </li> <li>**Descripción:**<br/> Se establece en true cuando el usuario final ha optado por no compartir sus datos entre Adobe Analytics y otras soluciones de Experience Cloud (por ejemplo, Audience Manager). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.dmp) </li> <li> **Heartbeats:**<br/> (s:meta:cm.ssf) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Contenido </li> <li> **Datos de contexto:**<br/> N/D </li> <li> **Fuente de datos:**<br/>video </li> <li> **Audience Manager:**<br/> N/A </li> </ul> |

### Exclusión del uso compartido

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> N/D </li> <li> **Clave de API:**<br/> analytics.optOutShare </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> booleano </li> <li> **Enviado con:**<br/> Inicio de contenidos </li> <li> **Versión del SDK Versión del SDK:** N/A </li> <li> **Valor de muestra:**<br/> “true” </li> <li>**Descripción:**<br/> Se establece en true cuando el usuario final ha optado por no publicar sus datos (por ejemplo, para otros clientes de Adobe Analytics). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.oos) </li> <li> **Heartbeats:**<br/> (s:meta:cm.oos) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Contenido </li> <li> **Datos de contexto:**<br/> N/D </li> <li> **Fuente de datos:**<br/>video </li> <li> **Audience Manager:**<br/> N/A </li> </ul> |

## API relacionadas {#section_Related_APIs}

### API createMediaObject {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript  -[createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast: [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### API MediaHeartbeatConfig {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

