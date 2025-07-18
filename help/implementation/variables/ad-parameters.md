---
title: 'Parámetros de anuncio '
description: Obtenga información acerca de los parámetros de publicidad, incluidas las variables de implementación, red e informes para los datos de vídeo de anuncio.
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 89%

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
>&#x200B;>se describan en Informes/Variables reservadas como “clasificación”.
>&#x200B;>Las clasificaciones de contenidos se definen cuando un grupo de informes está habilitado para los contenidos
>&#x200B;>seguimiento. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede,
>&#x200B;>los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las nuevas
>&#x200B;>propiedades de contenidos. Durante el proceso de actualización, Adobe determina si las
>&#x200B;>clasificaciones están habilitadas comprobando los nombres de las variables. Si alguna de ellas
>&#x200B;>falta, Adobe las agrega de nuevo.

## Datos de vídeo de anuncio {#ad-video-data}

### ID de anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.id </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** cualquiera  </li> <li> **Valor de muestra:**<br/> “2125” </li><li> **Descripción:**<br/> ID del anuncio. (Cualquier combinación de cifras y/o letras)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **Latido:**<br/> (<code>s:asset:ad_id</code>) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según VISIT </li> <li> **Nombre del informe:**<br/> Anuncio </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>name) </li> <li> **Fuente de datos:**<br/> videoad </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetReference._id </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.name </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.name </li> </ul> |



### Posición del anuncio en la secuencia

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.podPosition </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 1 </li><li> **Descripción:**<br/> La posición (índice) del anuncio dentro del salto de anuncio principal. El primer anuncio tiene el índice 0, el segundo tiene el índice 1, etc.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Latido:**<br/> (<code>s:asset:pod_position</code>) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Posición del anuncio en la secuencia </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Fuente de datos:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.index </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.podPosition </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.podPosition </li> </ul> |



### Duración del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.length </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** 1.5.1 </li> <li> **Valor de muestra:**<br/> “15”  </li><li> **Descripción:**<br/> Duración del anuncio de vídeo en segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **Latido:**<br/> (<code>l:asset:ad_length</code>) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar y clasificación </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Duración del anuncio y Duración del anuncio (variable) </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>length) </li> <li> **Fuente de datos:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetReference.<br/>_xmpDM.duration </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.length </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.length </li> </ul> |



### Nombre del reproductor del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.playerName </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> “Freewheel” </li><li> **Descripción:**<br/> Nombre del reproductor responsable de procesar el anuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Heartbeat:**<br/> (<code>s:sp:player_name</code>) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Nombre del reproductor del anuncio </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Fuente de datos:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.playerName </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.<br/>playerName </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.<br/>playerName </li> </ul> |



### Nombre del desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.podFriendlyName </li> <li> **Obligatorio:**<br/> SDK: Sí; API: No. </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> “anuncio previo a la emisión” </li><li> **Descripción:**<br/> Nombre descriptivo del desglose de anuncios.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Heartbeat:**<br/> (<code>s:asset:pod_name</code>) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> clasificación </li> <li> **Nombre del informe:**<br/> Nombre de secuencia </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.<br/>adBreak._dc.title </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingPodDetails.<br/>friendlyName </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingPodDetails.<br/>friendlyName </li> </ul> |



### Índice del desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.podIndex </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> </li> <li> **Mínima mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 1 </li><li> **Descripción:**<br/>&#x200B;Índice de desglose de anuncios dentro del contenido que comienza en 1. Esta propiedad la utiliza **solo** el Media SDK para generar el ID de la secuencia.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> no </li> <li> **Variable reservada:**<br/> N/D </li> <li> **Nombre del informe:**<br/> N/D </li> <li> **Datos de contexto:**<br/> </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.index </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingPodDetails.index </li> </ul> |



### Posición de desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.podSecond </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 90 </li><li> **Descripción:**<br/> El desplazamiento del desglose de anuncios dentro del contenido, en segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Latido:**<br/> (<code>l:asset:pod_offset</code>) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> clasificación </li> <li> **Nombre del informe:**<br/> Posición de secuencia </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.adBreak.<br/>offset </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingPodDetails.<br/>offset </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingPodDetails.<br/>offset </li> </ul> |



### ID de desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **Latido:**<br/> (<code>s:asset:pod_id</code>) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Pod de anuncios </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>pod) </li> <li> **Fuente de datos:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.adBreak._id </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingPodDetails.<br/>ID </li> </ul> |



### Nombre de publicidad

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/> media.ad.name </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** 1.5.1 </li> <li> **Valor de muestra:**<br/> “Ford F-150” </li><li> **Descripción:**<br/> Nombre descriptivo del desglose de anuncios.  En los informes, “Nombre del anuncio” es la clasificación y “Nombre del anuncio (variable)” es la eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Latido:**<br/> (<code>s:asset:ad_name</code>) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar y clasificación </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Nombre del anuncio y Nombre del anuncio (variable) </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Fuente de datos:**<br/> videoadname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetReference._dc.title </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.friendlyName </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.friendlyName </li> </ul> |



