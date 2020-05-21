---
title: Parámetros de estado del reproductor
description: En este tema se describen los parámetros de seguimiento del estado del reproductor.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 3c24b69265287084393be830193da14ae85cc5ba
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 28%

---


# Parámetros de estado del reproductor{#player-state-parameters}

En este tema se presenta una lista de los datos del estado del reproductor que Adobe recopila a través de variables de solución.

Descripción de los datos de la tabla:

* **Implementación:** Información sobre los valores y requisitos de implementación
   * *Clave*: Variable establecida manualmente en la aplicación o automáticamente por el SDK de Adobe Media.
   * *Obligatorio*: Indica si el parámetro es necesario para el seguimiento de vídeo básico.
   * *Tipo*: Especifica el tipo de la variable que se va a establecer, la cadena o el número.
   * *Enviado con*: indica cuándo se envían los datos: *Inicio de contenidos* es la llamada de análisis enviada al inicio del contenido, *Inicio de publicidad* es la llamada de análisis enviada al iniciar el anuncio, etc., las llamadas *Cierre* son llamadas de análisis compiladas enviadas directamente desde el servidor de latidos al servidor de análisis al final de la sesión de contenido, o al final del anuncio, capítulo, etc. Las llamadas Cierre no están disponibles en las llamadas a paquetes de red.
   * *Mínima Versión del SDK*: Indica la versión del SDK a la que debería acceder el parámetro.
   * *Valor de muestra*: Proporciona un ejemplo del uso común de variables.
* **Parámetros de red:** Muestra los valores que se pasan a los servidores de Adobe Analytics o Heartbeat. Esta columna muestra los nombres de los parámetros que se ven en las llamadas de red generadas por los SDK de medios de Adobe.
* **Sistema de informes:** Información sobre cómo ver y analizar datos de vídeo.
   * *Disponible*: Indica si los datos están disponibles en el sistema de informes de forma predeterminada (*Sí*) o si requieren una configuración personalizada (*Personalizado*)
   * *Variable reservada*: Indica si los datos se capturan como un evento, una eVar, una propiedad o una clasificación en una variable reservada.
   * *Nombre del informe*: Nombre del informe de Adobe Analytics para la variable
   * *Datos de contexto*: Nombre de los datos de contexto de Adobe Analytics pasados al servidor de sistema de informes y utilizados en reglas de procesamiento.
   * *Fuente de datos*: Nombre de columna para la variable que se encuentra en las fuentes de datos de flujo de navegación o flujo en directo
   * *Audience Manager*: Nombre de la función de Adobe Audience Manager.

>[!IMPORTANT]
>
>No cambie los nombres de clasificación de ninguna de las variables enumeradas a continuación que se describan en Informes/Variables reservadas como “clasificación”.\
>Las clasificaciones de contenidos se definen cuando se habilita un grupo de informes para el seguimiento de contenidos. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las propiedades de los nuevos contenidos. Durante el proceso de actualización, Adobe determina si las clasificaciones están habilitadas mediante la comprobación de los nombres de las variables. Si falta alguno de ellos, Adobe agrega los que faltan de nuevo.



## Propiedades de estado del reproductor {#player-state-properties}

Las tablas de propiedades de seguimiento de estado del reproductor están organizadas en las siguientes cinco secciones:

* Pantalla completa
   * Flujos afectados por la pantalla completa
   * Recuentos a pantalla completa
   * Duración total de pantalla completa
* Cerrar rótulo
   * Flujos afectados por subtítulos opcionales
   * Recuentos de subtítulos opcionales
   * Duración total de los subtítulos opcionales
* Silenciar
   * Flujos afectados por el silencio
   * Silenciar recuentos
   * Silenciar duración total
* Imagen en imagen
   * Flujo afectado por imagen en imagen
   * Recuentos de imágenes
   * Duración total de la imagen
* En Enfoque
   * Flujos afectados por el enfoque
   * Recuentos de enfoque
   * Duración total del enfoque

### Propiedades de pantalla completa

#### Flujos afectados por la pantalla completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El número de flujos afectados por la pantalla completa. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.state.fullscreen.set)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Flujos de nombres **<br/>de informes afectados por pantalla completa</li> <li> **Datos **<br/>de contexto (a.media.state.fullscreen.set)<br/> </li> <li> **Fuente **<br/>de datos videostatefullscreen</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.a.media.state.fullscreen.set)</li> </ul> |

#### Recuentos a pantalla completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El número de veces que se ha mostrado una pantalla completa. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreencount)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Nombre **<br/>del informe Recuento de pantalla completa</li> <li> **Datos **<br/>de contexto (videostatefullscreencount)<br/> </li> <li> **Fuente **<br/>de datos videostatefullscreencount</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.videostatefullscreencount)</li> </ul> |



#### Duración total de pantalla completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El tiempo que se ha mostrado una pantalla completa. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreentime)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Nombre **<br/>del informe Duración de pantalla completa</li> <li> **Datos **<br/>de contexto (videostatefullscreentime)<br/> </li> <li> **Fuente **<br/>de datos videostatefullscreentime</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.videostatefullscreentime)</li> </ul> |


### Cerrar propiedades de rótulo

