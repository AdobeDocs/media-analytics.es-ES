---
title: Parámetros de capítulo
description: null
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Parámetros de capítulo {#chapter-parameters}

En este tema se presenta una lista de datos de capítulo o segmento, incluidos los valores de datos de contexto que Adobe recopila mediante variables de solución.

Descripción de los datos de la tabla:

* **Implementación**: información sobre los valores y requisitos de implementación.
   * *Clave*: variable que se establece manualmente en la aplicación o automáticamente mediante el Adobe Media SDK.
   * *Requerido*: indica si el parámetro es necesario para el seguimiento básico de vídeos.
   * *Tipo*: especifica el tipo de variable que se va a definir, una cadena o un número.
   * *Enviado con*: indica cuándo se envían los datos: *Inicio de contenidos* es la llamada de análisis enviada al inicio del contenido, *Inicio de publicidad* es la llamada de análisis enviada al iniciar el anuncio, etc., las llamadas *Cierre* son llamadas de análisis compiladas enviadas directamente desde el servidor de latidos al servidor de análisis al final de la sesión de contenido, o al final del anuncio, capítulo, etc. Las llamadas Cierre no están disponibles en las llamadas a paquetes de red.
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
>No cambie los nombres de clasificación de ninguna de las variables enumeradas a continuación que se describan en Informes/Variables reservadas como “clasificación”.\
>Las clasificaciones de contenidos se definen cuando se habilita un grupo de informes para el seguimiento de contenidos. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las propiedades de los nuevos contenidos. Durante el proceso de actualización, Adobe determina si las clasificaciones están habilitadas mediante la comprobación de los nombres de las variables. Si falta alguno de ellos, Adobe agrega los que faltan de nuevo.

## Metadatos del capítulo {#chapter-metadata}

### Nombre del capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/>media.chapter.friendlyName </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio del capítulo, Cierre del capítulo </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> **Valor de muestra:**<br/> “The Big Bang Chapter 2 - Dating” </li><li> **Descripción:**<br/>Nombre del capítulo y/o segmento.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_name) </li> </ul> | <ul> <li> **Disponible:**<br/>creado por defecto...  </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Nombre del capítulo </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> </ul> |

### Posición del capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/>media.chapter.index </li> <li> **Obligatorio:**<br/> SDK: No; API: Sí. </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> **Valor de muestra:**<br/> 2 </li><li> **Descripción:**<br/>La posición (índice, total) del capítulo dentro del contenido.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>position) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_pos) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Posición del capítulo </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>position) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>position) </li> </ul> |

### Desplazamiento de capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/>media.chapter.offset </li> <li> **Obligatorio:**<br/> SDK: No; API: Sí. </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> **Valor de muestra:**<br/> 58 </li><li> **Descripción:**<br/>El desplazamiento del capítulo dentro del contenido (en segundos) desde el inicio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_offset) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Desplazamiento de capítulo </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>offset) </li> </ul> |

### Duración del capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.chapter.length </li> <li> **Obligatorio:**<br/> SDK: No; API: Sí. </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> **Valor de muestra:**<br/> 486 </li><li> **Descripción:**<br/>Duración del capítulo, expresada en segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>length) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Longitud del capítulo </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>length) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>length) </li> </ul> |

### Capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>El ID del capítulo generado automáticamente.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>name) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Capítulo </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>name) </li> <li> **Fuente de datos:**<br/>videochapter </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>name) </li> </ul> |

## Métricas del capítulo {#chapter-Metrics}

### Inicio del capítulo.

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente  </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/>Inicio del capítulo </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> **Valor de muestra:**<br/> “TRUE” </li><li> **Descripción:**<br/>El número de capítulos iniciados.  **Importante:** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>view) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> Capítulos iniciados g </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>view) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>view) </li> </ul> |

### Capítulo completado

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente  </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Versión del SDK mínima:** 1.3</li> <li> **Valor de muestra:**<br/> “TRUE” </li><li> **Descripción:**<br/>El número de capítulos completados.  **Importante:** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> Capítulos completados g </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> </ul> |

### tiempo invertido en el capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente  </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Versión del SDK mínima:** 1.3 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>El tiempo utilizado en el capítulo.  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/>**Fecha de la versión: 13/9/18**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> Tiempo utilizado en el capítulo g </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> </ul> |

## API relacionadas {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
