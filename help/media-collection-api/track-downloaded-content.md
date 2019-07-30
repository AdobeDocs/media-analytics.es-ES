---
seo-title: Seguimiento del contenido descargado
title: Seguimiento del contenido descargado
uuid: 0718689 d -9602-4 e 3 f -833 c -8297 aae 1 d 909
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Seguimiento del contenido descargado{#track-downloaded-content}

## Información general {#section_hcy_3pk_cfb}

Downloaded Content API proporciona la capacidad de realizar un seguimiento del consumo de medios cuando un usuario está sin conexión. Por ejemplo, un usuario descarga e instala una aplicación en un dispositivo móvil. A continuación, descarga contenido a través de la aplicación en el almacenamiento local del dispositivo. Para realizar un seguimiento de los datos descargados, Adobe ha desarrollado Downloaded Content API. Con esta API, cuando el usuario reproduce contenido desde el almacenamiento de un dispositivo, los datos de seguimiento se almacenan en el dispositivo, independientemente de la conectividad de este. Cuando el usuario termina la sesión de reproducción y el dispositivo está en línea, la información de seguimiento almacenada se envía al back-end de la API de Media Collection dentro de una única carga útil. Allí, se realizan las tareas de procesamiento y creación de informes habituales en la API de Media Collection, en la que se basa esta API.

Contrastar los dos métodos:

* API de Media Collection

   Con este método en tiempo real, el reproductor de medios envía los datos de seguimiento sobre cada evento de reproductor y envía los recorridos de red cada diez segundos (cada segundo para publicidades), de uno en uno.

* Downloaded Content API

   Con este método de procesamiento por lotes, es necesario generar los mismos eventos de sesión pero almacenarlos en el dispositivo hasta que se envíen al back-end como una sola sesión (ver ejemplo más abajo).

Cada enfoque tiene sus ventajas e inconvenientes: la API de Media Collection realiza un seguimiento en tiempo real, pero requiere una comprobación de conectividad antes de cada llamada de red; Downloaded Content API solo necesita una comprobación de conectividad de red, pero también requiere mayor cantidad de memoria en el dispositivo.

## Implementación {#section_jhp_jpk_cfb}

### Esquemas de eventos

La API de contenido descargado se basa en la API de Media Collection, por lo que los datos de eventos que los lotes y envíos del reproductor requieren que los mismos esquemas de eventos se utilicen como en la API de Media Collection. For information on these schemas, see: [Overview;](/help/media-collection-api/mc-api-overview.md) and [Validating event requests.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Orden de los eventos

* El primer evento de la carga por lotes debe ser `sessionStart`.
* You must include `media.downloaded: true` in the standard metadata parameters ( `params` key) on the `sessionStart` event. Si este parámetro no está presente o se establece como falso, Downloaded Content API devolverá un código de respuesta 400 (solicitud no válida). Esto es así para que el back-end pueda distinguir entre contenido descargado y activo y procesarlo según corresponda. (Tenga en cuenta que si `media.downloaded: true` se establece en una sesión activa, la API de Media Collection emitirá igualmente una respuesta 400).

* Es responsabilidad de la implementación almacenar correctamente los eventos del reproductor por orden de aparición.

### Códigos de respuesta

* 201 - Creada: solicitud correcta, los datos son válidos, y la sesión se ha creado y se procesará.
* 400 - Solicitud no válida: el esquema de validación ha fallado, se han descargado todos los datos y no se procesarán datos de sesión.

## Integración con Adobe Analtyics {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called `ts`. Son marcas de hora del primer y último evento recibido (inicio y finalización). Este mecanismo permite colocar una sesión de medios completada en el momento correcto (es decir, aunque el usuario no vuelve en línea durante varios días, se informa de que la sesión de medios ha tenido lugar en el momento en que se vio el contenido en realidad). Debe habilitar este mecanismo en Adobe Analytics. Para ello, cree un *grupo de informes con marca de hora opcional*. Para habilitar un grupo de informes con marca de hora opcional, consulte [Marcas de hora opcionales.](https://marketing.adobe.com/resources/help/en_US/reference/timestamp-optional.html)

## Comparación de sesión de muestra {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### API de Media Collection

```
{ 
  eventType: "sessionStart", 
  playerTime: { 
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ } 
}
```

### Downloaded Content API

```
[{ 
    eventType: "sessionStart", 
    playerTime:{playhead: 0, ts: 1529997923478},  
    params:{
        "media.downloaded": true
    }, 
    customMetadata:{},  
    qoeData:{} 
}, 
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559} 
}]
```

