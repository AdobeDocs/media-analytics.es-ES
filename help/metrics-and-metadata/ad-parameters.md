---
seo-title: Parámetros de anuncio
title: Parámetros de anuncio
uuid: 92 cd 7 f 97-bb 5 a -4 de 6-8946-453 d 30271 d 0 f
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# Parámetros de anuncio{#ad-parameters}

En este tema se presenta una lista de datos de anuncios de vídeo, incluidos los valores de datos de contexto, que Adobe recopila a través de variables de solución.

Descripción de los datos de la tabla:

* **Implementación**: información sobre los valores y requisitos de implementación.
   * *Clave*: variable que se establece manualmente en la aplicación o automáticamente mediante el Adobe Media SDK.
   * *Requerido*: indica si el parámetro es necesario para el seguimiento básico de vídeos.
   * *Tipo*: especifica el tipo de variable que se va a definir, una cadena o un número.
   * *Enviado con* : Indica cuándo se envían los datos: *Start Start* es la llamada de análisis enviada al inicio de medios, Inicio *de anuncio* es la llamada de análisis enviada al inicio de la publicidad, etc. Las *llamadas Cerrar* son las llamadas de análisis compiladas enviadas directamente desde el servidor de Heartbeat al servidor de Analytics al final de la sesión de medios, o al final de la publicidad, capítulo, etc. Las llamadas Cerrar no están disponibles en llamadas de paquetes de red.
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
>No cambie los nombres de clasificación de las variables enumeradas a continuación
>descrita en Informes/Variable reservada como "clasificación".
>Las clasificaciones de medios se definen cuando un grupo de informes está habilitado para medios
>seguimiento. Cada cierto tiempo, Adobe agrega nuevas propiedades y, cuando esto ocurre,
>Los clientes deben volver a habilitar sus grupos de informes para obtener acceso al nuevo medio
>propiedades. Durante el proceso de actualización, Adobe determina si la variable
>las clasificaciones se habilitan marcando los nombres de las variables. Si alguno de
>faltan, Adobe agrega los que faltan de nuevo.

## Datos de vídeo de anuncio {#section_hq3_nbv_51b}

### ID de anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.id </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera  </li> <li> **Valor de muestra:**<br/> " 2125 " </li><li> **Descripción:**<br/>ID del anuncio. (Cualquier combinación de cifras y/o letras)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>name) </li> <li> **Heartbeat:**<br/> (s: recurso: ad_ id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según VISIT </li> <li> **Nombre del informe:**<br/>Anuncio </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>name) </li> <li> **Fuente de datos:**<br/>videoad </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.name) </li> </ul> |



### Posición del anuncio en la secuencia

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.podPosition </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 1 </li><li> **Descripción:**<br/>Posición (índice) del anuncio dentro de la pausa publicitaria principal. El primer anuncio tiene el índice 0, el segundo tiene el índice 1, etc.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Podposition) </li> <li> **Heartbeat:**<br/> (s: recurso: pod_ position) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Posición del anuncio en la secuencia </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>Podposition) </li> <li> **Fuente de datos:**<br/>videoadinpod </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Duración del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.length </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.1 </li> <li> **Valor de muestra:**<br/> " 15 "  </li><li> **Descripción:**<br/>Duración de la publicidad de video en segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>length) </li> <li> **Heartbeat:**<br/> (l: recurso: ad_ length) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar y clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Duración del anuncio y Duración del anuncio (variable) </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>length) </li> <li> **Fuente de datos:**<br/>videoadlength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.length) </li> </ul> |



