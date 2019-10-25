---
seo-title: Parámetros de calidad
title: Parámetros de calidad
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: 44b12731c4a701f0f2536c1c83a9ad4a8b27b49b

---


# Parámetros de calidad{#quality-parameters}

En este tema se presenta una lista de los datos de calidad de la experiencia (QoE/QoS), incluidos los valores de datos de contexto, que Adobe recopila a través de variables de solución.

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

## Metadatos de calidad {#quality-metadata}

### Velocidad de bits media

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/>media.qoe.bitrate </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> **Enviado con:**<br/>Cerrar </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 800-899 </li><li> **Descripción:**<br/>la velocidad de bits media (en kbps). Este valor está predefinido como bloques a intervalos de 100 kbps. La velocidad media se calcula como un promedio ponderado de todos los valores de velocidad de bits según la duración de reproducción durante una sesión determinada.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> ****<br/> Heartbeat: (l:stream:bitrate) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Velocidad de bits media </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Fuente de datos:**<br/>videoqoebitrateaverageevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> </ul> |


### Tiempo para el inicio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.qoe.timeToStart </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 30.000 </li><li> **Descripción:**<br/>este valor tiene el valor predeterminado cero si no lo establece mediante el objeto QoSObject. Este se establece en milisegundos. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> Heartbeat: (l:stream:startup_time) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Tiempo para el inicio </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>timeToStart) </li> <li> **Fuente de datos:**<br/>videoqoetimetostartevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |


### FPS

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.qoe.framesPerSecond </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Inicio de medios, cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 24 </li><li> **Descripción:**<br/>el valor actual de la velocidad de fotogramas del flujo (en fotogramas por segundo).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> ****<br/> Heartbeat: (l:stream:fps) </li> </ul> | <ul> <li> **Disponible:**<br/>no </li> <li> **Variable reservada:**<br/>N/D </li> <li> **Nombre del informe:**<br/>N/D </li> <li> **Datos de contexto:**<br/> </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Fotogramas perdidos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>droppedFrames </li> <li> **Clave de API:**<br/>media.qoe.droppedFrames </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 3 </li><li> **Descripción:**<br/>El número de cuadros perdidos (Int). Este valor se calcula como una suma de todos los fotogramas perdidos durante una sesión de reproducción. Este valor se toma del último valor de (l:stream:dropped_frames).  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> Heartbeat: (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Fotogramas perdidos </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Fuente de datos:**<br/>videoqoedroppedframecountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> </ul> |



### Eventos de búfer

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 2 </li><li> **Descripción:**<br/>El número de eventos de búfer. Esta métrica se calcula como un recuento de los distintos estados del búfer que se produjeron durante una sesión de reproducción. Es la cantidad de veces que el reproductor entra en estado de búfer desde otros estados, por ejemplo: reproducción o pausa.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Eventos de búfer </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>bufferCount) </li> <li> **Fuente de datos:**<br/>videoqoebuffercountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Duración total del búfer

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** </li> <li> ****<br/> Valor de muestra: 30 </li><li> **Descripción:**<br/>la cantidad total de tiempo, en segundos, que se ha pasado en el almacenamiento en búfer. Este valor se calcula como la suma de todas las duraciones de eventos de búfer que se produjeron durante una sesión de reproducción. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/>**Fecha de la versión: 13/9/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> Heartbeat: (l:event:duration) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Duración total del búfer </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>bufferTime) </li> <li> **Fuente de datos:**<br/>videoqoebuffertimeevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Cambios en la velocidad de bits

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/>media.qoe.bitrateChange </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 3 </li><li> **Descripción:**<br/>El número de cambios de velocidad de bits (entero). Este valor se calcula como una suma de todos los eventos de cambios en la velocidad de bits que se dan durante una sesión de reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Cambios en la velocidad de bits </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Fuente de datos:**<br/>videoqoebitratechangecountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Errores/eventos de error

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/> </li> <li> **Clave de API:**<br/> </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 1 </li><li> **Descripción:**<br/>El número de errores producidos (entero). Este valor se calcula como una suma de todos los eventos de error que se produjeron durante una sesión de reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>errorCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Errores </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>errorCount) </li> <li> **Fuente de datos:**<br/>videoqoeerrorcountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### ID de error de SDK de reproductor

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>los ID de error únicos generados por el SDK del reproductor. Los clientes deben proporcionar códigos o ID de error en el momento de la implementación mediante las API de error proporcionadas.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Errores </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> Fuente de datos: videoqoeplayersdkerrors </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> </ul> |



