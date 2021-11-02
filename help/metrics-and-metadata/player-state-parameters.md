---
title: Parámetros de estado del reproductor
description: '"Obtenga información sobre los parámetros de seguimiento del estado del reproductor para la pantalla completa, el subtítulo, el silencio y la imagen en las propiedades de la imagen".'
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: cd51ed3a-fe37-41e9-8243-dfd9deb514c1
feature: Media Analytics, Variables
role: User, Admin, Data Engineer
source-git-commit: c53c97ce06a5a6e2e7d7b20ed06b097a29b71fcb
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 96%

---

# Parámetros de estado del reproductor{#player-state-parameters}

En este tema se presenta una lista de los datos del estado del reproductor que Adobe recopila a través de variables de solución.

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

## Propiedades de estado del reproductor {#player-state-properties}

La funcionalidad de seguimiento de estado del reproductor se puede adjuntar a un flujo de audio o vídeo. Las métricas de seguimiento de estado del reproductor estandarizado se almacenan como variables de solución. Los estados estándar son: fullScreen, mute, closeCaption, pictureInPicture, and inFocus.

### Propiedades de pantalla completa

#### Transmisiones afectadas por Pantalla completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> cantidad de transmisiones afectadas por la pantalla completa. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de pantalla completa durante una sesión de reproducción. <br/> **Importante:**<br/> si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.state.fullscreen.set<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre de informe:**<br/> Transmisiones afectadas por pantalla completa </li> <li> **Datos de contexto:**<br/> a.media.state.fullscreen.set<br/> </li> <li> **Fuente de datos:**<br/> videostatefullscreen </li> <li> **Audience Manager:**<br/> c_contextdata.a.media.states.fullscreen.set </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet </li> </ul> |

#### Recuento de Pantalla completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> La cantidad de veces que se ha mostrado una pantalla completa. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de pantalla completa durante una sesión de reproducción. <br/> **Importante:**<br/> Si se establece este evento, el recuento es igual al número de veces que el vídeo estaba en el estado de pantalla completa. Si no se establece este evento, no se enviará ningún valor.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.fullscreen.count<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Recuento de pantalla completa </li> <li> **Datos de contexto:**<br/> a.media.states.fullscreen.count<br/> </li> <li> **Fuente de datos:**<br/> videostatefullscreencount </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.fullscreen.count </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount </li> </ul> |



#### Duración total de Pantalla completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> El tiempo que se ha mostrado una pantalla completa. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de pantalla completa durante una sesión de reproducción. <br/> **Importante:**<br/> Si se establece este evento, la hora es igual a la duración del vídeo en el estado de pantalla completa. Si no se establece este evento, no se enviará ningún valor.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.fullscreen.time<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Duración total de pantalla completa </li> <li> **Datos de contexto:**<br/> a.media.states.fullscreen.time<br/> </li> <li> **Fuente de datos:**<br/> videostatefullscreentime </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.fullscreen.time </li> <li> **Ruta de campo XDM:**<br/>  media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime </li> </ul> |


### Propiedades de subtítulos

#### Transmisiones afectadas por Subtítulos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> cantidad de transmisiones afectadas por los subtítulos. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de subtítulo durante una sesión de reproducción. <br/> **Importante:**<br/> si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.closedcaptioning.set<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre de informe:**<br/> Transmisiones afectadas por los subtítulos </li> <li> **Datos de contexto:**<br/> a.media.states.closedcaptioning.set<br/> </li> <li> **Fuente de datos:**<br/> videostateclosedcaptioning </li> <li> **Audience Manager:**<br/> c_contextdata.a.media.states.closedcaptioning.set </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet </li> </ul> |


#### Recuento de Subtítulos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> La cantidad de veces que se han mostrado Subtítulos. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de subtítulo durante una sesión de reproducción. <br/> **Importante:**<br/> Si se establece este evento, el recuento es igual al número de veces que el vídeo estaba en el estado Subtítulos. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.closedcaptioning.count<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre de informe:**<br/> Recuento de subtítulos </li> <li> **Datos de contexto:**<br/> a.media.states.closedcaptioning.count<br/> </li> <li> **Fuente de datos:**<br/> videostateclosedcaptioningcount </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.closedcaptioning.count </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount </li> </ul> |


#### Duración total de Subtítulos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> La cantidad de tiempo que se ha mostrado Subtítulos. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de pantalla completa durante una sesión de reproducción. <br/> **Importante:**<br/> Si se establece este evento, la hora es igual a la duración del vídeo en el estado Subtítulos. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.closedcaptioning.time<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre de informe:**<br/> Duración total de los subtítulos </li> <li> **Datos de contexto:**<br/> a.media.states.closedcaptioning.time<br/> </li> <li> **Fuente de datos:**<br/> videostateclosedcaptioningtime </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.closedcaptioning.time </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime </li> </ul> |


### Propiedades de Silenciar

#### Transmisiones afectadas por Silenciar

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> número de emisiones afectadas por Silenciar. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Silenciar durante una sesión de reproducción. <br/> **Importante:**<br/> si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.mute.set<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre de informe:**<br/> de Transmisiones afectadas por Silenciar </li> <li> **Datos de contexto:**<br/> a.media.states.mute.set<br/> </li> <li> **Fuente de datos:**<br/> videostatemute </li> <li> **Audience Manager:**<br/> c_contextdata.a.media.states.mute.set </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet </li> </ul> |

