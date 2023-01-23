---
title: Streaming Media Collection API ‐ Parámetros de solicitud
description: '"Cuáles son los parámetros de solicitud, las claves de solicitud y las descripciones de la Media Collection API".'
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '1329'
ht-degree: 100%

---

# Parámetros de solicitud{#request-parameters}

## Datos de análisis

| Clave de solicitud  | Requerido | Clave de tipo de solicitud | Establecer en... |  Descripción  |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | Y | string | `sessionStart` | La URL del servidor de Adobe Analytics |
| `analytics.reportSuite` | Y | string | `sessionStart` | El ID que identifica los datos de los informes de Analytics |
| `analytics.enableSSL` | N | booleano | `sessionStart` | True o false para activar SSL |
| `analytics.visitorId` | N | string | `sessionStart` | El ID de visitante de Adobe es un ID personalizado que se puede utilizar en varias aplicaciones de Adobe. Heartbeat `visitorId` es igual a Analytics `VID.` |

## Datos del visitante

| Clave de solicitud  | Requerido | Clave de tipo de solicitud | Establecer en... |  Descripción  |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | string | `sessionStart` | El ID de organización de Experience Cloud indentifica su organización en el sistema de Adobe Experience Cloud |
| `visitor.marketingCloudUserId` | N | string | `sessionStart` | Este es el ID de usuario de Experience Cloud (ECID). En la mayoría de los casos, este es el ID que debe utilizar para identificar a un usuario. Heartbeat `marketingCloudUserId` es igual a `MID` en Adobe Analytics. Aunque técnicamente no es obligatorio, este parámetro es necesario para acceder a la familia de aplicaciones de Experience Cloud. |
| `visitor.aamLocationHint` | N | entero | `sessionStart` | Proporciona datos de Adobe Audience Manager Edge - Si no se introduce un valor, el valor es nulo. |
| `appInstallationId` | N | string | `sessionStart` | La clase appInstallationId identifica exclusivamente la aplicación y el dispositivo |

## Datos de contenido

| Clave de solicitud  | Requerido | Clave de tipo de solicitud | Establecer en... |  Descripción  |
| --- | :---: | :---: | :---: | --- |
| `media.id` | Y | string | `sessionStart` | Identificador único para el contenido |
| `media.name` | N | string | `sessionStart` | Nombre reconocible para el contenido |
| `media.length` | Y | number | `sessionStart` | Longitud del contenido (segundos) |
| `media.contentType` | Y | string | `sessionStart` | Formato de la emisión (puede ser cualquier cadena, algunos valores recomendados son &quot;en directo&quot;, &quot;VOD&quot; o &quot;Lineal&quot;) |
| `media.playerName` | Y | string | `sessionStart` | Nombre del reproductor responsable de la renderización del contenido |
| `media.channel` | Y | string | `sessionStart` | Canal de distribución del contenido. Podría ser un nombre de aplicación móvil o un nombre de sitio Web, un nombre de propiedad |
| `media.resume` | N | booleano | `sessionStart` | Indica si un usuario está reanudando o no una sesión anterior (en lugar de iniciar una nueva) |
| `media.sdkVersion` | N | string | `sessionStart` | La versión de SDK utilizada por el reproductor |

## Metadatos de contenido estándar

