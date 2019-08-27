---
seo-title: Seguimiento del contenido descargado
title: Seguimiento del contenido descargado
uuid: 0718689 d -9602-4 e 3 f -833 c -8297 aae 1 d 909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# Seguimiento del contenido descargado{#track-downloaded-content}

## Información general {#section_hcy_3pk_cfb}

La función Contenido descargado permite rastrear el consumo de medios mientras un usuario está sin conexión. Por ejemplo, un usuario descarga e instala una aplicación en un dispositivo móvil. A continuación, descarga contenido a través de la aplicación en el almacenamiento local del dispositivo. Para rastrear los datos descargados, Adobe ha desarrollado la función Contenido descargado. Con esta función, cuando el usuario reproduce contenido desde el almacenamiento de un dispositivo, los datos de seguimiento se almacenan en el dispositivo, independientemente de la conectividad del dispositivo. Cuando el usuario termina la sesión de reproducción y el dispositivo vuelve en línea, la información de seguimiento almacenada se envía al back-end API de Media Collection dentro de una única carga útil. Desde allí, el procesamiento y los informes se comportan como normales en la API de recopilación de medios.

Contrastar los dos métodos:

* En línea

   Con este método en tiempo real, el reproductor de medios envía los datos de seguimiento sobre cada evento de reproductor y envía los recorridos de red cada diez segundos (cada segundo para publicidades), de uno en uno.

* Sin conexión (función Contenido descargado)

   Con este método de procesamiento por lotes, es necesario generar los mismos eventos de sesión, pero se almacenan en el dispositivo hasta que se envían al back-end como una sola sesión (ver ejemplo abajo).

Cada método tiene sus ventajas y desventajas:
* El escenario en línea rastrea en tiempo real; esto requiere una comprobación de conectividad antes de cada llamada de red.
* El escenario sin conexión (función Contenido descargado) solo necesita una comprobación de conectividad de red, pero también requiere un espacio de memoria mayor en el dispositivo.

## Implementación {#section_jhp_jpk_cfb}

### Esquemas de eventos

La función Contenido descargado es simplemente la versión sin conexión de la API de recopilación de medios en línea (estándar) en línea, por lo que los datos de eventos que los lotes del reproductor y envía al back-end deben utilizar los mismos esquemas de eventos que utiliza al realizar llamadas en línea. Para obtener información sobre estos esquemas, consulte:
* [Información general;](/help/media-collection-api/mc-api-overview.md)
* [Validación de solicitudes de eventos](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Orden de los eventos

* El primer evento de la carga útil por lotes debe ser `sessionStart` similar al de la API de Media Collection.
* **Debe incluir`media.downloaded: true`** en los parámetros de metadatos estándar (`params` clave) en el `sessionStart` evento para indicar al back-end que está enviando contenido descargado. Si este parámetro no está presente o se establece en false cuando se envían los datos descargados, la API devolverá un código de respuesta 400 (Solicitud errónea). Este parámetro distingue entre el contenido descargado y el activo al back-end. (Tenga en cuenta que si `media.downloaded: true` se establece en una sesión activa, la API de emitirá igualmente una respuesta 400).
* Es responsabilidad de la implementación almacenar correctamente los eventos del reproductor por orden de aparición.

### Códigos de respuesta

* 201 - Creada: solicitud correcta, los datos son válidos, y la sesión se ha creado y se procesará.
* 400 - Solicitud no válida: el esquema de validación ha fallado, se han descargado todos los datos y no se procesarán datos de sesión.

## Integración con Adobe Analtyics {#section_cty_kpk_cfb}

Al calcular las llamadas de inicio y cierre de Analytics para el escenario de contenido descargado, el back-end establece un campo adicional de Analytics denominado `ts.` These are timestamps for the first and last events received (start and complete). Este mecanismo permite colocar una sesión de medios completada en el momento correcto (es decir, aunque el usuario no vuelve en línea durante varios días, se informa de que la sesión de medios ha tenido lugar en el momento en que se vio el contenido en realidad). Debe habilitar este mecanismo en Adobe Analytics. Para ello, cree un _grupo de informes con marca de hora opcional._ Para habilitar un grupo de informes con marca de hora opcional, consulte [Marcas de hora opcionales.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Comparación de sesión de muestra {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### Contenido en línea

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

### Contenido descargado

```
[{ 
    eventType: "sessionStart", 
    playerTime:{
      playhead: 0, 
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
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

