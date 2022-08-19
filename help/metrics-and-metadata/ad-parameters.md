---
title: 'Parámetros de anuncio '
description: “Obtenga información sobre los parámetros de publicidad, incluidas las variables de implementación, red e informes para los datos de vídeo de anuncio”.
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 01afcf648f13af4d47b5fb41b7c9e89c2a89f590
workflow-type: tm+mt
source-wordcount: '2108'
ht-degree: 91%

---

# Parámetros de anuncio {#ad-parameters}

En este tema se presenta una lista de datos de anuncios de vídeo, incluidos los valores de datos de contexto, que Adobe recopila a través de variables de solución.

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
   * *Audience Manager:* Nombre de la función de Adobe Audience Manager.

>[!IMPORTANT]
>
>No cambie los nombres de clasificación de ninguna de las variables enumeradas a continuación que
>se describan en Informes/Variables reservadas como “clasificación”.
>Las clasificaciones de contenidos se definen cuando un grupo de informes está habilitado para los contenidos
>seguimiento. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede,
>los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las nuevas
>propiedades de contenidos. Durante el proceso de actualización, Adobe determina si las
>clasificaciones están habilitadas comprobando los nombres de las variables. Si alguna de ellas
>falta, Adobe las agrega de nuevo.

## Datos de vídeo de anuncio {#ad-video-data}

### ID de anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.id </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:** Cualquiera  </li> <li> **Valor de muestra:**<br/> “2125” </li><li> **Descripción:**<br/> ID del anuncio. (Cualquier combinación de cifras y/o letras)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **Heartbeat:**<br/> (s:asset:ad_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según VISIT </li> <li> **Nombre del informe:**<br/> Anuncio </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>name) </li> <li> **Fuente de datos:**<br/> videoad </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetReference.@id </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.ID </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.ID </li> </ul> |



### Posición del anuncio en la secuencia

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.podPosition </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:** Cualquiera </li> <li> **Valor de muestra:**<br/> 1 </li><li> **Descripción:**<br/> La posición (índice) del anuncio dentro del salto de anuncio principal. El primer anuncio tiene el índice 0, el segundo tiene el índice 1, etc.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Heartbeat:**<br/> (s:asset:pod_position) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Posición del anuncio en la secuencia </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Fuente de datos:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetViewDetails.index </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.index </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.index </li> </ul> |



### Duración del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.length </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:**  1.5.1 </li> <li> **Valor de muestra:**<br/> “15”  </li><li> **Descripción:**<br/> Duración del anuncio de vídeo en segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **Heartbeat:**<br/> (l:asset:ad_length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar y clasificación </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Duración del anuncio y Duración del anuncio (variable) </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>length) </li> <li> **Fuente de datos:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetReference.<br/>xmpDM:duration </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.length </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.length </li> </ul> |



### Nombre del reproductor del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.playerName </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:** Cualquiera </li> <li> **Valor de muestra:**<br/> “Freewheel” </li><li> **Descripción:**<br/> Nombre del reproductor responsable de procesar el anuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Heartbeat:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Nombre del reproductor del anuncio </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Fuente de datos:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetViewDetails.playerName </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.<br/>playerName </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.<br/>playerName </li> </ul> |



### Nombre del desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.podFriendlyName </li> <li> **Obligatorio:**<br/> SDK:Sí; API:No. </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:** Cualquiera </li> <li> **Valor de muestra:**<br/> “anuncio previo a la emisión” </li><li> **Descripción:**<br/> Nombre descriptivo del desglose de anuncios.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Heartbeat:**<br/> (s:asset:pod_name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> clasificación </li> <li> **Nombre del informe:**<br/> Nombre de secuencia </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetViewDetails.<br/>adBreak.dc:title </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingPodDetails.<br/>friendlyName </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingPodDetails.<br/>friendlyName </li> </ul> |



### Índice del desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.podPosition </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> </li> <li> **Mínima Versión de SDK:** Cualquiera </li> <li> **Valor de muestra:**<br/> 1 </li><li> **Descripción:**<br/>&#x200B;Índice de desglose de anuncios dentro del contenido que comienza en 1. Esta propiedad la utiliza **solo** el Media SDK para generar el ID de la secuencia.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> no </li> <li> **Variable reservada:**<br/> N/D </li> <li> **Nombre del informe:**<br/> N/D </li> <li> **Datos de contexto:**<br/> </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetViewDetails.index </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingPodDetails.index </li> </ul> |



### Posición de desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.podSecond </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:** Cualquiera </li> <li> **Valor de muestra:**<br/> 90 </li><li> **Descripción:**<br/> El desplazamiento del desglose de anuncios dentro del contenido, en segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Heartbeat:**<br/> (l:asset:pod_offset) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> clasificación </li> <li> **Nombre del informe:**<br/> Posición de secuencia </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetViewDetails.adBreak.<br/>offset </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingPodDetails.<br/>second </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingPodDetails.<br/>segundo </li> </ul> |



### ID de desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:** Cualquiera </li> <li> **Valor de muestra:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **Heartbeat:**<br/> (s:asset:pod_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Pod de anuncios </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>pod) </li> <li> **Fuente de datos:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetViewDetails.adBreak.@id </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingPodDetails.<br/>adBreakID </li> </ul> |