| Clave de solicitud  | Requerido | Clave de tipo de solicitud | Establecer en... |  Descripción  |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | N | string | `sessionStart` | Formato del flujo, por ejemplo &quot;HD&quot;. |
| `media.show` | N | string | `sessionStart` | El nombre del programa o serie |
| `media.season` | N | string | `sessionStart` | La temporada a la que pertenece el programa o la serie |
| `media.episode` | N | string | `sessionStart` | El número del episodio |
| `media.assetId` | N | string | `sessionStart` | El identificador único del contenido del recurso de vídeo, como el identificador de episodio de series de TV, el identificador de recursos de una película o el identificador de eventos en directo. Normalmente, estos ID se derivan de autoridades de metadatos como EIDR, TMS/Gracenote o Rovi. Estos identificadores también pueden proceder de otros sistemas propietarios o internos. |
| `media.genre` | N | string | `sessionStart` | El tipo de contenido definido por el productor de contenido |
| `media.firstAirDate` | N | string | `sessionStart` | La fecha en la que el contenido se emitió por primera vez en televisión |
| `media.firstDigitalDate` | N | string | `sessionStart` | La fecha en la que el contenido se emitió por primera vez en cualquier plataforma digital |
| `media.rating` | N | string | `sessionStart` | Clasificación según las pautas de clasificación por edades de la TV |
| `media.originator` | N | string | `sessionStart` | El creador del contenido |
| `media.network` | N | string | `sessionStart` | Nombre de la plataforma o canal |
| `media.showType` | N | string | `sessionStart` | El tipo de contenido, expresado con un número entero entre 0 y 3: <ul> <li>0 - Episodio completo </li> <li>1 - Vista previa </li> <li>2 - Clip </li> <li>3 - Otros </li> </ul> |
| `media.adLoad` | N | string | `sessionStart` | El tipo de publicidad cargada |
| `media.pass.mvpd` | N | string | `sessionStart` | La MVPD proporcionada por la autentificación de Adobe |
| `media.pass.auth` | N | string | `sessionStart` | Indica que Adobe ha autorizado el usuario (solo puede ser true si está configurado) |
| `media.dayPart` | N | string | `sessionStart` | Hora del día en que se emite el contenido |
| `media.feed` | N | string | `sessionStart` | El tipo de fuente, por ejemplo, &quot;West-HD&quot; |

## Datos de publicidad

| Clave de solicitud  | Requerido | Clave de tipo de solicitud | Establecer en... |  Descripción  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | string | `adBreakStart` | Nombre reconocible de la pausa publicitaria |
| `media.ad.podIndex` | Y | entero | `adBreakStart` | Índice de pod de anuncios en el vídeo |
| `media.ad.podSecond` | Y | number | `adBreakStart` | El segundo en el que comenzó el pod |
| `media.ad.podPosition` | Y | entero | `adStart` | Índice de la publicidad dentro de la pausa publicitaria comenzando en 1 |
| `media.ad.name` | N | string | `adStart` | Nombre descriptivo del anuncio |
| `media.ad.id` | Y | string | `adStart` | Nombre de la publicidad |
| `media.ad.length` | Y | number | `adStart` | Longitud del vídeo publicitario, en segundos |
| `media.ad.playerName` | Y | string | `adStart` | Nombre del reproductor responsable de procesar el anuncio |

## Metadatos estándar de publicidad

| Clave de solicitud  | Requerido | Clave de tipo de solicitud | Establecer en... |  Descripción  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | N | string | `adStart` | Empresa o marca cuyo producto aparece en el anuncio |
| `media.ad.campaignId` | N | string | `adStart` | ID de la campaña de publicidad |
| `media.ad.creativeId` | N | string | `adStart` | El ID del creador de la publicidad |
| `media.ad.siteId` | N | string | `adStart` | ID del sitio de publicidad |
| `media.ad.creativeURL` | N | string | `adStart` | La dirección URL del creador de la publicidad |
| `media.ad.placementId` | N | string | `adStart` | ID de colocación de la publicidad |

## Datos de capítulo

| Clave de solicitud  | Requerido | Clave de tipo de solicitud | Establecer en... |  Descripción  |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | Y | entero | `chapterStart` | Identifica la posición del capítulo en el contenido |
| `media.chapter.offset` | Y | number | `chapterStart` | El segundo de la reproducción en el que comienza el capítulo |
| `media.chapter.length` | Y | number | `chapterStart` | Duración del capítulo en segundos |
| `media.chapter.friendlyName` | N | string | `chapterStart` | Nombre reconocible del capítulo |

## Datos de calidad

| Clave de solicitud  | Requerido | Clave de tipo de solicitud | Establecer en... |  Descripción  |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | N | entero | Cualquiera | La tasa de bits media (en bps). La velocidad media se calcula como un promedio ponderado de todos los valores de velocidad de bits según la duración de reproducción durante una sesión determinada. |
| `media.qoe.droppedFrames` | N | entero | Cualquiera | Número de fotogramas perdidos en la emisión |
| `media.qoe.framesPerSecond` | N | entero | Cualquiera | Número de fotogramas por segundo |
| `media.qoe.timeToStart` | N | entero | Cualquiera | Cantidad de tiempo (en milisegundos) transcurrido entre el momento en que el usuario pulsa el botón Reproducir y el momento en que se carga el contenido y se reproduce |