### Nombre del reproductor del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.playerName </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> " Rueda Freewheel " </li><li> **Descripción:**<br/>Nombre del reproductor responsable de procesar la publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>playerName) </li> <li> **Heartbeat:**<br/> (s: sp: player_ name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Nombre del reproductor del anuncio </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>playerName) </li> <li> **Fuente de datos:**<br/>videoadplayername </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Nombre del desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.podFriendlyName </li> <li> **Obligatorio:**<br/> SDK: Sí; API: No. </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> " pre-roll " </li><li> **Descripción:**<br/>Nombre descriptivo de la pausa publicitaria.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Podfriendlyname) </li> <li> **Heartbeat:**<br/> (s: recurso: pod_ name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Nombre de secuencia </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>Podfriendlyname) </li> <li> **Fuente de datos:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Índice del desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.podPosition </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 1 </li><li> **Descripción:**<br/>Índice de la pausa publicitaria dentro del contenido que empieza en 1. Esta propiedad la utiliza **solo** el Media SDK para generar el ID de la secuencia.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/>no </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>N/D </li> <li> **Datos de contexto:**<br/> </li> <li> **Fuente de datos:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Posición de desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.podSecond </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 90 </li><li> **Descripción:**<br/>Desplazamiento de la pausa publicitaria dentro del contenido, en segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Podsecond) </li> <li> **Heartbeat:**<br/> (l: recurso: pod_ offset) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>clasificación </li> <li> **Nombre del informe:**<br/>Posición de secuencia </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>Podsecond) </li> <li> **Fuente de datos:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID de desglose de anuncios

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> c 4 a 577424 c 84067899 b 807 c 76722 d 495_ 1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>pod) </li> <li> **Heartbeat:**<br/> (s: recurso: pod_ id) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Pod de anuncios </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>pod) </li> <li> **Fuente de datos:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Nombre de publicidad

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clave de API:**<br/>media.ad.name </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.1 </li> <li> **Valor de muestra:**<br/> " Ford F -150 " </li><li> **Descripción:**<br/>Nombre descriptivo del anuncio. En los informes, "Nombre del anuncio" es la clasificación y "Nombre del anuncio (variable)" es la eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Friendlyname) </li> <li> **Heartbeat:**<br/> (s: recurso: ad_ name) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar y clasificación </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Nombre del anuncio y Nombre del anuncio (variable) </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>Friendlyname) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Metadatos de anuncio estándar {#section_EFB805867916411E84DE1BA5A183D86A}

### Anunciante

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>ADVERTISER </li> <li> **Clave de API:**<br/>media.ad.advertiser </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>Empresa o marca cuyo producto se encuentra en la publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>advertiser) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.ad vertiser) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i>Anunciante </i> </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>advertiser) </li> <li> **Fuente de datos:**<br/>videoadvertiser </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### ID de campaña

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>CAMPAIGN_ID </li> <li> **Clave de API:**<br/>media.ad.campaignId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> Número entero o nombre (cadena).  </li><li> **Descripción:**<br/>ID de la campaña de publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>campaign) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.ca mpaign) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i>ID de campaña </i> </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>campaign) </li> <li> **Fuente de datos:**<br/>videocampaign </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### ID del creativo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>CREATIVE_ID </li> <li> **Clave de API:**<br/>media.ad.creativeId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> Número entero o nombre (cadena).  </li><li> **Descripción:**<br/>ID del elemento creativo publicitario.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>elemento creativo) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.cr eative) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i>ID del creativo </i> </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>elemento creativo) </li> <li> **Fuente de datos:**<br/>adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.creative) </li> </ul> |



### ID del sitio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>SITE_ID </li> <li> **Clave de API:**<br/>media.ad.siteId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>ID del sitio de publicidad.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>site) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.si te) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Utilizar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i> </i> </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>site) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.site) </li> </ul> |



### URL del anuncio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>CREATIVE_URL </li> <li> **Clave de API:**<br/>media.ad.creativeURL </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>URL del elemento creativo publicitario.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Creativeurl) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.cr Eativeurl) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Utilizar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i> </i> </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>Creativeurl) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### ID de colocación

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>PLACEMENT_ID </li> <li> **Clave de API:**<br/>media.ad.placementId </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> inicio de publicidad, cierre de publicidad </li> <li> **Versión del SDK mínima:** 1.5.7 </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>ID de ubicación del anuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>placement) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.pl acement) </li> </ul> | <ul> <li> **Disponible:**<br/> <i>Utilizar regla de procesamiento personalizada </i> </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/> <i> </i> </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>placement) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Métricas del anuncio {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### Inicio de publicidad

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/>inicio de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/>Número de inicios de anuncios en vídeo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>view) </li> <li> **Heartbeat:**<br/> (s: event: type = start)<br/> (s: recurso: type = ad) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Inicios de publicidad </li> <li> **Fuente de datos:**<br/>videoadstart </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>view) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.view) </li> </ul> |



### Publicidad completa

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/>cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/>Número de finalizaciones de anuncios de vídeo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>complete) </li> <li> **Heartbeat:**<br/> (s: event: type = complete)<br/> (s: recurso: type = ad)  </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Finalizaciones de publicidad </li> <li> **Fuente de datos:**<br/>videoadcomplete </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.complete) </li> </ul> |



### tiempo invertido en publicidad

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/> sí </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/>cierre de publicidad </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 15 </li><li> **Descripción:**<br/>Cantidad total de tiempo, en segundos, que se invirtió en la publicidad (es decir, la cantidad de segundos reproducidos). El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  <br/>**Fecha de la versión: 13/9/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Timeplayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Tiempo invertido en publicidad </li> <li> **Fuente de datos:**<br/>videoadtime </li> <li> **Datos de contexto:**<br/> (a. media. ad.<br/>Timeplayed) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## Related APIs {#section_Related_APIs}

### API createadobject:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### API createadbreakobject:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### API de mediaheartbeatconfig:

* Android: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS: [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

