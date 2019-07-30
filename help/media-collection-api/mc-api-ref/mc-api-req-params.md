---
seo-title: Parámetros de solicitud
title: Parámetros de solicitud
uuid: f 83 e 9 ef 1-803 d -4152-a 6 c 7-acaa 325036 b 9
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Parámetros de solicitud{#request-parameters}

## Datos de análisis

| Clave de solicitud  | Requerido | Definir en... |  Descripción  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | La URL del servidor de Adobe Analytics |
| `analytics.reportSuite` | Y | `sessionStart` | El ID que identifica los datos de los informes de Analytics |
| `analytics.enableSSL` | N | `sessionStart` | Verdadero o falso para activar SSL |
| `analytics.visitorId` | N | `sessionStart` | El ID de visitante de Adobe es un ID personalizado que puede utilizar en varias aplicaciones de Adobe. The Heartbeat `visitorId` equals the Analytics `VID.` |

## Datos del visitante

| Clave de solicitud  | Requerido | Definir en... |  Descripción  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | El ID de organización de Experience Cloud indentifica su organización en el sistema de Adobe Experience Cloud |
| `visitor.marketingCloudUserId` | N | `sessionStart` | Este es el ID de usuario de Experience Cloud (ECID). En la mayoría de los escenarios, es el ID que debe utilizarse para identificar a un usuario. The Heartbeat `marketingCloudUserId` equals the `MID` in Adobe Analytics. Aunque técnicamente no es necesario, este parámetro es necesario para acceder a la familia de aplicaciones de Experience Cloud. |
| `visitor.aamLocationHint` | N | `sessionStart` | Proporciona datos de Adobe Audience Manager Edge |
| `appInstallationId` | N | `sessionStart` | La clase appInstallationId identifica exclusivamente la aplicación y el dispositivo |

## Datos de contenido

| Clave de solicitud  | Requerido | Definir en... |  Descripción  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | Identificador único para el contenido |
| `media.name` | N | `sessionStart` | Nombre reconocible para el contenido |
| `media.length` | Y | `sessionStart` | Longitud del contenido (segundos) |
| `media.contentType` | Y | `sessionStart` | Formato de la emisión (puede ser cualquier cadena, algunos valores recomendados son "en directo", "VOD" o "Lineal") |
| `media.playerName` | Y | `sessionStart` | Nombre del reproductor responsable de la renderización del contenido |
| `media.channel` | Y | `sessionStart` | Canal de distribución del contenido. Podría ser un nombre de aplicación móvil o de un sitio web, nombre de propiedad |
| `media.resume` | N | `sessionStart` | Indica si un usuario está reanudando una sesión anterior (en oposición a comenzar una nueva sesión) |
| `media.sdkVersion` | N | `sessionStart` | La versión de SDK utilizada por el reproductor |

## Metadatos de contenido estándar

| Clave de solicitud  | Requerido | Definir en... |  Descripción  |
| --- | :---: | :---: | --- |
| `media.show` | N | `sessionStart` | El nombre del programa o serie |
| `media.season` | N | `sessionStart` | La temporada a la que pertenece el programa o la serie |
| `media.episode` | N | `sessionStart` | El número del episodio |
| `media.assetId` | N | `sessionStart` | El identificador exclusivo del contenido del recurso de vídeo, como el del episodio de la serie de TV, de la película o del evento en directo. Estos ID se derivan de autoridades de metadatos como EIDR, TMS/Gracenote o Rovi. Estos identificadores también pueden ser de otros sistemas privados o internos. |
| `media.genre` | N | `sessionStart` | El tipo de contenido definido por el productor de contenido |
| `media.firstAirDate` | N | `sessionStart` | La fecha en la que el contenido se emitió por primera vez en televisión |
| `media.firstDigitalDate` | N | `sessionStart` | La fecha en la que el contenido se emitió por primera vez en cualquier plataforma digital |
| `media.rating` | N | `sessionStart` | Clasificación según las pautas de clasificación por edades de la TV |
| `media.originator` | N | `sessionStart` | El creador del contenido |
| `media.network` | N | `sessionStart` | Nombre de la plataforma o canal |
| `media.showType` | N | `sessionStart` | Tipo de contenido, expresado como un número entero entre 0 y 3: <ul> <li>0: Episodio completo </li> <li>1: Vista previa </li> <li>2: Clip </li> <li>3: Otros </li> </ul> |
| `media.adLoad` | N | `sessionStart` | El tipo de publicidad cargada |
| `media.pass.mvpd` | N | `sessionStart` | La MVPD proporcionada por la autentificación de Adobe |
| `media.pass.auth` | N | `sessionStart` | Indica que Adobe ha autorizado el usuario (solo puede ser verdadero si está configurado) |
| `media.dayPart` | N | `sessionStart` | Hora del día en que se emite el contenido |
| `media.feed` | N | `sessionStart` | El tipo de fuente, por ejemplo, "West-HD" |

## Datos de publicidad

| Clave de solicitud  | Requerido | Definir en... |  Descripción  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Nombre reconocible de la pausa publicitaria |
| `media.ad.podIndex` | Y | `adBreakStart` | Índice de pod de anuncios en el vídeo |
| `media.ad.podSecond` | Y | `adBreakStart` | El segundo en el que comenzó el pod |
| `media.ad.podPosition` | Y | `adStart` | Índice de la publicidad dentro de la pausa publicitaria comenzando en 1 |
| `media.ad.name` | N | `adStart` | Nombre descriptivo del anuncio |
| `media.ad.id` | Y | `adStart` | Nombre de la publicidad |
| `media.ad.length` | Y | `adStart` | Longitud del vídeo publicitario, en segundos |
| `media.ad.playerName` | Y | `adStart` | Nombre del reproductor responsable de procesar el anuncio |

## Metadatos estándar de publicidad

| Clave de solicitud  | Requerido | Definir en... |  Descripción  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | Empresa o marca cuyo producto aparece en el anuncio |
| `media.ad.campaignId` | N | `adStart` | ID de la campaña de publicidad |
| `media.ad.creativeId` | N | `adStart` | El ID del creador de la publicidad |
| `media.ad.siteId` | N | `adStart` | ID del sitio de publicidad |
| `media.ad.creativeURL` | N | `adStart` | La dirección URL del creador de la publicidad |
| `media.ad.placementId` | N | `adStart` | ID de colocación de la publicidad |

## Datos de capítulo

| Clave de solicitud  | Requerido | Definir en... |  Descripción  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | Identifica la posición del capítulo en el contenido |
| `media.chapter.offset` | Y | `chapterStart` | El segundo de la reproducción en el que comienza el capítulo |
| `media.chapter.length` | Y | `chapterStart` | Duración del capítulo en segundos |
| `media.chapter.friendlyName` | N | `chapterStart` | Nombre reconocible del capítulo |

## Datos de calidad

| Clave de solicitud  | Requerido | Definir en... |  Descripción  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Cualquiera | Velocidad de bits de la emisión |
| `media.qoe.droppedFrames` | N | Cualquiera | El número de fotogramas perdidos en la emisión |
| `media.qoe.framesPerSecond` | N | Cualquiera | Número de fotogramas por segundo |
| `media.qoe.timeToStart` | N | Cualquiera | La cantidad de tiempo (en milisegundos) entre el momento en que el usuario inicia la reproducción y la carga y comienzo del contenido |

## Detalles adicionales {#section_ryt_ccy_lcb}

### visitor.marketingCloudUserId

Pass the Experience Cloud User ID (also known as the `MID` or `MCID`) on the `sessionStart` call by including it inside the `params` map using the following key: **visitor.marketingCloudUserId**. Esta función es útil si ya se integra con otros productos de Experience Cloud y ya se ha obtenido el MCID.

>[!NOTE]
>
>Media Analytics (MA) está integrado con la familia de aplicaciones de Experience Cloud (Adobe Analytics, Audience Manager, Target, etc.). Necesita un Experience Cloud ID para acceder a estas aplicaciones. _El ECID es lo que debe utilizarse para identificar a los usuarios en la mayoría de los escenarios._

### appInstallationId

* ***Si*no pasa`appInstallationId`un valor,** el back-end de MA ya no generará un MCID, sino que se basará en Adobe Analytics para hacerlo. La recomendación de Adobe es enviar una MCID si está disponible, o bien una `appInstallationId` (junto con la `marketingCloudOrgId` obligatoria) para que la API de Media Collection genere la MCID y la envíe en todas las llamadas.

* ***Si*se transfiere`appInstallationId`un valor,** el MCID *puede* generarse mediante el back-end de MA, si pasa valores para `appInstallationId` y los `marketingCloudOrgId` parámetros (obligatorios). Si transmite `appInstallationId` usted mismo, debe mantener su valor en el lado del cliente. Debe ser exclusivo de la aplicación en un dispositivo y persistente durante todo el tiempo en que la aplicación no se reinstale.

>[!NOTE]
>
>The `appInstallationId` uniquely identifies the app *and the device*. Debe ser exclusivo para cada aplicación en cada dispositivo, es decir, dos usuarios que utilicen la misma versión de la misma aplicación en distintos dispositivos deben enviar un `appInstallationId` diferente (exclusivo).

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor.marketingCloudOrgId

In addition to being necessary for MCID generation when that is not provided, this parameter is also used as the value for the publisher ID (based on which Media Analytics performs [federation rule matching.](/help/federated-analytics.md))

### ID de usuario heredado de Analytics (ayuda) e ID de usuario declarado (customerIDs)

* **analytics. aid:**

   el valor de esta clave debe ser una cadena que represente el ID de usuario heredado de Analytics
* **visitor. customerids:**

   el valor de esta clave debe ser un objeto con el formato siguiente:

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>> 
   }
   ```

Tenga en cuenta que el valor de `visitor.customerIDs` puede tener cualquier número de objetos en el formato presentado.

### visitor.aamLocationHint

Este parámetro indica qué borde de Adobe Audience Manager (AAM) se visita cuando Adobe Analytics envía los datos del cliente a Audience Manager. Si no transmite este parámetro, Adobe le asigna el valor 1 en el código. Esto es especialmente importante cuando los usuarios finales tienden a utilizar sus dispositivos en ubicaciones distantes geográficamente (por ejemplo, las costas de EE. UU., Europa, Asia). De lo contrario, los datos del usuario se esparcirán en varios límites de AAM.

### media.resume

Si la aplicación determina que se ha cerrado una sesión y después se reanuda, por ejemplo, cuando el usuario abandonó el vídeo pero regresa y el reproductor reanuda el vídeo desde la última posición del cabezal, puede enviar un parámetro booleano **media.resume** opcional dentro del bloque de parámetros de la llamada `sessionStart`.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