#### Flujos afectados por subtítulos opcionales

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El número de flujos afectados por los subtítulos opcionales. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.state.closedcaptioning.set)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Flujos de nombres **<br/>de informes afectados por subtítulos opcionales</li> <li> **Datos **<br/>de contexto (a.media.state.closedcaptioning.set)<br/> </li> <li> **Fuente **<br/>de datos videostateclosedesubtítulos</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.a.media.state.closedcaptioning.set)</li> </ul> |


#### Recuentos de subtítulos opcionales

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El número de veces que se ha seleccionado Subtítulos opcionales. This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningcount)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Recuento de subtítulos opcionales de nombre **<br/>del informe</li> <li> **Datos **<br/>de contexto (videostateclosedcaptioningcount)<br/> </li> <li> **Fuente **<br/>de datos videostateclosedcaptioningcount</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.videostateclosedcaptioningcount)</li> </ul> |


#### Duración total de los subtítulos opcionales

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El tiempo que se seleccionó Subtítulos opcionales. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningtime)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Duración de los subtítulos opcionales del nombre **<br/>del informe</li> <li> **Datos **<br/>de contexto (videostateclosedcaptioningtime)<br/> </li> <li> **Fuente **<br/>de datos videostateclosedcaptioningtime</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.videostateclosedcaptioningtime)</li> </ul> |


### Silenciar propiedades

#### Flujos afectados por el silencio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El número de flujos afectados por Silencio. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.state.mute.set)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Flujos de nombres **<br/>de informes afectados por silencio</li> <li> **Datos **<br/>de contexto (a.media.state.mute.set)<br/> </li> <li> **Video statemute de fuente **<br/>de datos</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.a.media.state.mute.set)</li> </ul> |

#### Silenciar recuentos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El número de veces que se ha seleccionado Silenciar. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutecount)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Número de silencios de nombre **<br/>del informe</li> <li> **Datos **<br/>de contexto (videostatemutecount)<br/> </li> <li> **Fuente **<br/>de datos videostatemutecount</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.videostatemutecount)</li> </ul> |

#### Silenciar duración total

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El tiempo que se seleccionó Silenciar. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutetime)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Duración de silencio del nombre **<br/>del informe</li> <li> **Datos **<br/>de contexto (videostatemutetime)<br/> </li> <li> **Fuente **<br/>de datos videostatemutetime</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.videostatemutetime)</li> </ul> |


### Imagen en propiedades de imagen


#### Flujos afectados por imágenes

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El número de flujos afectados por Picture in Picture. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.state.pictureinpicture.set)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Flujos de nombres **<br/>de informes afectados por imágenes</li> <li> **Datos **<br/>de contexto (a.media.state.pictureinpicture.set)<br/> </li> <li> **Fuente **<br/>de datos videostatepictureinpicture</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.a.media.state.pictureinpicture.set)</li> </ul> |


#### Recuentos de imágenes

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El número de veces que se ha mostrado la imagen en imagen. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturecount)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Nombre **<br/>del informe Imagen en el recuento de imágenes</li> <li> **Datos **<br/>de contexto (videostatepictureinpicturecount)<br/> </li> <li> **Fuente **<br/>de datos videostatepictureinpicturecount</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.videostatepictureinpicturecount)</li> </ul> |


#### Duración total de la imagen

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>DescripciónDuración de la visualización de la imagen en imagen. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturetime)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Nombre **<br/>del informe Imagen en la duración de la imagen</li> <li> **Datos **<br/>de contexto (videostatepictureinpicturetime)<br/> </li> <li> **Fuente **<br/>de datos videostatepictureinpicturetime</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.videostatepictureinpicturetime)</li> </ul> |


### En las propiedades de enfoque

#### Flujos afectados por el enfoque

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El número de flujos afectados por In Focus. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.state.infocus.set)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Flujos de nombres **<br/>de informes afectados por el enfoque</li> <li> **Datos **<br/>de contexto (a.media.state.infocus.set)<br/> </li> <li> **Fuente **<br/>de datos videostateinfocus</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.a.media.state.infocus.set)</li> </ul> |


#### Recuentos de enfoque

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>Descripción El número de veces que se ha visualizado En el enfoque. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocuscount)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Nombre **<br/>del informe en el recuento de enfoque</li> <li> **Datos **<br/>de contexto (videostateinfocuscount)<br/> </li> <li> **Fuente **<br/>de datos videostateinfocuscount</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.videostateinfocuscount)</li> </ul> |


#### Duración total del enfoque

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave **<br/>SDK definida automáticamente</li> <li> **Clave **<br/>de API N/D</li> <li> **No requerido **<br/></li> <li> **Número de tipo **<br/></li> <li> **Enviado con **<br/>cierre de medios</li> <li> **Mínima SDK Version **<br/>3.0</li> <li> **Valor **<br/>de muestra TRUE</li><li> ****<br/>DescripciónTiempo que se mostraba en el foco. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Importante** Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocustime)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponible **<br/>Sí</li> <li> **evento de variable **<br/>reservada</li> <li> **Nombre **<br/>del informe en la duración del enfoque</li> <li> **Datos **<br/>de contexto (videostateinfocustime)<br/> </li> <li> **Fuente **<br/>de datos videostateinfocustime</li> <li> **Administrador **<br/>de Audiencias (c_contextdata.videostateinfocustime)</li> </ul> |



## API relacionadas {#related_apis_section}

NECESIDAD: Añadir vínculos de API a documentos:
* Android - [createStateObject](https://need)
* iOS - [createStateObjectWithName](https://need)
* Javascript - [createStateObject](https://need)
