---
seo-title: Parámetros de capítulo
title: Parámetros de capítulo
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 4a14e2faae6401a3f885eb5e341c1344d7f1e94d

---


# Parámetros de capítulo{#chapter-parameters}

En este tema se presenta una lista de datos de capítulo o segmento, incluidos los valores de datos de contexto que Adobe recopila mediante variables de solución.

Descripción de los datos de la tabla:

* **Implementación**: información sobre los valores y requisitos de implementación.
   * *Clave*: variable que se establece manualmente en la aplicación o automáticamente mediante el Adobe Media SDK.
   * *Requerido*: indica si el parámetro es necesario para el seguimiento básico de vídeos.
   * *Tipo*: especifica el tipo de variable que se va a definir, una cadena o un número.
   * *Sent With - Indicates when the data is sent: Media Start is the analytics call sent on media start, Ad Start is the analytics call sent on ad start, and so on; the Close calls are the compiled analytics calls sent directly from the heartbeat server to the analytics server at the end of the media session, or the end of the ad, chapter, etc.******* The close calls are not available in network packet calls.
   * *Versión del SDK mínima*: indica la versión del SDK necesaria para acceder al parámetro.
   * *Valor de muestra*: proporciona un ejemplo de uso de una variable común.
* **Parámetros de red**: muestra los valores que se transfieren a los servidores de Adobe Analytics o Heartbeat. En esta columna se muestran los nombres de los parámetros que aparecen en las llamadas de red generadas por los Adobe Media SDK.
* **Informes**: información sobre cómo ver y analizar los datos de vídeo.
   * *Disponible*: indica si los datos están disponibles en los informes de manera predeterminada (*Sí*) o se requiere una configuración personalizada (*Personalizado*)
   * *Variable reservada*: indica si los datos se capturan como un evento, eVar, prop o clasificación en una variable reservada.
   * *Nombre del informe*: nombre del informe de Adobe Analytics para la variable
   * *Datos de contexto*: nombre de los datos de contexto de Adobe Analytics que se transfieren al servidor de informes y se utilizan en las reglas de procesamiento.
   * *Fuente de datos*: nombre de columna para la variable que se encuentra en fuentes de datos Clickstream o Live Stream
   * *Audience Manager*: nombre de característica que se encuentra en Adobe Audience Manager

>[!IMPORTANT]
>
>No cambie los nombres de clasificación de ninguna de las variables enumeradas a continuación que se describan en Informes/Variable reservada como "clasificación".\
>The media classifications are defined when a report suite is enabled for media tracking. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las propiedades de los nuevos medios. During the update process Adobe determines whether the classifications are enabled by checking the names of the variables. Si falta alguno de ellos, Adobe agrega los que faltan de nuevo.

## Metadatos del capítulo {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### Nombre del capítulo

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/>media.chapter.friendlyName </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Sent with: Chapter Start, Chapter Close </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> ****<br/> Valor de muestra: "The Big Bang Chapter 2 - Dating" </li><li> **Descripción:**<br/>el nombre del capítulo y/o segmento.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>friendlyName) </li> <li> ****<br/> Heartbeat: (s:stream:chapter_name) </li> </ul> | <ul> <li> **Disponible:**<br/>creado por defecto...  </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Nombre del capítulo </li> <li> ****<br/> Datos de contexto: (a.media.chapter.<br/>friendlyName) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> </ul> |

### Posición del capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/>media.chapter.index </li> <li> ****<br/> Requerido: SDK: No; API: Sí. </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cerrar capítulo </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> ****<br/> Valor de muestra: 2 </li><li> **Descripción:**<br/>la posición (índice, entero) del capítulo dentro del contenido.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>position) </li> <li> ****<br/> Heartbeat: (l:stream:chapter_pos) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Posición del capítulo </li> <li> ****<br/> Context Data: (a.media.chapter.<br/>position) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>position) </li> </ul> |

### Desplazamiento de capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/>media.chapter.offset </li> <li> **Required:**<br/> SDK: No; API: Yes. </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cerrar capítulo </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> ****<br/> Valor de muestra: 58 </li><li> **Description:**<br/>The offset of the chapter inside the content (in seconds) from the start.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>desplazamiento) </li> <li> ****<br/> Heartbeat: (l:stream:chapter_offset) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Desplazamiento de capítulo </li> <li> ****<br/> Datos de contexto: (a.media.chapter.<br/>desplazamiento) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>desplazamiento) </li> </ul> |

### Duración del capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.chapter.length </li> <li> ****<br/> Requerido: SDK: No; API: Sí. </li> <li> **Tipo:**<br/>número </li> <li> **Sent with:**<br/> Chapter Close </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> ****<br/> Valor de muestra: 486 </li><li> **Description:**<br/>The length of the chapter, in seconds.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>length) </li> <li> ****<br/> Heartbeat: (l:stream:chapter_length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Longitud del capítulo </li> <li> ****<br/> Datos de contexto: (a.media.chapter.<br/>length) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>length) </li> </ul> |

### Capítulo

|   Implementación   | Network Parameters | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Sent with:**<br/> Chapter Close </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>El ID generado automáticamente del capítulo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>name) </li> <li> ****<br/> Heartbeat: (s:stream:chapter_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Capítulo </li> <li> ****<br/> Datos de contexto: (a.media.chapter.<br/>name) </li> <li> **Fuente de datos:**<br/>videochapter </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>name) </li> </ul> |

## Métricas del capítulo {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### Inicio del capítulo.

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente  </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/>Inicio del capítulo </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> ****<br/> Valor de muestra: TRUE </li><li> **Descripción:**<br/>Número de inicios de capítulo.  **Importante:** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>view) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Report Name:**<br/> Chapter Starts g </li> <li> ****<br/> Datos de contexto: (a.media.chapter.<br/>view) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>view) </li> </ul> |

### Capítulo completado

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente  </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cerrar capítulo </li> <li> **Versión del SDK mínima:** 1.3</li> <li> ****<br/> Valor de muestra: TRUE </li><li> **Descripción:**<br/>Número de capítulos completados.  **Importante:** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>complete) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> ****<br/> Nombre del informe: Capítulo Completa g </li> <li> ****<br/> Datos de contexto: (a.media.chapter.<br/>complete) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> </ul> |

### tiempo invertido en el capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente  </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cerrar capítulo </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> **Sample Value:**<br/> </li><li> **Description:**<br/>The time spent on the chapter.  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/>**Fecha de la versión: 13/9/18**   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Report Name:**<br/> Chapter Time Spent g </li> <li> ****<br/> Datos de contexto: (a.media.chapter.<br/>timePlayed) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> </ul> |

## Related APIs {#related_apis_section}

* Android - createChapterObject[](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - createChapterObjectWithName[](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - createChapterObject[](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