## Parámetros de la Ley de privacidad del consumidor de California (CCPA)  {#ccpa-params}

| Clave de solicitud  | Requerido | Clave de tipo de solicitud | Establecer en... |  Descripción  |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | booleano | `sessionStart` | Se establece en true cuando el usuario final ha optado por no compartir sus datos entre Adobe Analytics y otras soluciones de Experience Cloud (por ejemplo, Audience Manager) |
| `analytics.optOutShare` | N | booleano | `sessionStart` | Se establece en true cuando el usuario final ha optado por no publicar sus datos (por ejemplo, para otros clientes de Adobe Analytics). |

## Detalles adicionales {#additional-details}

### visitor.marketingCloudUserId

Pase el ID de usuario de Experience Cloud (también conocido como `MID` o `MCID`) en la llamada a `sessionStart`, incluyéndolo en el mapa de `params` mediante la siguiente clave: **visitor.marketingCloudUserId**. Esta función es útil si ya se integra con otros productos de Experience Cloud y ya se ha obtenido el MCID.

>[!NOTE]
>
>Media Analytics (MA) está integrado con la gama de aplicaciones de Experience Cloud (Adobe Analytics, Audience Manager, Target, etc.). Necesita un Experience Cloud ID para acceder a estas aplicaciones. _El ECID es lo que debe utilizarse para identificar a los usuarios en la mayoría de los casos._

### appInstallationId

* **Si *no* transmite `appInstallationId` como un valor:** El servidor back-end de MA dejará de generar una MCID y, en su lugar, dependerá de Adobe Analytics para hacerlo. La recomendación de Adobe es enviar una MCID si está disponible, o bien una `appInstallationId` (junto con la `marketingCloudOrgId` obligatoria) para que la API de Media Collection genere la MCID y la envíe en todas las llamadas.

* **Si *transmite* el valor `appInstallationId`:** El MCID *puede* generarse en el final de MA si transmite valores para los parámetros `appInstallationId` y `marketingCloudOrgId` (obligatorios). Si transmite `appInstallationId` usted mismo, debe mantener su valor en el lado del cliente. Debe ser exclusivo de la aplicación en un dispositivo y persistente durante todo el tiempo en que la aplicación no se reinstale.

>[!NOTE]
>
>`appInstallationId` identifica exclusivamente la aplicación *y el dispositivo*. Debe ser exclusivo para cada aplicación en cada dispositivo, es decir, dos usuarios que utilicen la misma versión de la misma aplicación en distintos dispositivos deben enviar un `appInstallationId` diferente (exclusivo).

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

Además de ser necesario para generar MCID cuando no se proporciona, este parámetro se utiliza también como el valor del ID del editor (en los que Media Analytics lleva a cabo [la coincidencia de reglas de federación.](/help/use-cases/federated-analytics.md))

### ID de usuario heredado de Analytics (ayuda) e ID de usuario declarado (customerIDs)

* **analytics.aid:**

   el valor de esta clave debe ser una cadena que represente el ID de usuario heredado de Analytics
* **visitor.customerIDs:**

   el valor de esta clave debe ser un objeto con el formato siguiente:

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>>
   }
   ```

Tenga en cuenta que el valor de `visitor.customerIDs` puede tener cualquier número de objetos en el formato presentado.

### visitor.aamLocationHint

Este parámetro indica qué Adobe Audience Manager (AAM) se inicia cuando Adobe Analytics envía los datos del cliente a Audience Manager. Si no se introduce ningún valor, el valor es nulo. Esto es particularmente importante cuando los usuarios finales tienden a utilizar sus dispositivos en ubicaciones geográficamente distantes (por ejemplo, EE. UU.-Este, EE. UU.-Oeste, Europa o Asia). De lo contrario, los datos de usuario se distribuirán en varios perímetros de AAM.

### media.resume

Si la aplicación determina que se ha cerrado una sesión y después se reanuda, por ejemplo, cuando el usuario abandonó el vídeo pero regresa y el reproductor reanuda el vídeo desde la última posición del cabezal, puede enviar un parámetro booleano **media.resume** opcional dentro del bloque de parámetros de la llamada `sessionStart`.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