## Metadatos de anuncio estándar {#standard-ad-metadata}

### Anunciante

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> ADVERTISER </li> <li> **Clave de API:**<br/> media.ad.advertiser </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>  </li><li> **Descripción:**<br/> Empresa/marca de cuyo producto se hace publicidad en el anuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Latido:**<br/> (<code>s:meta:</code><br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> <i>Anunciante </i> </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Fuente de datos:**<br/> videoadadvertiser </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetReference.advertiser </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.advertiser </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.advertiser </li> </ul> |



### ID de campaña

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> CAMPAIGN_ID </li> <li> **Clave de API:**<br/> media.ad.campaignId </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> Total o nombre (cadena).  </li><li> **Descripción:**<br/> ID de la campaña de publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>campaign) </li> <li> **Latido:**<br/> (<code>s:meta:</code><br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> <i>ID de campaña </i> </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>campaign) </li> <li> **Fuente de datos:**<br/> videoadcampaign </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.campaign) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetReference.campaign </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.<br/>campaignID </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.<br/>campaignID </li> </ul> |



### ID del creativo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> CREATIVE_ID </li> <li> **Clave de API:**<br/> media.ad.creativeId </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> Total o nombre (cadena).  </li><li> **Descripción:**<br/> ID del creativo de publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creative) </li> <li> **Latido:**<br/> (<code>s:meta:</code><br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> <i>ID del creativo </i> </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>creative) </li> <li> **Fuente de datos:**<br/> adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetReference.creativeID </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.creativeID </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.creativeID </li> </ul> |



### ID del sitio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> SITE_ID </li> <li> **Clave de API:**<br/> media.ad.siteId </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>  </li><li> **Descripción:**<br/> ID del sitio de publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>site) </li> <li> **Latido:**<br/> (<code>s:meta:</code><br/>a.media.ad.site) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Utilizar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>site) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetReference.siteID </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.siteID </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.siteID </li> </ul> |



### URL del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> CREATIVE_URL </li> <li> **Clave de API:**<br/> media.ad.creativeURL </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>  </li><li> **Descripción:**<br/> URL del creativo de publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Heartbeat:**<br/> (<code>s:meta:&lt;c/ode><br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Utilizar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetReference.creativeURL </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.<br/>creativeURL </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.<br/>creativeURL </li> </ul> |



### ID de colocación

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> PLACEMENT_ID </li> <li> **Clave de API:**<br/> media.ad.placementId </li> <li> **Requerido:**<br/> no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Mínima mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/>  </li><li> **Descripción:**<br/> ID de colocación de la publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>placement) </li> <li> **Latido:**<br/> (<code>s:meta:</code><br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Utilizar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/> eVar </li> <li> **Caducidad:**<br/> según HIT </li> <li> **Nombre del informe:**<br/> Personalizado </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>placement) </li> <li> **Fuente de datos:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.adAssetReference.placementID </li> <li> **Ruta del campo XDM de recopilación:**<br/> mediaCollection.advertisingDetails.<br/>placementID </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.<br/>placementID </li> </ul> |




## Métricas del anuncio {#ad-metrics}

### Inicio del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad </li> <li> **Mínima mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> “TRUE” </li><li> **Descripción:**<br/> Número de inicios de anuncios de vídeo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>view) </li> <li> **Heartbeat:**<br/> (<code>s:event:type=start</code>)<br/> (<code>s:asset:type=ad<code>) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Inicios de publicidad </li> <li> **Fuente de datos:**<br/> videoadstart </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>view) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.view) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.impressions.value > 0 => &quot;TRUE&quot; </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.isStarted </li> </ul> |



### Publicidad completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> cierre de publicidad </li> <li> **Mínima mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> “TRUE” </li><li> **Descripción:**<br/> Número de anuncios de vídeo completados.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>complete) </li> <li> **Heartbeat:**<br/> (<code>s:event:type=complete</code>)<br/> (<code>s:asset:type=ad</code>)  </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Finalizaciones de publicidad </li> <li> **Fuente de datos:**<br/> videoadcomplete </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.completes.value > 0 => &quot;TRUE&quot; </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.<br/>isCompleted </li> </ul> |



### Tiempo invertido en publicidad

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clave de SDK:**<br/> establecida automáticamente </li> <li> **Clave de API:**<br/> N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> cierre de publicidad </li> <li> **Mínima mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 15 </li><li> **Descripción:**<br/> Cantidad total de tiempo, en segundos, que se emplea para mirar la publicidad (es decir, el número de segundos reproducidos).  El valor se mostrará con formato de hora (<code>HH:MM:SS</code>) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/>**Fecha de la versión: 13/9/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/> evento </li> <li> **Nombre del informe:**<br/> Tiempo invertido en publicidad </li> <li> **Fuente de datos:**<br/> videoadtime </li> <li> **Datos de contexto:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> <li> **Ruta de campo XDM:** (obsoleto)<br/> advertising.timePlayed.value </li> <li> **Ruta del campo XDM de creación de informes:**<br/> mediaReporting.advertisingDetails.<br/>timePlayed </li> </ul> |



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
