---
title: Parámetros de estado del reproductor
description: En este tema se describen los parámetros de seguimiento del estado del reproductor.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 73c579ec013d15ab47faa936cca1297f7052a8fb
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 75%

---


# Parámetros de estado del reproductor {#player-state-parameters}

En este tema se presenta una lista de los datos del estado del reproductor que Adobe recopila a través de variables de solución.

Descripción de los datos de la tabla:

* **Implementación:** Información sobre los valores y requisitos de implementación
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
   * *Fuente de datos:* Nombre de columna para la variable que se encuentra en las fuentes de datos de flujo de navegación o flujo en directo
   * *Audience Manager:* Nombre de la función de Adobe Audience Manager.

>[!IMPORTANT]
>
>No cambie los nombres de clasificación de ninguna de las variables enumeradas a continuación que se describan en Informes/Variables reservadas como “clasificación”.\
>Las clasificaciones de contenidos se definen cuando se habilita un grupo de informes para el seguimiento de contenidos. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las propiedades de los nuevos contenidos. Durante el proceso de actualización, Adobe determina si las clasificaciones están habilitadas mediante la comprobación de los nombres de las variables. Si falta alguno de ellos, Adobe agrega los que faltan de nuevo.

## Propiedades de estado del reproductor {#player-state-properties}

Las funciones de seguimiento de estado del reproductor se pueden adjuntar a un flujo de audio o vídeo. Las métricas de seguimiento de estado del reproductor estandarizado se almacenan como variables de solución. Los estados estándar son: fullScreen, mute, closeCaption, pictureInPicture e inFocus.

### Propiedades de pantalla completa

#### Transmisiones afectadas por Pantalla completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción:**<br/> cantidad de transmisiones afectadas por la pantalla completa. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de pantalla completa durante una sesión de reproducción.<br/> **Importante:**<br/> si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.fullscreen.set<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre de informe **<br/> Transmisiones afectadas por pantalla completa</li> <li> **Datos **<br/>de contexto a.media.state.fullscreen.set<br/> </li> <li> **Fuente de datos **<br/> videostatefullscreen</li> <li> **Audience Manager **<br/>c_contextdata.a.media.state.fullscreen.set</li> </ul> |

#### Recuento de Pantalla completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción **<br/> La cantidad de veces que se ha mostrado una pantalla completa. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de pantalla completa durante una sesión de reproducción.<br/> **Importante **<br/>Si se establece este evento, el recuento es igual al número de veces que el vídeo estaba en el estado Pantalla completa. Si no se establece este evento, no se enviará ningún valor.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.fullscreen.count<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre del informe **<br/> Recuento de pantalla completa</li> <li> **Context Data **<br/>a.media.States.fullscreen.count<br/> </li> <li> **Fuente de datos **<br/> videostatefullscreencount</li> <li> **Audience Manager **<br/>c_contextdata.media.state.fullscreen.count</li> </ul> |



#### Duración total de Pantalla completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción **<br/> El tiempo que se ha mostrado una pantalla completa. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de pantalla completa durante una sesión de reproducción.<br/> **Importante **<br/>Si se establece este evento, la hora es igual a la duración del vídeo en el estado de pantalla completa. Si no se establece este evento, no se enviará ningún valor.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.fullscreen.time<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre **<br/>del informe Duración total de pantalla completa</li> <li> **Datos **<br/>de contexto a.media.state.fullscreen.time<br/> </li> <li> **Fuente de datos **<br/> videostatefullscreentime</li> <li> **Audience Manager **<br/>c_contextdata.media.state.fullscreen.time</li> </ul> |


### Propiedades de subtítulos

#### Transmisiones afectadas por Subtítulos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción:**<br/> cantidad de transmisiones afectadas por los subtítulos. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de subtítulo durante una sesión de reproducción.<br/> **Importante:**<br/> si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.closedcaptioning.set<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre de informe **<br/> Transmisiones afectadas por los subtítulos</li> <li> **Context Data **<br/>a.media.States.closedcaptioning.set<br/> </li> <li> **Fuente de datos **<br/> videostateclosedesubtítulos</li> <li> **Audience Manager **<br/>c_contextdata.a.media.state.closedcaptioning.set</li> </ul> |


