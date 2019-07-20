---
seo-title: Parámetros de calidad
title: Parámetros de calidad
uuid: 0 d 9 fa 764-edef -4178-8650-90 c 9 a 0852 a 57
translation-type: tm+mt
source-git-commit: 180eafdfc536039820ade0b52e5c55f874719d8e

---


# Parámetros de calidad{#quality-parameters}

En este tema se presenta una lista de los datos de calidad de la experiencia (QoE/QoS), incluidos los valores de datos de contexto, que Adobe recopila a través de variables de solución.

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

## Metadatos de calidad {#section_8467F9729DA04A888A2657712234D7C7}

### Velocidad de bits media

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/>media.qoe.bitrate </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/>Cerrar </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 800-899 </li><li> **Descripción:**<br/>La velocidad de bits media (en kbps). Este valor está predefinido como bloques a intervalos de 100 kbps. La velocidad media se calcula como un promedio ponderado de todos los valores de velocidad de bits según la duración de reproducción durante una sesión determinada.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitrateaveragebucket) </li> <li> **Heartbeat:**<br/> (l: stream: bitrate) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Velocidad de bits media </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Bitrateaveragebucket) </li> <li> **Fuente de datos:**<br/>videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitrateaveragebucket) </li> </ul> |



### Tiempo para el inicio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.qoe.timeToStart </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 30.000 </li><li> **Descripción:**<br/>El valor predeterminado es cero si no se establece a través del qosobject. Este se establece en milisegundos. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l: stream: startup_ time) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Tiempo para el inicio </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Fuente de datos:**<br/>videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### FPS

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.qoe.framesPerSecond </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Inicio de medios, Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 24 </li><li> **Descripción:**<br/>Valor actual de la velocidad de fotogramas del flujo (en fotogramas por segundo).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> (l: stream: fps) </li> </ul> | <ul> <li> **Disponible:**<br/>no </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>N/D </li> <li> **Datos de contexto:**<br/> </li> <li> **Fuente de datos:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Fotogramas perdidos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>droppedFrames </li> <li> **Clave de API:**<br/>media.qoe.droppedFrames </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 3 </li><li> **Descripción:**<br/>Número de cuadros perdidos (entero). Este valor se calcula como una suma de todos los fotogramas perdidos durante una sesión de reproducción. Este valor se toma del último valor de (l: stream: dropped_ frames.)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Heartbeat:**<br/> (l: stream:<br/>dropped_ frames) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Fotogramas perdidos </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Fuente de datos:**<br/>videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframecount) </li> </ul> |



### Eventos de búfer

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 2 </li><li> **Descripción:**<br/>Número de eventos de búfer. Esta métrica se calcula como un recuento de los distintos estados del búfer que se produjeron durante una sesión de reproducción. Es la cantidad de veces que el reproductor entra en estado de búfer desde otros estados, por ejemplo: reproducción o pausa.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = buffer) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Eventos de búfer </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Fuente de datos:**<br/>videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffercount) </li> </ul> |



### Duración total del búfer

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** </li> <li> **Valor de muestra:**<br/> 30 </li><li> **Descripción:**<br/>Cantidad total de tiempo, en segundos, que se tarda en almacenar en búfer. Este valor se calcula como la suma de todas las duraciones de eventos de búfer que se produjeron durante una sesión de reproducción. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/>**Fecha de la versión: 13/9/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Heartbeat:**<br/> (l: event: duration) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Duración total del búfer </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Fuente de datos:**<br/>videoqoebuffertimeevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffertime) </li> </ul> |



### Cambios en la velocidad de bits

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.qoe.bitrateChange </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 3 </li><li> **Descripción:**<br/>Número de cambios en la velocidad de bits (entero). Este valor se calcula como una suma de todos los eventos de cambios en la velocidad de bits que se dan durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Cambios en la velocidad de bits </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Fuente de datos:**<br/>videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechangecount) </li> </ul> |



### Errores/eventos de error

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/> </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 1 </li><li> **Descripción:**<br/>Número de errores producidos (Entero). Este valor se calcula como una suma de todos los eventos de error que se produjeron durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Errores </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Fuente de datos:**<br/>videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Errorcount) </li> </ul> |