### Nombre de publicidad

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.name </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:**  1,5,1 </li> <li> **Valor de muestra:**<br/> “Ford F-150” </li><li> **Descripción:**<br/> Nombre descriptivo del desglose de anuncios.  En los informes, &quot;Nombre del anuncio&quot; es la clasificación y &quot;Nombre del anuncio (variable)&quot; es la eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:asset:ad_name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar y clasificación </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Nombre del anuncio y Nombre del anuncio (variable) </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetReference.dc:title </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.name </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.name </li> </ul> |



## Metadatos de anuncio estándar {#standard-ad-metadata}

### Anunciante

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> ADVERTISER </li> <li> **Clave de API:**<br/> media.ad.advertiser </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:**  1.5.7 </li> <li> **Valor de muestra:**<br/>  </li><li> **Descripción:**<br/> Empresa/marca de cuyo producto se hace publicidad en el anuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> <i>Anunciante </i> </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Fuente de datos:**<br/> videoadvertiser </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetReference.advertiser </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.advertiser </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.advertiser </li> </ul> |



### ID de campaña

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> CAMPAIGN_ID </li> <li> **Clave de API:**<br/> media.ad.campaignId </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:**  1,5,7 </li> <li> **Valor de muestra:**<br/> Total o nombre (cadena).  </li><li> **Descripción:**<br/> ID de la campaña de publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>campaign) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> <i>ID de campaña </i> </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>campaign) </li> <li> **Fuente de datos:**<br/> videocampaign </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.campaign) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetReference.campaign </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.<br/>campaignID </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.<br/>campaignID </li> </ul> |



### ID del creativo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> CREATIVE_ID </li> <li> **Clave de API:**<br/> media.ad.creativeId </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:**  1,5,7 </li> <li> **Valor de muestra:**<br/> Total o nombre (cadena).  </li><li> **Descripción:**<br/> ID del creativo de publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creative) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> <i>ID del creativo </i> </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>creative) </li> <li> **Fuente de datos:**<br/> adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetReference.creativeID </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.creativeID </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.creativeID </li> </ul> |



### ID del sitio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> SITE_ID </li> <li> **Clave de API:**<br/> media.ad.siteId </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:**  1,5,7 </li> <li> **Valor de muestra:**<br/>  </li><li> **Descripción:**<br/> ID del sitio de publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>site) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Utilizar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>site) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetReference.siteID </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.siteID </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.siteID </li> </ul> |



### URL del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> CREATIVE_URL </li> <li> **Clave de API:**<br/> media.ad.creativeURL </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:**  1,5,7 </li> <li> **Valor de muestra:**<br/>  </li><li> **Descripción:**<br/> URL del creativo de publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Utilizar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetReference.creativeURL </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.<br/>creativeURL </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.<br/>creativeURL </li> </ul> |



### ID de colocación

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> PLACEMENT_ID </li> <li> **Clave de API:**<br/> media.ad.placementId </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima Versión de SDK:**  1,5,7 </li> <li> **Valor de muestra:**<br/>  </li><li> **Descripción:**<br/> ID de colocación de la publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>placement) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Utilizar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>placement) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> <li> **Ruta de campo XDM:**<br/> advertising.adAssetReference.placementID </li> <li> **Ruta de campo XDM de colección:**<br/> mediaCollection.advertisingDetails.<br/>placementID </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.<br/>placementID </li> </ul> |




## Métricas del anuncio {#ad-metrics}

### Inicio del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad </li> <li> **Mínima Versión de SDK:** Cualquiera </li> <li> **Valor de muestra:**<br/> “TRUE” </li><li> **Descripción:**<br/> Número de inicios de anuncios de vídeo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>view) </li> <li> **Ruta de campo XDM:**<br/> (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Inicios de publicidad </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>view) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.view) </li> <li> **Ruta de campo XDM:**<br/> advertising.starts.value > 0 => &quot;TRUE&quot; </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.isStarted </li> </ul> |



### Publicidad completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> cierre de publicidad </li> <li> **Mínima Versión de SDK:** Cualquiera </li> <li> **Valor de muestra:**<br/> “TRUE” </li><li> **Descripción:**<br/> Número de anuncios de vídeo completados.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>complete) </li> <li> **Heartbeat:**<br/> (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Finalizaciones de publicidad </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> <li> **Ruta de campo XDM:**<br/> advertising.completes.value > 0 => &quot;TRUE&quot; </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.<br/>isCompleted </li> </ul> |



### Tiempo invertido en publicidad

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> cierre de publicidad </li> <li> **Mínima Versión de SDK:** Cualquiera </li> <li> **Valor de muestra:**<br/> 15 </li><li> **Descripción:**<br/> Cantidad total de tiempo, en segundos, que se emplea para mirar la publicidad (es decir, el número de segundos reproducidos).  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace e Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/>**Fecha de la versión: 13/9/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Tiempo invertido en publicidad </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> <li> **Ruta de campo XDM:**<br/> advertising.timePlayed.value </li> <li> **Ruta de campo XDM de informes:**<br/> mediaReporting.advertisingDetails.<br/>timePlayed </li> </ul> |



## API relacionadas {#section_Related_APIs}

### API createAdObject:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### API createAdBreakObject:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### API MediaHeartbeatConfig:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)
