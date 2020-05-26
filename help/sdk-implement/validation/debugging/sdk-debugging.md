---
title: Depuración de SDK
description: En este tema se describe el seguimiento/registro disponible en Media SDK.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
translation-type: ht
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a
workflow-type: ht
source-wordcount: '271'
ht-degree: 100%

---


# Depuración de SDK {#sdk-debugging}

Puede habilitar y deshabilitar el registro. Media SDK proporciona un amplio mecanismo de seguimiento/registro en toda la pila de seguimiento de contenido. Puede habilitar o deshabilitar este registro estableciendo el indicador `debugLogging` en el objeto de configuración.

## Código de muestra para el registro de depuración

### Android

```java
// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
config.debugLogging = true; 

// Use this space for setting other config values 
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config); 
```

### iOS

```
// Media Heartbeat Initialization 
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
config.debugLogging = YES; 

// Use this space for setting other config values 
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
```

### JavaScript

```js
// Media Heartbeat initialization 
var mediaConfig = new MediaHeartbeatConfig(); 
mediaConfig.debugLogging = true; 
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
```

### OTT (Chromecast, Roku)

La biblioteca ADBMobile proporciona un registro de depuración a través del método `setDebugLogging`. El registro de depuración se debe establecer en `false` para todas las aplicaciones de producción.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Uso de Adobe Bloodhound para probar aplicaciones Chromecast

Durante el desarrollo de la aplicación, Bloodhound permite ver llamadas de servidor localmente y permite la opción reenviar los datos a los servidores de recopilación de Adobe.

<!--
For more information about Bloodhound, see the following guides:

* [Bloodhound 3.x for Mac](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=2ahUKEwiimfSUypDpAhVZHzQIHS6WDQIQFjABegQIChAD&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound%2F&usg=AOvVaw3t4s0gcvuWEpLIqBkhKdGH) 
* [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)
-->

>[!IMPORTANT]
>
>Adobe Bloodhound expiró el 30 de abril de 2017. Desde el 1 de mayo de 2017 no se proporcionarán nuevas mejoras ni se ofrecerá más soporte técnico de ingeniería o Adobe Expert Care.

## Mensajes de registro

Los mensajes de registro usan este formato:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** Hora de CPU actual (zona horaria GMT)
* **level:** Hay 4 niveles de mensaje definidos:
   * INFO: Generalmente incluye los datos de entrada de la aplicación (validación del nombre del reproductor, ID de vídeo, etc.)
   * DEBUG: Registros de depuración, utilizados por los desarrolladores para depurar problemas más complejos
   * WARN: Indica posibles errores de integración/configuración o del SDK de Heartbeat
   * ERROR: Indica errores importantes de integración o del SDK de Heartbeat
* **tag:** El nombre del subcomponente que emitió el mensaje de registro (generalmente el nombre de la clase)
* **message:** El mensaje de seguimiento real

Puede utilizar el resultado de los registros de la biblioteca de Media SDK para comprobar la implementación. Una buena estrategia es buscar en los registros la cadena `#track`. Esto resaltará todas las llamadas a `track*()` realizadas por la aplicación.

Por ejemplo, después de aplicar el filtro `#track`, los registros podrían quedar así:

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad() 
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart() 
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay() 
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart() 
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart() 
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete() 
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart() 
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause() 
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete() 
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```