### ID de error de SDK de reproductor

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>ID de error exclusivos generados por el SDK del reproductor. Los clientes deben proporcionar códigos o ID de error en el momento de la implementación mediante las API de error proporcionadas.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Playersdkerrors) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Errores </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Playersdkerrors) </li> <li> **Fuente de datos:**<br/> videoqoeplayersdkerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Playersdkerrors) </li> </ul> |



### ID de error externo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>ID de error exclusivos de cualquier origen externo, por ejemplo, errores CDN. Los clientes deben proporcionar códigos o ID de error en el momento de la implementación mediante las API de error proporcionadas.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Externalerrors) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Errores </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Externalerrors) </li> <li> **Fuente de datos:**<br/> videoqoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Externalerrors) </li> </ul> |



### ID de error de Media SDK

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>ID de error exclusivos generados por el SDK de Media durante la reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Mediasdkerrors) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Errores </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Mediasdkerrors) </li> <li> **Fuente de datos:** <br/>mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Mediasdkerrors) </li> </ul> |




### Fin de la sesión {#session-end}

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** 2.1 </li> <li> **Valor de muestra:**<br/> end </li><li> **Descripción:**<br/>El evento end significa que el SDK envía una llamada cerrar al servidor. Cuando ocurra este evento, el servidor cerrará la sesión de este vídeo y dejará de procesar. <br/>Si el medio se ha completado al 100%, debe enviarse después `s:event:type=complete.` de Ver [contenido completado](audio-video-parameters.md#content-complete) para obtener información relacionada. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> **Latidos:**<br/> (s: event: type = end) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>N/D </li> <li> **Datos de contexto:**<br/> </li> <li> **Fuente de datos:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



## Métricas de calidad {#section_8EB0C9CBC09340C8915E1D2707D0A9EE}

### Tiempo para el inicio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 30.000 </li><li> **Descripción:**<br/>El valor predeterminado es cero si no se establece a través del qosobject. Este se establece en milisegundos. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/>**Fecha de la versión: 13/9/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l: stream: startup_ time) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Tiempo para el inicio </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Fuente de datos:**<br/>videoqoetimetostart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### Eventos de búfer

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 2 </li><li> **Descripción:**<br/>Número de eventos de búfer (Entero). Esta métrica se calcula como un recuento de los eventos de búfer que se produjeron durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = buffer) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Eventos de búfer </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Fuente de datos:**<br/>videoqoebuffercount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffercount) </li> </ul> |



### Duración total del búfer

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 15 </li><li> **Descripción:**<br/>La cantidad total de tiempo invertido en almacenamiento en búfer (segundos; entero). Este valor se calcula como la suma de todas las duraciones de eventos de búfer que se produjeron durante una sesión de reproducción. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/>**Fecha de la versión: 13/9/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Heartbeat:**<br/> (l: event: duration) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Duración total del búfer </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Fuente de datos:**<br/>videoqoebuffertime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffertime) </li> </ul> |



### Cambios en la velocidad de bits

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>evento </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> " 3 " </li><li> **Descripción:**<br/>Número de cambios en la velocidad de bits. Este valor se calcula como una suma de todos los eventos de cambios en la velocidad de bits que se dan durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Cambios en la velocidad de bits </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Fuente de datos:**<br/>videoqoebitratechangecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechangecount) </li> </ul> |



### Errores

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 1 </li><li> **Descripción:**<br/>Número de errores que se produjeron (Entero). Este valor se calcula como una suma de todos los eventos de error que se produjeron durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Eventos de error </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Fuente de datos:**<br/>videoqoeerrorcount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Errorcount) </li> </ul> |



### Fotogramas perdidos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 1 </li><li> **Descripción:**<br/>Número de cuadros perdidos (entero). Este valor se calcula como una suma de todos los fotogramas perdidos durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Heartbeat:**<br/> (l: stream:<br/>dropped_ frames) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Fotogramas perdidos </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Fuente de datos:**<br/>videoqoedroppedframecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframecount) </li> </ul> |



### Pérdidas antes del inicio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/>Número de veces que un usuario cierra el vídeo antes de su inicio. Esta métrica se define como 1 solo si no se procesó ningún contenido, independientemente de los anuncios.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Dropbeforestart) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = aa_ start) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Pérdidas antes del inicio </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Dropbeforestart) </li> <li> **Fuente de datos:**<br/>videoqoedropbeforestart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Dropbeforestart) </li> </ul> |