#### Recuento de Subtítulos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> ****<br/>Descripción El número de veces que se mostraban los subtítulos opcionales. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de subtítulo durante una sesión de reproducción.<br/> **Importante **<br/>Si se establece este evento, el recuento es igual al número de veces que el vídeo estaba en el estado de subtítulos opcionales. Si no se establece este evento, no se enviará ningún valor.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>C19<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre de informe **<br/> Recuento de subtítulos</li> <li> **Datos **<br/>de contexto a.media.state.closedcaptioning.count<br/> </li> <li> **Fuente de datos **<br/> videostateclosedcaptioningcount</li> <li> **Audience Manager **<br/>c_contextdata.media.statossubtítulos.count</li> </ul> |


#### Duración total de Subtítulos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> ****<br/>Descripción El tiempo que se mostraba el subtítulo cerrado. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de pantalla completa durante una sesión de reproducción.<br/> **Importante **<br/>Si se establece este evento, la hora es igual a la duración del vídeo en el estado de subtítulos opcionales. Si no se establece este evento, no se enviará ningún valor.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.closedcaptioning.time<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre **<br/>del informe Subtítulos opcionales Duración total</li> <li> **Context Data **<br/>a.media.States.closedcaptioning.time<br/> </li> <li> **Fuente de datos **<br/> videostateclosedcaptioningtime</li> <li> **Audience Manager **<br/>c_contextdata.media.state.closedcaptioning.time</li> </ul> |


### Propiedades de Silenciar

#### Transmisiones afectadas por Silenciar

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción:**<br/> número de emisiones afectadas por Silenciar. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Silenciar durante una sesión de reproducción.<br/> **Importante:**<br/> si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.mute.set<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre de informe **<br/> de Transmisiones afectadas por Silenciar</li> <li> **Datos **<br/>de contexto a.media.state.mute.set<br/> </li> <li> **Fuente de datos **<br/> videostatemute</li> <li> **Audience Manager **<br/>c_contextdata.a.media.state.mute.set</li> </ul> |

#### Recuentos de Silenciar

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> ****<br/>Descripción El número de veces que se ha mostrado Silencio. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Silenciar durante una sesión de reproducción.<br/> **Importante **<br/>Si se establece este evento, el recuento es igual al número de veces que el vídeo estaba en estado de silencio. Si no se establece este evento, no se enviará ningún valor.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.mute.count<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre de informe **<br/> Cantidad de Silenciar</li> <li> **Datos **<br/>de contexto a.media.state.mute.count<br/> </li> <li> **Fuente de datos **<br/> videostatemutecount</li> <li> **Audience Manager **<br/>c_contextdata.media.state.mute.count</li> </ul> |

#### Duración total de Silenciar

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> ****<br/>Descripción El tiempo que se ha estado mutando. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Silenciar durante una sesión de reproducción.<br/> **Importante **<br/>Si se establece este evento, la hora es igual a la duración del vídeo en el estado de silencio. Si no se establece este evento, no se enviará ningún valor.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.mute.time<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Duración total del silencio del nombre **<br/>del informe</li> <li> **Context Data **<br/>a.media.state.mute.time<br/> </li> <li> **Fuente de datos **<br/> videostatemutetime</li> <li> **Audience Manager **<br/>c_contextdata.media.state.mute.time</li> </ul> |


### Propiedades de Imagen en imagen


#### Transmisiones afectadas por Imagen en imagen

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción **<br/> Cantidad de transmisiones afectadas por Imagen en imagen. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Imagen en imagen durante una sesión de reproducción.<br/> **Importante:**<br/> si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.pictureinpicture.set<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre de informe **<br/> Transmisiones afectadas por Imagen en imagen</li> <li> **Context Data **<br/>a.media.States.pictureinpicture.set<br/> </li> <li> **Fuente de datos **<br/> videostatepictureinpicture</li> <li> **Audience Manager **<br/>c_contextdata.a.media.state.pictureinpicture.set</li> </ul> |