### ID de error externo

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>los ID de error únicos de cualquier origen externo, por ejemplo, errores CDN. Los clientes deben proporcionar códigos o ID de error en el momento de la implementación mediante las API de error proporcionadas.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Errores </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> Fuente de datos: videoqoeextneralerrors </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> </ul> |



### ID de error de Media SDK

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> **Valor de muestra:**<br/> </li><li> **Descripción:**<br/>los ID de error únicos generados por el SDK de medios durante la reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>mediaSdkErrors) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>eVar </li> <li> **Caducidad:**<br/>según HIT </li> <li> **Nombre del informe:**<br/>Errores </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Fuente de datos:** <br/>mediaqoeexternalerrors </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> </ul> |




### Fin de la sesión {#session-end}

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/> </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** 2.1 </li> <li> ****<br/> Valor de muestra: end </li><li> **Descripción:**<br/>El evento end significa que el SDK está enviando una llamada de cierre al servidor. Cuando ocurra este evento, el servidor cerrará la sesión de este vídeo y dejará de procesar. <br/>Si el medio se completó al 100%, debe enviarse después de `s:event:type=complete.` Ver [contenido completado](audio-video-parameters.md#content-complete) para obtener información relacionada. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>N/D </li> <li> ****<br/> Latidos: (s:event:type=end) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>N/D </li> <li> **Datos de contexto:**<br/> </li> <li> **Fuente de datos:**<br/>N/D </li> <li> **Audience Manager:**<br/> </li> </ul> |



## Métricas de calidad {#quality-metrics}

### Tiempo para el inicio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 30.000 </li><li> **Descripción:**<br/>este valor tiene el valor predeterminado cero si no lo establece mediante el objeto QoSObject. Este se establece en milisegundos. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/>**Fecha de la versión: 13/9/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> Heartbeat: (l:stream:startup_time) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Tiempo para el inicio </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>timeToStart) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### Eventos de búfer

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 2 </li><li> **Descripción:**<br/>El número de eventos de búfer (entero). Esta métrica se calcula como un recuento de los eventos de búfer que se produjeron durante una sesión de reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Eventos de búfer </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>bufferCount) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Duración total del búfer

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 15 </li><li> **Descripción:**<br/>la cantidad total de tiempo empleado en el almacenamiento en búfer (segundos; integer). Este valor se calcula como la suma de todas las duraciones de eventos de búfer que se produjeron durante una sesión de reproducción. El valor se mostrará con formato de hora (HH:MM:SS) en Analysis Workspace y Reports &amp; Analytics. En las fuentes de datos, el Data Warehouse y las API de informes, los valores se mostrarán en segundos. <br/>**Fecha de la versión: 13/9/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> Heartbeat: (l:event:duration) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Duración total del búfer </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>bufferTime) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Cambios en la velocidad de bits

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>evento </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: "3" </li><li> **Descripción:**<br/>El número de cambios en la velocidad de bits. Este valor se calcula como una suma de todos los eventos de cambios en la velocidad de bits que se dan durante una sesión de reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Cambios en la velocidad de bits </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Errores

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 1 </li><li> **Descripción:**<br/>El número de errores que se han producido (entero). Este valor se calcula como una suma de todos los eventos de error que se produjeron durante una sesión de reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>errorCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Eventos de error </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>errorCount) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### Fotogramas perdidos

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 1 </li><li> **Descripción:**<br/>El número de fotogramas perdidos (entero). Este valor se calcula como una suma de todos los fotogramas perdidos durante una sesión de reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> Heartbeat: (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Fotogramas perdidos </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> </ul> |



### Pérdidas antes del inicio

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: TRUE </li><li> **Descripción:**<br/>el número de veces que un usuario sale del vídeo antes de que se inicie. Esta métrica se define como 1 solo si no se procesó ningún contenido, independientemente de los anuncios.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>dropBeforeStart) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Pérdidas antes del inicio </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.