>[!IMPORTANT]
>Si este evento está establecido, el único valor posible es VERDADERO. Si no se establece este evento, no se enviará ningún valor.

### Flujos afectados por el búfer

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/>Número de flujos afectados por el almacenamiento en búfer. Esta métrica se define como 1 solo si tuvo lugar al menos un evento de búfer durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>buffer) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = buffer) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Emisiones afectadas por almacenamiento en búfer </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>buffer) </li> <li> **Fuente de datos:**<br/>videoqoebuffer </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>Si este evento está establecido, el único valor posible es VERDADERO. Si no se establece este evento, no se enviará ningún valor.

### Flujos afectados por el cambio en la velocidad de bits

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/>Número de flujos en los que se produjeron los cambios en la velocidad de bits. Esta métrica se define como 1 solo si tuvo lugar al menos un cambio en la velocidad de bits durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechange) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Emisiones afectadas por cambio en la velocidad de bits </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Bitratechange) </li> <li> **Fuente de datos:**<br/>videoqoebitratechange </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechange) </li> </ul> |



>[!IMPORTANT]
>Si este evento está establecido, el único valor posible es VERDADERO. Si no se establece este evento, no se enviará ningún valor.

### Velocidad de bits media

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> 3200 </li><li> **Descripción:**<br/>La velocidad de bits media (en kbps, entero). Esta métrica se calcula como una media ponderada de todos los valores de velocidad de bits relacionados con la duración de reproducción que se dan durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitrateaverage) </li> <li> **Heartbeat:**<br/> (l: stream: bitrate) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Velocidad de bits media </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Bitrateaverage) </li> <li> **Fuente de datos:**<br/>videoqoebitrateaverage </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitrateaverage) </li> </ul> |



### Flujos afectados por el error

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/>Número de flujos en los que se produjeron los cambios en la velocidad de bits. Esta métrica se define como 1 solo si tuvo lugar al menos un cambio en la velocidad de bits durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>error) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Emisiones afectadas por el error </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>error) </li> <li> **Fuente de datos:**<br/>videoqoeerror </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>Si este evento está establecido, el único valor posible es VERDADERO. Si no se establece este evento, no se enviará ningún valor.

### Flujos afectados por la pérdida de cuadros

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/>Número de flujos en los que se perdieron fotogramas. Esta métrica se define como 1 solo si se perdió al menos un fotograma durante una sesión de reproducción.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>droppedFrames) </li> <li> **Heartbeat:**<br/> (l: stream:<br/>dropped_ frames) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Flujos afectados por la pérdida de cuadros </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>droppedFrames) </li> <li> **Fuente de datos:**<br/>videoqoedroppedframes </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>Si este evento está establecido, el único valor posible es VERDADERO. Si no se establece este evento, no se enviará ningún valor.

### Flujos afectados por demoras

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5 o superior </li> <li> **Valor de muestra:**<br/> TRUE </li><li> **Descripción:**<br/>Número de flujos en los que ocurrió un evento con demora. Esta métrica se establece en 1 solo si se produjo al menos una interrupción durante la reproducción. Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>stall) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = stall) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>stall) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>Si este evento está establecido, el único valor posible es VERDADERO. Si no se establece este evento, no se enviará ningún valor.

### Eventos de demora

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5 o superior </li> <li> **Valor de muestra:**<br/> " 3 " </li><li> **Descripción:**<br/>El número de veces que se detuvo la reproducción durante una sesión de reproducción. Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Stallcount) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = stall) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Stallcount) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Stallcount) </li> </ul> |



### Duración total de demora

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/> Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5 o superior </li> <li> **Valor de muestra:**<br/> 12 </li><li> **Descripción:**<br/>El tiempo total (segundos; entero) La reproducción se detuvo durante una sesión de reproducción. Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Stalltime) </li> <li> **Heartbeat:**<br/> (s: event:<br/>type = stall) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> </li> <li> **Datos de contexto:**<br/> (a. media. qoe.<br/>Stalltime) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Stalltime) </li> </ul> |



## Related APIs {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