#### Recuentos de Silenciar

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> La cantidad de veces que se ha mostrado Silenciar. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Silenciar durante una sesión de reproducción. <br/> **Importante:**<br/> Si se establece este evento, el recuento es igual al número de veces que el vídeo estaba en estado Silenciar. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.mute.count<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre de informe:**<br/> Cantidad de Silenciar </li> <li> **Datos de contexto:**<br/> a.media.states.mute.count<br/> </li> <li> **Fuente de datos:**<br/> videostatemutecount </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.mute.count </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount </li> </ul> |

#### Duración total de Silenciar

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> La cantidad de tiempo que se ha mostrado Silenciar. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Silenciar durante una sesión de reproducción. <br/> **Importante:**<br/> Si se establece este evento, la hora es igual a la duración del vídeo en el estado Silenciar. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.mute.time<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre de informe:**<br/> Duración total de Silenciar </li> <li> **Datos de contexto:**<br/> a.media.states.mute.time<br/> </li> <li> **Fuente de datos:**<br/> videostatemutetime </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.mute.time </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime </li> </ul> |


### Propiedades de Imagen en imagen


#### Transmisiones afectadas por Imagen en imagen

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> Cantidad de transmisiones afectadas por Imagen en imagen. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Imagen en imagen durante una sesión de reproducción. <br/> **Importante:**<br/> si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.pictureinpicture.set<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre de informe:**<br/> Transmisiones afectadas por Imagen en imagen </li> <li> **Datos de contexto:**<br/> a.media.states.pictureinpicture.set<br/> </li> <li> **Fuente de datos:**<br/> videostatepictureinpicture </li> <li> **Audience Manager:**<br/> c_contextdata.a.media.states.pictureinpicture.set </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet </li> </ul> |


#### Recuentos de Imagen en imagen

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> La cantidad de veces que se ha mostrado Imagen en imagen. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Imagen en imagen durante una sesión de reproducción. <br/> **Importante:** <br/> Si se establece este evento, el recuento es igual al número de veces que el vídeo estaba en el estado Imagen en imagen. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.pictureinpicture.count<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Cantidad de Imagen en imagen </li> <li> **Datos de contexto:**<br/> a.media.states.pictureinpicture.count<br/> </li> <li> **Fuente de datos:**<br/> videostatepictureinpicturecount </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.pictureinpicture.count </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount </li> </ul> |


#### Duración total de Imagen en imagen

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> Duración de la visualización de la imagen en imagen. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Imagen en imagen durante una sesión de reproducción. <br/> **Importante:** <br/> Si se establece este evento, la hora es igual a la duración del vídeo en el estado Imagen en imagen. Si no se establece este evento, no se enviará ningún valor..   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.pictureinpicture.time<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Duración total de Imagen en imagen </li> <li> **Datos de contexto:**<br/> a.media.states.pictureinpicture.time<br/> </li> <li> **Fuente de datos:**<br/> videostatepictureinpicturetime </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.pictureinpicture.time </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime </li> </ul> |


### Propiedades de Enfocado

#### Transmisiones afectadas por Enfocado

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> número de emisiones afectadas por Enfocado. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Enfocado durante una sesión de reproducción. <br/> **Importante:**<br/> si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.infocus.set<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre de informe:**<br/> Transmisiones afectadas por Enfocado </li> <li> **Datos de contexto:**<br/> a.media.states.infocus.set<br/> </li> <li> **Fuente de datos:**<br/> videostateinfocus </li> <li> **Audience Manager:**<br/> c_contextdata.a.media.states.infocus.set </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet </li> </ul> |


#### Recuentos de Enfocado

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> La cantidad de veces que se ha visualizado Enfocado. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Enfocado durante una sesión de reproducción. <br/> **Importante:**<br/> Si se establece este evento, el recuento es igual al número de veces que el vídeo estaba en el estado Enfoque. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.infocus.count<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Recuento de Enfocados </li> <li> **Datos de contexto:**<br/> a.media.states.infocus.count<br/> </li> <li> **Fuente de datos:**<br/> videostateinfocuscount </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.infocus.count </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount </li> </ul> |


#### Duración total de Enfocado

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente  </li> <li> **Clave de API:**<br/> N/D </li> <li> **Obligatorio:**<br/> no </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> cierre de medios </li> <li> **Mínima Versión de SDK:**<br/> 3.0</li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/> La cantidad de tiempo que se ha visualizado Enfocado. Esta métrica se define como 1 solo si tuvo lugar al menos un estado de Enfocado durante una sesión de reproducción. <br/> **Importante:** <br/> Si se establece este evento, la hora es igual a la duración del vídeo en el estado Enfoque. Si no se establece este evento, no se enviará ningún valor.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.infocus.time<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Duración total del Enfoque </li> <li> **Datos de contexto:**<br/> a.media.states.infocus.time<br/> </li> <li> **Fuente de datos:**<br/> videostateinfocustime </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.infocus.time </li> <li> **Ruta de campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime </li> </ul> |


## API relacionadas {#related_apis_section}

* Android: [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS: [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* JavaScript: [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