#### Recuentos de Imagen en imagen

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción **<br/> La cantidad de veces que se ha mostrado Imagen en imagen. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Imagen en imagen durante una sesión de reproducción.<br/> **Importante** <br/> Si se establece este evento, el recuento es igual al número de veces que el vídeo estaba en el estado Imagen en imagen. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.pictureinpicture.count<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre del informe **<br/> Cantidad de Imagen en imagen</li> <li> **Context Data **<br/>a.media.States.pictureinpicture.count<br/> </li> <li> **Fuente de datos **<br/> videostatepictureinpicturecount</li> <li> **Audience Manager **<br/>c_contextdata.media.state.pictureinpicture.count</li> </ul> |


#### Duración total de Imagen en imagen

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción **<br/> Duración de la visualización de la imagen en imagen. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Imagen en imagen durante una sesión de reproducción.<br/> **Importante** <br/> Si se establece este evento, la hora es igual a la duración del vídeo en el estado Imagen en imagen. Si no se establece este evento, no se enviará ningún valor..   </li> </ul> | <ul> <li> **Adobe **<br/>Analytics.media.state.pictureinpicture.time<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre **<br/>del informe Imagen en imagen Duración total</li> <li> **Context Data **<br/>a.media.States.pictureinpicture.time<br/> </li> <li> **Fuente de datos **<br/> videostatepictureinpicturetime</li> <li> **Audience Manager **<br/>c_contextdata.media.state.pictureinpicture.time</li> </ul> |


### Propiedades de Enfocado

#### Transmisiones afectadas por Enfocado

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción:**<br/> número de emisiones afectadas por Enfocado. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Enfocado durante una sesión de reproducción.<br/> **Importante:**<br/> si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.States.infocus.set<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre de informe **<br/> Transmisiones afectadas por Enfocado</li> <li> **Datos **<br/>de contexto a.media.States.infocus.set<br/> </li> <li> **Fuente de datos **<br/> videostateinfocus</li> <li> **Audience Manager **<br/>c_contextdata.a.media.state.infocus.set</li> </ul> |


#### Recuentos de Enfocado

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción **<br/> La cantidad de veces que se ha visualizado Enfocado. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Enfocado durante una sesión de reproducción.<br/> **Importante **<br/>Si se establece este evento, el recuento es igual al número de veces que el vídeo estaba en el estado Enfoque. Si no se establece este evento, no se enviará ningún valor.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.States.infocus.count<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre del informe **<br/> Recuento de Enfocados</li> <li> **Datos **<br/>de contexto a.media.state.infocus.count<br/> </li> <li> **Fuente de datos **<br/> videostateinfocuscount</li> <li> **Audience Manager **<br/>c_contextdata.media.state.infocus.count</li> </ul> |


#### Duración total de Enfocado

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente</li> <li> **Clave de API:**<br/> N/D</li> <li> **Obligatorio:**<br/>no</li> <li> **Tipo:**<br/> número</li> <li> **Enviado con:**<br/> cierre de medios</li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE</li><li> **Descripción **<br/> La cantidad de tiempo que se ha visualizado Enfocado. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Enfocado durante una sesión de reproducción.<br/> **Importante** <br/> Si se establece este evento, la hora es igual a la duración del vídeo en el estado Enfoque. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.state.infocus.time<br/></li> <li> **Heartbeat **<br/> N/D</li> </ul> | <ul> <li> **Disponible:**<br/> sí</li> <li> **Variable reservada:**<br/> evento</li> <li> **Nombre **<br/>Del Informe En Duración Total Del Enfoque</li> <li> **Datos **<br/>de contexto a.media.state.infocus.time<br/> </li> <li> **Fuente de datos **<br/> videostateinfocustime</li> <li> **Audience Manager **<br/>c_contextdata.media.state.infocus.time</li> </ul> |

## Lista de propiedades para identidades XDM

Los datos almacenados en Analytics se pueden usar para cualquier fin y las métricas de estado del reproductor se pueden importar en la plataforma de Adobe Experience Platform mediante XDM y se pueden usar con el análisis de viajes del cliente.

| Propiedad de estado del reproductor | Asignación |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## API relacionadas {#related_apis_section}

* Android: [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS: [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* JavaScript: [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