### Flujos afectados por el búfer

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: TRUE </li><li> **Descripción:**<br/>el número de flujos afectados por el almacenamiento en búfer. Esta métrica se define como 1 solo si tuvo lugar al menos un evento de búfer durante una sesión de reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>buffer) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Emisiones afectadas por almacenamiento en búfer </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>buffer) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.

### Flujos afectados por el cambio en la velocidad de bits

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: TRUE </li><li> **Descripción:**<br/>El número de flujos en los que se produjeron cambios en la velocidad de bits. Esta métrica se define como 1 solo si tuvo lugar al menos un cambio en la velocidad de bits durante una sesión de reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateChange) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> ****<br/> Nombre del informe: Flujos afectados por el cambio de velocidad de bits </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>bitrateChange) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.

### Velocidad de bits media

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: 3200 </li><li> **Descripción:**<br/>la velocidad de bits media (en kbps, entero). Esta métrica se calcula como una media ponderada de todos los valores de velocidad de bits relacionados con la duración de reproducción que se dan durante una sesión de reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateAverage) </li> <li> ****<br/> Heartbeat: (l:stream:bitrate) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Velocidad de bits media </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>bitrateAverage) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> </ul> |



### Flujos afectados por el error

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: TRUE </li><li> **Descripción:**<br/>el número de flujos en los que se produjo un evento de error (es decir, `trackError` se llamó durante la sesión de reproducción y se generó una llamada de `type=error` Heartbeat). </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>error) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Emisiones afectadas por el error </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>error) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.

### Flujos afectados por la pérdida de cuadros

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** cualquiera </li> <li> ****<br/> Valor de muestra: TRUE </li><li> **Descripción:**<br/>el número de flujos en los que se han eliminado fotogramas. Esta métrica se define como 1 solo si se perdió al menos un fotograma durante una sesión de reproducción.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>droppedFrames) </li> <li> ****<br/> Heartbeat: (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponible:**<br/> sí </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/>Flujos afectados por la pérdida de cuadros </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>droppedFrames) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.

### Flujos afectados por demoras

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5 o superior </li> <li> ****<br/> Valor de muestra: TRUE </li><li> **Descripción:**<br/>El número de flujos en los que se produjo un evento de detención. Esta métrica se establece en 1 solo si se produjo al menos una interrupción durante la reproducción. Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>stall) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>stall) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>Si se establece este evento, el único valor posible es TRUE. Si no se establece este evento, no se enviará ningún valor.

### Eventos de demora

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/> cadena </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5 o superior </li> <li> ****<br/> Valor de muestra: "3" </li><li> **Descripción:**<br/>el número de veces que la reproducción se ha detenido durante una sesión de reproducción. Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>stallCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>stallCount) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> </ul> |



### Duración total de demora

|   Implementación   | Parámetros de red | Creación de informes |
| --- | --- | --- |
| <ul> <li> **Clave de SDK:**<br/>establecida automáticamente </li> <li> **Clave de API:**<br/>N/D </li> <li> **Requerido:**<br/>no </li> <li> **Tipo:**<br/>número </li> <li> ****<br/> Enviado con: Cierre de medios </li> <li> **Versión del SDK mínima:** 1.5 o superior </li> <li> ****<br/> Valor de muestra: 12 </li><li> **Descripción:**<br/>El tiempo total (segundos; integer) la reproducción se detuvo durante una sesión de reproducción. Los clientes deberán crear sus propias reglas de procesamiento si desean tener el valor disponible para los informes.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>stallTime) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponible:**<br/>utilizar regla de procesamiento personalizada </li> <li> **Variable reservada:**<br/>evento </li> <li> **Nombre del informe:**<br/> </li> <li> ****<br/> Datos de contexto: (a.media.qoe.<br/>stallTime) </li> <li> **Fuente de datos:**<br/>N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> </ul> |



## API relacionadas {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

