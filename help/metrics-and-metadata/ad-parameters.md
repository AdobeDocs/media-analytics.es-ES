---
title: Parámetros de anuncio
description: null
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Parámetros de anuncio{#ad-parameters}

En este tema se presenta una lista de datos de anuncios de vídeo, incluidos los valores de datos de contexto, que Adobe recopila a través de variables de solución.

Descripción de los datos de la tabla:

* **Implementación**: información sobre los valores y requisitos de implementación.
   * *Clave*: variable que se establece manualmente en la aplicación o automáticamente mediante el Adobe Media SDK.
   * *Requerido*: indica si el parámetro es necesario para el seguimiento básico de vídeos.
   * *Tipo*: especifica el tipo de variable que se va a definir, una cadena o un número.
   * *Enviado con* : indica cuándo se envían los datos: Inicio *de* medios es la llamada de análisis que se envía al inicio de medios, Inicio de *publicidad* es la llamada de análisis que se envía al inicio de anuncio, etc.; las llamadas de *cierre* son las llamadas de análisis compiladas que se envían directamente desde el servidor de Heartbeat al servidor de Analytics al final de la sesión de medios o al final del anuncio, capítulo, etc. Las llamadas de cierre no están disponibles en llamadas de paquetes de red.
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
>No cambie los nombres de clasificación de ninguna de las variables enumeradas a continuación que
>se describe en Informes/Variable reservada como "clasificación".
>Las clasificaciones de medios se definen cuando un grupo de informes está habilitado para los medios
>seguimiento. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede,
>los clientes deben volver a habilitar sus grupos de informes para obtener acceso a los nuevos medios
>propiedades. Durante el proceso de actualización, Adobe determina si la variable
>las clasificaciones se habilitan comprobando los nombres de las variables. Si alguno de los
>faltan, Adobe agrega los que faltan de nuevo.

## Datos de vídeo de anuncio {#ad-video-data}

### ID de anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.id </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera  </li> <li> ****<br/> Valor de muestra: "2125" </li><li> **Descripción:**<br/>ID de la publicidad. (Cualquier combinación de cifras y/o letras)  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>name) </li> <li> ****<br/> Heartbeat: (s:asset:ad_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Anuncio </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>name) </li> <li> **Fuente de datos:**<br/>videoad </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### Posición del anuncio en la secuencia

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.podPosition </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 1 </li><li> **Descripción:**<br/>la posición (índice) de la publicidad dentro de la pausa publicitaria principal. El primer anuncio tiene el índice 0, el segundo tiene el índice 1, etc.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>podPosition) </li> <li> ****<br/> Heartbeat: (s:asset:pod_position) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Posición del anuncio en la secuencia </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>podPosition) </li> <li> **Fuente de datos:**<br/>videoadinpod </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Duración del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.length </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.1 </li> <li> ****<br/> Valor de muestra: "15"  </li><li> **Descripción:**<br/>Duración del anuncio de vídeo en segundos.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>length) </li> <li> ****<br/> Heartbeat: (l:asset:ad_length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar y clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Duración del anuncio y Duración del anuncio (variable) </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>length) </li> <li> **Fuente de datos:**<br/>videoadlength </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### Nombre del reproductor del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.playerName </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: "FreeWheel" </li><li> **Descripción:**<br/>El nombre del reproductor responsable de la representación del anuncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>playerName) </li> <li> ****<br/> Heartbeat: (s:sp:player_name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Nombre del reproductor del anuncio </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>playerName) </li> <li> **Fuente de datos:**<br/>videoadplayername </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Nombre del desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.podFriendlyName </li> <li> ****<br/> Requerido: SDK:Sí; API:No. </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: "pre-roll" </li><li> **Descripción:**<br/>El nombre descriptivo del intervalo de anuncios.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>podFriendlyName) </li> <li> ****<br/> Heartbeat: (s:asset:pod_name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Nombre de secuencia </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>podFriendlyName) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Índice del desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.podPosition </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 1 </li><li> **Descripción:**<br/>índice del desglose de publicidad dentro del contenido que empieza en 1. Esta propiedad la utiliza **solo** el Media SDK para generar el ID de la secuencia.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/>no </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>N/D </li> <li> **Datos de contexto:**<br/> </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Posición de desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.podSecond </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 90 </li><li> **Descripción:**<br/>desplazamiento de la pausa publicitaria dentro del contenido, en segundos.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>podSecond) </li> <li> ****<br/> Heartbeat: (l:asset:pod_offset) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Posición de secuencia </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>podSecond) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID de desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>pod) </li> <li> ****<br/> Heartbeat: (s:asset:pod_id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Pod de anuncios </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>pod) </li> <li> **Fuente de datos:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Nombre de publicidad

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.name </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.1 </li> <li> ****<br/> Valor de muestra: "Ford F-150" </li><li> **Descripción:Nombre**<br/>descriptivo de la publicidad.  En los informes, "Nombre del anuncio" es la clasificación y "Nombre del anuncio (variable)" es la eVar.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>friendlyName) </li> <li> ****<br/> Heartbeat: (s:asset:ad_name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar y clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Nombre del anuncio y Nombre del anuncio (variable) </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>friendlyName) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Metadatos de anuncio estándar {#standard-ad-metadata}

### Anunciante

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>ADVERTISER </li> <li> **Clave de API:**<br/>media.ad.advertiser </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>Empresa/Marca cuyo producto aparece en la publicidad.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>anunciante) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i>Anunciante </i> </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>anunciante) </li> <li> **Fuente de datos:**<br/>videoadvertiser </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### ID de campaña

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>CAMPAIGN_ID </li> <li> **Clave de API:**<br/>media.ad.campaignId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> ****<br/> Valor de muestra: Entero o nombre (cadena).  </li><li> **Descripción:**<br/>ID de la campaña de publicidad.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>campaign) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.campagn) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i>ID de campaña </i> </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>campaign) </li> <li> **Fuente de datos:**<br/>videocampaign </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### ID del creativo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>CREATIVE_ID </li> <li> **Clave de API:**<br/>media.ad.creativeId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> ****<br/> Valor de muestra: Entero o nombre (cadena).  </li><li> **Descripción:**<br/>ID del elemento creativo de la publicidad.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>creative) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i>ID del creativo </i> </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>creative) </li> <li> **Fuente de datos:**<br/>adclassificationcreative </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### ID del sitio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SITE_ID </li> <li> **Clave de API:**<br/>media.ad.siteId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>ID del sitio de publicidad.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>site) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Usar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i> </i> </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>site) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### URL del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>CREATIVE_URL </li> <li> **Clave de API:**<br/>media.ad.creativeURL </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>URL del elemento creativo de la publicidad.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>creativeURL) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Usar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i> </i> </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>creativeURL) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### ID de colocación

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>PLACEMENT_ID </li> <li> **Clave de API:**<br/>media.ad.placementId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:ID**<br/>de ubicación de la publicidad.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>ubicación) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Usar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i> </i> </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>ubicación) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Métricas del anuncio {#ad-metrics}

### Inicio de publicidad

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/>inicio de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: TRUE </li><li> **Descripción:**<br/>Número de inicios de anuncios de vídeo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>view) </li> <li> ****<br/> Heartbeat:  (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Inicios de publicidad </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>view) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### Publicidad completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/>cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: TRUE </li><li> **Descripción:**<br/>Número de finalizaciones de anuncios de vídeo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>complete) </li> <li> ****<br/> Heartbeat: (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Finalizaciones de publicidad </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>complete) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### tiempo invertido en publicidad

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/>cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 15 </li><li> **Descripción:**<br/>la cantidad total de tiempo, en segundos, dedicado a ver el anuncio (es decir, el número de segundos reproducidos).  El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/>**Fecha de la versión: 13/9/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Tiempo invertido en publicidad </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Datos de contexto: (a.media.ad.<br/>timePlayed) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## API relacionadas {#section_Related_APIs}

### API createAdObject:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### API createAdBreakObject:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### API de MediaHeartbeatConfig:

* Android: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS: [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

