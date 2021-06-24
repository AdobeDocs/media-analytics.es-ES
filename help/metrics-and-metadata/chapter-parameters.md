---
title: Parámetros de capítulo
description: '"Obtenga información sobre los parámetros de capítulo para la implementación, la red y los informes".'
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 93%

---

# Parámetros de capítulo{#chapter-parameters}

En este tema se presenta una lista de datos de capítulo o segmento, incluidos los valores de datos de contexto que Adobe recopila mediante variables de solución.

Descripción de los datos de la tabla:

* **Implementación:** Información sobre los valores y requisitos de implementación.
   * *Clave*: Variable establecida manualmente en la aplicación o automáticamente por el SDK de Adobe Media.
   * *Obligatorio:* Indica si el parámetro es necesario para el seguimiento de vídeo básico.
   * *Tipo*: Especifica el tipo de la variable que se va a establecer, la cadena o el número.
   * *Enviado con*: indica cuándo se envían los datos: *Inicio de contenidos* es la llamada de análisis enviada al inicio del contenido, *Inicio de publicidad* es la llamada de análisis enviada al iniciar el anuncio, etc., las llamadas *Cierre* son llamadas de análisis compiladas enviadas directamente desde el servidor de latidos al servidor de análisis al final de la sesión de contenido, o al final del anuncio, capítulo, etc. Las llamadas Cierre no están disponibles en las llamadas a paquetes de red.
   * *Mínima Versión del SDK*: Indica la versión del SDK a la que debería acceder el parámetro.
   * *Valor de muestra:* Proporciona un ejemplo del uso común de variables.
* **Parámetros de red:** Muestra los valores que se pasan a los servidores de Adobe Analytics o Heartbeat. Esta columna muestra los nombres de los parámetros que se ven en las llamadas de red generadas por los Media SDK de Adobe.
* **Sistema de informes:** Información sobre cómo ver y analizar datos de vídeo.
   * *Disponible*: Indica si los datos están disponibles en el sistema de informes de forma predeterminada (*Sí*) o si requieren una configuración personalizada (*Personalizado*)
   * *Variable reservada:* Indica si los datos se capturan como un evento, una eVar, una propiedad o una clasificación en una variable reservada.
   * *Nombre del informe:* Nombre del informe de Adobe Analytics para la variable
   * *Datos de contexto:* Nombre de los datos de contexto de Adobe Analytics pasados al servidor de sistema de informes y utilizados en reglas de procesamiento.
   * *Fuente de datos:* Nombre de columna para la variable que se encuentra en las fuentes de datos de flujo de navegación o flujo en directo.
   * *Audience Manager:* Nombre de la función de Adobe Audience Manager.

>[!IMPORTANT]
>
>No cambie los nombres de clasificación de ninguna de las variables enumeradas a continuación que se describan en Informes/Variables reservadas como “clasificación”.\
>Las clasificaciones de contenidos se definen cuando se habilita un grupo de informes para el seguimiento de contenidos. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las propiedades de los nuevos contenidos. Durante el proceso de actualización, Adobe determina si las clasificaciones están habilitadas mediante la comprobación de los nombres de las variables. Si falta alguno de ellos, Adobe agrega los que faltan de nuevo.

## Metadatos del capítulo {#chapter-metadata}

### Nombre del capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/> media.chapter.friendlyName </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio del capítulo, Cierre del capítulo </li> <li> **Mínima Versión de SDK:** 1,3 </li> <li> **Valor de muestra:**<br/> “The Big Bang Chapter 2 - Dating” </li><li> **Descripción:**<br/> Nombre del capítulo y/o segmento.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (:stream:nombre_capítulo) </li> </ul> | <ul> <li> **Disponible:**<br/> creado por defecto...  </li> <li> **Variable reservada:**<br/> clasificación </li> <li> **Nombre del informe:**<br/> Nombre del capítulo </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> </ul> |

### Posición del capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/> media.chapter.index </li> <li> **Obligatorio:**<br/> SDK: No; API: Sí. </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Mínima Versión de SDK:** 1,3 </li> <li> **Valor de muestra:**<br/> 2 </li><li> **Descripción:**<br/> La posición (índice, total) del capítulo dentro del contenido.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.chapter).<br/>position) </li> <li> **Heartbeat:**<br/> (:stream:lchapter_pos) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> clasificación </li> <li> **Nombre del informe:**<br/> Posición del capítulo </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>position) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/>  (c_contextdata.<br/>a.media.chapter.<br/>position) </li> </ul> |

### Desplazamiento de capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/> media.chapter.offset </li> <li> **Obligatorio:**<br/> SDK: No; API: Sí. </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Mínima Versión de SDK:** 1,3 </li> <li> **Valor de muestra:**<br/> 58 </li><li> **Descripción:**<br/> El desplazamiento del capítulo dentro del contenido (en segundos) desde el inicio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.chapter).<br/>offset) </li> <li> **Heartbeat:**<br/> (:stream:lchapter_offset) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> clasificación </li> <li> **Nombre del informe:**<br/> Desplazamiento de capítulo </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/>  (c_contextdata.<br/>a.media.chapter.<br/>offset) </li> </ul> |

### Duración del capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/> media.chapter.length </li> <li> **Obligatorio:**<br/> SDK: No; API: Sí. </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Mínima Versión de SDK:** 1,3 </li> <li> **Valor de muestra:**<br/> 486 </li><li> **Descripción:**<br/> Duración del capítulo, expresada en segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.chapter).<br/>length) </li> <li> **Heartbeat:**<br/> (:stream:lchapter_length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> clasificación </li> <li> **Nombre del informe:**<br/> Longitud del capítulo </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>length) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/>  (c_contextdata.<br/>a.media.chapter.<br/>length) </li> </ul> |

### Capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Mínima Versión de SDK:** 1,3 </li> <li> **Valor de muestra:**<br/>  </li><li> **Descripción:**<br/> El ID del capítulo generado automáticamente.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.chapter).<br/>name) </li> <li> **Heartbeat:**<br/> (:stream:schapter_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Capítulo </li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>name) </li> <li> **Fuente de datos:**<br/> videochapter </li> <li> **Audience Manager:**<br/>  (c_contextdata.<br/>a.media.chapter.<br/>name) </li> </ul> |

## Métricas del capítulo {#chapter-Metrics}

### Inicio del capítulo.

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Inicio del capítulo </li> <li> **Mínima Versión de SDK:** 1,3 </li> <li> **Valor de muestra:**<br/> “TRUE” </li><li> **Descripción:**<br/> El número de capítulos iniciados.  **Importante:** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.chapter).<br/>view) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=chapter_start) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Inicio del capítulo</li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>view) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/>  (c_contextdata.<br/>a.media.chapter.<br/>view) </li> </ul> |

### Capítulo completado

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Mínima Versión de SDK:** 1,3</li> <li> **Valor de muestra:**<br/> “TRUE” </li><li> **Descripción:**<br/> El número de capítulos completados.  **Importante:** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.chapter).<br/>complete) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=chapter_complete) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Capítulo completado</li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/>  (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> </ul> |

### Tiempo invertido en el capítulo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> Cierre de capítulos </li> <li> **Mínima Versión de SDK:** 1,3 </li> <li> **Valor de muestra:**<br/>  </li><li> **Descripción:**<br/> El tiempo utilizado en el capítulo.  El valor se muestra en el formato de hora (HH:MM:SS) en Analysis Workspace y en Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/>**Fecha de la versión: 13/9/18**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.chapter).<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Tiempo utilizado en el capítulo</li> <li> **Datos de contexto:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/>  (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> </ul> |

## API relacionadas {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
